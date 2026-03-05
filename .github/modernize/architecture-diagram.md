# Architecture Diagram

This diagram illustrates the N-Tier architecture of the eShopLegacyNTier application, consisting of a Windows Forms desktop client, a WCF back-end service, and a SQL Server database.

## Application Architecture

```mermaid
flowchart TD
    subgraph Presentation["Presentation Tier — eShopWinForms (.NET Framework 4.7, Windows Forms)"]
        UI["CatalogView\nWindows Forms UI"]
        CTRL["CatalogController\nMVC-style Controller"]
        SVC_REF["WCF Service Reference\neShopServiceReference\nNewtonsoft.Json 6.0"]
    end

    subgraph Service["Service Tier — eShopWCFService (.NET Framework 4.6.1, WCF hosted on IIS)"]
        ISVC["ICatalogService\nWCF Service Contract"]
        SVC["CatalogService\nService Implementation"]
        MOCK["CatalogServiceMock\nIn-Memory Mock"]
        EF["EntityModel\nEntity Framework 6 DbContext"]
        subgraph Models["Domain Models"]
            M1["CatalogItem"]
            M2["CatalogBrand"]
            M3["CatalogType"]
            M4["CatalogItemsStock"]
            M5["DiscountItem"]
        end
        subgraph Infra["Infrastructure"]
            DBINIT["CatalogDBInitializer\nSeed Data"]
            CFG["CatalogConfiguration\nApp Settings"]
        end
    end

    subgraph Data["Data Tier"]
        DB[("SQL Server LocalDB\neShopDatabase")]
    end

    UI --> CTRL
    CTRL --> SVC_REF
    SVC_REF -->|"basicHttpBinding over HTTP"| ISVC
    ISVC --> SVC
    ISVC --> MOCK
    SVC --> EF
    EF --> Models
    EF --> Infra
    EF -->|"ADO.NET SqlClient"| DB
```
