## Why

Centaur’s brain is durable state, not a chat adapter. Drizzle schemas and migrations must encode the assignment, execution, event, outbox, auth, workflow, and capability tables that survive restarts.

## What Changes

- Create `packages/db` with Drizzle schema and migration tooling.
- Add Docker Compose Postgres for local development.
- Model core Centaur tables plus future workflow/tool/overlay/security tables.

## Capabilities

### New Capabilities
- `drizzle-durable-state`: Create Drizzle durable state.

### Modified Capabilities

None.

## Impact

Adds Postgres dependency, drizzle-kit config, schema definitions, migrations, and local database commands.
