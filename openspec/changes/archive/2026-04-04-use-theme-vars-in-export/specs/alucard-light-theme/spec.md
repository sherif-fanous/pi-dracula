## MODIFIED Requirements

### Requirement: HTML export colors from Alucard UI palette

The `export` section SHALL define three background colors derived from the Alucard UI color palette using variable references rather than literal hex values.

The following mappings SHALL be used:

| Export Key | Variable     | Resolved Hex | Source                                     |
| ---------- | ------------ | ------------ | ------------------------------------------ |
| `pageBg`   | `bgDarker`   | `#BCBAB3`    | Alucard UI — Background Darker             |
| `cardBg`   | `background` | `#FFFBEB`    | Alucard Background                         |
| `infoBg`   | `bgLight`    | `#EFEDDC`    | Alucard UI — Floating interactive elements |

#### Scenario: Export section uses required variable mappings

- **WHEN** the `export` section is inspected
- **THEN** `pageBg` SHALL be `bgDarker`, `cardBg` SHALL be `background`, and `infoBg` SHALL be `bgLight`

#### Scenario: Export mappings resolve to the expected Alucard colors

- **WHEN** the `export` variable references are resolved through the theme `vars` section
- **THEN** the resulting colors SHALL be `#BCBAB3` for `pageBg`, `#FFFBEB` for `cardBg`, and `#EFEDDC` for `infoBg`
