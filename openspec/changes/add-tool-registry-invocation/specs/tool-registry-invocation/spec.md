## ADDED Requirements

### Requirement: Declarative tool definitions
Tools SHALL declare name, version, description, input schema, output schema, and required secret bindings.

#### Scenario: Tool registered
- **WHEN** a tool is registered
- **THEN** clients can inspect its metadata without seeing secret values

### Requirement: Validated invocation
Tool invocations SHALL validate input against the declared schema before running handler code.

#### Scenario: Invalid tool args
- **WHEN** an invocation omits a required field
- **THEN** the invocation is rejected and no handler side effect occurs

### Requirement: Audited tool calls
Every tool invocation SHALL append durable audit events with tool name, status, and sanitized arguments/result metadata.

#### Scenario: Tool succeeds
- **WHEN** a tool invocation completes
- **THEN** the event log contains sanitized start and completion events

### Requirement: Runner integration
Runner-emitted tool calls SHALL route through the registry rather than arbitrary local code execution.

#### Scenario: LLM calls tool
- **WHEN** the runner emits a known tool call
- **THEN** the control plane invokes the registered tool and returns the result to the runner
