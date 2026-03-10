# Architecture Diagram

This diagram represents the high-level architecture of the eShopLegacyNTier application, a classic N-Tier Windows desktop e-commerce catalog system built on .NET Framework.

## Application Architecture

```mermaid
flowchart TD
    subgraph Presentation["Presentation Layer - eShopWinForms (.NET 4.7 / WinForms)"]
        View["CatalogView\n(Windows Form)\n- Product grid with discounts\n- Brand and type filters\n- Discount banner\n- Stock management UI"]
        Controller["CatalogController\n(MVP Presenter)\n- Handles view events\n- Orchestrates service calls\n- Updates view with results"]
        Proxy["CatalogServiceClient\n(WCF Auto-generated Proxy)\n- BasicHttpBinding\n- DataContract serialization"]
    end

    subgraph Service["Service Layer - eShopWCFService (.NET 4.6.1 / WCF / IIS)"]
        Contract["ICatalogService\n(WCF Service Contract)\n- GetCatalogItems\n- GetCatalogBrands / GetCatalogTypes\n- FindCatalogItem\n- GetDiscount\n- CreateCatalogItem / UpdateCatalogItem / RemoveCatalogItem\n- GetAvailableStock / CreateAvailableStock"]
        SvcImpl["CatalogService\n(WCF Service Implementation)\n- Hosted in IIS Express port 62314\n- basicHttpBinding + mexHttpBinding"]
    end

    subgraph Data["Data Layer - Entity Framework 6 / SQL Server LocalDB"]
        DbCtx["EntityModel\n(DbContext - Code First)\n- CatalogItems\n- CatalogBrands\n- CatalogTypes\n- CatalogItemsStocks\n- DiscountItems"]
        DB[("SQL Server LocalDB\neShopDatabase")]
        DBInit["CatalogDBInitializer\n- Auto-create DB if missing\n- Seed with sample data\n(products, brands, discounts, stock)"]
    end

    View <-->|"UI events and data binding"| Controller
    Controller <-->|"Service method calls"| Proxy
    Proxy <-->|"HTTP BasicHttpBinding\nlocalhost:62314"| Contract
    Contract --> SvcImpl
    SvcImpl <-->|"Entity Framework ORM"| DbCtx
    DbCtx <-->|"SQL queries"| DB
    DBInit -->|"Initializes schema and seed data"| DB
```
