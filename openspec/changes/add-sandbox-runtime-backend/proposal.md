## Why

The faithful Centaur architecture isolates agent execution in sandboxes. The TypeScript version should start with a local process backend and preserve a Kubernetes backend interface for production.

## What Changes

- Define sandbox backend interface for create, attach, execute, stream events, and release.
- Implement local process sandbox backend for development.
- Add Kubernetes backend design seam using `@kubernetes/client-node` without making it mandatory for local tests.

## Capabilities

### New Capabilities
- `sandbox-runtime-backend`: Add sandbox runtime backend.

### Modified Capabilities

None.

## Impact

Adds sandbox package/module, runtime assignment integration, configuration, and future deployment dependency seams.
