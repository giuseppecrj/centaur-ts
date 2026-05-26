## Context

centaur-ts is a Bun-first TypeScript rebuild of Centaur's durable shared-agent control plane. The project follows the Centaur invariant that Slack, browser, API, and future clients remain thin while durable execution state, event replay, worker leases, delivery, capabilities, and security boundaries live in the control plane.

This change covers: **Define Zod contracts**.

## Goals / Non-Goals

**Goals:**
- Preserve Centaur's durable-control-plane architecture in TypeScript.
- Keep implementation testable with deterministic local defaults before cloud or paid-provider paths.
- Use Bun, Hono, Drizzle, Zod, pi-mono, and OpenAI according to the project decisions.

**Non-Goals:**
- Do not add unrelated product surfaces outside this change's capability.
- Do not require Slack, Kubernetes, or paid OpenAI calls unless this change explicitly covers that path.
- Do not bypass durable state with process-memory execution state.

## Decisions

- **Capability-first OpenSpec split:** Each major subsystem has its own change so implementation can proceed independently while preserving the project roadmap. Alternative considered: one giant proposal; rejected because it would hide dependencies and make validation/review harder.
- **Test-first implementation:** Production behavior from this change will be implemented behind failing tests first. Alternative considered: scaffold everything at once; rejected because Centaur's correctness depends on state-machine edge cases.
- **Local deterministic path first:** Where a real external service is involved, the design keeps a local fake/deterministic path for tests. Alternative considered: direct integration-only tests; rejected because paid APIs and cloud services would make the baseline loop brittle.

## Risks / Trade-offs

- Scope creep → Keep this change bounded to `zod-contracts` and use separate OpenSpec changes for neighboring subsystems.
- Spec drift → Validate OpenSpec artifacts and keep README/commands updated when implementation lands.
- Over-abstraction → Add seams only where Centaur architecture requires future backends, credentials, tools, workflows, or clients.

## Migration Plan

This is new-project work. Implement behind tests, keep local commands runnable after each task, and push changes in small commits. Rollback is deleting or reverting this change's files before dependent changes land.

## Open Questions

- Which implementation slice should be applied first after all proposals are reviewed?
- Which future external clients beyond dev/API should be prioritized after the local loop is proven?
