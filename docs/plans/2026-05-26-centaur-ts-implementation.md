# Centaur TypeScript Implementation Plan

> **For Hermes:** Use subagent-driven-development skill to implement this plan task-by-task.

**Goal:** Build a Bun-first TypeScript monorepo implementation of Centaur's durable agent control-plane loop using Hono, Drizzle, Zod, pi-mono's LLM SDK, and OpenAI.

**Architecture:** Translate the Centaur rebuild tutorial from Python/FastAPI/SQLAlchemy into a TypeScript monorepo. Keep the same core invariants: durable Postgres state, one active assignment per thread, assignment-generation checks, append-only events, worker leases, final delivery outbox, and thin API/client surfaces. Start with a local fake/LLM harness before Kubernetes or Slack.

**Tech Stack:** Bun workspaces, TypeScript, Hono, Drizzle ORM + drizzle-kit, Zod, Postgres, Vitest, `@earendil-works/pi-ai`, OpenAI.

---

## Fixed decisions from user

- Package manager/runtime: Bun.
- Server API: Hono.
- Database schemas/migrations: Drizzle.
- Runtime/public types: Zod.
- LLM SDK: pi-mono, package `@earendil-works/pi-ai`.
- Model provider: OpenAI.
- Repository shape: monorepo.

## Working defaults

- Root: `/Users/g/Code/centaur-ts`.
- Workspace packages:
  - `apps/api` — Hono HTTP API and local worker startup.
  - `packages/contracts` — Zod schemas and shared API types.
  - `packages/db` — Drizzle schema, migrations, and DB client.
  - `packages/control-plane` — assignment/message/execution/event services.
  - `packages/runner` — fake runner first, OpenAI/pi runner next.
- Local database: Postgres via Docker Compose.
- API port: `8000` to match the Centaur tutorial.
- Environment prefix: `CENTAUR_`.
- First faithful slice: `spawn -> message -> execute -> events -> completed result`.
- Do not add Slack, Kubernetes, credential proxy, or overlays until the durable local loop passes.

## Task 1: Create root monorepo skeleton

**Objective:** Create the minimal Bun workspace and docs/agent guide without unused architecture folders.

**Files:**
- Create: `package.json`
- Create: `bunfig.toml`
- Create: `tsconfig.base.json`
- Create: `README.md`
- Create: `AGENTS.md`
- Create: `docs/plans/2026-05-26-centaur-ts-implementation.md`

**Verification:**
- Run `bun install`.
- Run `bun pm ls`.

## Task 2: Add contracts package with failing tests first

**Objective:** Define Zod schemas for health, spawn, message, execute, execution state, release, and SSE event payloads.

**Files:**
- Create: `packages/contracts/package.json`
- Create: `packages/contracts/src/index.ts`
- Create: `packages/contracts/test/contracts.test.ts`

**TDD:**
1. Write tests for valid/invalid request parsing.
2. Run package test and verify failure.
3. Implement schemas and exported inferred types.
4. Run test and verify pass.

## Task 3: Add Hono API health endpoints

**Objective:** Build a runnable Hono app with `/health` and `/health/ready`.

**Files:**
- Create: `apps/api/package.json`
- Create: `apps/api/src/app.ts`
- Create: `apps/api/src/server.ts`
- Create: `apps/api/test/health.test.ts`

**Verification:**
- Package test passes.
- `bun run --filter @centaur-ts/api test` passes.
- Starting the server and curling `/health` returns `{ "status": "ok" }`.

## Task 4: Add Drizzle schema and migration commands

**Objective:** Make Postgres the durable state source with Drizzle schema covering Centaur's core tables.

**Files:**
- Create: `docker-compose.yml`
- Create: `packages/db/package.json`
- Create: `packages/db/drizzle.config.ts`
- Create: `packages/db/src/schema.ts`
- Create: `packages/db/src/client.ts`

**Tables:**
- `api_keys`
- `agent_runtime_assignments`
- `agent_spawn_requests`
- `agent_message_requests`
- `agent_execution_requests`
- `agent_execution_events`
- `agent_final_delivery_outbox`
- `agent_release_requests`

**Verification:**
- `bun run --filter @centaur-ts/db db:generate`
- `docker compose up -d postgres`
- `bun run --filter @centaur-ts/db db:migrate`

## Task 5: Implement durable control-plane services

**Objective:** Implement spawn, persist message, enqueue execution, get execution, list events, release assignment, and append event.

**Files:**
- Create: `packages/control-plane/package.json`
- Create: `packages/control-plane/src/controlPlane.ts`
- Create: `packages/control-plane/test/controlPlane.test.ts`

**Key invariants:**
- Spawn is idempotent for an existing active thread assignment.
- Only one active assignment exists per thread.
- Message/execute require matching active assignment generation.
- Events are append-only and cursor-replayable.

## Task 6: Add agent Hono routes

**Objective:** Expose Centaur's tutorial API contract in TypeScript.

**Routes:**
- `POST /agent/spawn`
- `POST /agent/message`
- `POST /agent/execute`
- `GET /agent/executions/:executionId`
- `GET /agent/threads/:threadKey/events`
- `POST /agent/threads/:threadKey/release`

**Files:**
- Create: `apps/api/src/routes/agent.ts`
- Modify: `apps/api/src/app.ts`
- Create: `apps/api/test/agent-routes.test.ts`

## Task 7: Add local execution worker with fake runner

**Objective:** Prove queued executions complete durably without a real sandbox.

**Files:**
- Create: `packages/runner/src/fakeRunner.ts`
- Create: `packages/control-plane/src/executionWorker.ts`
- Create: `packages/control-plane/test/executionWorker.test.ts`

**Behavior:**
- Claim queued execution with lock/lease semantics.
- Append `execution.running`, `assistant.message`, and `turn.done` events.
- Mark execution completed with `PONG`.
- Move final delivery outbox to pending.

## Task 8: Replace fake runner option with OpenAI/pi runner

**Objective:** Add a runner implementation that uses `@earendil-works/pi-ai` with OpenAI while keeping fake runner for tests.

**Files:**
- Create: `packages/runner/src/piOpenAiRunner.ts`
- Create: `packages/runner/src/types.ts`
- Create: `packages/runner/test/piOpenAiRunner.test.ts`

**Rules:**
- Tests must not call paid/provider APIs.
- Use a fake provider/event stream in tests.
- Runtime requires `OPENAI_API_KEY` only for manual smoke.

## Task 9: Add smoke script and docs

**Objective:** Make the local loop reproducible from shell commands.

**Files:**
- Create: `scripts/smoke-local.ts`
- Update: `README.md`
- Update: `AGENTS.md`

**Verification:**
- `bun run check`
- `bun run test`
- `docker compose up -d postgres`
- `bun run db:migrate`
- `bun run dev:api`
- `bun run smoke:local`

## Non-goals for the first implementation

- Slack client.
- Kubernetes sandbox backend.
- Iron-proxy-compatible credential injection.
- Full overlay mounting.
- Workflow replay engine beyond schema placeholders.
- Production auth hardening beyond API-key skeleton.
