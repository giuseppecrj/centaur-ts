## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/monorepo-foundation/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Create root package metadata and Bun workspace configuration.
- [ ] 2.2 Add shared TypeScript and formatter/check scripts.
- [ ] 2.3 Write README and AGENTS guidance.
- [ ] 2.4 Run `bun install` and confirm the workspace resolves.

## 3. Verification

- [ ] 3.1 Run targeted tests for `monorepo-foundation`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate build-monorepo-foundation --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
