## ADDED Requirements

### Requirement: Health endpoint
The API SHALL return `{ "status": "ok" }` from `GET /health` without requiring a database.

#### Scenario: Health check
- **WHEN** a client requests `/health`
- **THEN** the API returns HTTP 200 with status `ok`

### Requirement: Readiness endpoint
The API SHALL return environment and configured harness information from `GET /health/ready`.

#### Scenario: Ready check
- **WHEN** `CENTAUR_DEFAULT_HARNESS=openai` is set
- **THEN** the readiness response reports `default_harness` as `openai`

### Requirement: No implicit migrations
The API SHALL NOT run database migrations during HTTP startup.

#### Scenario: Startup safety
- **WHEN** the API starts in an environment with a stale schema
- **THEN** startup does not mutate the database schema automatically
