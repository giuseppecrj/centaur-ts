# Centaur parity decisions

Date: 2026-05-26

The project direction is now strict Centaur parity from day 1.

## Core decision

`centaur-ts` is a TypeScript rewrite of Centaur, not a simplified product inspired by Centaur. The architecture, boundaries, contracts, and operational semantics should match Centaur unless a TypeScript-specific implementation detail requires translation.

When an OpenSpec question asks how to handle behavior that Centaur already defines, the answer is: **follow Centaur**.

## Decisions from review questions

1. **Tenancy / ownership:** follow Centaur from day 1. Do not assume a reduced single-tenant architecture if Centaur models broader ownership or workspace semantics.
2. **Auth timing:** protect non-health routes from the start, matching Centaur's intended security posture.
3. **Event transport:** use SSE or whichever event streaming/replay mechanism Centaur uses. The TypeScript rewrite should preserve the Centaur client contract.
4. **Schema ownership:** model everything Centaur models. Drizzle migrations should represent Centaur's complete durable state architecture, translated to TypeScript/Drizzle/Postgres.
5. **Cancellation / execution semantics:** follow Centaur's execution, release, cancellation, event, and final delivery behavior.
6. **Secrets / egress:** follow Centaur's credential firewall and proxy/egress model. Do not weaken raw-secret boundaries for convenience.
7. **Sandbox:** follow Centaur's sandbox architecture and isolation model from day 1, translated into TypeScript interfaces and implementations.
8. **Runner:** follow Centaur's agent harness semantics. The OpenAI/pi implementation should fit the same harness/control-plane architecture rather than inventing a new simplified loop.
9. **Tools / workflows / overlays / delivery / observability:** follow Centaur's architecture and contracts unless a deliberate deviation is documented and approved.

## Implementation rule

Before implementing each OpenSpec change, inspect the corresponding Centaur source and research docs, then translate the architecture into the TypeScript stack:

- Bun workspaces/package management
- Hono API
- Drizzle/Postgres schemas and migrations
- Zod contracts/types
- `@earendil-works/pi-ai` for LLM SDK integration
- OpenAI provider for the first real model path

Do not replace Centaur behavior with a smaller MVP unless explicitly requested.
