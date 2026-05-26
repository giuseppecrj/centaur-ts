## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/drizzle-durable-state/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Create db package, Drizzle config, and schema file.
- [ ] 2.2 Add local Postgres compose service.
- [ ] 2.3 Generate and apply initial migrations.
- [ ] 2.4 Add schema tests or migration smoke checks.

## 3. Verification

- [ ] 3.1 Run targeted tests for `drizzle-durable-state`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate create-drizzle-durable-state --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
