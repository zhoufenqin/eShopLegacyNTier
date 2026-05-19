# Scenario: Legacy .NET Modernization Assessment

## Scope
- Repository: `D:\a\eShopLegacyNTier\eShopLegacyNTier`
- Solution: `eShopLegacyNTier.sln`
- Assessment-first modernization workflow for legacy .NET Framework projects.

## Settings File
- **`ua-setting.json`**: `D:\a\eShopLegacyNTier\eShopLegacyNTier\.github\upgrades\legacy-dotnet-modernization\ua-setting.json`
- **`UA_SETTINGS_FILE_PATHA`**: `D:\a\eShopLegacyNTier\eShopLegacyNTier\.github\upgrades\legacy-dotnet-modernization\UA_SETTINGS_FILE_PATHA`
  - File content: `D:\a\eShopLegacyNTier\eShopLegacyNTier\.github\upgrades\legacy-dotnet-modernization\ua-setting.json`
  - `ua-setting.json` also retains `UA_SETTINGS_FILE_PATHA` as a mirrored key for machine-readable lookup.

## User Preferences
### Execution Style
- Flow Mode: **Automatic**
- Run workflow end-to-end without pausing unless genuinely blocked.
- Run mode: **assessment-only** — do NOT generate or execute a plan as part of any run unless explicitly instructed otherwise.

### Assessment Output
- All assessment outputs MUST be placed under a **timestamped subfolder** of:
  `D:\a\eShopLegacyNTier\eShopLegacyNTier\.github\upgrades\legacy-dotnet-modernization\assessments\`
- Folder naming convention: `YYYY-MM-DDTHH-mm-ss` (e.g., `2026-05-19T07-11-28`).
- Root `assessment.md` serves as an **index** pointing to the latest timestamped folder.

### Custom Instructions
- Interpret ambiguous request item `2) create ...` as creating standard scenario scaffolding and assessment artifacts.
- Always print full absolute artifact paths.
- Never leave a `plan.md` artifact unless the user explicitly requests plan generation.
- No plan execution: assessment artifacts only until explicitly directed to plan/execute.

## Decisions
- Use scenario folder `.github/upgrades/legacy-dotnet-modernization`.
- Keep current repository branch model and run modernization work on `copilot/add-assessment-setup`.
- `ua-setting.json` is the canonical settings file; `UA_SETTINGS_FILE_PATHA` is also materialized as a standalone pointer file that contains the absolute path to `ua-setting.json`.
- Assessment folder for this run: `assessments/2026-05-19T07-11-28/`.
