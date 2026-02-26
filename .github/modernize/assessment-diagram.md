# eShopLegacyNTier Architecture Diagram

## Overview

eShopLegacyNTier is a classic N-Tier .NET application consisting of a Windows Forms desktop client and a WCF SOAP backend service, backed by a SQL Server database via Entity Framework.

## Architecture Diagram

```mermaid
flowchart TD
    subgraph Presentation["Presentation Layer (eShopWinForms - .NET 4.7)"]
        UI["CatalogView\nWindows Forms UI"]
        CTRL["CatalogController\nMVC Controller"]
        UI <--> CTRL
    end

    subgraph Service["Service Layer (eShopWCFService - .NET 4.6.1)"]
        WCF["CatalogService\nWCF SOAP Service"]
        IFACE["ICatalogService\nService Contract"]
        MOCK["CatalogServiceMock\nMock Implementation"]
        WCF --> IFACE
        MOCK --> IFACE
    end

    subgraph DataAccess["Data Access Layer"]
        EF["Entity Framework 6\nCode First ORM"]
        CTX["CatalogDBContext\nEntityModel"]
        INIT["CatalogDBInitializer\nSeed Data"]
        EF --> CTX
        INIT --> CTX
    end

    subgraph Data["Data Storage"]
        SQL[("SQL Server\nDatabase")]
    end

    subgraph Models["Domain Models"]
        M1["CatalogItem"]
        M2["CatalogBrand"]
        M3["CatalogType"]
        M4["DiscountItem"]
        M5["CatalogItemsStock"]
    end

    CTRL -- "WCF Client\nSOAP over HTTP" --> WCF
    WCF --> Models
    CTX --> Models
    CTX -- "SQL Queries" --> SQL
```

## Technology Stack

| Layer | Technology |
|-------|-----------|
| Presentation | Windows Forms (.NET 4.7) |
| Service | WCF SOAP Web Service (.NET 4.6.1, IIS) |
| Data Access | Entity Framework 6.1.3 (Code First) |
| Database | SQL Server |
| Serialization | Newtonsoft.Json 6.0.4 |
| Service Communication | WCF / SOAP (System.ServiceModel) |

## Key Components

- **eShopWinForms**: Desktop application using MVC pattern (CatalogView + CatalogController) that communicates with the backend via a WCF service reference proxy.
- **eShopWCFService**: WCF SOAP service hosted on IIS exposing `ICatalogService` contract with operations for catalog management (items, brands, types, discounts, stock).
- **EntityModel**: Entity Framework 6 DbContext managing persistence for all catalog domain models against SQL Server.
- **CatalogDBInitializer**: Seeds the database with preconfigured catalog data on first run.
