## Why

Centaur’s platform/overlay split lets organizations add tools, prompts, skills, and workflows without forking the kernel. The TypeScript rebuild needs this extension seam early, even if loading starts from local files.

## What Changes

- Define overlay manifest schema and package layout.
- Load local overlays containing prompts, skills, tools, and workflows.
- Merge overlay content into runner prompt bundles and capability registries.

## Capabilities

### New Capabilities
- `extension-overlay-model`: Add extension overlay model.

### Modified Capabilities

None.

## Impact

Adds overlay contracts, loader package/module, sample overlay, and runner/control-plane integration.
