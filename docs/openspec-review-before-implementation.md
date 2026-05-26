# OpenSpec review before implementation

Review date: 2026-05-26  
Scope: all active OpenSpec changes under `openspec/changes/`.

## Validation result

All 17 active changes validate with:

```bash
openspec validate <change> --strict --no-interactive
```

Validated changes:

1. `build-monorepo-foundation`
2. `define-zod-contracts`
3. `build-hono-api-shell`
4. `create-drizzle-durable-state`
5. `implement-control-plane-services`
6. `expose-agent-http-protocol`
7. `run-local-execution-worker`
8. `integrate-pi-openai-runner`
9. `add-api-key-auth-admin`
10. `add-tool-registry-invocation`
11. `add-workflow-checkpoints`
12. `add-extension-overlay-model`
13. `add-sandbox-runtime-backend`
14. `add-secret-egress-boundary`
15. `add-delivery-clients-outbox`
16. `add-observability-operations-deploy`
17. `add-local-smoke-docs`

## High-level verdict

The proposals are directionally strong and cover the major Centaur subsystems:

- monorepo/dev foundation
- shared contracts
- API shell
- durable database state
- control-plane state machine
- agent HTTP protocol
- local execution worker
- pi/OpenAI runner
- auth/admin
- tools
- workflows
- overlays
- sandbox backend
- secret/egress boundary
- delivery outbox
- observability/deploy
- smoke/docs

They are ready as a roadmap, but not quite ready as an implementation contract. The main issue is that several cross-cutting requirements are currently specified too late or too vaguely: auth, tenancy, secret handling, sandbox seams, state-machine transitions, and event/delivery semantics.

## Critical findings

### 1. Cross-change dependencies are not encoded strongly enough

`docs/openspec-roadmap.md` gives a linear order, but individual changes do not encode dependency metadata, and most task files only say “Identify dependent changes and implementation order before coding.”

Risk: parallel implementation can start in the wrong place or bake in assumptions before the dependent seam exists.

Recommended fix: add a lightweight dependency section to each proposal/design, or maintain an authoritative DAG in the roadmap.

### 2. Auth is ordered too late for non-health routes

`add-api-key-auth-admin` is currently step 9, after agent HTTP routes, worker, and OpenAI runner.

Risk: early route implementation defaults to unauthenticated surfaces, then auth is retrofitted.

Recommended fix: introduce an auth middleware/scope seam before or with `expose-agent-http-protocol`. Full admin lifecycle can remain step 9, but non-health route protection should be designed earlier.

### 3. Tenancy/ownership model is missing

Current specs use `thread_key`, execution ids, workflow ids, tool ids, secret bindings, and outbox rows without saying whether this is a single-user instance, workspace instance, org/tenant system, or per-API-key isolation model.

Risk: event replay by guessable thread key, cross-client access, and later schema churn.

Recommended fix: decide whether MVP is single-tenant self-hosted or multi-tenant. If single-tenant, state that explicitly. If multi-tenant, add tenant/workspace/user ownership to schemas and route filters from day one.

### 4. Secret/egress boundary is ordered too late

`add-secret-egress-boundary` is step 14, after OpenAI runner and tool invocation. But it is required before real tools/sandboxes handle sensitive systems.

Risk: early runner/tools read raw credentials or persist sensitive data before the sanitization/provider model exists.

Recommended fix: move a minimal secret provider + sanitizer earlier, before OpenAI runner and tool invocation. Keep proxy/egress enforcement as a later hardening step if needed.

### 5. Sandbox backend seam is ordered too late

`add-sandbox-runtime-backend` is step 13, after local worker, OpenAI runner, tools, and workflows.

Risk: runner/tool/workflow code assumes in-process execution and becomes harder to isolate later.

Recommended fix: introduce the sandbox/runtime interface earlier, even if the first implementation is a local no-op/process backend. Kubernetes can remain later.

### 6. Durable execution state machine needs a stricter spec

The control-plane and worker changes mention queued/running/completed/failed/cancelled, leases, release, and cancellation, but do not define the exact transitions.

Missing details:

- lease timeout and heartbeat behavior
- reclaim of stuck `running` executions
- max attempts / poison queue / dead-letter state
- cancellation during queued vs running vs tool-call phases
- terminal state race handling
- event ordering around partial output and cancellation

Recommended fix: add a dedicated execution state-machine section before coding `packages/control-plane` and the worker.

### 7. Drizzle durable state is too broad for one early migration

`create-drizzle-durable-state` reserves tables for future auth, workflows, tools, overlays, secrets, and sandboxes before those specs fully define behavior.

Risk: premature schema lock-in and migration churn.

Recommended fix: first migration should own core agent loop tables plus minimal outbox. Later changes should add their own migrations for auth/tools/workflows/overlays/secrets/sandboxes, unless we intentionally define all schemas now.

### 8. Event protocol is ambiguous

`expose-agent-http-protocol` says event stream or event response with cursor support.

Risk: contracts, tests, smoke scripts, and client assumptions diverge.

