## ADDED Requirements

### Requirement: Idempotent spawn
The control plane SHALL return the existing active assignment when spawning an already-active thread.

#### Scenario: Repeated spawn
- **WHEN** spawn is called twice for the same active thread
- **THEN** both calls return the same assignment generation and runtime id

### Requirement: Generation safety
The control plane SHALL reject message and execute requests whose assignment generation does not match the active assignment.

#### Scenario: Stale client
- **WHEN** a client posts a message for an old assignment generation
- **THEN** the service rejects the request with a stale assignment error

### Requirement: Durable execution enqueue
The control plane SHALL enqueue execution requests and create a final delivery outbox obligation in the same durable operation.

#### Scenario: Execution queued
- **WHEN** execute is called for an active assignment
- **THEN** an execution row and matching outbox row are persisted

### Requirement: Cursor event listing
The control plane SHALL list execution events after a supplied event cursor for one thread.

#### Scenario: Reconnect
- **WHEN** a client reconnects with `after_event_id`
- **THEN** only newer events for that thread are returned in ascending order
