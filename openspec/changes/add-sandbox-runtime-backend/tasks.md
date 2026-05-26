## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/sandbox-runtime-backend/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Define sandbox backend interface and runtime record types.
- [ ] 2.2 Implement local development backend.
- [ ] 2.3 Wire spawn/release to sandbox backend seam.
- [ ] 2.4 Add Kubernetes backend skeleton behind optional dependency/config.
- [ ] 2.5 Test backend selection and release lifecycle.

## 3. Verification

- [ ] 3.1 Run targeted tests for `sandbox-runtime-backend`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate add-sandbox-runtime-backend --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
