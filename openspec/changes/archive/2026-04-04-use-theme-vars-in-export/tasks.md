## 1. Update specifications

- [x] 1.1 Update the `dracula-dark-theme` delta spec so the export requirement mandates variable references for `pageBg`, `cardBg`, and `infoBg`
- [x] 1.2 Update the `alucard-light-theme` delta spec so the export requirement mandates variable references for `pageBg`, `cardBg`, and `infoBg`
- [x] 1.3 Review both delta specs to confirm they preserve the current resolved export colors while changing only the required representation

## 2. Update theme files

- [x] 2.1 Change `themes/dracula.json` so `export.pageBg`, `export.cardBg`, and `export.infoBg` reference `bgDarker`, `background`, and `bgLight`
- [x] 2.2 Change `themes/alucard.json` so `export.pageBg`, `export.cardBg`, and `export.infoBg` reference `bgDarker`, `background`, and `bgLight`
- [x] 2.3 Review both theme files to confirm no palette values or unrelated color mappings changed

## 3. Verify resolved behavior

- [x] 3.1 Verify the Dracula export mappings still resolve to `#191A21`, `#282A36`, and `#343746`
- [x] 3.2 Verify the Alucard export mappings still resolve to `#BCBAB3`, `#FFFBEB`, and `#EFEDDC`
- [x] 3.3 Review the final diff to confirm the change is limited to spec updates and export representation cleanup
