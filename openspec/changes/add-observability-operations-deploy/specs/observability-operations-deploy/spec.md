## ADDED Requirements

### Requirement: Structured trace context
The system SHALL include thread key, execution id, worker id, and request id in relevant logs/events.

#### Scenario: Execution logged
- **WHEN** a worker processes an execution
- **THEN** logs include execution id and thread key for correlation

### Requirement: Doctor command
The project SHALL provide a doctor/readiness command that checks database connectivity, migrations, required env, and runner configuration.

#### Scenario: Doctor run
- **WHEN** a developer runs the doctor command with missing database
- **THEN** the command fails with a specific remediation message

### Requirement: Metrics surface
The system SHALL expose or produce metrics for queued executions, worker claims, failures, and delivery outbox state.

#### Scenario: Queue inspected
- **WHEN** executions are queued
- **THEN** operators can see queue depth through the metrics/status surface

### Requirement: Deployable artifact
The project SHALL include container/deploy documentation that separates migration execution from app startup.

#### Scenario: Deployment docs
- **WHEN** an operator reads deployment instructions
- **THEN** they see explicit migration and rollback guidance separate from server startup
