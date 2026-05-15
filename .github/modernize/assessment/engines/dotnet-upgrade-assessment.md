# .NET Upgrade Assessment

- workspace-path: `.`
- assessment_dir: `.github/modernize/assessment\engines`
- target-framework: `.NET8`
- resolved target framework moniker: `net8.0`

## Findings

### src\eShopWCFService\eShopWCFService.csproj

- Api.0002 — Source incompatible for selected .NET version
- NuGet.0002 — NuGet package upgrade is recommended
- NuGet.0005 — NuGet package is deprecated
- Project.0001 — Project file needs to be converted to SDK-style
- Project.0002 — Project's target framework(s) needs to be changed

### src\eShopWinForms\eShopWinForms.csproj

- Api.0001 — Binary incompatible for selected .NET version
- Api.0002 — Source incompatible for selected .NET version
- NuGet.0001 — NuGet package is incompatible
- NuGet.0002 — NuGet package upgrade is recommended
- NuGet.0004 — NuGet package contains security vulnerability
- NuGet.0005 — NuGet package is deprecated
- Project.0001 — Project file needs to be converted to SDK-style
- Project.0002 — Project's target framework(s) needs to be changed
