## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/api-key-auth-admin/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Implement key generation and hashing utilities.
- [ ] 2.2 Add auth middleware/dependencies and scope model.
- [ ] 2.3 Add admin routes for create/revoke/list metadata.
- [ ] 2.4 Write tests for missing, invalid, revoked, and under-scoped keys.

## 3. Verification

- [ ] 3.1 Run targeted tests for `api-key-auth-admin`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate add-api-key-auth-admin --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
