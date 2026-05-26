## ADDED Requirements

### Requirement: Overlay manifest
An overlay SHALL declare id, version, prompts, skills, tools, workflows, and secret declarations in a validated manifest.

#### Scenario: Manifest loaded
- **WHEN** a valid overlay manifest is present
- **THEN** the loader returns typed overlay metadata

### Requirement: Kernel/overlay separation
Overlay code and content SHALL be loaded through extension interfaces without modifying base control-plane code.

#### Scenario: New tool overlay
- **WHEN** a local overlay adds a tool
- **THEN** the registry discovers it without editing core registry source

### Requirement: Prompt bundle assembly
The runner SHALL assemble base system prompt content with selected overlay prompts and skills.

#### Scenario: Overlay prompt active
- **WHEN** a thread selects an overlay/persona
- **THEN** the runner receives a prompt bundle including overlay guidance

### Requirement: Overlay validation errors
Invalid overlays SHALL produce actionable validation errors before runtime execution.

#### Scenario: Bad manifest
- **WHEN** an overlay references a missing prompt file
- **THEN** the loader reports the missing path and refuses to activate that overlay
