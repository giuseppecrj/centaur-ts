## ADDED Requirements

### Requirement: Durable delivery obligation
Every execute request with delivery metadata SHALL create or update a durable final delivery outbox obligation.

#### Scenario: Execute with delivery
- **WHEN** a client executes with platform `dev`
- **THEN** an outbox row is created before execution completes

### Requirement: Delivery worker
The delivery worker SHALL claim pending outbox rows, send through the configured adapter, and mark delivered or failed.

#### Scenario: Dev delivery
- **WHEN** a completed execution has pending dev delivery
- **THEN** the worker records delivered state after writing/sending the final payload

### Requirement: Retryable failures
Failed delivery attempts SHALL preserve error details and remain retryable according to policy.

#### Scenario: Adapter failure
- **WHEN** a delivery adapter throws
- **THEN** the outbox row stores failure details without losing the final result

### Requirement: Thin client adapters
Slack/Discord/API callback adapters SHALL use the same outbox contract instead of owning execution state.

#### Scenario: Slack adapter added
- **WHEN** a future Slack client is implemented
- **THEN** it reads final payloads from outbox rather than polling in-memory worker state
