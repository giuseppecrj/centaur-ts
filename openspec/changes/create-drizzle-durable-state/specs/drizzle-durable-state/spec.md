## ADDED Requirements

### Requirement: Core agent tables
The database SHALL persist runtime assignments, spawn requests, message requests, execution requests, execution events, and final delivery outbox rows.

#### Scenario: Migration applied
- **WHEN** a developer runs the migration command against local Postgres
- **THEN** all core agent tables exist

### Requirement: One active assignment guard
The database SHALL enforce at most one active runtime assignment per thread.

#### Scenario: Duplicate active assignment
- **WHEN** code attempts to insert a second active assignment for the same thread
- **THEN** the database rejects it or the service handles the conflict without creating two active rows

### Requirement: Append-only event order
The database SHALL assign monotonically increasing event ids suitable for reconnect cursors.

#### Scenario: Event replay
- **WHEN** events are appended for a thread
- **THEN** clients can request events after a known event id and receive only newer events in order

### Requirement: Future state surfaces
The schema SHALL reserve durable tables for API keys, workflow runs/checkpoints, tool definitions, overlay registrations, secret bindings, and sandbox runtime records.

#### Scenario: Future implementation
- **WHEN** a later workflow or tool proposal is implemented
- **THEN** it can use existing schema foundations or add narrow migrations rather than inventing a separate persistence layer
