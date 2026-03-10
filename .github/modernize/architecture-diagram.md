# Architecture Diagram

This diagram shows the high-level architecture of the eShopLegacyNTier application  a legacy N-Tier catalog management system built on .NET Framework.

## Application Architecture

```mermaid
flowchart TD
    subgraph Presentation["Presentation Tier  eShopWinForms (.NET Framework 4.7)"]
        UI["WinForms Desktop Client\n(CatalogView / ICatalogView)"]
        Controller["MVP Controller\n(CatalogController)"]
        WCFProxy["WCF Client Proxy\n(eShopServiceReference)\nSOAP / basicHttpBinding"]
    end

    subgraph Service["Service Tier  eShopWCFService (.NET Framework 4.6.1)"]
        WCFSvc["WCF Service\n(CatalogService.svc)\nIIS Express :62314"]
        ServiceContract["Service Contract\n(ICatalogService)\nCRUD + Stock + Discount"]
    end

    subgraph Data["Data Tier"]
        EF["Entity Framework 6.1.3\n(EntityModel DbContext)"]
        DB[(SQL Server LocalDB\neShopDatabase)]
    end

    subgraph Domain["Domain Models"]
        Models["CatalogItem\nCatalogBrand\nCatalogType\nCatalogItemsStock\nDiscountItem"]
    end

    UI -->|user events| Controller
    Controller -->|service calls| WCFProxy
    WCFProxy -->|HTTP SOAP| WCFSvc
    WCFSvc --> ServiceContract
    ServiceContract --> EF
    EF -->|LINQ to Entities| DB
    EF --- Models

    classDef tier fill:#dbe9f4,stroke:#5a8fc0,color:#000
    classDef component fill:#fff,stroke:#5a8fc0,color:#000
    classDef storage fill:#fef9c3,stroke:#b8a000,color:#000
    classDef domain fill:#f0f4e8,stroke:#7a9a4a,color:#000

    class Presentation,Service,Data,Domain tier
    class UI,Controller,WCFProxy,WCFSvc,ServiceContract,EF component
    class DB storage
    class Models domain
```
