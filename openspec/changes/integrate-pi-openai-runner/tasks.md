## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/pi-openai-runner/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Inspect pi-ai exported API before coding.
- [ ] 2.2 Add pi-ai dependency and runner interfaces.
- [ ] 2.3 Write tests with fake pi client/event stream.
- [ ] 2.4 Implement OpenAI runner and output-to-event mapping.
- [ ] 2.5 Document required environment for manual smoke.

## 3. Verification

- [ ] 3.1 Run targeted tests for `pi-openai-runner`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate integrate-pi-openai-runner --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
