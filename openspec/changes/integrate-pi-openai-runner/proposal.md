## Why

The first real agent harness should use the user-selected pi-mono LLM SDK and OpenAI provider while preserving deterministic tests through the same runner interface.

## What Changes

- Add `@earendil-works/pi-ai` dependency and OpenAI runner implementation.
- Convert stored message parts into pi SDK input.
- Stream or collect assistant output into durable execution events.
- Keep fake runner as the default test runner.

## Capabilities

### New Capabilities
- `pi-openai-runner`: Integrate pi OpenAI runner.

### Modified Capabilities

None.

## Impact

Adds runner package implementation, OpenAI configuration, and optional manual smoke path requiring `OPENAI_API_KEY`.
