## Why

The project needs a runnable HTTP surface early, but without owning durable execution state in process memory. A small Hono shell proves server startup, readiness, config loading, and test wiring before the agent protocol is added.

## What Changes

- Create `apps/api` with Hono app and Bun server entrypoint.
- Add `/health` and `/health/ready` endpoints.
- Load environment-backed settings with `CENTAUR_` defaults.

## Capabilities

### New Capabilities
- `hono-api-shell`: Build Hono API shell.

### Modified Capabilities

None.

## Impact

Adds API app package, Hono dependency, and server/test commands.
