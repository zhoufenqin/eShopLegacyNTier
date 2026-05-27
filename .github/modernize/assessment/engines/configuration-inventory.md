# Configuration & Externalized Settings Inventory

This solution uses two XML-based .NET Framework configuration files (`Web.config` and `App.config`) as its sole configuration sources, with no runtime profiles, secret stores, or feature flag frameworks.

## Configuration Sources

| Source | Type | Path/Location | Notes |
|---|---|---|---|
| Web.config | XML (.NET Framework app config) | `src/eShopWCFService/Web.config` | Service-side config: EF connection string, WCF service endpoints, ASP.NET compilation settings |
| App.config | XML (.NET Framework app config) | `src/eShopWinForms/App.config` | Client-side config: WCF client endpoint address, .NET 4.7 runtime declaration, Windows Forms DPI settings |
| Environment variable | Runtime override | `ConnectionString` (env var) | Read in `CatalogConfiguration.cs`; overrides the `EntityModel` named connection string when set |

No external config servers (Spring Cloud Config, Azure App Configuration), Kubernetes ConfigMaps/Secrets, Docker Compose environment sections, or `.env` files are used.

## Build Profiles

| Profile | Activation | Purpose | Key Dependencies/Plugins |
|---|---|---|---|
| Debug | Default / Visual Studio IDE | Development build with debug symbols and full debug output | `DebugSymbols=true`, `DebugType=full`, `Optimize=false` |
| Release | Manual (`/p:Configuration=Release`) | Optimized build for deployment | `DebugType=pdbonly`, `Optimize=true` |

No Maven/Gradle profiles, MSBuild custom targets, or conditional compilation symbols beyond `DEBUG` and `TRACE` are defined.

## Runtime Profiles

| Profile | Activation Method | Config Files | Key Overrides |
|---|---|---|---|
| Default (single profile) | No profile switching; static config files only | `Web.config`, `App.config` | `ConnectionString` environment variable can override the database connection at runtime |

There are no `appsettings.Development.json`, `appsettings.Production.json`, or `application-{profile}.yml` equivalents. The application uses a single static configuration for all environments. No `ASPNETCORE_ENVIRONMENT` or Spring profile mechanism is in use.

## Properties Inventory

### eShopWCFService (Web.config)

| Property Key | Default Value | Profiles | Source |
|---|---|---|---|
| `aspnet:UseTaskFriendlySynchronizationContext` | `true` | All | `Web.config` appSettings |
| `compilation[@debug]` | `true` | All | `Web.config` system.web |
| `compilation[@targetFramework]` | `4.6.1` | All | `Web.config` system.web |
| `httpRuntime[@targetFramework]` | `4.6.1` | All | `Web.config` system.web |
| WCF `serviceMetadata[@httpGetEnabled]` | `true` | All | `Web.config` system.serviceModel |
| WCF `serviceMetadata[@httpsGetEnabled]` | `true` | All | `Web.config` system.serviceModel |
| WCF `serviceDebug[@includeExceptionDetailInFaults]` | `false` | All | `Web.config` system.serviceModel |
| WCF `protocolMapping` binding for HTTPS | `basicHttpsBinding` | All | `Web.config` system.serviceModel |
| WCF service endpoint contract | `eShopWCFService.ICatalogService` | All | `Web.config` system.serviceModel |
| WCF service endpoint binding | `basicHttpBinding` | All | `Web.config` system.serviceModel |
| `directoryBrowse[@enabled]` | `true` | All | `Web.config` system.webServer |
| EF default connection factory | `LocalDbConnectionFactory` (mssqllocaldb) | All | `Web.config` entityFramework |
| EF SQL provider | `System.Data.Entity.SqlServer.SqlProviderServices` | All | `Web.config` entityFramework |
| Connection string `EntityModel` | `Data Source=(localdb)\MSSQLLocalDB;Initial Catalog=eShopDatabase;Persist Security Info=True;` | All | `Web.config` connectionStrings |
| `ConnectionString` (env var override) | _(not set)_ | All | Environment variable; overrides named connection string when set |

### eShopWinForms (App.config)

