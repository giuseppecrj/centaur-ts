## 1. Preparation

- [ ] 1.1 Read `proposal.md`, `design.md`, and `specs/tool-registry-invocation/spec.md`.
- [ ] 1.2 Identify dependent changes and implementation order before coding.

## 2. Test-first implementation

- [ ] 2.1 Design tool definition types and registry interfaces.
- [ ] 2.2 Implement in-process registry for local tools.
- [ ] 2.3 Add validated invocation service and audit events.
- [ ] 2.4 Expose tool list/invoke routes.
- [ ] 2.5 Connect runner tool-call events to invocation service.

## 3. Verification

- [ ] 3.1 Run targeted tests for `tool-registry-invocation`.
- [ ] 3.2 Run project-level check/test commands that exist at that point.
- [ ] 3.3 Run `openspec validate add-tool-registry-invocation --strict --no-interactive`.
- [ ] 3.4 Update README/AGENTS/docs if commands or behavior changed.
