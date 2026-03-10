# Architecture Diagram

eShopLegacyNTier is a legacy .NET Framework N-Tier desktop application for managing a product catalog, consisting of a Windows Forms client and a WCF service backed by SQL Server.

## Application Architecture

```mermaid
flowchart TD
    subgraph Presentation["Presentation Layer"]
        WF["eShopWinForms\n(.NET Framework 4.7 WinForms)\nCatalogView + CatalogController"]
    end

    subgraph Service["Service Layer"]
        WCF["eShopWCFService\n(.NET Framework 4.6.1 WCF)\nCatalogService via BasicHttpBinding\nHosted in IIS"]
    end

    subgraph DataAccess["Data Access Layer"]
        EF["Entity Framework 6\nEntityModel DbContext\nCatalogItem, CatalogBrand\nCatalogType, CatalogItemsStock\nDiscountItem"]
    end

    subgraph Storage["Data Storage"]
        DB[("SQL Server LocalDB\neShopDatabase")]
    end

    WF -- "HTTP BasicHttpBinding\nWCF Service Reference" --> WCF
    WCF --> EF
    EF -- "SQL queries via LINQ-to-Entities" --> DB
```
