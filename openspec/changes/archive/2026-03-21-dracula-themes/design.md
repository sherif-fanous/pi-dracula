## Context

The Dracula theme ecosystem provides two official color palettes — Dracula (dark) and Alucard (light) — with a formal [specification](https://draculatheme.com/spec) covering syntax highlighting, UI colors, and ANSI mappings. The Pi coding agent requires themes to define all 51 color tokens across six categories: Core UI, Backgrounds & Content, Markdown, Tool Diffs, Syntax Highlighting, Thinking Levels, and Bash Mode.

Pi themes are JSON files with a `vars` section (reusable palette) and a `colors` section (token-to-variable mappings). The package structure uses `themes/*.json` discovered via the `pi.themes` manifest in `package.json`.

## Goals / Non-Goals

**Goals:**

- Faithfully implement both Dracula Classic and Alucard Classic palettes using official hex values from the Dracula spec
- Map all 51 Pi color tokens to semantically appropriate Dracula palette colors
- Follow the Dracula Specification for syntax highlighting (Pink=keywords, Green=functions, Cyan=types, etc.)
- Maintain structural symmetry — both themes use identical token-to-variable mappings, differing only in `vars` values
- Include HTML export colors derived from each palette's UI color set

**Non-Goals:**

- Dracula PRO variants (premium, not open source)
- ANSI color overrides (Pi themes don't control terminal ANSI palette)
- Custom font or styling recommendations

## Decisions

### 1. Theme file naming: `dracula.json` and `alucard.json`

**Chosen:** Canonical names from the Dracula project — `dracula` for dark, `alucard` for light.

**Alternatives considered:**

- `dracula-dark.json` / `dracula-light.json` — Redundant; "Dracula" already implies dark. "dracula-light" is semantically confused.
- `dracula-classic.json` / `dracula-alucard.json` — Unnecessarily verbose for Pi's theme selector.

**Rationale:** Every Dracula user knows Alucard is the light variant. Clean names show well in `/settings`.

### 2. Structural symmetry — identical `colors`, different `vars`

Both themes use the same variable names in `vars` (e.g., `purple`, `comment`, `currentLine`) and the same token-to-variable mappings in `colors`. Only the hex values in `vars` differ between dark and light.

**Rationale:** This enforces consistency, simplifies maintenance, and makes the relationship between the two themes immediately clear.

### 3. Accent color: Purple

**Chosen:** `purple` as the Pi `accent` token.

**Alternatives considered:**

- Pink — strong but reserved for keywords in the Dracula spec
- Cyan — used for types/classes, too cool for a primary accent

**Rationale:** Purple (`#BD93F9` dark / `#644AC9` light) is Dracula's signature color for reserved words and constants. It provides excellent contrast on both dark and light backgrounds and is the most distinctively "Dracula" choice.

### 4. No empty-string fallbacks for text tokens

All text-related color tokens use explicit `foreground` variable references rather than `""` (terminal default). This ensures consistent rendering regardless of terminal configuration.

### 5. UI background colors from Dracula's UI palette

The Dracula spec defines UI-specific background shades beyond the main Background:

| Role                       | Dracula   | Alucard   |
| -------------------------- | --------- | --------- |
| Floating/elevated surfaces | `#343746` | `#EFEDDC` |
| Darker recessed surfaces   | `#21222C` | `#CECCC0` |
| Darkest surfaces           | `#191A21` | `#BCBAB3` |

These map to tool backgrounds, user message backgrounds, and export backgrounds.

### 6. Syntax highlighting follows the Dracula Specification directly

| Dracula Spec Rule                    | Pi Token            | Dracula Color |
| ------------------------------------ | ------------------- | ------------- |
| Keywords & Storage → Pink            | `syntaxKeyword`     | `pink`        |
| Functions & Methods → Green          | `syntaxFunction`    | `green`       |
| Classes & Types → Cyan               | `syntaxType`        | `cyan`        |
| Strings & Text → Yellow              | `syntaxString`      | `yellow`      |
| Numbers & Constants → Orange         | `syntaxNumber`      | `orange`      |
| Comments → Comment                   | `syntaxComment`     | `comment`     |
| Variables & Identifiers → Foreground | `syntaxVariable`    | `foreground`  |
| Operators → Pink                     | `syntaxOperator`    | `pink`        |
| Punctuation → Foreground             | `syntaxPunctuation` | `foreground`  |

### 7. Thinking level gradient: cool → warm → hot

Thinking level borders escalate visually through the Dracula palette:

| Level   | Color         | Rationale                                      |
| ------- | ------------- | ---------------------------------------------- |
| Off     | `currentLine` | Dimmest structural color — invisible by design |
| Minimal | `comment`     | Slightly visible — comment-level subtlety      |
| Low     | `cyan`        | Cool, calm — low cognitive intensity           |
| Medium  | `green`       | Noticeable without alarming                    |
| High    | `orange`      | Warm — draws attention                         |
| Xhigh   | `red`         | Hottest — maximum visual urgency               |

## Color Token Mapping

Complete mapping of all 51 Pi tokens. Both themes use these identical variable references:

| Pi Token             | Dracula Variable | Reason                                                 |
| -------------------- | ---------------- | ------------------------------------------------------ |
| `accent`             | `purple`         | Dracula's signature color — reserved words/constants   |
| `border`             | `comment`        | Canonical Dracula border/structural color              |
| `borderAccent`       | `pink`           | Strong contrast for highlighted borders                |
| `borderMuted`        | `currentLine`    | Subtle structural color                                |
| `success`            | `green`          | Semantic match: green = success                        |
| `error`              | `red`            | Semantic match: red = errors                           |
| `warning`            | `orange`         | Semantic match: orange = warning                       |
| `muted`              | `comment`        | Dracula's secondary text color                         |
| `dim`                | `currentLine`    | Dimmer than comment — tertiary text                    |
| `text`               | `foreground`     | Explicit foreground for consistent rendering           |
| `thinkingText`       | `comment`        | Secondary text for thinking blocks                     |
| `selectedBg`         | `currentLine`    | Dracula's selection/current-line background            |
| `userMessageBg`      | `bgLight`        | Slightly elevated surface                              |
| `userMessageText`    | `foreground`     | Explicit foreground                                    |
| `customMessageBg`    | `bgLight`        | Same elevated surface for extension messages           |
| `customMessageText`  | `foreground`     | Explicit foreground                                    |
| `customMessageLabel` | `purple`         | Accent color for labels                                |
| `toolPendingBg`      | `bgDark`         | Recessed surface for pending state                     |
| `toolSuccessBg`      | `bgDark`         | Recessed surface — success indicated by border/title   |
| `toolErrorBg`        | `bgDark`         | Recessed surface — error indicated by border/title     |
| `toolTitle`          | `purple`         | Tool titles match accent                               |
| `toolOutput`         | `comment`        | Tool output as secondary text                          |
| `mdHeading`          | `pink`           | Bold and prominent — keywords color for headings       |
| `mdLink`             | `cyan`           | Types/support color — links are structural references  |
| `mdLinkUrl`          | `comment`        | URLs are secondary information                         |
| `mdCode`             | `green`          | Functions color — inline code is functional/actionable |
| `mdCodeBlock`        | `foreground`     | Full foreground for code readability                   |
| `mdCodeBlockBorder`  | `comment`        | Structural element at comment level                    |
| `mdQuote`            | `yellow`         | Strings color for quoted text — semantic parallel      |
| `mdQuoteBorder`      | `yellow`         | Matching border for quotes                             |
| `mdHr`               | `comment`        | Horizontal rules are structural                        |
| `mdListBullet`       | `cyan`           | Structural markers in types/support color              |
| `toolDiffAdded`      | `green`          | Universal: green = added                               |
| `toolDiffRemoved`    | `red`            | Universal: red = removed                               |
| `toolDiffContext`    | `comment`        | Context lines are secondary                            |
| `syntaxComment`      | `comment`        | Dracula spec: Comments → Comment                       |
| `syntaxKeyword`      | `pink`           | Dracula spec: Keywords & Storage → Pink                |
| `syntaxFunction`     | `green`          | Dracula spec: Functions & Methods → Green              |
| `syntaxVariable`     | `foreground`     | Dracula spec: Variables & Identifiers → Foreground     |
| `syntaxString`       | `yellow`         | Dracula spec: Strings & Text → Yellow                  |
| `syntaxNumber`       | `orange`         | Dracula spec: Numbers & Constants → Orange             |
| `syntaxType`         | `cyan`           | Dracula spec: Classes & Types → Cyan                   |
| `syntaxOperator`     | `pink`           | Operators relate to keywords/control flow              |
| `syntaxPunctuation`  | `foreground`     | Dracula spec: braces/parens match foreground           |
| `thinkingOff`        | `currentLine`    | Dimmest structural color                               |
| `thinkingMinimal`    | `comment`        | Comment-level subtlety                                 |
| `thinkingLow`        | `cyan`           | Cool color — low intensity                             |
| `thinkingMedium`     | `green`          | Noticeable without alarming                            |
| `thinkingHigh`       | `orange`         | Warm — draws attention                                 |
| `thinkingXhigh`      | `red`            | Maximum visual urgency                                 |
| `bashMode`           | `orange`         | Distinct from purple accent — clear mode indicator     |

## Risks / Trade-offs

- **[Dracula's Current Line ambiguity]** → The README palette lists Current Line as `#44475A` while the spec lists it as `#6272A4` (same as Comment). We use the README values which are what 400+ implementations use. The `currentLine` var is `#44475A` (dark) / `#6C664B` (light), distinct from `comment` at `#6272A4` / `#6C664B`. Note: for Alucard, Current Line and Comment share the same value (`#6C664B`) per the official palette — this is intentional.
- **[No terminal ANSI control]** → Pi themes cannot override the terminal's ANSI color palette. Users with a Dracula terminal theme will get the best experience. Mitigation: all tokens use explicit hex values via vars, not ANSI indices.
- **[Identical tool backgrounds]** → `toolPendingBg`, `toolSuccessBg`, and `toolErrorBg` all use `bgDark`. State differentiation comes from border/title colors. This follows the Dracula approach of minimal background variation with accent-driven state indication.
