## Why

Thin clients should not infer completion from open connections. Final answers must be delivered through durable outbox rows that can retry, fail, and be inspected.

## What Changes

- Implement final delivery worker over `agent_final_delivery_outbox`.
- Add dev delivery adapter first and preserve seams for Slack/Discord/API callbacks.
- Expose outbox inspection and retry behavior for operations.

## Capabilities

### New Capabilities
- `delivery-clients-outbox`: Add delivery clients and outbox.

### Modified Capabilities

None.

## Impact

Adds delivery package/module, worker command, route/admin status, and event updates.
