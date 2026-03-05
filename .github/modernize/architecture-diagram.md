# Architecture Diagram

This diagram shows the current architecture of the eShopLegacyNTier application, a two-tier .NET desktop solution composed of a WinForms client and a WCF back-end service backed by SQL Server.

## Application Architecture

```mermaid
flowchart TD
    subgraph Client["Presentation Layer – eShopWinForms (.NET 4.7)"]
        UI["CatalogView\n(Windows Forms)"]
        Controller["CatalogController\n(MVC-style controller)"]
        WCFClient["WCF Client Proxy\n(eShopServiceReference)"]
        UI --> Controller
        Controller --> WCFClient
    end

    subgraph Service["Service Layer – eShopWCFService (.NET 4.6.1 / IIS)"]
        WCFEndpoint["CatalogService\n(WCF / basicHttpBinding)"]
        ServiceInterface["ICatalogService\n(service contract)"]
        MockImpl["CatalogServiceMock\n(mock implementation)"]
        WCFEndpoint --> ServiceInterface
        ServiceInterface --> MockImpl
    end

    subgraph DataAccess["Data Access Layer"]
        EF["Entity Framework 6\n(Code-First / DbContext)"]
        DBInit["CatalogDBInitializer\n(seed data)"]
        EF --> DBInit
    end

    subgraph Storage["Data Storage"]
        SQL[("SQL Server\n(MSSQLLocalDB – eShopDatabase)")]
    end

    subgraph Models["Domain Models"]
        CatalogItem["CatalogItem"]
        CatalogBrand["CatalogBrand"]
        CatalogType["CatalogType"]
        CatalogItemsStock["CatalogItemsStock"]
        DiscountItem["DiscountItem"]
    end

    WCFClient -- "HTTP / basicHttpBinding" --> WCFEndpoint
    MockImpl --> EF
    EF -- "System.Data.SqlClient" --> SQL
    EF --> Models
```
