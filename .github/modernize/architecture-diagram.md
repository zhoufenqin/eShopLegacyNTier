# Architecture Diagram

This diagram illustrates the N-Tier architecture of the eShopLegacyNTier application, a Windows desktop catalog management system built on .NET Framework with a WCF service backend and SQL Server database.

## Application Architecture

```mermaid
flowchart TD
    subgraph Presentation["Presentation Layer (eShopWinForms - .NET 4.7 WinForms)"]
        View["CatalogView\nWindows Forms UI\nProduct grid, filters, CRUD controls"]
        Controller["CatalogController\nMVP Presenter\nBusiness logic orchestration"]
        Helpers["Helpers\nNotifications, JSON, Image Upload"]
        View -- "UI Events" --> Controller
        Controller -- "View Updates" --> View
    end

    subgraph ServiceLayer["Service Layer (eShopWCFService - .NET 4.6.1)"]
        WCFContract["ICatalogService\nWCF Service Contract\nBasicHttpBinding"]
        ServiceImpl["CatalogService\nService Implementation\nCRUD, Stock, Discounts"]
        WCFContract --> ServiceImpl
    end

    subgraph DataAccess["Data Access Layer (Entity Framework 6.1.3 Code-First)"]
        EFContext["EntityModel DbContext\nDbSet CatalogItem\nDbSet CatalogBrand\nDbSet CatalogType\nDbSet CatalogItemsStock\nDbSet DiscountItem"]
        DBInit["CatalogDBInitializer\nAuto-seed on create\nPreconfiguredData"]
        EFContext --> DBInit
    end

    subgraph Database["Data Store"]
        SQLDB["SQL Server LocalDB\neShopDatabase\nCatalogItems, Brands, Types\nStock, Discounts"]
    end

    subgraph ProxyGen["WCF Proxy (Auto-generated)"]
        Proxy["eShopServiceReference\nCatalogServiceClient\nNewtonsoft.Json 6.0.4"]
    end

    Controller -- "Service calls via proxy" --> Proxy
    Proxy -- "HTTP BasicHttpBinding\nlocalhost:62314" --> WCFContract
    ServiceImpl -- "EF queries" --> EFContext
    EFContext -- "SQL Client\nADO.NET" --> SQLDB
```
