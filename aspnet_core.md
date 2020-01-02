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

- Installing VSCode

Nuget Package: Microsoft.EntityFrameworkCore (must be exaclty this)

- Add a Database Provider

Nuget Package: Microsoft.EntityFrameworkCore.Sqlite (must be exaclty this)

- Configuring Connection

https://docs.microsoft.com/en-us/ef/core/miscellaneous/connection-strings#aspnet-core

- Safe Storage in Development:

https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-3.1&tabs=windows
https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-3.1&tabs=windows#enable-secret-storage
