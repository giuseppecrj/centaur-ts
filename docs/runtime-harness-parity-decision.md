# Runtime and harness parity decision

Date: 2026-05-26

## Decision

`centaur-ts` follows Centaur's runtime architecture for agent execution.

The runtime is not a direct `OpenAI -> response` SDK loop. It is a Centaur-compatible sandbox/harness protocol:

```text
API/control plane
  -> create or reuse sandbox session
  -> attach to sandbox stdin/stdout
  -> write harness-native NDJSON input to stdin
  -> read harness-native NDJSON output from stdout
  -> normalize raw harness events
  -> persist session and turn state
  -> stream canonical events over SSE
  -> detect terminal turn events
  -> persist final turn result before emitting terminal event
```

`@earendil-works/pi-ai` is allowed and expected, but it is not the architecture. It should be used inside a harness/provider implementation where appropriate. The surrounding runtime model remains Centaur's sandbox/session/event protocol.

## Consequences

- Build `packages/harness-protocol` early.
- Port Centaur's harness protocol semantics:
  - `build_user_input`
  - `messages_to_content_blocks`
  - `is_turn_done`
  - `extract_result`
  - `extract_thread_id`
  - harness event normalization
- Build `packages/sandbox` early with a `SandboxBackend` interface matching Centaur's model:
  - `create`
  - `attach`
  - `writeStdin`
  - `streamStdout`
  - `stop`
  - `status`
  - `interruptById`
  - `refreshTokenById`
  - warm-pool recovery seam
- Treat `pi-mono` as a Centaur harness/engine option, like Centaur does.
- Do not implement the first real runtime as `POST /execute -> call OpenAI via pi-ai -> save answer`.
- A fake/local harness for tests must still emit Centaur-compatible NDJSON events.
- The API event stream should follow Centaur's persistent SSE wire model, including `wire.ready`, lease heartbeat, normalized events, and terminal `turn.done` behavior.

## Implementation order adjustment

Before implementing the OpenAI/pi runner, implement the runtime substrate:

1. `packages/harness-protocol`
2. `packages/sandbox`
3. Centaur-compatible session state in `packages/db` and `packages/control-plane`
4. Hono API routes for spawn/connect/inject/execute/event streaming
5. fake/local Centaur-compatible harness
6. pi-mono or pi-ai-backed harness implementation

## Non-goal

Do not simplify Centaur's runner into a direct model-call abstraction unless explicitly approved.
