## MODIFIED Requirements

### Requirement: HTML export colors from Dracula UI palette

The `export` section SHALL define three background colors derived from the Dracula UI color palette using variable references rather than literal hex values.

The following mappings SHALL be used:

| Export Key | Variable     | Resolved Hex | Source                                     |
| ---------- | ------------ | ------------ | ------------------------------------------ |
| `pageBg`   | `bgDarker`   | `#191A21`    | Dracula UI — Background Darker             |
| `cardBg`   | `background` | `#282A36`    | Dracula Background                         |
| `infoBg`   | `bgLight`    | `#343746`    | Dracula UI — Floating interactive elements |

#### Scenario: Export section uses required variable mappings

- **WHEN** the `export` section is inspected
- **THEN** `pageBg` SHALL be `bgDarker`, `cardBg` SHALL be `background`, and `infoBg` SHALL be `bgLight`

#### Scenario: Export mappings resolve to the expected Dracula colors

- **WHEN** the `export` variable references are resolved through the theme `vars` section
- **THEN** the resulting colors SHALL be `#191A21` for `pageBg`, `#282A36` for `cardBg`, and `#343746` for `infoBg`
