## ADDED Requirements

### Requirement: Workflow registry
The system SHALL register named workflow handlers with typed input schemas.

#### Scenario: Workflow listed
- **WHEN** a workflow is registered
- **THEN** clients can discover its name and input schema

### Requirement: Checkpointed steps
Workflow handlers SHALL execute side effects behind named checkpoints and reuse checkpoint results on replay.

#### Scenario: Replay after checkpoint
- **WHEN** a workflow restarts after a completed step
- **THEN** the completed step is not executed again and its stored result is returned

### Requirement: Agent child execution
Workflows SHALL be able to enqueue an agent execution and durably wait for its terminal state.

#### Scenario: Workflow runs agent
- **WHEN** a workflow calls `ctx.runAgent`
- **THEN** a child execution is created and the workflow records a wait checkpoint

### Requirement: Terminal workflow state
Workflow runs SHALL persist completed, failed, and waiting states.

#### Scenario: Workflow failure
- **WHEN** a workflow handler throws
- **THEN** the run is marked failed with an error message
