## ADDED Requirements

### Requirement: Hashed storage
The system SHALL store only hashes of API keys, never plaintext keys.

#### Scenario: Key creation
- **WHEN** an admin creates an API key
- **THEN** the response shows plaintext once and the database stores only its hash

### Requirement: Scope checks
The API SHALL enforce required scopes for protected agent/admin operations.

#### Scenario: Missing scope
- **WHEN** a client uses a valid key without the required scope
- **THEN** the API returns HTTP 403

### Requirement: Revocation
The system SHALL reject revoked API keys.

#### Scenario: Revoked key
- **WHEN** a revoked key is used for a protected route
- **THEN** the API returns HTTP 401

### Requirement: Local dev clarity
Any local development auth bypass SHALL be explicit in configuration and visible from readiness output.

#### Scenario: Dev readiness
- **WHEN** local auth bypass is enabled
- **THEN** readiness reports that dev auth mode is active
