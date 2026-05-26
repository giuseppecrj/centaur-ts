## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/hono-api-shell/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Create API package and Hono app factory.
- [ ] 2.2 Add config loader and health/readiness routes.
- [ ] 2.3 Write route tests using Hono test requests.
- [ ] 2.4 Add root scripts for API test/start commands.

## 3. Verification

- [ ] 3.1 Run targeted tests for `hono-api-shell`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate build-hono-api-shell --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
