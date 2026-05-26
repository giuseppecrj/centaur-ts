## Why

Centaur clients must remain thin and share one API contract with the server. Zod schemas give the Hono API, tests, runners, and future clients a single runtime-validatable protocol.

## What Changes

- Create `packages/contracts` for public schemas and inferred TypeScript types.
- Model health, spawn, message, execute, event stream, execution state, release, admin, tool, workflow, and overlay contracts.
- Reject stale or malformed requests at the boundary before they reach control-plane services.

## Capabilities

### New Capabilities
- `zod-contracts`: Define Zod contracts.

### Modified Capabilities

None.

## Impact

Adds `packages/contracts` and makes API/routes/control-plane code depend on shared schemas.
