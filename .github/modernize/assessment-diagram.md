# eShopLegacyNTier Architecture Diagram

```mermaid
flowchart TD
    subgraph Presentation["Presentation Layer"]
        WinForms["eShopWinForms\n.NET Framework 4.7\nWindows Forms App"]
        View["CatalogView\nWindows Forms UI"]
        Controller["CatalogController\nMVC Controller"]
    end

    subgraph ServiceLayer["Service Layer (IIS-hosted)"]
        WCFService["eShopWCFService\n.NET Framework 4.6.1\nWCF Service"]
        CatalogSvc["CatalogService\nICatalogService contract"]
    end

    subgraph DataAccess["Data Access Layer"]
        EF["Entity Framework 6\nDbContext - EntityModel"]
    end

    subgraph DataStore["Data Storage"]
        SQL["SQL Server\nCatalog Database"]
    end

    subgraph Models["Domain Models"]
        CatalogItem["CatalogItem"]
        CatalogBrand["CatalogBrand"]
        CatalogType["CatalogType"]
        CatalogItemsStock["CatalogItemsStock"]
        DiscountItem["DiscountItem"]
    end

    View --> Controller
    Controller --> WCFProxy["WCF Client Proxy\neShopServiceReference"]
    WCFProxy -- "SOAP over HTTP" --> CatalogSvc
    WCFService --> CatalogSvc
    CatalogSvc --> EF
    EF --> SQL
    EF --> CatalogItem
    EF --> CatalogBrand
    EF --> CatalogType
    EF --> CatalogItemsStock
    EF --> DiscountItem
```

## Architecture Overview

| Layer | Technology | Description |
|-------|-----------|-------------|
| Presentation | Windows Forms (.NET 4.7) | Desktop GUI app (`eShopWinForms`) with MVC pattern |
| Service | WCF (.NET 4.6.1, IIS) | `eShopWCFService` exposes `ICatalogService` via SOAP |
| Data Access | Entity Framework 6 | `EntityModel` DbContext with code-first migrations |
| Data Storage | SQL Server | Relational database for catalog and stock data |

## Key Dependencies

- **EntityFramework 6.1.3** – ORM for SQL Server data access
- **System.ServiceModel (WCF)** – Service communication between WinForms and WCF
- **Newtonsoft.Json 6.0.4** – JSON serialization in the WinForms client
- **Microsoft.AspNet.WebApi.Client 5.2.3** – HTTP client utilities in WinForms
