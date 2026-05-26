## Why

The project needs a reproducible proof that the Centaur loop works end to end. A smoke script and docs make the architecture tangible and keep future changes honest.

## What Changes

- Add scripted local smoke test for spawn/message/execute/events/result.
- Document setup, commands, environment, OpenAI smoke, and troubleshooting.
- Keep docs aligned with actual commands and OpenSpec scope.

## Capabilities

### New Capabilities
- `local-smoke-docs`: Add local smoke tests and docs.

### Modified Capabilities

None.

## Impact

Adds `scripts/smoke-local.ts`, README sections, examples, and troubleshooting docs.
