# Development Flow

## Contents

- [Umbraco Extension Template | CMS](#umbraco-extension-template-cms)
- [Vite Package Setup | CMS](#vite-package-setup-cms)

---

## Umbraco Extension Template | CMS

Use the `umbraco-extension` .NET template to create a new Umbraco extension.

Umbraco provides a .NET template to help you get started with building extensions for the Umbraco backoffice. This template sets up a new project with all the necessary files and configurations to build an extension. The template is called `umbraco-extension`

and can be used to create a new Umbraco extension project with a single command.

version 9.0 or later

version 22 or later


To install the Umbraco extension template, run the following command in your terminal:

```
dotnet new install Umbraco.Templates::17.1.0
```

The numbers at the end, `x.x.x`

determines the specific version. It is important to match this with the version of the project you're creating the extension project in.

This command installs both the `umbraco`

and `umbraco-extension`

templates, which you can use to create new Umbraco and Umbraco extension projects. If a new Umbraco project has previously been created using `dotnet new umbraco`

, the templates may already be installed.

To create a new Umbraco extension project, run the following command in your terminal. It should be executed in a folder where you want to create the new project, for example, in the root of your solution:

```
dotnet new umbraco-extension -n MyExtension -ex
```

This command creates a new folder called `MyExtension`

with the following files and folders:

`MyExtension.csproj`

: The project file for the extension.`Constants.cs`

: A file containing constants for the extension.`Client`

: A folder containing the source code for the extension, a`package.json`

file, a`tsconfig.json`

file, and the`vite.config.ts`

configuration file.`README.md`

: A readme file with instructions on how to build and run the extension.

The `-ex`

flag indicates that you want to include examples of how to use the extension. This flag is optional, but it is recommended to include it if you are new to building extensions for Umbraco. It will additionally give you:

`Composers`

: A folder containing an example composer that registers a custom Swagger API.`Controllers`

: A folder containing an example API controller for a dashboard.`Client/src/api`

: A folder containing an example API client that calls the API controller.`Client/src/dashboards`

: A folder containing an example dashboard Web Component that uses the API client.

After setup, the dashboard appears in the main **Content** section of the Backoffice.

By default, the Umbraco Extensions project has a reference to the latest version of Umbraco. Specify your preferred Umbraco version for the Extensions template by using the `--version`

flag:

To include the extension in your Umbraco project, you need to add a reference to the extension project in your Umbraco project.

Right-click the

**Dependencies**node in the Umbraco project.Select

**Add Reference**.Choose the

`MyExtension`

project.Click

**OK**.

Run the following command in the root folder of your Umbraco project:

This command adds a reference to the `MyExtension`

project in your Umbraco project. You can then build your Umbraco project and see the extension in action.

To build and run the extension, install the dependencies and start the Vite development server. To do this, run the following commands in the `Client`

folder of your extension project:

The project also builds automatically when running the Umbraco project. To start the Vite development server in watch mode, run the following command:

This command compiles the TypeScript files and copies them over to the `wwwroot`

output folder. Once complete, run the Umbraco project to view the extension in action.

The output files are automatically copied to the `wwwroot`

folder of your Umbraco project. They are also included in the publishing process when you publish your Umbraco project. You can publish your Umbraco project using the following command:

To publish your extension as a package, create a NuGet package. Run the following command in the root folder of your extension project:

This command creates a NuGet package in the `bin/Release`

folder of your extension project. You can then publish this package to a NuGet feed or share it with others.

The `umbraco-extension`

template is opinionated until a certain point. It is a starting point for building extensions for the Umbraco backoffice. The template includes a basic structure and configuration for building extensions, but you can customize it to fit your needs. You can add additional files, folders, and configurations as needed.

To publish your extension as an Umbraco Package, you need some additional files. For details, see the [Umbraco Package](/umbraco-cms/customizing/umbraco-package) article.

Another option is to use the . This is a template that includes all the files and configurations needed to build an Umbraco package. It builds on top of the `umbraco-extension`

template and includes additional files and configurations for building Umbraco packages. This template is a great starting point for building Umbraco packages and includes everything you need to get started.

To install this template, run the following command in your terminal:

To create a new package project, run the following command:

Last updated

Was this helpful?

---

## Vite Package Setup | CMS

Get started with a Vite Package, setup with TypeScript and Lit

Umbraco recommends building extensions with a setup using TypeScript and a build tool such as Vite. Umbraco uses the library Lit for building web components which we will use throughout this guide.

These are general recommendations for working with and building extensions for the Umbraco backoffice. You can use any framework or library of your choice. For Umbraco's recommended approach, see the [Umbraco Extension Template](/umbraco-cms/customizing/development-flow/umbraco-extension-template).

Make sure to read the [Setup Your Development Environment](/umbraco-cms/customizing/development-flow) article before continuing.

Vite comes with a set of good presets to get you quickly up and running with libraries and languages. For example: Lit, Svelte, and Vanilla Web Components with both JavaScript and TypeScript.

Open your terminal and navigate to the folder where you want to create the new Vite package.

Run the following command:


```
npm create vite@latest
```

This command starts a setup prompt.

For this tutorial, it is recommended to use the names given below. However, feel free to choose other names if preferred.

When prompted:

Enter

**client**as the**Project Name**.Select

**Lit**as the framework.Select

**TypeScript**as the variant.

This creates a new folder called

**client**with your project files.

For Windows environments the command should be slightly different::

or you will still see the interactive prompts, especially when using PowerShell.

Navigate into the new

**client**folder and install the packages:

Before proceeding, ensure that you install the version of the Backoffice package compatible with your Umbraco installation. You can find the appropriate version on the .

Install the Backoffice package using the following command, where

`x.x.x`

should be replaced with your Umbraco version:

To avoid installing Umbraco’s sub-dependencies such as the entire Monaco Editor, use the

`--legacy-peer-deps`

flag:

This disables IntelliSense for external references but keeps the install lean.

Open the

`tsconfig.json`

file.Add the array

`types`

inside`compilerOptions`

, with the entry of`@umbraco-cms/backoffice/extension-types`:


Create a new

`vite.config.ts`

file in the**client**folder:

The `outDir`

parameter specifies where the compiled files are placed. In this example, they are stored in the `App_Plugins/client`

folder. If you are working with a different structure, such as a Razor Class Library (RCL) project, update this path to `wwwroot`.


This alters the Vite default output into a **library mode**, where the output is a JavaScript file with the same name as the `name`

attribute in `package.json`

. The name is `client.js`

if you followed this tutorial with no changes.

The source code that is compiled lives in the `src`

folder of your package folder and that is where you can see a `my-element.ts`

file. You can confirm that this file is the one specified as our entry on the Vite config file that we recently created.

The `build:lib:entry`

parameter can accept an array which will allow you to export multiple files during the build. You can read more about .

Build the

`ts`

file in the**client**folder:

To continuously work on the package and have each change built, add a `watch`

script in your `package.json`

with `vite build --watch`.


The example below indicates where in the structure this change should be implemented:

Run `npm run watch`

in the terminal.

Declare your package to Umbraco via a file called `umbraco-package.json`

. This should be added in the `public`

folder under the root of your package. Once built the `umbraco-package.json`

file should be located at `/App_Plugins/`

or `/App_Plugins/{YourPackageName}`

for Umbraco to detect it.

This example declares a Dashboard as part of your Package, using the Vite example element.

Umbraco needs the name of the element that will render as default when our dashboard loads.

This is specified in the

**manifest**as the`elementName`

.Another approach would be to define your default element in the TS code. To do this, in the

`src/my-element.ts`

add

to your**default**`MyElement`

class in the file like so:

Learn more about the abilities of the manifest file in the [Umbraco Package Manifest](/umbraco-cms/customizing/umbraco-package) article.

To test your package, run your site.

Before doing this, make sure to run `npm run build`

to compile your TypeScript files and copy them to the `App_Plugins/client`

folder.

If you try to include some of these resources via Visual Studio (VS), then make sure not to include TypeScript files. Otherwise, VS will try to include a few lines on your `.csproj`

file to compile the TypeScript code that exists in your project folder. When you run your website, VS will try to compile these files and fail.

The final result looks like this:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1a623c467ba67ee5683d23d7f6d9746b0f938a6d%252FVite_Package_Setup_Dashboard.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5b07a237&sv=2)

In the `src/my-element.ts`

file, update the `styles`

property to make any styling changes. You can change the `background-color`

of the `button`

to white so it is more visible:

With this, you have set up your Package and created an Extension for the Backoffice.

In more advanced cases, you can add more elements to your package and create more complex extensions. In that case, you can benefit greatly from creating another project in your solution to hold the files. This way, you can keep your solution clean and organized. We recommend creating a for this purpose. You can read more about this in the [Development Flow](/umbraco-cms/customizing/development-flow#source-code) article.

This Dashboard appears in all sections and does not do much. To extend it to interact with the Umbraco Backoffice, follow the tutorial on [Creating Your First Extension](/umbraco-cms/tutorials/creating-your-first-extension).

Last updated

Was this helpful?

---
