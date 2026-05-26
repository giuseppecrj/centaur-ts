## ADDED Requirements

### Requirement: Pi SDK usage
The OpenAI runner SHALL call OpenAI through `@earendil-works/pi-ai`, not direct provider-specific fetch code.

#### Scenario: Runner implementation
- **WHEN** the OpenAI runner is inspected
- **THEN** LLM calls are routed through the pi SDK abstraction

### Requirement: No paid tests
Automated tests SHALL NOT require real OpenAI credentials or paid provider calls.

#### Scenario: Test suite
- **WHEN** provider credentials are absent
- **THEN** runner tests still pass using a fake pi-compatible stream or client

### Requirement: Durable assistant output
The runner SHALL convert assistant output into durable `assistant.message` and terminal events.

#### Scenario: OpenAI run succeeds
- **WHEN** the runner receives assistant text
- **THEN** the execution event log records the assistant text before completion

### Requirement: Credential boundary
The runner SHALL read `OPENAI_API_KEY` only from process environment/config and SHALL NOT persist raw keys in database events or logs.

#### Scenario: Event audit
- **WHEN** an OpenAI run emits events
- **THEN** no event payload contains the raw API key
