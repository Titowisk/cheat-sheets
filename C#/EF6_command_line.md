# Cheat Sheet of EF 6 commands for code-first approach

## NAME
    **Get-Migrations**
    
SYNOPSIS
    Displays the migrations that have been applied to the target database.
    
    
SYNTAX
```
Get-Migrations [-ProjectName <String>] [-StartUpProjectName <String>] [-ConfigurationTypeName <String>] [-ConnectionStringName <String>] [-AppDomainBaseDirectory <String>] [<CommonParameters>]
    
Get-Migrations [-ProjectName <String>] [-StartUpProjectName <String>] [-ConfigurationTypeName <String>] -ConnectionString <String> -ConnectionProviderName <String> [-AppDomainBaseDirectory <String>] [<CommonParameters>]
```

    
DESCRIPTION

Displays the migrations that have been applied to the target database.
    
---

## NAME
    **Update-Database**
    
SYNOPSIS

Applies any pending migrations to the database.
    
    
SYNTAX
```

Update-Database [-SourceMigration <String>] [-TargetMigration <String>] [-Script] [-Force] [-ProjectName <String>] [-StartUpProjectName <String>] [-ConfigurationTypeName <String>] [-ConnectionStringName <String>] [-AppDomainBaseDirectory <String>] [<CommonParameters>]
    

Update-Database [-SourceMigration <String>] [-TargetMigration <String>] [-Script] [-Force] [-ProjectName <String>] [-StartUpProjectName <String>] [-ConfigurationTypeName <String>] -ConnectionString <String> -ConnectionProviderName <String> [-AppDomainBaseDirectory <String>] [<CommonParameters>]
```
    
DESCRIPTION
    Updates the database to the current model by applying pending migrations.
