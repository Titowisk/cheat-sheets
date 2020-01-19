# ASPNET CORE API
https://dotnet.microsoft.com/apps/aspnet/apis
https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-web-api?view=aspnetcore-3.1&tabs=visual-studio-code#overview

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

## Controllers
https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controllerbase?view=aspnetcore-3.1
https://forums.asp.net/t/2007350.aspx?ActionResult+vs+Task+ActionResult+question (ActionResult vs Task)

## Querying
https://docs.microsoft.com/en-us/ef/core/querying/related-data#related-data-and-serialization

### Self loop problem
```
 {
        "id": 1,
        "itemId": 3,
        "itemName": "amendoim",
        "brandId": 1,
        "brand": {
            "id": 1,
            "name": "dori",
            "itemsDetail": [
                {
                    "id": 1,
                    "itemId": 3,
                    "item": {
                        "id": 3,
                        "name": "amendoim",
                        "itemsDetail": [
                            {
                                "id": 2,
                                "itemId": 3,
                                "brandId": 1,
                                "storeId": 1,
                                "store": {
                                    "id": 1,
                                    "name": "redemix",
                                    "itemsDetail": []
```
This `ItemDetail` has a `Item` and a `Brand`. Each `Item` and `Brand` has a list of `ItemDetail`. So Net Core serializes the objects and brings all nested objects.

Using the repository pattern, `Dtos` (Data transfer objects) and `AutoMapper` I can create a `ItemDetailForListDto` that brings only the **ItemName instead** of bringing a `Item` that also has a `ItemDetail`...

```
public class ItemsDetailProfile : Profile
    {
        public ItemsDetailProfile()
        {
            CreateMap<ItemDetail, ItemDetailForCreationDto>();
            CreateMap<ItemDetail, ItemsDetailForListDto>()
                .ForMember(dest => dest.ItemName,
                    opt => opt.MapFrom(src => src.Item.Name));
        }
    }
```

```
public class ItemsDetailForListDto
    {
        public int Id { get; set; }
        public int ItemId { get; set; }
        // public Item Item { get; set; }
        public string ItemName { get; set; }
        public int BrandId { get; set; }
        public Brand Brand { get; set; }
        ...
```

# Entity FrameWork

https://docs.microsoft.com/en-us/ef/core/

https://entityframeworkcore.com/model-data-annotations

## Installing in VSCode

Nuget Package: Microsoft.EntityFrameworkCore (must be exaclty this)

## Add a Database Provider

Nuget Package: Microsoft.EntityFrameworkCore.Sqlite (must be exaclty this)

## Configuring Connection

https://docs.microsoft.com/en-us/ef/core/miscellaneous/connection-strings#aspnet-core

## Safe Storage in Development:

https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-3.1&tabs=windows
https://docs.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-3.1&tabs=windows#enable-secret-storage

## Migrations
https://docs.microsoft.com/en-us/ef/core/managing-schemas/migrations/?tabs=dotnet-core-cli

Requirements: 
dotnet tool install --global dotnet-ef  (dotnet Entity Framework Tools)
Microsoft.EntityFrameworkCore.Design 

### Migrations Problems (recover from updated migration in sqlite)
- drop database from ef
- remove desired migration
- re-apply migrations without the undesired one


