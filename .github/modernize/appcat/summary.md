# Modernization Assessment Summary

**Target Azure Services**: Azure App Service, Azure Kubernetes Service, Azure Container Apps, Azure App Service Container

## Overall Statistics

**Total Applications**: 2

**Name: eShopWCFService**
- Mandatory: 0 issues
- Potential: 1 issues
- Optional: 3 issues

**Name: eShopWinForms**
- Mandatory: 0 issues
- Potential: 3 issues
- Optional: 2 issues

> **Severity Levels Explained:**
> - **Mandatory**: The issue has to be resolved for the migration to be successful.
> - **Potential**: This issue may be blocking in some situations but not in others. These issues should be reviewed to determine whether a change is required or not.
> - **Optional**: The issue discovered is real issue fixing which could improve the app after migration, however it is not blocking.

## Applications Profile

### Name: eShopWCFService
- **Frameworks**: .NETFramework,Version=v4.6.1
- **Languages**: C#
- **Build Tools**: MSBuild

**Key Findings**:
- **Potential Issues (1 locations)**:
  - <!--ruleid=Database.0002-->SQL database connection detected (1 location found)
- **Optional Issues (4 locations)**:
  - <!--ruleid=Runtime.0002-->Upgrade to newer target framework to get better cloud experience (1 location found)
  - <!--ruleid=Database.0003-->System.Data.SqlClient dependency detected (1 location found)
  - <!--ruleid=Security.0002-->Connection strings without configuration builders detected (2 locations found)

### Name: eShopWinForms
- **Frameworks**: .NETFramework,Version=v4.7
- **Languages**: C#
- **Build Tools**: MSBuild

**Key Findings**:
- **Potential Issues (47 locations)**:
  - <!--ruleid=Local.0003-->Local or network IO operations detected (1 location found)
  - <!--ruleid=Local.0007-->Local OS environment access detected (1 location found)
  - <!--ruleid=Local.0006-->Hardcoded URLs detected (45 locations found)
- **Optional Issues (2 locations)**:
  - <!--ruleid=Runtime.0002-->Upgrade to newer target framework to get better cloud experience (1 location found)
  - <!--ruleid=Scale.0001-->Static content detected (1 location found)

## Next Steps

For comprehensive migration guidance and best practices, visit:
- [GitHub Copilot modernization](https://aka.ms/ghcp-appmod)
