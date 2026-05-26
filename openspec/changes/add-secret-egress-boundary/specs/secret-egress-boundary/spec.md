## ADDED Requirements

### Requirement: No raw secret persistence
The system SHALL NOT write raw secret values to database rows, events, prompts, or logs.

#### Scenario: Secret-bound tool
- **WHEN** a tool uses a configured secret
- **THEN** event payloads and logs contain only secret binding identifiers, never raw values

### Requirement: Secret provider interface
The system SHALL resolve secrets through a provider interface rather than direct arbitrary environment reads in tool handlers.

#### Scenario: Tool needs secret
- **WHEN** a tool declares a required binding
- **THEN** the invoker resolves it through the secret provider before calling the handler

### Requirement: Egress policy seam
The system SHALL represent allowed host/location bindings for tools and sandboxes.

#### Scenario: Policy rendered
- **WHEN** a sandbox/tool declares allowed hosts
- **THEN** the security layer can render a proxy/egress config without exposing secret values

### Requirement: Sanitized failures
Secret resolution failures SHALL be reported without leaking requested secret values.

#### Scenario: Missing secret
- **WHEN** a binding cannot be resolved
- **THEN** the error identifies the binding id and remediation without printing secret contents
