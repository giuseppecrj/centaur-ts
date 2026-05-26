## Why

Even a self-hosted control plane needs a clear authentication boundary before Slack, browser, or remote clients use it. API keys provide the first durable admin and client authentication primitive.

## What Changes

- Add hashed API key creation, verification, revocation, and last-used tracking.
- Protect non-health routes with scope checks while preserving explicit local-dev behavior.
- Expose minimal admin endpoints for API-key lifecycle.

## Capabilities

### New Capabilities
- `api-key-auth-admin`: Add API key auth and admin.

### Modified Capabilities

None.

## Impact

Uses `api_keys` table, modifies API dependencies/middleware, adds admin routes.
