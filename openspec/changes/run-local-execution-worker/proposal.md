## Why

A queued execution proves nothing until a worker claims it, appends events, and marks a terminal state durably. A local worker with a fake runner validates the control-plane loop before sandboxing and real LLM calls.

## What Changes

- Add execution worker loop with lease/claim semantics.
- Add fake runner that returns `PONG` for deterministic tests.
- Start worker from API only in local/dev configuration or as a separate command.

## Capabilities

### New Capabilities
- `local-execution-worker`: Run local execution worker.

### Modified Capabilities

None.

## Impact

Adds worker code in control-plane/runner packages and API lifecycle wiring.
