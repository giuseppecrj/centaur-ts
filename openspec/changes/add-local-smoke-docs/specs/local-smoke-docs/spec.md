## ADDED Requirements

### Requirement: End-to-end smoke
The project SHALL provide a local smoke command that exercises spawn, message, execute, event replay, and final execution state.

#### Scenario: Smoke passes
- **WHEN** Postgres and API are running
- **THEN** the smoke command completes with a terminal successful result

### Requirement: Deterministic default
The default smoke path SHALL use the fake runner and not require OpenAI credentials.

#### Scenario: No credentials
- **WHEN** `OPENAI_API_KEY` is absent
- **THEN** the default smoke command still passes

### Requirement: Optional OpenAI smoke
The project SHALL document an explicit optional OpenAI/pi smoke path requiring credentials.

#### Scenario: OpenAI smoke requested
- **WHEN** a developer opts into OpenAI runner with credentials
- **THEN** the docs explain required env vars and expected behavior

### Requirement: Troubleshooting docs
The docs SHALL include remediation for database, migration, port, auth, and runner configuration failures.

#### Scenario: Smoke fails
- **WHEN** a common local dependency is missing
- **THEN** the README points to the command or setting needed to fix it
