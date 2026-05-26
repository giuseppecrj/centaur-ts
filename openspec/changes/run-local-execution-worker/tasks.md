## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/local-execution-worker/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Create Centaur-compatible harness protocol package and fake/local harness.
- [ ] 2.2 Implement queued execution claim with DB locking/lease semantics.
- [ ] 2.3 Implement sandbox/session attach, stdin injection, stdout streaming, event normalization, and event appends.
- [ ] 2.4 Add worker/runtime lifecycle command or API dev startup hook.
- [ ] 2.5 Test success, duplicate-worker, failure, and raw-harness-event normalization paths.

## 3. Verification

- [ ] 3.1 Run targeted tests for `local-execution-worker`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate run-local-execution-worker --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
