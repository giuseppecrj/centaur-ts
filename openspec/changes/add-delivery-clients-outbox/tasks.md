## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/delivery-clients-outbox/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Define delivery adapter interface and dev adapter.
- [ ] 2.2 Implement outbox claim/send/update worker.
- [ ] 2.3 Add delivery status/retry operations.
- [ ] 2.4 Wire execution completion to pending delivery.
- [ ] 2.5 Test success and failure delivery paths.

## 3. Verification

- [ ] 3.1 Run targeted tests for `delivery-clients-outbox`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate add-delivery-clients-outbox --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
