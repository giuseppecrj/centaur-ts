## ADDED Requirements

### Requirement: Pi SDK usage
The pi/OpenAI harness SHALL call OpenAI through `@earendil-works/pi-ai`, not direct provider-specific fetch code.

#### Scenario: Harness implementation
- **WHEN** the pi/OpenAI harness is inspected
- **THEN** LLM calls are routed through the pi SDK abstraction

### Requirement: Centaur harness protocol compatibility
The pi/OpenAI harness SHALL fit Centaur's sandbox/stdin/stdout harness protocol: it receives harness-native NDJSON input and emits raw NDJSON events that can be normalized by the shared harness protocol layer.

#### Scenario: Harness event flow
- **WHEN** a user turn is injected into the pi/OpenAI harness
- **THEN** the harness emits Centaur-compatible raw events that normalize into canonical assistant, usage, tool, and terminal turn events

### Requirement: Pi is not the runtime architecture
The system SHALL NOT implement agent execution as a direct API route to pi-ai/OpenAI response path that bypasses sandbox sessions, harness input/output, event normalization, or durable turn state.

#### Scenario: Runtime boundary inspection
- **WHEN** the API execution path is inspected
- **THEN** it creates or reuses a Centaur-compatible sandbox/session and routes execution through the harness protocol rather than calling pi-ai directly from the route handler

### Requirement: No paid tests
Automated tests SHALL NOT require real OpenAI credentials or paid provider calls.

#### Scenario: Test suite
- **WHEN** provider credentials are absent
- **THEN** runner tests still pass using a fake Centaur-compatible harness or fake pi-compatible stream/client

### Requirement: Durable assistant output
The harness/runtime SHALL convert assistant output into durable canonical assistant and terminal events before completion is exposed to clients.

#### Scenario: OpenAI run succeeds
- **WHEN** the pi/OpenAI harness receives assistant text from pi-ai
- **THEN** the execution event log records normalized assistant output and terminal turn state before completion

### Requirement: Credential boundary
The harness SHALL read `OPENAI_API_KEY` only from approved process environment/config or Centaur secret boundary and SHALL NOT persist raw keys in database events or logs.

#### Scenario: Event audit
- **WHEN** an OpenAI run emits events
- **THEN** no event payload contains the raw API key
