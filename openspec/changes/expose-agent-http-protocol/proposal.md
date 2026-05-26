## Why

Centaur’s primary contract is the thin-client agent protocol. Hono routes must expose the same spawn/message/execute/events/release flow while delegating durable behavior to control-plane services.

## What Changes

- Add `/agent` routes for spawn, message, execute, execution state, thread events, and release.
- Validate inputs with shared Zod contracts.
- Return conflict/not-found errors that map to control-plane state failures.

## Capabilities

### New Capabilities
- `agent-http-protocol`: Expose agent HTTP protocol.

### Modified Capabilities

None.

## Impact

Modifies API app route composition and adds integration tests.
