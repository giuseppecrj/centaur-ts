## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/local-smoke-docs/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Create smoke script for local API loop.
- [ ] 2.2 Add README quickstart and command reference.
- [ ] 2.3 Add troubleshooting section for common failures.
- [ ] 2.4 Run smoke script against fake runner.
- [ ] 2.5 Document optional OpenAI smoke separately.

## 3. Verification

- [ ] 3.1 Run targeted tests for `local-smoke-docs`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate add-local-smoke-docs --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
