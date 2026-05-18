# Install the Starter Kit | CMS

Outcome

Steps

Option 1: Install via .NET CLI

```
dotnet add package Umbraco.TheStarterKit
```

```
dotnet build
```

Option 2: Install via Visual Studio

Summary

Last updated

Was this helpful?

Installing the Starter Kit provides a pre-built set of templates, content types, and demo content to explore or kickstart your Umbraco project.

Outcome

You’ll have the Umbraco Starter Kit installed in your local project, ready to explore in the backoffice. This setup adds example content and templates, perfect for learning or quick prototyping.

Steps

You can install the Starter Kit in two ways, depending on your preference:

Option 1: Install via .NET CLI

To install the Starter Kit via the .Net CLI, follow these steps:

Open a terminal in your Umbraco project folder.

Run the following command to add the Starter Kit package:


```
dotnet add package Umbraco.TheStarterKit
```

Build the project:


```
dotnet build
```

Run the project:


Go to

`https://localhost:xxxx/`

to view the Starter Kit content.

Option 2: Install via Visual Studio

To install the starter Kit via Visual Studio, follow these steps:

Open your Umbraco project in Visual Studio.

Go to

**Tools**->**NuGet Package Manager**->**Manage NuGet Packages for Solution...**.Browse for

**Umbraco.TheStarterKit**.Select the appropriate version from the Version drop-down depending on the Umbraco version you are using.

Click

**Install**.Open the

**.csproj**file to make sure the package reference is added:

Summary

You now have a fully functional Umbraco site with demo content, templates, and structure to explore. Use this setup as the foundation for the upcoming lessons in this Starter Kit tutorial.

If `Umbraco:CMS:Runtime:Mode=Development`

and `Umbraco:CMS:ModelsBuilder:ModelsMode`

is set to `SourceCodeAuto`

or `SourceCodeManual`

, an error occurs the first time the app runs.

To fix this, log into **Umbraco Backoffice**, go to **Settings** → **Models Builder**, and click **Generate Models**. Restart the app to clear the error.

Last updated

Was this helpful?

Was this helpful?

```
dotnet run
```

```
<ItemGroup>
<PackageReference Include="Umbraco.TheStarterKit" Version="xx.x.x" />
</ItemGroup>
```