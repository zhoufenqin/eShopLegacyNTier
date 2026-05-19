# Scenario: Legacy .NET Modernization Assessment

## Scope
- Repository: `D:\a\eShopLegacyNTier\eShopLegacyNTier`
- Solution: `eShopLegacyNTier.sln`
- Assessment-first modernization workflow for legacy .NET Framework projects.

## User Preferences
### Execution Style
- Flow Mode: **Automatic**
- Run workflow end-to-end without pausing unless genuinely blocked.

### Custom Instructions
- Interpret ambiguous request item `2) create ...` as creating standard scenario scaffolding and assessment artifacts.
- Always print full absolute artifact paths.

## Decisions
- Use scenario folder `.github/upgrades/legacy-dotnet-modernization`.
- Keep current repository branch model and run modernization work on `modernization/automatic-assessment`.
