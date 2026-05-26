## Why

Centaur is a capability control plane, not just an LLM proxy. Tool definitions and invocations must be declared, validated, audited, and routed through a controlled boundary.

## What Changes

- Add tool definition registry with Zod input/output schemas and secret declarations.
- Expose tool listing and invocation APIs for approved tools.
- Persist tool call audit events and connect runner tool calls to registry invocation.

## Capabilities

### New Capabilities
- `tool-registry-invocation`: Add tool registry and invocation.

### Modified Capabilities

None.

## Impact

Adds capability package or control-plane module, new API routes, DB tables/events, and runner tool-call handling.
