## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/secret-egress-boundary/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Define secret declaration and binding schemas.
- [ ] 2.2 Implement local environment-backed secret provider.
- [ ] 2.3 Add sanitizer utilities and tests.
- [ ] 2.4 Integrate secret resolution into tool invocation.
- [ ] 2.5 Add proxy/egress config representation seam.

## 3. Verification

- [ ] 3.1 Run targeted tests for `secret-egress-boundary`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate add-secret-egress-boundary --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
