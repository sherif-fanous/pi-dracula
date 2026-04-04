## Context

This repository contains two Pi theme files, `themes/dracula.json` and `themes/alucard.json`, plus corresponding OpenSpec capability specs. Both themes already define shared palette entries in `vars` and use those variables throughout `colors`, but their `export` sections still duplicate the same palette values as literal hex strings.

Pi's theme runtime now resolves `export` colors through the same variable-resolution path used for normal theme colors. That means the repository can express export colors in the same style as the rest of each theme without changing the resulting rendered colors.

The change is small in code footprint but cross-cuts source-of-truth concerns:
- theme JSON files must be updated
- capability specs must be updated to require variable references rather than exact literal hex values
- the change should preserve the current resolved export colors exactly

## Goals / Non-Goals

**Goals:**
- Make `export.pageBg`, `export.cardBg`, and `export.infoBg` reference existing theme vars instead of duplicating hex literals.
- Preserve the exact effective export colors for both themes after resolution.
- Update the related capability specs so requirements match the intended representation.
- Keep Dracula and Alucard structurally aligned, using the same token-to-var pattern across both themes.

**Non-Goals:**
- Changing any palette values in `vars`.
- Redesigning export styling or adding new export fields.
- Introducing new theme variables solely for this migration.
- Modifying unrelated theme color mappings.

## Decisions

### 1. Use existing vars for export values
The `export` section will reference existing vars rather than introduce new dedicated export vars.

Chosen mappings:
- `pageBg -> bgDarker`
- `cardBg -> background`
- `infoBg -> bgLight`

Rationale:
- These already match the current literal export values in both themes.
- Reusing existing vars keeps each palette authoritative in one place.
- It avoids unnecessary variable proliferation.

Alternative considered:
- Add export-specific vars such as `exportPageBg`, `exportCardBg`, `exportInfoBg`.
- Rejected because the export colors are not semantically distinct from the existing palette entries; extra vars would only duplicate meaning.

### 2. Change the specs to require variable-referenced export values
The capability specs will be updated so the requirement is about representation as vars, not just resolved color outcome.

Rationale:
- The user's requested change is normative: the files should use vars, not literals.
- Keeping the specs at literal hexs would make the implementation and specs contradict each other.

Alternative considered:
- Allow either literal hex or var references in the spec.
- Rejected because it weakens the intended repository convention and would not fully capture the desired cleanup.

### 3. Preserve resolved color behavior exactly
Although representation changes, the effective colors must remain identical to today's output.

Rationale:
- This keeps the change low risk.
- It limits the blast radius to maintainability and consistency rather than visible rendering changes.

Alternative considered:
- Use different nearby palette vars to refine export contrast.
- Rejected because that would turn a representation cleanup into a visual design change.

### 4. Keep both theme files parallel
Dracula and Alucard should continue mirroring each other structurally, with different underlying var values but equivalent export mappings.

Rationale:
- The repo already treats Alucard as the light-theme counterpart to Dracula.
- Structural parity makes future maintenance easier and spec comparison simpler.

## Risks / Trade-offs

- **[Spec wording could become too implementation-specific]** -> Mitigation: describe the requirement in terms of variable references that resolve to the existing palette colors, not arbitrary JSON formatting details.
- **[Pi behavior could differ across versions]** -> Mitigation: base the change on the current runtime behavior already investigated in Pi source, and keep the change scoped to this repo's supported workflow.
- **[A future var rename would affect export and colors together]** -> Mitigation: accept this as an intentional trade-off of using a single source of truth; if vars change later, dependent mappings should change with them.
- **[Readers may expect exact hex values from current specs]** -> Mitigation: update the specs clearly so the new convention is explicit.

## Migration Plan

1. Update the Dracula and Alucard capability specs to require variable-referenced export values with the chosen mappings.
2. Update `themes/dracula.json` and `themes/alucard.json` so `export` uses those vars.
3. Verify that the resolved export colors remain equivalent to the previous literal hex values.
4. Review the diff to ensure only the intended export representation and corresponding spec text changed.

Rollback strategy:
- Revert the spec changes and theme file changes together, restoring literal hex values in `export`.

## Open Questions

- None currently. The main compatibility question was whether Pi resolves vars in `export`, and that has already been confirmed for the current runtime.