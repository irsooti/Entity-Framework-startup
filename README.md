# Startup a project with EF Core
 To get started a new project wich depends upon Entity Framework there are some preliminar steps to follow.
 First of all, we have to install all these following packages, paying attention of the  database you want to use.

## Index
 - [Initial project configuration](#Initial_project_configuration)
 - [Scaffolding existing database](#Scaffolding_existing_database)

## Prerequisites
 - Visual studio code
 - This project uses the Sakila database, available from mysql site used for demo purpose. If you want to follow this guide step-by-step, you can download Sakila db from [here](./SakilaDB/sakila-db.zip).

## Initial project configuration

 `dotnet add package` - is the command that adds a package reference to a project file.

 - `dotnet add package Microsoft.EntityFrameworkCore`
 - `dotnet add package Microsoft.EntityFrameworkCore.Design`
 - `dotnet add package Microsoft.EntityFrameworkCore.Tools`
 - `dotnet add package Microsoft.EntityFrameworkCore.Tools.DotNet`
 - `dotnet add package Pomelo.EntityFrameworkCore.MySql`
 - `dotnet add package Pomelo.EntityFrameworkCore.MySql.Design`

 **Note:** Remember to change in your `*Project.csproj` these lines

 ```xml
    <PackageReference Include="Microsoft.EntityFrameworkCore.Tools" Version="2.0.1" />
    <PackageReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.1" />
 ```

 in:

 ```xml
    <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools" Version="2.0.1" />
    <DotNetCliToolReference Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.1" />
 ```

 ## Scaffolding existing database


  ### Scaffold from cli
  In order to scaffold (wich means: get my database structure and convert it into some classes in my project), you have to launch this command:

  ```ps
  dotnet ef dbcontext scaffold "server=192.168.42.128;userid=root;pwd=d0808!;port=3306;database=sakila" Pomelo.EntityFrameworkCore.MySql -o Entites
  ```

  Analyzing this command we could say:

  ```ps
  dotnet ef dbcontext scaffold "<MY DATABASE CONNECTION STRING>" <THE PROVIDER> <-o WHERE TO PLACE THE OUTPUT> <MY FOLDER>
  ```
  ### Pluralize the properties in the new DbContext
   The classes generated from the migration now appears like this:

   ```cs
   public partial class sakilaContext : DbContext
    {
        public virtual DbSet<Actor> Actor { get; set; }
        public virtual DbSet<Address> Address { get; set; }
        public virtual DbSet<Category> Category { get; set; }
    // Hidden for brevity
   ```
   In order to pluralize in all project these property without generate any errors, rename them selecting the property and pressing <kbd>F2</kbd>.
   
   Then the expected class should appear like: 
   ```cs
   public partial class sakilaContext : DbContext
    {
        public virtual DbSet<Actor> Actors { get; set; }
        public virtual DbSet<Address> Addressess { get; set; }
        public virtual DbSet<Category> Categories { get; set; }
    // Hidden for brevity
   ```