## 1. Dracula Dark Theme

- [x] 1.1 Create `themes/dracula.json` with `$schema`, `name` set to `"dracula"`, `vars` section containing all 14 Dracula Classic palette variables with exact hex values from the spec, `colors` section mapping all 51 Pi tokens to variable references per the Color Token Mapping in design.md, and `export` section with `pageBg`, `cardBg`, `infoBg` from the Dracula UI palette

## 2. Alucard Light Theme

- [x] 2.1 Create `themes/alucard.json` with `$schema`, `name` set to `"alucard"`, `vars` section containing all 14 Alucard Classic palette variables with exact hex values from the spec, `colors` section identical to `dracula.json` (same token-to-variable mappings), and `export` section with `pageBg`, `cardBg`, `infoBg` from the Alucard UI palette

## 3. Verification

- [x] 3.1 Verify both theme files contain all 51 required color tokens with no missing or extra keys
- [x] 3.2 Verify the `colors` sections of both themes are identical (structural symmetry)
- [x] 3.3 Verify all `colors` values reference keys that exist in the respective `vars` section — no literal hex values, no empty strings
