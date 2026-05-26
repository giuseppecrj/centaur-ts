## ADDED Requirements

### Requirement: Bun workspace root
The system SHALL use Bun workspaces as the only package-management entrypoint for project packages.

#### Scenario: Workspace install
- **WHEN** a developer runs `bun install` at the repository root
- **THEN** Bun installs all workspace dependencies without requiring npm, pnpm, or yarn lockfiles

### Requirement: Shared TypeScript settings
The system SHALL provide shared strict TypeScript configuration for all apps and packages.

#### Scenario: Package inheritance
- **WHEN** a new workspace package is added
- **THEN** the package can extend the root TypeScript configuration instead of duplicating compiler policy

### Requirement: Developer guide
The system SHALL document project invariants and local commands in a root developer guide.

#### Scenario: Agent onboarding
- **WHEN** an agent or developer opens `AGENTS.md`
- **THEN** they can identify the required test discipline, package layout, and core Centaur invariants before editing code