Recommended fix: choose a v0 event transport. Suggested default: JSON polling/replay first for testability, SSE as a follow-up or dual route once the durable cursor contract is stable.

### 9. Delivery outbox ownership overlaps between proposals

Outbox behavior appears in durable state, control-plane services, local worker, and delivery clients/outbox.

Risk: duplicate or inconsistent state transition definitions.

Recommended fix: define outbox states and ownership explicitly:

- execute creates `awaiting_terminal`
- worker moves to `pending` on completed result or appropriate cancelled/failed handling
- delivery worker owns `pending -> delivered|failed|dead_letter`

### 10. Observability is too late for trace context

Full ops/deploy can be late, but request id/thread key/execution id/worker id propagation should exist earlier.

Risk: retrofitting trace context across API, control plane, workers, runner, tools, workflows, delivery.

Recommended fix: add minimal trace/log context in foundation/API/control-plane phases. Keep metrics, doctor, deploy docs later.

## Important but not blocking

### Tool policy and approval gates

Tool registry validates schemas and audits calls, but it does not define dangerous-tool gating, human approval checkpoints, per-tool enablement, or side-effect classes.

Decision needed before sensitive tools, not before fake/local loop.

### Workflow scheduling semantics

Workflow checkpoints are good, but the proposal needs scheduler/wakeup rules:

- same worker framework or separate workflow worker?
- how waiting workflows resume after child execution completion
- duplicate replay prevention
- concurrency limits

Decision can happen before workflow implementation.

### Overlay lifecycle

Local overlay loading is covered. Missing for later:

- enable/disable
- version pinning
- trust/signing
- conflict resolution
- tenant-specific activation

Not needed for first local loop unless overlays are first-class from day one.

### LLM runner depth

The pi/OpenAI runner covers assistant output, but not a full agent loop:

- tool-call loop
- streaming deltas
- provider retries/rate limits
- model selection
- token accounting
- timeout policy

For v0, this is acceptable if runner is explicitly “single-turn text runner first; tool loop later.”

## Questions for the user before implementation

### Must answer before coding core data/API/worker

1. **Tenancy:** Is v0 single-tenant self-hosted, or do we need workspace/org/user ownership in every table and route from day one?
2. **Auth timing:** Should all non-health routes be protected from the start, or is early implementation explicitly local/dev-only until auth lands?
3. **Event transport:** Should v0 use polling JSON event replay, SSE, or both?
4. **Schema ownership:** Should initial Drizzle migrations include only core agent-loop tables, or should they pre-create tables for auth/tools/workflows/overlays/secrets/sandboxes?
5. **Execution state machine:** What terminal/cancellation behavior do you want for cancelled executions: no final delivery, delivery of a cancellation notice, or configurable by delivery metadata?

### Should answer before OpenAI/tools/sandbox work

6. **Secret model:** Should tool handlers ever receive raw secret values, or should we design around opaque handles / short-lived scoped credentials wherever possible?
7. **Sandbox guarantees:** Is the first implementation allowed to run the runner/tools in-process/local process, or must all LLM-directed code execution go through a sandbox abstraction immediately?
8. **OpenAI runner:** Is v0 a single-turn text runner, or should we implement iterative tool-calling from the first OpenAI runner?
9. **Tool approval:** Do we need human approval or policy gating before any destructive or external side-effect tool can run?

### Can answer later, but should be tracked

10. **Client scope:** Is this rebuild API/dev-only for now, or should Slack/Discord/browser ingress proposals be added before we call the roadmap complete?
11. **Admin surface:** Do we need day-2 admin operations for threads, executions, workers, sandboxes, workflows, overlays, tools, secrets, replay, cancellation, and repair?
12. **Retention:** Are events/checkpoints/outbox records permanent, TTL-managed, or user/tenant-deletable?
13. **Deployment target:** Are we targeting local/Docker first, Kubernetes first, or both in parallel?

## Recommended implementation kickoff plan

Before implementation, patch the roadmap/proposals with these decisions:

1. Add dependency/DAG notes to the roadmap.
2. Split `create-drizzle-durable-state` into core schema first; future schemas later.
3. Move minimal auth seam before agent HTTP protocol, or mark early API explicitly dev-only.
4. Move minimal secret provider/sanitizer before OpenAI runner/tool invocation.
5. Introduce sandbox backend interface before real runner/tool/workflow code relies on execution location.
6. Add a small execution state-machine spec section before control-plane implementation.
7. Choose event transport for v0.

Suggested revised first implementation order:

1. `build-monorepo-foundation`
2. `define-zod-contracts` — core agent contracts only, plus extension placeholders
3. `build-hono-api-shell`
4. Minimal trace/config + auth seam
5. `create-drizzle-durable-state` — core loop schema only
6. Execution state-machine patch
7. `implement-control-plane-services`
8. `expose-agent-http-protocol`
9. `run-local-execution-worker`
10. `add-local-smoke-docs` for fake runner loop
11. Minimal secret provider/sanitizer
12. `integrate-pi-openai-runner`
13. Tools/workflows/overlays/sandbox/delivery/ops hardening
