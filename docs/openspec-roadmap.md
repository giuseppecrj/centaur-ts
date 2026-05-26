# OpenSpec roadmap

This repo uses OpenSpec to split the Centaur TypeScript rewrite into independently reviewable proposals.

Architecture rule: `centaur-ts` follows Centaur's architecture and contracts from day 1. When an implementation question is already answered by Centaur, inspect the Centaur source/research and translate that behavior into the TypeScript stack rather than inventing a smaller MVP. See [`centaur-parity-decisions.md`](centaur-parity-decisions.md).

## Build order

1. `build-monorepo-foundation` — Bun workspace, TypeScript settings, README/AGENTS, local commands.
2. `define-zod-contracts` — shared Zod schemas and inferred public API types.
3. `build-hono-api-shell` — Hono app, health/readiness, config loading.
4. `create-drizzle-durable-state` — Postgres + Drizzle schema/migrations for durable state.
5. `implement-control-plane-services` — assignment/message/execution/event/release services.
6. `expose-agent-http-protocol` — `/agent/spawn`, `/message`, `/execute`, `/events`, `/release` routes.
7. `run-local-execution-worker` — fake runner and durable worker loop.
8. `integrate-pi-openai-runner` — `@earendil-works/pi-ai` OpenAI runner behind the same runner interface.
9. `add-api-key-auth-admin` — API key hashing, scopes, admin lifecycle.
10. `add-tool-registry-invocation` — declarative tools, validation, audited invocation.
11. `add-workflow-checkpoints` — replay-safe workflow runs and checkpoints.
12. `add-extension-overlay-model` — overlay manifests for tools, workflows, prompts, skills.
13. `add-sandbox-runtime-backend` — local sandbox first, Kubernetes backend seam.
14. `add-secret-egress-boundary` — secret provider, sanitization, egress/proxy policy seam.
15. `add-delivery-clients-outbox` — final delivery outbox worker and client adapters.
16. `add-observability-operations-deploy` — logs, metrics, doctor, deploy docs.
17. `add-local-smoke-docs` — reproducible local smoke loop and troubleshooting docs.

## Validation

All changes were validated with:

```bash
for c in $(find openspec/changes -mindepth 1 -maxdepth 1 -type d -exec basename {} \; | sort); do
  [ "$c" = "archive" ] && continue
  openspec validate "$c" --strict --no-interactive
done
```
