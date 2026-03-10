# Architecture Diagram

This diagram represents the N-Tier architecture of the eShop application, consisting of a Windows Forms desktop client and a WCF backend service backed by SQL Server.

## Application Architecture

```mermaid
flowchart TD
    subgraph Presentation["Presentation Layer - eShopWinForms (.NET 4.7 / Windows Forms)"]
        CV["CatalogView\n(Windows Forms UI)"]
        CC["CatalogController\n(MVC Controller)"]
        CV <--> CC
    end

    subgraph ServiceLayer["Service Layer - eShopWCFService (.NET 4.6.1 / IIS)"]
        ICS["ICatalogService\n(WCF Contract)"]
        CS["CatalogService\n(WCF Implementation)"]
        CSM["CatalogServiceMock\n(Mock Implementation)"]
        ICS --> CS
        ICS --> CSM
    end

    subgraph DataLayer["Data Access Layer"]
        EF["Entity Framework 6\n(ORM)"]
        EM["EntityModel\n(DbContext)"]
        EF --> EM
    end

    subgraph Models["Domain Models"]
        CI["CatalogItem"]
        CB["CatalogBrand"]
        CT["CatalogType"]
        DI["DiscountItem"]
        CIS["CatalogItemsStock"]
    end

    subgraph Storage["Data Storage"]
        DB[("SQL Server LocalDB\neShopDatabase")]
    end

    CC -->|"WCF basicHttpBinding\nHTTP localhost:62314"| ICS
    CS --> EF
    EM --> Models
    EM -->|"SQL queries"| DB
```
