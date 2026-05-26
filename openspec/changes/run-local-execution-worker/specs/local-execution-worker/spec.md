## ADDED Requirements

### Requirement: Execution claim
The worker SHALL claim queued executions without allowing two workers to run the same execution simultaneously.

#### Scenario: Concurrent workers
- **WHEN** two workers poll for queued executions
- **THEN** only one worker claims a given execution

### Requirement: Terminal completion
The worker SHALL append running, assistant message, and turn done events before marking successful execution completed.

#### Scenario: Fake run completes
- **WHEN** a queued execution is processed by the fake runner
- **THEN** events include `execution.running`, `assistant.message`, and `turn.done`, and the execution status is `completed`

### Requirement: Outbox transition
The worker SHALL move final delivery outbox rows to pending when an execution reaches a terminal successful state.

#### Scenario: Delivery pending
- **WHEN** a fake execution completes
- **THEN** the matching outbox row moves from awaiting terminal to pending

### Requirement: Failure durability
The worker SHALL persist failed execution status and error details when a runner throws.

#### Scenario: Runner failure
- **WHEN** the runner throws during execution
- **THEN** the execution is marked failed and an error event is appended
