## Why

Centaur’s security model depends on agents using capabilities without receiving raw long-lived secrets. The rebuild needs a credential and egress boundary before real tools or sandboxes handle sensitive systems.

## What Changes

- Model secret declarations and bindings separately from tool definitions.
- Implement secret provider interface with environment-backed local provider first.
- Add sanitization and policy checks so secrets are never persisted in events.
- Define proxy/egress configuration rendering seam for future iron-proxy-like behavior.

## Capabilities

### New Capabilities
- `secret-egress-boundary`: Add secret and egress boundary.

### Modified Capabilities

None.

## Impact

Adds security package/module, secret binding schema, policy checks, event sanitization, and sandbox/tool integration points.
