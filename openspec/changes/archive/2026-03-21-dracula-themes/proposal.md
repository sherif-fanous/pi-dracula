## Why

The pi-dracula package needs its two theme files — Dracula (dark) and Alucard (light) — created to ship as a Pi coding agent theme package. The Dracula theme ecosystem spans 400+ applications and has an official color specification. This change implements that specification as Pi themes, mapping the Dracula palette to all 51 Pi color tokens.

## What Changes

- Add `themes/dracula.json` — dark theme using the Dracula Classic palette
- Add `themes/alucard.json` — light theme using the Alucard Classic palette
- Both themes follow the official [Dracula Specification](https://draculatheme.com/spec) for color accuracy and syntax highlighting rules
- Both themes share identical token-to-variable mappings, differing only in palette values

## Capabilities

### New Capabilities

- `dracula-dark-theme`: Dracula Classic dark theme — maps the Dracula dark palette to all 51 Pi color tokens with syntax highlighting per the Dracula spec
- `alucard-light-theme`: Alucard Classic light theme — maps the Alucard light palette to all 51 Pi color tokens with syntax highlighting per the Dracula spec

### Modified Capabilities

_(none — this is the initial release)_

## Impact

- Creates `themes/` directory with two JSON files
- No runtime dependencies — themes are static JSON consumed by Pi's theme loader
- Package discovery relies on the `pi.themes` manifest in `package.json` (already configured)
