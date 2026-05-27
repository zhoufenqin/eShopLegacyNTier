# Configuration & Externalized Settings Inventory

This inventory captures configuration sources, profile behavior, sensitive settings, and runtime-related configuration for eShopLegacyNTier.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| WCF service config | XML config | `src/eShopWCFService/Web.config` | ServiceModel endpoints, metadata, connection string, EF provider |
| WinForms config | XML config | `src/eShopWinForms/App.config` | WCF client endpoint address and binding |
| Project file config | MSBuild XML | `src/eShopWCFService/eShopWCFService.csproj` | Build properties, framework target, IIS Express settings |
| Project file config | MSBuild XML | `src/eShopWinForms/eShopWinForms.csproj` | Framework target, build output config |
| Package declarations | NuGet packages.config | `src/**/packages.config` | Declared package versions |
| Environment variable | Process env | `ConnectionString` | Optional override for default EF connection name |

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| Debug | `Configuration=Debug` | Local development builds with symbols | Standard .NET Framework build targets |
| Release | `Configuration=Release` | Optimized production build output | Standard .NET Framework build targets |

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| Default runtime | Service host startup | `Web.config`, `App.config` | Basic HTTP endpoint and SQL LocalDB connection |
| ConnectionString override | Environment variable `ConnectionString` | Runtime environment | Replaces `name=EntityModel` resolution in service |

## Properties Inventory

| Property Key | Default | Profiles | Source |
|---|---|---|---|
| connectionStrings:EntityModel | `(localdb)\MSSQLLocalDB;Initial Catalog=eShopDatabase` | Default | `Web.config` |
| system.serviceModel/services/service endpoint | `basicHttpBinding` on `/CatalogService.svc` | Default | `Web.config` |
| system.serviceModel/client endpoint address | `http://localhost:62314/CatalogService.svc` | Default | `App.config` |
| aspnet:UseTaskFriendlySynchronizationContext | `true` | Default | `Web.config` |
| ConnectionString | Not set | Environment override | Environment variable |

## Startup Parameters & Resource Requirements

| Service | JVM/Runtime Options | Memory | Instance Count |
|---|---|---|---|
| eShopWCFService | .NET Framework service hosted in IIS/IIS Express | Not explicitly configured | Single local instance expected |
| eShopWinForms | .NET Framework desktop executable | Not explicitly configured | Single desktop process |

## Startup Dependency Chain

1. SQL Server LocalDB availability  required by `eShopWCFService` data context initialization.
2. `eShopWCFService` host startup (`CatalogService.svc`)  required before client calls.
3. `eShopWinForms` startup and service proxy initialization  depends on running WCF endpoint.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage (masked) |
|---|---|---|
| `connectionStrings:EntityModel` | Database connection string | Stored in `Web.config` (no secret value masking in file) |
| `ConnectionString` environment variable | Database connection string override | Environment source `[MASKED]` |

### Secrets Provisioning Workflow

Current configuration primarily uses file-based settings and optional environment override. A deployment/runtime environment can provide `ConnectionString` to replace the default named connection at startup; no dedicated secret vault integration is configured in repository files.

## Feature Flags

| Flag Name | Default | Controlled By |
|---|---|---|
| None detected | N/A | N/A |

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| .NET Framework (WCF Service) | 4.6.1 | `eShopWCFService.csproj` |
| .NET Framework (WinForms) | 4.7 | `eShopWinForms.csproj` |
| Entity Framework | 6.1.3 | `packages.config` |
| Newtonsoft.Json | 6.0.4 | `eShopWCFService/packages.config` |
| Microsoft.AspNet.WebApi.Client | 5.2.3 | `eShopWCFService/packages.config` |
| WCF basicHttpBinding | Framework-provided | `Web.config`, `App.config` |
