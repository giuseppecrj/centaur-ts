## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/workflow-checkpoints/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Add workflow schema/tables if not already present.
- [ ] 2.2 Implement workflow registry and context primitives.
- [ ] 2.3 Add checkpoint get-or-run semantics.
- [ ] 2.4 Add trigger/status routes.
- [ ] 2.5 Test replay, failure, and child execution wait behavior.

## 3. Verification

- [ ] 3.1 Run targeted tests for `workflow-checkpoints`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate add-workflow-checkpoints --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
