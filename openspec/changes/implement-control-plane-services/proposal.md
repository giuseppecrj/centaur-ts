## Why

The Hono routes should stay thin while the Centaur state machine lives in a testable service package. This preserves the core invariant that execution state is durable and replayable.

## What Changes

- Create `packages/control-plane` for assignment, message, execution, event, release, and outbox services.
- Implement idempotency and assignment-generation checks.
- Expose functions that routes and workers can call without knowing SQL details.

## Capabilities

### New Capabilities
- `control-plane-services`: Implement control-plane services.

### Modified Capabilities

None.

## Impact

Adds control-plane package using contracts and db packages.
