# Architecture Diagram

This diagram shows the current architecture of the eShopLegacyNTier application, a two-tier .NET desktop solution composed of a WinForms client and a WCF back-end service backed by SQL Server.

## Application Architecture

```mermaid
flowchart TD
    subgraph Client["Presentation Layer - eShopWinForms (.NET 4.7 WinForms)"]
        UI["CatalogView\n(Windows Forms UI)"]
        Controller["CatalogController\n(MVC-style controller)"]
        WCFClient["WCF Client Proxy\n(eShopServiceReference / Newtonsoft.Json)"]
        UI <--> Controller
        Controller <--> WCFClient
    end

    subgraph Service["Service Layer - eShopWCFService (.NET 4.6.1 / IIS Express)"]
        WCFEndpoint["CatalogService\n(WCF SOAP Service)"]
        ServiceInterface["ICatalogService\n(ServiceContract)"]
        MockImpl["CatalogServiceMock\n(test mock)"]
        WCFEndpoint --> ServiceInterface
        MockImpl --> ServiceInterface
    end

    subgraph DataAccess["Data Access Layer - Entity Framework 6"]
        EF["EntityModel\n(DbContext / Code-First)"]
        DBInit["CatalogDBInitializer\n(seed data on startup)"]
        EF --> DBInit
    end

    subgraph Storage["Data Storage"]
        SQL[("SQL Server LocalDB\n(eShopDatabase)")]
    end

    subgraph Models["Domain Models"]
        CatalogItem["CatalogItem"]
        CatalogBrand["CatalogBrand"]
        CatalogType["CatalogType"]
        CatalogItemsStock["CatalogItemsStock"]
        DiscountItem["DiscountItem"]
    end

    WCFClient -- "BasicHttpBinding over HTTP\nlocalhost:62314" --> WCFEndpoint
    WCFEndpoint --> EF
    EF -- "System.Data.SqlClient" --> SQL
    EF --> Models
```
