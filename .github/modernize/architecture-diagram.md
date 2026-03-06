# Architecture Diagram

This diagram represents the current architecture of the eShopLegacyNTier application, a .NET Framework N-Tier solution composed of a Windows Forms client and a WCF backend service.

## Application Architecture

```mermaid
flowchart TD
    subgraph Client["Client Tier - eShopWinForms (.NET Framework 4.7)"]
        UI["Windows Forms UI\n(CatalogView)"]
        Controller["CatalogController\n(MVC-style Controller)"]
        WCFClient["WCF Client Proxy\n(eShopServiceReference)"]
    end

    subgraph Service["Service Tier - eShopWCFService (.NET Framework 4.6.1)"]
        WCFEndpoint["WCF Endpoint\nCatalogService.svc\n(basicHttpBinding / SOAP)"]
        BizLogic["Business Logic\nCatalogService\nICatalogService"]
        EF["Data Access\nEntity Framework 6\n(EntityModel / DbContext)"]
    end

    subgraph Data["Data Tier"]
        DB[("SQL Server\nMSSQLLocalDB\neShopDatabase")]
    end

    UI -->|"user actions"| Controller
    Controller -->|"calls"| WCFClient
    WCFClient -->|"SOAP over HTTP\nlocalhost:62314"| WCFEndpoint
    WCFEndpoint --> BizLogic
    BizLogic -->|"CRUD operations\n(CatalogItem, CatalogBrand,\nCatalogType, DiscountItem)"| EF
    EF -->|"SQL queries\nSystem.Data.SqlClient"| DB
```
