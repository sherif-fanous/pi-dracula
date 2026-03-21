## ADDED Requirements

### Requirement: Valid Pi theme file at themes/alucard.json

The file `themes/alucard.json` SHALL be a valid Pi theme JSON file containing a `$schema` reference, `name` set to `"alucard"`, a `vars` section, a `colors` section with all 51 required tokens, and an `export` section.

#### Scenario: Theme file passes Pi schema validation

- **WHEN** Pi loads `themes/alucard.json`
- **THEN** the file SHALL contain all 51 required color tokens and no unknown keys

### Requirement: Alucard Classic light palette in vars

The `vars` section SHALL define reusable color variables using exact hex values from the official Alucard Classic palette as documented in the Dracula theme README.

The following variables SHALL be defined with these exact values:

| Variable      | Hex Value | Source                                     |
| ------------- | --------- | ------------------------------------------ |
| `background`  | `#FFFBEB` | Alucard Background                         |
| `currentLine` | `#6C664B` | Alucard Current Line                       |
| `foreground`  | `#1F1F1F` | Alucard Foreground                         |
| `comment`     | `#6C664B` | Alucard Comment                            |
| `cyan`        | `#036A96` | Alucard Cyan                               |
| `green`       | `#14710A` | Alucard Green                              |
| `orange`      | `#A34D14` | Alucard Orange                             |
| `pink`        | `#A3144D` | Alucard Pink                               |
| `purple`      | `#644AC9` | Alucard Purple                             |
| `red`         | `#CB3A2A` | Alucard Red                                |
| `yellow`      | `#846E15` | Alucard Yellow                             |
| `bgLight`     | `#EFEDDC` | Alucard UI — Floating interactive elements |
| `bgDark`      | `#CECCC0` | Alucard UI — Background Dark               |
| `bgDarker`    | `#BCBAB3` | Alucard UI — Background Darker             |

#### Scenario: All palette variables present with correct values

- **WHEN** the `vars` section is inspected
- **THEN** every variable listed above SHALL be present with its exact hex value

### Requirement: Token-to-variable mapping in colors

The `colors` section SHALL map all 51 Pi color tokens to variable names defined in `vars`. No token SHALL use a literal hex value — all SHALL reference variables. No token SHALL use an empty string (`""`) — all SHALL reference a named variable. The mapping SHALL be identical to the Dracula dark theme — only the `vars` values differ.

#### Scenario: All 51 tokens reference variables

- **WHEN** the `colors` section is inspected
- **THEN** every value SHALL be a string matching a key in the `vars` section

#### Scenario: Color mappings match Dracula theme

- **WHEN** the `colors` sections of `dracula.json` and `alucard.json` are compared
- **THEN** they SHALL be identical — same token-to-variable mappings

### Requirement: Syntax highlighting follows Dracula Specification

Syntax highlighting tokens SHALL follow the official Dracula Specification token classification rules, using the Alucard palette values.

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

### Requirement: HTML export colors from Alucard UI palette

The `export` section SHALL define three background colors derived from the Alucard UI color palette:

| Export Key | Hex Value | Source                                     |
| ---------- | --------- | ------------------------------------------ |
| `pageBg`   | `#BCBAB3` | Alucard UI — Background Darker             |
| `cardBg`   | `#FFFBEB` | Alucard Background                         |
| `infoBg`   | `#EFEDDC` | Alucard UI — Floating interactive elements |

#### Scenario: Export section present with correct values

- **WHEN** the `export` section is inspected
- **THEN** `pageBg`, `cardBg`, and `infoBg` SHALL be present with the exact hex values above
