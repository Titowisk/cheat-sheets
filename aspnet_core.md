# ASPNET CORE API
https://dotnet.microsoft.com/apps/aspnet/apis

launchSettings.json

If I keep the Https url, POSTMAN doesn't work
```
"ComparatorApp.API": {
      "commandName": "Project",
      "launchBrowser": true,
      "launchUrl": "weatherforecast",
      "applicationUrl": "http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
```

## Entity FrameWork

https://docs.microsoft.com/en-us/ef/core/

https://entityframeworkcore.com/model-data-annotations

### Installing VSCode

Nuget Package: Microsoft.EntityFrameworkCore (must be exaclty this)

### Add a Database Provider

Nuget Package: Microsoft.EntityFrameworkCore.Sqlite (must be exaclty this)

### Configuring Connection

https://docs.microsoft.com/en-us/ef/core/miscellaneous/connection-strings#aspnet-core

### Safe Storage in Development:

https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-3.1&tabs=windows
https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-3.1&tabs=windows#enable-secret-storage

### Migrations
https://docs.microsoft.com/en-us/ef/core/managing-schemas/migrations/?tabs=dotnet-core-cli

Requirements: 
dotnet tool install --global dotnet-ef  (dotnet Entity Framework Tools)
Microsoft.EntityFrameworkCore.Design 


## Controllers
https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase?view=aspnetcore-3.1
https://forums.asp.net/t/2007350.aspx?ActionResult+vs+Task+ActionResult+question (ActionResult vs Task)
