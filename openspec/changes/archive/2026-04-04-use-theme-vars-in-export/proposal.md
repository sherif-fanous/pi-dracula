## Why

Pi's theme runtime now supports variable references in the `export` section, but this repo's theme files still use hard-coded hex values there. Capturing this as a change lets us update the specs and theme definitions together so the repository reflects current Pi behavior and uses a single source of truth for shared palette values.

## What Changes

- Update the Dracula and Alucard theme requirements so the `export` section uses theme variables rather than literal hex values.
- Align the theme files with those updated requirements by mapping `export.pageBg`, `export.cardBg`, and `export.infoBg` to existing palette vars.
- Document the compatibility assumption behind this change: Pi resolves `export` values through the same variable resolution path used by `colors`.

## Capabilities

### New Capabilities

- None.

### Modified Capabilities

- `dracula-dark-theme`: Change the export section requirement from exact literal hex values to variable-referenced values that resolve to the same Dracula palette colors.
- `alucard-light-theme`: Change the export section requirement from exact literal hex values to variable-referenced values that resolve to the same Alucard palette colors.

## Impact

- Affected files: `themes/dracula.json`, `themes/alucard.json`
- Affected specs: `openspec/specs/dracula-dark-theme/spec.md`, `openspec/specs/alucard-light-theme/spec.md`
- No API changes or external dependency changes
- Low implementation risk because the resolved output colors remain the same; the primary change is how those colors are expressed in the theme files
