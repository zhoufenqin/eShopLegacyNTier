# Architecture Diagram

This is a legacy .NET N-Tier application consisting of a Windows Forms desktop client communicating with a WCF service backed by a SQL Server database.

## Application Architecture

```mermaid
flowchart TD
    subgraph Presentation["Presentation Tier - eShopWinForms (.NET Framework 4.7)"]
        WinForms["Windows Forms Desktop App\nCatalogView (WinForms UI)"]
        Controller["CatalogController\nMVC-style controller"]
        WCFClient["WCF Client Proxy\nSystem.ServiceModel"]
        WinForms --> Controller
        Controller --> WCFClient
    end

    subgraph Service["Service Tier - eShopWCFService (.NET Framework 4.6.1)"]
        IIS["IIS Express Host"]
        WCFService["CatalogService (WCF)\nbasicHttpBinding"]
        ServiceMock["CatalogServiceMock"]
        EF["Entity Framework 6\nCode First ORM"]
        IIS --> WCFService
        WCFService --> ServiceMock
        WCFService --> EF
    end

    subgraph Data["Data Tier"]
        SQL["SQL Server LocalDB\neShopDatabase"]
    end

    subgraph Models["Domain Models"]
        CatalogItem["CatalogItem"]
        CatalogBrand["CatalogBrand"]
        CatalogType["CatalogType"]
        CatalogItemsStock["CatalogItemsStock"]
        DiscountItem["DiscountItem"]
    end

    WCFClient -- "HTTP / basicHttpBinding\nSOAP over WCF" --> IIS
    EF -- "ADO.NET / SQL Client" --> SQL
    WCFService --> Models
```
