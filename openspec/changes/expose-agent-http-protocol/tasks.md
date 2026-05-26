## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/agent-http-protocol/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Add agent router and route registration.
- [ ] 2.2 Write route tests for happy path and stale generation conflicts.
- [ ] 2.3 Implement Zod request validation and error mapping.
- [ ] 2.4 Implement event response/stream behavior.

## 3. Verification

- [ ] 3.1 Run targeted tests for `agent-http-protocol`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate expose-agent-http-protocol --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
