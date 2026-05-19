# Assessment

## Repository Baseline
- Workspace: `D:\a\eShopLegacyNTier\eShopLegacyNTier`
- Solution: `D:\a\eShopLegacyNTier\eShopLegacyNTier\eShopLegacyNTier.sln`
- Projects discovered:
  - `src\eShopWinForms\eShopWinForms.csproj` (WinForms, .NET Framework **v4.7**)
  - `src\eShopWCFService\eShopWCFService.csproj` (ASP.NET/WCF web app, .NET Framework **v4.6.1**)

## Project System / Tooling
- Both projects are **legacy non-SDK csproj** format.
- Dependencies are managed via `packages.config` and assembly `HintPath` references.
- Solution metadata indicates Visual Studio legacy format (`Visual Studio 15`, minimum `10.0`).

## Dependency Findings
- `EntityFramework` 6.1.3
- `Microsoft.AspNet.WebApi.Client` 5.2.3 (WinForms client)
- `Newtonsoft.Json` 6.0.4 (WinForms client)
- WCF service references present in WinForms connected service metadata and `.svcmap`.

## Build/Validation Baseline
Command run:
- `dotnet build D:\a\eShopLegacyNTier\eShopLegacyNTier\eShopLegacyNTier.sln -v minimal`

Observed blockers:
1. Missing web application targets:
   - `Microsoft.WebApplication.targets` import not found for `eShopWCFService.csproj`.
2. Missing restored assemblies for legacy package references in WinForms:
   - `EntityFramework`, `EntityFramework.SqlServer`, `Newtonsoft.Json`, `System.Net.Http.Formatting`.
3. Resource generation compatibility errors on WinForms under current CLI-only build path:
   - `MSB3822`, `MSB3823` (non-string resources / System.Resources.Extensions).

## Modernization Risk/Complexity
- **High**: mixed desktop + WCF web-hosted service on full framework, legacy project format, service references, and old package versions.
- Recommended phased migration:
  1) Stabilize build reproducibility in CI/CLI.
  2) Convert project format/dependency management.
  3) Migrate service stack and client contract integration.
