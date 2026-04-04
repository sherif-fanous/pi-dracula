## Purpose

Specification for the Dracula Classic dark theme (`themes/dracula.json`) — a Pi coding agent theme implementing the official Dracula dark palette.

## Requirements

### Requirement: Valid Pi theme file at themes/dracula.json

The file `themes/dracula.json` SHALL be a valid Pi theme JSON file containing a `$schema` reference, `name` set to `"dracula"`, a `vars` section, a `colors` section with all 51 required tokens, and an `export` section.

#### Scenario: Theme file passes Pi schema validation

- **WHEN** Pi loads `themes/dracula.json`
- **THEN** the file SHALL contain all 51 required color tokens and no unknown keys

### Requirement: Dracula Classic dark palette in vars

The `vars` section SHALL define reusable color variables using exact hex values from the official Dracula Classic palette as documented in the Dracula theme README.

The following variables SHALL be defined with these exact values:

| Variable      | Hex Value | Source                                     |
| ------------- | --------- | ------------------------------------------ |
| `background`  | `#282A36` | Dracula Background                         |
| `currentLine` | `#44475A` | Dracula Current Line / Selection           |
| `foreground`  | `#F8F8F2` | Dracula Foreground                         |
| `comment`     | `#6272A4` | Dracula Comment                            |
| `cyan`        | `#8BE9FD` | Dracula Cyan                               |
| `green`       | `#50FA7B` | Dracula Green                              |
| `orange`      | `#FFB86C` | Dracula Orange                             |
| `pink`        | `#FF79C6` | Dracula Pink                               |
| `purple`      | `#BD93F9` | Dracula Purple                             |
| `red`         | `#FF5555` | Dracula Red                                |
| `yellow`      | `#F1FA8C` | Dracula Yellow                             |
| `bgLight`     | `#343746` | Dracula UI — Floating interactive elements |
| `bgDark`      | `#21222C` | Dracula UI — Background Dark               |
| `bgDarker`    | `#191A21` | Dracula UI — Background Darker             |

#### Scenario: All palette variables present with correct values

- **WHEN** the `vars` section is inspected
- **THEN** every variable listed above SHALL be present with its exact hex value

### Requirement: Token-to-variable mapping in colors

The `colors` section SHALL map all 51 Pi color tokens to variable names defined in `vars`. No token SHALL use a literal hex value — all SHALL reference variables. No token SHALL use an empty string (`""`) — all SHALL reference a named variable.

#### Scenario: All 51 tokens reference variables

- **WHEN** the `colors` section is inspected
- **THEN** every value SHALL be a string matching a key in the `vars` section

### Requirement: Syntax highlighting follows Dracula Specification

Syntax highlighting tokens SHALL follow the official Dracula Specification token classification rules.

| Pi Token            | Variable     | Dracula Spec Rule                    |
| ------------------- | ------------ | ------------------------------------ |
| `syntaxKeyword`     | `pink`       | Keywords & Storage → Pink            |
| `syntaxFunction`    | `green`      | Functions & Methods → Green          |
| `syntaxType`        | `cyan`       | Classes & Types → Cyan               |
| `syntaxString`      | `yellow`     | Strings & Text → Yellow              |
| `syntaxNumber`      | `orange`     | Numbers & Constants → Orange         |
| `syntaxComment`     | `comment`    | Comments → Comment                   |
| `syntaxVariable`    | `foreground` | Variables & Identifiers → Foreground |
| `syntaxOperator`    | `pink`       | Operators → Pink (keywords family)   |
| `syntaxPunctuation` | `foreground` | Braces/parens → Foreground           |

#### Scenario: Syntax tokens match Dracula spec

- **WHEN** the syntax highlighting tokens are inspected
- **THEN** each token SHALL map to the variable specified in the table above

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
