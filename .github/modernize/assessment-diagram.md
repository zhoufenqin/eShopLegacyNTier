# eShopLegacyNTier Architecture Diagram

## Application Architecture

```mermaid
flowchart TD
    subgraph PresentationLayer["Presentation Layer"]
        WF["eShopWinForms\n.NET Framework 4.7\nWindows Forms MVC"]
        CV["CatalogView\nWinForms UI"]
        CC["CatalogController\nMVC Controller"]
        WF --> CV
        WF --> CC
    end

    subgraph ServiceLayer["Service Layer"]
        WCF["eShopWCFService\n.NET Framework 4.6.1\nWCF SOAP Service"]
        CS["CatalogService\nICatalogService contract"]
        WCF --> CS
    end

    subgraph DataLayer["Data Access Layer"]
        EF["Entity Framework 6.1.3\nDbContext - EntityModel"]
        MODELS["Domain Models\nCatalogItem, CatalogBrand\nCatalogType, DiscountItem\nCatalogItemsStock"]
        EF --> MODELS
    end

    subgraph Storage["Data Storage"]
        DB["SQL Server LocalDB\neShopDatabase"]
    end

    CC -- "basicHttpBinding\nSOAP over HTTP" --> WCF
    CS --> EF
    EF -- "ADO.NET SqlClient" --> DB
```

## Technology Stack

| Layer | Technology |
|-------|-----------|
| Presentation | .NET Framework 4.7, Windows Forms |
| Service | .NET Framework 4.6.1, WCF (System.ServiceModel) |
| Data Access | Entity Framework 6.1.3 |
| Database | SQL Server (LocalDB - mssqllocaldb) |
| Serialization | Newtonsoft.Json 6.0.4 |
| HTTP Client | Microsoft.AspNet.WebApi.Client 5.2.3 |

## Key Observations

- **N-Tier Architecture**: Classic 3-tier design with Presentation, Service, and Data layers
- **WCF Communication**: WinForms client communicates with backend via SOAP/basicHttpBinding
- **ORM**: Entity Framework 6 (Code First with DB initializer) manages data persistence
- **Windows-only**: WinForms and WCF with localdb are Windows-platform-specific technologies
- **Static Assets**: Application contains 98 static asset files (images, fonts) stored in the repo
