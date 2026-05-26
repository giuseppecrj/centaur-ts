## Why

A queued execution proves nothing until the runtime attaches to a Centaur-compatible sandbox/harness, injects input over stdin, reads raw NDJSON output over stdout, normalizes events, and marks terminal state durably. The local/fake implementation must validate Centaur's runtime protocol before real model calls.

## What Changes

- Add execution/runtime loop with Centaur-compatible session, wire, and lease semantics.
- Add fake/local harness that emits Centaur-compatible NDJSON events rather than returning `PONG` from an in-process shortcut.
- Start worker/runtime from API only in local/dev configuration or as a separate command.

## Capabilities

### New Capabilities
- `local-execution-worker`: Run local execution worker.

### Modified Capabilities

None.

## Impact

Adds worker code in control-plane/runner packages and API lifecycle wiring.
