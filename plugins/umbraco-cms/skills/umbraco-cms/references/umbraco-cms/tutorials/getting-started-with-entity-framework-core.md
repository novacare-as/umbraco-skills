# Creating Custom Database Tables with Entity Framework | CMS

Learn how to create custom database tables in Umbraco using Entity Framework Core, including migrations, composers, and notification handlers.

Custom database tables allow you to store additional data in the Umbraco database that you don't want to store as normal content nodes.

Use custom tables when:

You need to store large datasets.

The data does not need backoffice editing.

You want better performance by decoupling data from Umbraco content.

The data should not be indexed or cached as content.


Data stored in custom database tables:

Is not manageable from the backoffice by default.

Requires custom implementation for editing or display.

Is not automatically synchronized between environments.

Is not deployable using Umbraco Deploy by default.


Ensure the following requirements are met before starting:

An existing Umbraco project with content.

The

`Umbraco.Cms.Persistence.EFCore`

NuGet package installed.If your model and context live in a separate project, that project must also reference:

`Microsoft.EntityFrameworkCore`

`Microsoft.EntityFrameworkCore.Relational`


Install the EF Core CLI tool by running the following command in your terminal:

`dotnet tool install --global dotnet-ef`.


For .NET 10 Compatibility: To avoid Roslyn compiler version conflicts during migration generation, ensure the following packages are explicitly added to your

`.csproj`

. Match the version required by your EF Core Design tools:`Microsoft.CodeAnalysis.CSharp`

(Version 5.0.0 or later)`Microsoft.CodeAnalysis.CSharp.Workspaces`

(Version 5.0.0 or later)`Microsoft.EntityFrameworkCore.Design`

(Version 10.0.x)


You will:

Create a file named

`BlogComment.cs`

.Add the following code:


Create a file named

`BlogContext.cs`

.Add the following code:


The `DbContext`

must be registered so Umbraco can resolve it. The recommended place to register it is inside an `IComposer`.


Create a file named

`BlogCommentsComposer.cs`

.Register the context using

`AddUmbracoDbContext`

inside the`Compose`

method:

Using `UseDatabaseProvider(providerName, connectionString)`

is the recommended approach. It reads the provider name and connection string directly from your Umbraco configuration (`appsettings.json`

). It works correctly for SQL Server, SQLite, and any other supported database without any hardcoding.

The `shareUmbracoConnection: true`

argument tells Umbraco that your `DbContext`

uses the Umbraco database. EF Core queries then run on the same connection and transaction as Umbraco's own data access. See [Using a separate database](/umbraco-cms/tutorials/getting-started-with-entity-framework-core#using-a-separate-database) below if your `DbContext`

targets a different database.

The database can now be accessed via `BlogContext`

. Before using it, generate a migration to create the custom tables. With EFCore, migrations can be auto-generated from the terminal.

Open your terminal.

Navigate to your project folder.

Run the following command to generate the migration:


If your models and `DbContext`

reside in a separate library like `Project.Core`

, while `Project.Web`

is the startup project, follow these steps:

Navigate to the class library folder, for example,

`/Project.Core`

Run the following command with the relative path to your startup project:


In this example, the migration is named `InitialCreate`

. You can choose any name you like.

The `DbContext`

class in this example is named `BlogContext`

. If you've used a different name, make sure to update the `--context`

argument accordingly.

When working with EFCore you would normally inject your `Context`

class directly. You can still do that, but it is not the recommended approach in Umbraco.

In Umbraco, the `Scope`

concept is an implementation of the `Unit of work`

pattern. This ensures that a transaction is started when using the database. If the scope is not completed (for example when an exception is thrown), it will roll back automatically.

To ensure migrations are applied automatically at startup:

Create a file named

`RunBlogCommentsMigration.cs`

.Implement

`INotificationAsyncHandler<UmbracoApplicationStartedNotification>`

.Add the following code:


Open

`BlogCommentsComposer.cs`

.Add the handler registration inside

`Compose`.


After registering the notification handler:

Build the project.

Run the application.

Open your database.

Confirm that the

`blogComment`

table has been created.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f5bae6652167e776ebfde12d72396efb7b3569e5%252Fdb-table%2520%281%29.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=21eed915&sv=2)

If you are using the default SQLite database, you cannot use SQL Server Management Studio (SSMS) to view your tables. Use a tool like **DB Browser for SQLite** and open the file located at `/umbraco/Data/Umbraco.sqlite.db`.


The custom database tables are now available to work with through Entity Framework.

To create, read, update, or delete data from your custom database tables, use the `IEFCoreScopeProvider<T>`

(where `T`

is your `DbContext`

class) to access the EFCore context.

The example below creates a `BlogCommentsController.cs`

file with an `UmbracoApiController`

to fetch and insert blog comments from a custom database table.

This example uses the `BlogComment`

class directly as a database model. The recommended approach would be to map it to a ViewModel instead, so your database and UI layers are not coupled. Error handling and data validation have been omitted for brevity.

By default, `AddUmbracoDbContext<T>(..., shareUmbracoConnection: true)`

binds your `DbContext`

to Umbraco's database connection and transaction scope. Every EF Core query runs against the Umbraco database, and writes commit or roll back together with the enclosing Umbraco scope. That is the right choice when your custom tables live inside the Umbraco database.

If your `DbContext`

targets a **different** database — for example, a separate SQLite file or an entirely different SQL Server instance — pass `shareUmbracoConnection: false`

. Without it, the connection string you configure through `UseSqlite(...)`

or `UseSqlServer(...)`

is replaced at runtime and your queries run against the Umbraco database instead.

When `shareUmbracoConnection`

is `false`

, the custom `DbContext`

has its own connection and transaction. Completing an Umbraco scope does not commit writes made through your EF Core scope (and vice versa). You still use `IEFCoreScopeProvider<T>`

and `IEfCoreScope<T>`

the same way as before — the scope manages the separate connection on your behalf.

The `shareUmbracoConnection`

parameter was added in Umbraco 17.4. Calls to `AddUmbracoDbContext<T>`

without it are marked as obsolete and scheduled for removal in Umbraco 19.

Last updated

Was this helpful?