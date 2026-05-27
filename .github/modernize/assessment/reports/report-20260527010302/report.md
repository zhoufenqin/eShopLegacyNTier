# eShopWCFService

## Summary

| Metric | Value |
|--------|-------|
| Total Issues | 8 |
| Mandatory Blockers | 0 |
| Potential Issues | 4 |

## Application Information

| Property | Value |
|----------|-------|
| Language | C# |
| Frameworks | .NETFramework,Version=v4.6.1 |
| Build tools | MSBuild |

## Cloud Readiness Issues

| Issue Name | Criticality | Story Points | Occurrences |
|------------|-------------|--------------|-------------|
| Hardcoded URLs detected | Potential | 1 | [45](#Hardcoded_URLs_detected) |
| SQL database connection detected | Potential | 3 | [1](#SQL_database_connection_detected) |
| Local or network IO operations detected | Potential | 3 | [1](#Local_or_network_IO_operations_detected) |
| Local OS environment access detected | Potential | 1 | [1](#Local_OS_environment_access_detected) |
| Upgrade to newer target framework to get better cloud experience | Optional | 3 | [2](#Upgrade_to_newer_target_framework_to_get_better_cloud_experience) |
| Connection strings without configuration builders detected | Optional | 3 | [2](#Connection_strings_without_configuration_builders_detected) |
| System.Data.SqlClient dependency detected | Optional | 3 | [1](#System_Data_SqlClient_dependency_detected) |
| Static content detected | Optional | 3 | [1](#Static_content_detected) |

### Issue Details

<details id="Hardcoded_URLs_detected">
<summary><b>Hardcoded URLs detected</b> — affected files</summary>

- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 17)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 190)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 251)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 405)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 312)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 530)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 533)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 530)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 533)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 536)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 539)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 536)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 539)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 500)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 503)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 500)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 503)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 524)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 527)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 524)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 527)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 506)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 509)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 506)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 509)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 512)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 515)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 512)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 515)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 518)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 521)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 518)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 521)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 554)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 557)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 554)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 557)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 548)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 551)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 548)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 551)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 542)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 545)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 542)`
- `src\eShopWinForms\Connected Services\eShopServiceReference\Reference.cs (line 545)`

</details>

<details id="SQL_database_connection_detected">
<summary><b>SQL database connection detected</b> — affected files</summary>

- `src\eShopWCFService\Web.config`

</details>

<details id="Local_or_network_IO_operations_detected">
<summary><b>Local or network IO operations detected</b> — affected files</summary>

- `src\eShopWinForms\Views\CatalogView.cs (line 57)`

</details>

<details id="Local_OS_environment_access_detected">
<summary><b>Local OS environment access detected</b> — affected files</summary>

- `src\eShopWinForms\Views\CatalogView.cs (line 56)`

</details>

<details id="Upgrade_to_newer_target_framework_to_get_better_cloud_experience">
<summary><b>Upgrade to newer target framework to get better cloud experience</b> — affected files</summary>

- `src\eShopWCFService\eShopWCFService.csproj`
- `src\eShopWinForms\eShopWinForms.csproj`

</details>

<details id="Connection_strings_without_configuration_builders_detected">
<summary><b>Connection strings without configuration builders detected</b> — affected files</summary>

- `src\eShopWCFService\Web.config`
- `src\eShopWCFService\Web.config`

</details>

<details id="System_Data_SqlClient_dependency_detected">
<summary><b>System.Data.SqlClient dependency detected</b> — affected files</summary>

- `src\eShopWCFService\Web.config`

</details>

<details id="Static_content_detected">
<summary><b>Static content detected</b> — affected files</summary>

- `src\eShopWinForms\eShopWinForms.csproj`

</details>

---

## Codebase Insights

> **Note:** These documents are generated by AI and may contain inaccuracies or incomplete information. Please review carefully.

1. **[Architecture Diagram](facts/architecture-diagram.md)** — Understand the big picture: system layers and component relationships
2. **[Dependency Map](facts/dependency-map.md)** — Know what the project depends on and where the risks are
3. **[API & Service Contracts](facts/api-service-contracts.md)** — See how services communicate and what contracts they expose
4. **[Data Architecture](facts/data-architecture.md)** — Explore data models, storage, and data flow patterns
5. **[Configuration Inventory](facts/configuration-inventory.md)** — Review how the application is configured across environments
6. **[Business Workflows](facts/business-workflows.md)** — Trace end-to-end business processes and domain logic

[Share feedback](https://aka.ms/ghcp-appmod/feedback)
