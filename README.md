![icon](https://raw.githubusercontent.com/uid100/EF_DatabaseFirst/master/images/EntityFramework.png)
# EF_DatabaseFirst
Scaffold Models, Context, Controllers, Views from existing SQL database

[MS-Docs EF Database First tutorial](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/database-first-development/setting-up-database)

The above linked Microsoft tutorial demonstrates:
  * Adding, configuring, and deploying a SQL database project from a Visual Studio Solution
  * Creating a Web App built on MVC Framework using .NET Framework 6 & Entity Framework 6 to scaffold data models and database context
  * Scaffolding simple CRUD Controller Actions and Views based on the existing database
  
The high-level concepts are relevant when applied to .NET Core (and .Net5) applications with the following changes.
   * Add another project to the solution using the ASP.NET Core Web App (Model-View-Controller) [C#] template.
   * Add Entity Framework Packages to the new project ( & _build and set as startup project_ )
      * EntityFrameworkCore
      * EntityFrameworkCore.Tools
      * EntityFrameworkCore.SqlServer
      * EntityFrameworkCore.Design
   * Scaffold Models & Context from Nuget Package Manager Console
      * from the correct project directory, and set the default project (from the Console)  [reference](https://docs.microsoft.com/en-us/ef/core/cli/powershell#scaffold-dbcontext)

    Scaffold-DbContext -Connection "_[your_connection_string]_" -Provider Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models


   * Scaffold controllers & views as before
   
   * _note_ After scaffolding, move the line to configure and use the dbcontext from the context file to the startup file.
   
   (Startup.cs)
   
      using [projectname].Models;
      using Microsoft.EntityFrameworkCore;

  (ConfigureServices(...)...)
  
     service.AddDbContext<dbContextName>( opt => opt.UseSqlServer( [connection_string] ) // or configuration lookup.
