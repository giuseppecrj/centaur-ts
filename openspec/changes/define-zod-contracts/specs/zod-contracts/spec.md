## ADDED Requirements

### Requirement: Agent protocol schemas
The system SHALL expose Zod schemas for spawn, message, execute, execution state, release, and event payloads.

#### Scenario: Invalid message rejected
- **WHEN** a message request has an unsupported role
- **THEN** schema parsing fails before the request reaches persistence

### Requirement: Shared inferred types
The system SHALL export inferred TypeScript types from every public Zod schema.

#### Scenario: Route typing
- **WHEN** a Hono route imports a request schema
- **THEN** the route can also import the matching request type from the same package

### Requirement: Extensible capability contracts
The system SHALL include schemas for future tool, workflow, overlay, auth, and sandbox contracts even when implementation ships later.

#### Scenario: Future proposal alignment
- **WHEN** a later tool-registry change is implemented
- **THEN** it can reuse the existing contract package instead of defining route-local ad hoc types
