## Why

Long-running agent work needs replay-safe orchestration. Workflow runs and checkpoints prevent restarts from repeating side effects and allow workflows to wait on agent executions.

## What Changes

- Add workflow registry, workflow run records, and checkpoint store.
- Implement `ctx.step` and `ctx.runAgent` primitives.
- Expose workflow trigger/status APIs.

## Capabilities

### New Capabilities
- `workflow-checkpoints`: Add workflow checkpoints.

### Modified Capabilities

None.

## Impact

Adds workflow service/package, DB tables, API routes, and tests for replay behavior.
