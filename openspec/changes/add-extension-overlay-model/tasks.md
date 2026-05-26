## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/extension-overlay-model/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Define overlay manifest Zod schema.
- [ ] 2.2 Implement local overlay loader and sample overlay.
- [ ] 2.3 Wire overlays into tool/workflow registration.
- [ ] 2.4 Wire overlay prompts/skills into runner prompt bundle builder.
- [ ] 2.5 Add validation tests for malformed overlays.

## 3. Verification

- [ ] 3.1 Run targeted tests for `extension-overlay-model`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate add-extension-overlay-model --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
