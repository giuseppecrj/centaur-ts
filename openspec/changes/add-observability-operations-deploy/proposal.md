## Why

A control plane needs operators to understand health, migrations, workers, queues, and deployment state. Observability and deploy artifacts should be part of the build, not a final polish pass.

## What Changes

- Add structured logs, request ids, execution ids, and worker metrics.
- Add doctor/readiness checks for database, migrations, runner config, and worker queues.
- Add Dockerfile and deployment documentation with production-safe migration flow.

## Capabilities

### New Capabilities
- `observability-operations-deploy`: Add observability, operations, and deploy.

### Modified Capabilities

None.

## Impact

Adds logging/metrics utilities, operational routes/commands, Docker/deployment files, and docs.
