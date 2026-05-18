# .NET Upgrade Assessment (.NET 8)

- workspace-path: `.`
- assessment_dir: `.github/modernize/assessment\engines`
- target-framework: `.NET8` (`net8.0`)
- solution: `D:\a\eShopLegacyNTier\eShopLegacyNTier\eShopLegacyNTier.sln`

## Project findings

### src\eShopWCFService\eShopWCFService.csproj
- Api.0002  Source incompatible for selected .NET version
- NuGet.0002  NuGet package upgrade is recommended
- NuGet.0005  NuGet package is deprecated
- Project.0001  Project file needs to be converted to SDK-style
- Project.0002  Project's target framework(s) needs to be changed

### src\eShopWinForms\eShopWinForms.csproj
- Api.0001  Binary incompatible for selected .NET version
- Api.0002  Source incompatible for selected .NET version
- NuGet.0001  NuGet package is incompatible
- NuGet.0002  NuGet package upgrade is recommended
- NuGet.0004  NuGet package contains security vulnerability
- NuGet.0005  NuGet package is deprecated
- Project.0001  Project file needs to be converted to SDK-style
- Project.0002  Project's target framework(s) needs to be changed

## Available target frameworks
- net8.0 (.NET 8, LTS)
- net9.0 (.NET 9, STS)
- net10.0 (.NET 10, LTS)
- net11.0 (.NET 11, Preview)