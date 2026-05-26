# Centaur parity decisions

Date: 2026-05-26

The project direction is now strict Centaur parity from day 1.

## Core decision

`centaur-ts` is a TypeScript rewrite of Centaur, not a simplified product inspired by Centaur. The architecture, boundaries, contracts, and operational semantics should match Centaur unless a TypeScript-specific implementation detail requires translation.

When an OpenSpec question asks how to handle behavior that Centaur already defines, the answer is: **follow Centaur**.

## Decisions from review questions

1. **Tenancy / ownership:** follow Centaur from day 1. Do not assume a reduced single-tenant architecture if Centaur models broader ownership or workspace semantics.
2. **Auth timing:** protect non-health routes from the start, matching Centaur's intended security posture.
3. **Event transport:** use SSE or whichever event streaming/replay mechanism Centaur uses. The TypeScript rewrite should preserve the Centaur client contract.
4. **Schema ownership:** model everything Centaur models. Drizzle migrations should represent Centaur's complete durable state architecture, translated to TypeScript/Drizzle/Postgres.
5. **Cancellation / execution semantics:** follow Centaur's execution, release, cancellation, event, and final delivery behavior.
6. **Secrets / egress:** follow Centaur's credential firewall and proxy/egress model. Do not weaken raw-secret boundaries for convenience.
7. **Sandbox:** follow Centaur's sandbox architecture and isolation model from day 1, translated into TypeScript interfaces and implementations.
8. **Runner:** follow Centaur's agent harness semantics. The OpenAI/pi implementation should fit the same sandbox/stdin/stdout/harness-event/control-plane architecture rather than inventing a direct model-call loop.
9. **Runtime wire:** follow Centaur's runtime wire: create/reuse sandbox session, attach stdin/stdout, write harness-native NDJSON input, read raw NDJSON output, normalize harness events, persist session/turn state, and stream canonical SSE events.
10. **Tools / workflows / overlays / delivery / observability:** follow Centaur's architecture and contracts unless a deliberate deviation is documented and approved.

## Implementation rule

Before implementing each OpenSpec change, inspect the corresponding Centaur source and research docs, then translate the architecture into the TypeScript stack:

- Bun workspaces/package management
- Hono API
- Drizzle/Postgres schemas and migrations
- Zod contracts/types
- `@earendil-works/pi-ai` for LLM SDK integration
- OpenAI provider for the first real model path

Do not replace Centaur behavior with a smaller MVP unless explicitly requested.

## Stack decisions after second Centaur source reread

Source anchor: `/Users/g/Code/centaur-v2/sources/centaur` at `9492ac21412fa84309a0a8ce168d3cbb66d1760a`.

These decisions resolve the pending technology questions from the second pass:

1. **Sandbox targets:** implement both a Kubernetes production backend and a local-process/dev backend. The local backend is only an adapter for tests and development; it must use the same `SandboxBackend` contract as Kubernetes.
2. **Sandbox images:** maintain both a thin development sandbox image and a full parity sandbox image. The full image should converge on Centaur's workstation-style sandbox contents.
3. **Tools/workflows language model:** design language-neutral tool/workflow registry contracts, with TypeScript-first implementations. Python plugin compatibility is deferred but should remain possible through a future adapter.
4. **Persistence parity:** follow Centaur at each storage layer. Use Postgres/ParadeDB/Postgres-extension compatibility wherever Centaur relies on it, including raw SQL migrations when Drizzle's schema DSL is too limited for exact parity.
5. **Migration strategy:** use Drizzle for TypeScript schema/type ergonomics, but allow hand-written SQL migrations for Postgres-specific constraints, indexes, extension usage, and Centaur-compatible state tables.
6. **Event streaming:** implement a small internal Hono/Bun SSE layer for Centaur's durable replay semantics. Hono's streaming primitives can be used, but event replay, cursoring, `wire.ready`, terminal ordering, and persistence are owned by our code.
7. **Pi/OpenAI harness:** follow Centaur's `pi-mono` harness semantics. `@earendil-works/pi-ai` is an internal engine/provider dependency; the control plane should see Centaur-compatible harness events.
8. **Auth/API keys:** preserve Centaur's API key and scope concepts, including service/root/sandbox/localhost source distinctions and sandbox-scoped tokens.
9. **Workers:** run API and workers as separate Bun process roles that share packages, rather than baking all long-running worker loops into the Hono API process.
10. **Slackbot:** include Slackbot as a monorepo boundary, but implement it after the agent HTTP protocol and durable events stabilize.
11. **TypeScript tooling:** use Bun/Hono/Zod and a modern TS lint/format/check stack. Prefer Centaur's current TS choices when they are stable enough, but do not block early implementation on preview TypeScript tooling.
12. **Harness events package:** port/copy Centaur's `packages/harness-events` semantics directly instead of reinventing event normalization.
13. **Credential boundary:** use iron-proxy as the parity credential/egress boundary rather than rewriting the secret proxy in TypeScript.
14. **Observability:** add trace IDs and structured logging from day one; keep Laminar/OpenTelemetry/VictoriaMetrics as adapter seams that follow Centaur's production design.
15. **Deployment:** Kubernetes/Helm is the real parity deployment target. Docker Compose may exist for lightweight local API/Postgres tests only.
