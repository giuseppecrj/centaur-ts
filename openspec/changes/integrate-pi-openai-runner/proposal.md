## Why

The first real agent harness should follow Centaur's sandbox/stdin/stdout harness protocol while using pi-mono/pi-ai and OpenAI inside that harness layer. pi is an engine/provider implementation detail, not a replacement for Centaur's runtime architecture.

## What Changes

- Add `@earendil-works/pi-ai` dependency where needed by the pi/OpenAI harness implementation.
- Implement pi/OpenAI as a Centaur-compatible harness that receives harness-native NDJSON input and emits Centaur-compatible NDJSON events.
- Convert pi-ai stream events into Centaur harness events, then through the shared harness normalizer into durable/SSE events.
- Preserve deterministic tests with a fake/local harness that uses the same Centaur harness protocol.

## Capabilities

### New Capabilities
- `pi-openai-runner`: Integrate pi OpenAI runner.

### Modified Capabilities

None.

## Impact

Adds runner package implementation, OpenAI configuration, and optional manual smoke path requiring `OPENAI_API_KEY`.
