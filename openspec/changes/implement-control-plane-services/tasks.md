## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/control-plane-services/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Create service package and public interfaces.
- [ ] 2.2 Write failing tests for spawn idempotency and generation safety.
- [ ] 2.3 Implement assignment/message/execution/event operations.
- [ ] 2.4 Implement release and cancellation behavior.
- [ ] 2.5 Run package tests against test database.

## 3. Verification

- [ ] 3.1 Run targeted tests for `control-plane-services`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate implement-control-plane-services --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
