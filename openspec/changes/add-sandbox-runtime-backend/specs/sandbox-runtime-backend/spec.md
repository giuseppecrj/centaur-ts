## ADDED Requirements

### Requirement: Backend interface
The system SHALL define a sandbox backend interface independent of any single runtime provider.

#### Scenario: Backend swap
- **WHEN** configuration selects local or kubernetes backend
- **THEN** control-plane assignment code uses the same interface

### Requirement: Local sandbox
The system SHALL support a local sandbox backend for development and tests.

#### Scenario: Local spawn
- **WHEN** a thread is spawned in local mode
- **THEN** a runtime id is created without requiring Kubernetes

### Requirement: Kubernetes seam
The system SHALL preserve a Kubernetes backend implementation seam for pod/session creation and attachment.

#### Scenario: Kubernetes configured
- **WHEN** the backend is configured as kubernetes
- **THEN** the sandbox package owns Kubernetes-specific client code rather than API routes

### Requirement: Release lifecycle
Sandbox release SHALL update runtime assignment state and stop or detach from the underlying runtime.

#### Scenario: Thread released
- **WHEN** a release request reaches sandbox backend
- **THEN** the runtime is stopped or marked released and assignment state is durable
