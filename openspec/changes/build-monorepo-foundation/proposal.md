## Why

centaur-ts needs a stable Bun workspace before any service code lands. The foundation must make repo structure, commands, TypeScript settings, and contributor rules explicit so later agent/control-plane changes do not drift.

## What Changes

- Create the Bun workspace root with package metadata and shared TypeScript configuration.
- Add repo-level README and AGENTS guidance for Centaur invariants, TDD, and local commands.
- Define predictable package/app locations without creating unused implementation folders.

## Capabilities

### New Capabilities
- `monorepo-foundation`: Build monorepo foundation.

### Modified Capabilities

None.

## Impact

Affects root `package.json`, `bunfig.toml`, `tsconfig.base.json`, `README.md`, `AGENTS.md`, and documentation under `docs/`.
