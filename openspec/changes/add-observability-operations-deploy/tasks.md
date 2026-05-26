## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/observability-operations-deploy/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Add structured logger and trace context helpers.
- [ ] 2.2 Add doctor command/checks.
- [ ] 2.3 Add queue/outbox metrics or status endpoint.
- [ ] 2.4 Add Dockerfile and deployment docs.
- [ ] 2.5 Verify local production-like startup path.

## 3. Verification

- [ ] 3.1 Run targeted tests for `observability-operations-deploy`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate add-observability-operations-deploy --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
