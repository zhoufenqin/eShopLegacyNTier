# Assessment Overview

This directory contains supplementary analysis documents generated during the assessment of the **eShopLegacyNTier** application. These documents provide architectural, dependency, API, data, configuration, and business workflow context to support cloud migration planning.

## Supplementary Documents

| Document | Description |
|---|---|
| [architecture-diagram.md](architecture-diagram.md) | Application architecture diagram showing the two-layer structure (WinForms client + WCF service), technology stack summary, and component relationships |
| [dependency-map.md](dependency-map.md) | Visual map of all external NuGet dependencies grouped by category, with version and compatibility risk analysis |
| [api-service-contracts.md](api-service-contracts.md) | WCF service contract inventory (all 10 operations on `ICatalogService`), communication patterns, DTOs, and service sequence diagram |
| [data-architecture.md](data-architecture.md) | Entity model (ER diagram), database configuration, EF6 data access patterns, and data classification analysis |
| [configuration-inventory.md](configuration-inventory.md) | Full inventory of configuration sources (`Web.config`, `App.config`), properties, build profiles, secrets handling, and framework versions |
| [business-workflows.md](business-workflows.md) | Core business workflows (catalog browsing, filtering, stock management), domain entities, business rules, and decision logic |
