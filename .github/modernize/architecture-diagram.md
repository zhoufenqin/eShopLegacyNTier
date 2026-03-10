# Architecture Diagram

eShopLegacyNTier is a legacy .NET N-Tier application consisting of a Windows Forms desktop client communicating with a WCF service backend backed by SQL Server via Entity Framework 6.

## Application Architecture

```mermaid
flowchart TD
    subgraph Presentation["Presentation Layer (eShopWinForms - .NET Framework 4.7)"]
        UI["CatalogView\nWindows Forms\nDataGridView, ComboBox filters, Discount banner"]
        Controller["CatalogController\nMVP Presenter\nLoadCatalogItems, CheckForDiscounts"]
        UI <-->|UI Events / Data Binding| Controller
    end

    subgraph ServiceLayer["Service Layer (eShopWCFService - .NET Framework 4.6.1 / IIS Express :62314)"]
        WCF["CatalogService.svc\nWCF Service\nFindCatalogItem, GetCatalogItems\nGetAvailableStock, GetDiscount\nCreateCatalogItem, UpdateCatalogItem\nRemoveCatalogItem, CreateAvailableStock"]
    end

    subgraph DataAccess["Data Access Layer"]
        EF["EntityModel\nEntity Framework 6 Code First DbContext\nDbSet: CatalogItems, CatalogBrands\nCatalogTypes, CatalogItemsStock\nDiscountItems"]
        Seed["CatalogDBInitializer\nDatabase Seeder\nPreconfiguredData"]
        EF --> Seed
    end

    subgraph Database["Database Layer"]
        DB[("eShopDatabase\nSQL Server LocalDB\n(localdb)\\MSSQLLocalDB")]
    end

    Controller -->|WCF BasicHttpBinding\nService Reference Proxy| WCF
    WCF -->|LINQ Queries / CRUD| EF
    EF -->|ADO.NET / SQL| DB
```