| Property Key | Default Value | Profiles | Source |
|---|---|---|---|
| Supported runtime version | `v4.0` | All | `App.config` startup |
| Supported runtime SKU | `.NETFramework,Version=v4.7` | All | `App.config` startup |
| WCF client endpoint address | `http://localhost:62314/CatalogService.svc` | All | `App.config` system.serviceModel client |
| WCF client binding | `basicHttpBinding` / `BasicHttpBinding_ICatalogService` | All | `App.config` system.serviceModel bindings |
| WCF client contract | `eShopServiceReference.ICatalogService` | All | `App.config` system.serviceModel client |
| Windows Forms DPI awareness | _(commented out, default system DPI)_ | All | `App.config` System.Windows.Forms.ApplicationConfigurationSection |

## Startup Parameters & Resource Requirements

| Service | Runtime Options | Memory | Instance Count |
|---|---|---|---|
| eShopWCFService | Hosted on IIS Express; no explicit JVM/CLR startup flags configured | Not specified | 1 (single IIS Express process) |
| eShopWinForms | Standard .NET 4.7 WinForms process; no special CLR flags | Not specified | 1 (single desktop process per user) |

No Docker/container resource limits, Kubernetes resource requests/limits, or JVM `-Xms`/`-Xmx` equivalents are configured.

## Startup Dependency Chain

```
eShopWCFService (IIS Express, port 62314) 
    → must be running before →
eShopWinForms (WinForms client connects on startup)
```

There are no automated wait mechanisms, health probes, Docker Compose `depends_on` configurations, or readiness checks. If `eShopWCFService` is unavailable when `eShopWinForms` starts, the application will throw an unhandled `CommunicationException` on the first WCF call.

## Secrets & Sensitive Configuration

| Secret Reference | Type | Storage |
|---|---|---|
| `EntityModel` connection string | Database connection string | Stored in plaintext in `Web.config` (`connectionStrings` section) |
| `ConnectionString` env var | Database connection string override | Injected via OS environment variable at runtime; not stored in source |

> **Note:** The connection string in `Web.config` does not contain a username/password in the default configuration (uses Windows Integrated Security / LocalDB). However, it is stored in plaintext in source-controlled configuration. No encryption (DPAPI, Jasypt, Azure Key Vault references, or similar) is applied.

### Secrets Provisioning Workflow

There is no formal secrets management workflow. The database connection string is stored as plaintext in `Web.config` and committed to source control. The only runtime override path is via the `ConnectionString` environment variable, which is read directly in `CatalogConfiguration.cs`. No secret store, managed identity, service principal, or encryption mechanism is in use. For production deployments, the connection string would need to be injected via environment variable or a secrets management solution.

## Feature Flags

No feature flag framework (LaunchDarkly, Unleash, .NET `Microsoft.FeatureManagement`, `@ConditionalOnProperty`, etc.) is used. There are no conditional beans, A/B testing flags, or gradual rollout configurations. The only conditional configuration is the commented-out Windows Forms DPI settings in `App.config`.

| Flag Name | Default | Controlled By |
|---|---|---|
| _(none detected)_ | N/A | N/A |

## Framework & Runtime Versions

| Component | Version | Source |
|---|---|---|
| .NET Framework (eShopWCFService) | 4.6.1 | `eShopWCFService.csproj` TargetFrameworkVersion |
| .NET Framework (eShopWinForms) | 4.7 | `eShopWinForms.csproj` TargetFrameworkVersion |
| Entity Framework | 6.1.3 | `packages.config` (both projects) |
| WCF (System.ServiceModel) | Built into .NET Framework 4.6.1 | `eShopWCFService.csproj` references |
| Windows Forms | Built into .NET Framework 4.7 | `eShopWinForms.csproj` references |
| Newtonsoft.Json | 6.0.4 | `src/eShopWinForms/packages.config` |
| Microsoft.AspNet.WebApi.Client | 5.2.3 | `src/eShopWinForms/packages.config` |
| MSBuild Tools | 15.0 (Visual Studio 2017 format) | Both `.csproj` files (`ToolsVersion="15.0"`) |
