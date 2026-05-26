## ADDED Requirements

### Requirement: Spawn route
The API SHALL expose `POST /agent/spawn` and return thread key, runtime id, assignment generation, and state.

#### Scenario: Client spawns
- **WHEN** a client posts a valid spawn request
- **THEN** the API returns HTTP 200 with an active assignment

### Requirement: Message route
The API SHALL expose `POST /agent/message` and persist canonical message parts for an active assignment.

#### Scenario: Client sends message
- **WHEN** a client posts valid message content for the active generation
- **THEN** the API returns an ok response with a message id

### Requirement: Execute route
The API SHALL expose `POST /agent/execute` and return a queued execution id.

#### Scenario: Client executes
- **WHEN** a client posts execute for an active generation
- **THEN** the API returns status `queued` with an execution id

### Requirement: Events route
The API SHALL expose `GET /agent/threads/{thread_key}/events` as a reconnectable event stream or event response with cursor support.

#### Scenario: Client replays events
- **WHEN** a client requests events after cursor zero
- **THEN** the API returns durable events for that thread in order

### Requirement: Release route
The API SHALL expose thread release with optional inflight cancellation.

#### Scenario: Client releases thread
- **WHEN** release is called with cancellation enabled
- **THEN** the assignment is released and queued/running executions are cancelled
