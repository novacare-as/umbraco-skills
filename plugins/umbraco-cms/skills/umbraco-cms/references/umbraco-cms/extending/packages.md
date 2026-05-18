# Packages

## Contents

- [Create accessible Umbraco packages | CMS](#create-accessible-umbraco-packages-cms)
- [Creating a Package | CMS](#creating-a-package-cms)
- [Example Package Repository | CMS](#example-package-repository-cms)
- [Good practice and defaults | CMS](#good-practice-and-defaults-cms)
- [Installing and Uninstalling Packages | CMS](#installing-and-uninstalling-packages-cms)
- [Language file for packages | CMS](#language-file-for-packages-cms)
- [Listing a Package on the Umbraco Marketplace | CMS](#listing-a-package-on-the-umbraco-marketplace-cms)
- [Maintaining packages | CMS](#maintaining-packages-cms)
- [Packages on Umbraco Cloud | CMS](#packages-on-umbraco-cloud-cms)

---

## Create accessible Umbraco packages | CMS

Creating accessible packages extends on accessibility in an .

The Umbraco UI components have been built to be accessible and have accessibility tests built within them. Building the user interface (UI) using these ensures that the package is as accessible as the Umbraco backoffice.

In addition, any fixes and updates to the UI components will be pushed through to the packages when you rebuild them with the updates.

Accessibility testing is more a specialist skillset than it is automated testing. The purpose of this document is to outline what can be done to help build accessible packages. It is not a complete list of accessibility tests that can be performed.

Build the components using the as these have accessibility tests built within them.

Use the keyboard to tab through the elements on the page checking:

Does the element tabbed to have a

**focus state**?Does the

**tab order**make sense?More on focus, tab orders, other common interactions and techniques for keyboard testing can be found at


Check the UI with a screen reader.


and some guidelines on screen reader testing are available from[Non Visual Desktop Access (NVDA) is a free Windows screen reader arrow-up-right](https://www.nvaccess.org/download/)

Install an accessibility testing tool as a plugin into your browser to run automated tests:

Tools like are built to reduce the number of false positives in a test.


If the UI does not follow the Umbraco Style, then check the contrast with a tool like the


. This will help ensure contrast.[Web Content Accessibility Guidelines (WCAG) Contrast Checker arrow-up-right](https://chrome.google.com/webstore/detail/wcag-color-contrast-check/plnahcmalebffmaghcpcmpaciebdhgdf)

Last updated

Was this helpful?

---

## Creating a Package | CMS

Tutorial to create a package in Umbraco

Creating a Package Schema in the Backoffice

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ec89f4f933fb29af28260ca51321fb8930ee1b35%252Fcreate-package.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c6c46063&sv=2)

Package Content section

| Property | Value | Note |
|---|---|---|
| Content | Empty | Here, you can include content. For example, if you want to create a starter kit. Not relevant for this package though. |
| Media | Empty | Here, you can include media. For example, if you want to add media to the starter kit. Not relevant for this package though. |
| Document Types | Empty | Similar to the Content picker above. If you include content, you will also need to pick all its dependencies in this and the next steps for them to be packaged together. |
| Media Types | Empty | Similar to the Media picker above. If you include media, you will also need to pick all its dependencies in this and the next steps for them to be packaged together. |
| Languages | Empty | See `Document Types` above. All text is hardcoded or within the lang folder in this package, so this is not needed. |
| Dictionary | Empty | See `Document Types` above |
| Data Types | Empty | See `Document Types` above |
| Templates | Empty | See `Document Types` above |
| Stylesheets | Empty | These will come from the wwwroot/css folder. If you have stylesheets you want to include from other locations (like App_Plugins folder) you can do so at a later step. |
| Scripts | Empty | These will come from the wwwroot/scripts folder. If you have scripts you want to include from other locations (like App_Plugins folder) you can do so at a later step. |
| Partial Views | Empty | See `Document Types` above |

Inspecting the Package ZIP

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9350caff0ed917f43d7faaef303713aad0d542c2%252Fzip-package-contents.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=817e2607&sv=2)

Creating a NuGet package

Generate an Empty Package Using a Template

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-80e276ce065a844f7c99a4f1fc258ed639ae8025%252Fempty-package-from-template-v15.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=998d0ffc&sv=2)

Transfer Files

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-698037168877590c00bfd8ad3703a74b03bc05e3%252Fapp-plugins-content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=46d6ec2b&sv=2)

Specify Package Properties

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8312d1e8cf743bd5d21bf4b63426463d51599c04%252FPackage-properties-Visual-Studio.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7ede7694&sv=2)

| Property | Value | Note |
|---|---|---|
| Version | 1.0.0 | This is automatically set to 1.0.0 but can be changed as appropriate. |
| Authors | Your name | Here you get to take credit for your awesome work! |
| PackageProjectUrl | https://umbraco.com | This URL will be shown as the package's URL when others install it. It will likely be a GitHub repository, or similar. |
| PackageLicenseExpression | MIT | The license is set to MIT. Please consider how you want your package licensed. If in doubt when deciding an open-source license there are
|

Pack the Package

Default Output

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0e53c020cae74043521ba7f8e79f71fb13bf514b%252Fpackage-default-location.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=199039c7&sv=2)

Custom Output Location

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6d6d28f8af879e0d6cd64c37ecee27a775094644%252Fpackage-custom-folder.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=bfec348c&sv=2)

Publish the Package

Installing a NuGet Package

Package Migration

Automatic Package Migration

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f3ac2e59a1ab0ab32ab5aefbf5a857a612902388%252Fembeded-resource.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6b5d807d&sv=2)

Custom Package Migration

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ee8e0b6a49e3c54668798df7378ed701ae80f89e%252Fembeded-resource-props.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e92e4a20&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4b85628f1a0b5026e9db6eec8c901eaecc63183e%252Fembeded-zip-resource.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3d29695&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-715cf1f9bcb94da8762ce88e4551710be2d3e45b%252Finstalled-package.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=632ef716&sv=2)

Attended/Unattended migration execution

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c6f31569b0206b9c7d32aa2707b1096996736362%252Fpackage-install-attended.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=28c4a5df&sv=2)

Last updated

Was this helpful?

---

## Example Package Repository | CMS

Suggestions for organizing an Umbraco package source code repository.

There are many ways to build and deploy your package to NuGet. You will likely have your own approach for organizing a solution and preferred tools for build and deployment.

It may be useful to review some practices shared here on how packages are built at Umbraco.

Some add-ons to the CMS created by Umbraco are closed-source, but some are made freely available with open-source repositories. An example is , which has a source code repository .

The solution consists of three projects.

The lives in `src/<ProjectName>`

. The project file contains a dependency on Umbraco CMS:

```
<PackageReference Include="Umbraco.Cms.Web.BackOffice" Version="[10.0, 14)" />
```

Here, an upper bound is provided on the package. This ensures that developers can only install it into projects that are using versions of Umbraco that the package has been tested with.

When the next major version of Umbraco is released, the range is tested and either extended or a new version is released, as appropriate.

There is a in `tests/<ProjectName>.Tests`

. It contains references to `Umbraco.Cms.Tests`

and a project reference to the package:

```
<ProjectReference Include="..\..\src\Umbraco.AuthorizedServices\Umbraco.AuthorizedServices.csproj" />
```

Finally there's an that is used for manual testing of the package. It also has a project reference to the package project, allowing updates to be tested as they are compiled.

As well as the projects, the following files are added to the solution:

`[.artifactignore](https://github.com/umbraco/Umbraco.AuthorizedServices/blob/main/.artifactignore)`

- used by Azure DevOps services to

. This helps to reduce pipeline execution time.[control which files are uploaded when you publish arrow-up-right](https://learn.microsoft.com/en-us/azure/devops/artifacts/reference/artifactignore?view=azure-devops)`[.editorconfig](https://github.com/umbraco/Umbraco.AuthorizedServices/blob/main/.editorconfig)`

- used to for multiple developers working on the same project across editors and IDEs.`[.gitignore](https://github.com/umbraco/Umbraco.AuthorizedServices/blob/main/.gitignore)`

- controls which files are added to source control.`[.globalconfig](https://github.com/umbraco/Umbraco.AuthorizedServices/blob/main/.globalconfig)`

- provides .`[Directory.Build.props](https://github.com/umbraco/Umbraco.AuthorizedServices/blob/main/Directory.Build.props)`

- used to provide common settings across all projects in the solution.`global.json`

- ensures that the solution is always . Added when a solution targets a single Umbraco major version.`[LICENSE.md](https://github.com/umbraco/Umbraco.AuthorizedServices/blob/main/LICENSE.md)`

- indicates the license through which the code is available.`[README.md](https://github.com/umbraco/Umbraco.AuthorizedServices/blob/main/README.md)`

- a top-level documentation page for the source code repository.[

`icon.png](https://github.com/umbraco/Umbraco.AuthorizedServices/blob/main/icon.png)`

- an icon used for the package on NuGet and the Umbraco Marketplace.`[umbraco-marketplace.json](https://github.com/umbraco/Umbraco.AuthorizedServices/blob/main/umbraco-marketplace.json)`

- provides

.[additional details about the package when listed on the Umbraco Marketplace arrow-up-right](/umbraco-dxp/marketplace/listing-your-package)`[version.json](https://github.com/umbraco/Umbraco.AuthorizedServices/blob/main/version.json)`

- provides package versioning information for use by . This tool is used for generating version numbers.

Azure DevOps pipelines are used for continuous integration and releasing new versions of the package. The definition of how the project is built is defined in a `.yaml`

file that's part of the source code repository.

The file can be found .

Even if using another tool, it may be worth reviewing how the pipeline has been set up. It may be that you can setup something similar with your own provider.

The build consists of two stages: building the solution and running unit tests. Only if both succeed is the build as a whole considered successful.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-763fbe991d381b3bcae7fe66fc4aefc86148a5e2%252Fazuredevops-build.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a32d850&sv=2)

The package is released manually in Azure DevOps, with a two-stage process. Firstly, the package is released to a "pre-releases" feed, and then after manual approval, to NuGet.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-426d86e170cd3fb9ae2287d35c4b0d908178bcc2%252Fazuredevops-release.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7108696c&sv=2)

Last updated

Was this helpful?

---

## Good practice and defaults | CMS

Information on good practices and common defaults for Umbraco package development.

This document provides guides and notes on package development. It includes good practice guidelines that will help you maintain and support your package through multiple releases and versions of Umbraco. These good practices are not prescriptive, but offer a guide as to what often works well, and not-so-well, when developing packages for Umbraco.

To extend the Umbraco backoffice, a package can provide files such as `umbraco-package.json`

and TypeScript/JavaScript files that should be stored within the `App_Plugins`

folder. It's recommended to put all files in a subfolder with a unique name, preferably using the package name, like `App_Plugins\MyPackage`.


For more information on how to extend the Umbraco backoffice, have a look at the [customizing the backoffice documentation](/umbraco-cms/customizing/overview)

Files in the `App_Plugins`

folder will be publicly available on the website even though they are not in the `wwwroot`

folder. You should not store sensitive information in the `App_Plugins`

folder.

Files in the `App_Plugins`

folder should be considered immutable. This means that they are not something a user of your package is expected to change on their site.

The default delivery method for files to the `App_Plugins`

folder is via a `.targets`

file within a package. This means when a website is built, the files in this folder are copied over from the NuGet cache. When this happens, any changes a user might have made to these files will be lost. Equally, if the user performs a `dotnet clean`

on a solution, all files in the `App_Plugins`

folder will be deleted.

If you have files that you expect users of your package to alter you should not place them in the `App_Plugins`

folder.

Views are used to render content on the front end of a website. If your package provides a way for the user to present the content publicly, you should copy these files to the views folder.

As the files will still be copied during build you should ensure your target file does not overwrite newer or altered files. You should also ensure that it doesn't delete files on clean.

When you have a package that contains many views you might consider building a dotnet template or Razor Class Library (RCL) instead. By doing this, the files will not pollute your user's solutions.

Umbraco products store their licenses in `/umbraco/Licenses`

. It is recommended for third-party packages that require license files to also store their license files in this location.

The default `.gitignore`

for Umbraco templates will include any files in the `/Licenses`

folder while ignoring most of the rest of the Umbraco folder.

The `/umbraco/Licenses`

folder does not exist on a fresh installation of Umbraco. You need to create it manually before you save your license file to this folder.

Umbraco a .NET application and can be run on multiple operating systems (Windows, Linux and macOS). When developing packages there are a few things you should be aware of for your package to run on all possible operating systems.

The Linux and macOS file systems are case-sensitive by default. This means that `App_Plugins/myPackage`

is a different location from `app_plugins/MyPACKAGE`

. When building your package you should ensure that you always refer to folders and paths in a consistent way.

A good way to ensure consistency is to use constants in your code to define file or folder locations.

You can adjust the case sensitivity of a Windows folder by running a command against a newly created/empty folder:

Some folders within Umbraco will already exist for all installations. If you access these folders, you need to be aware of the case used to ensure you end up in the correct place:

| Folder | Note |
|---|---|
| /App_Plugins | Uppercase `A` and `P` |
| /App_Plugins/[Ll]ang | Uppercase `L` |
| /Views | Uppercase `V` |
| /umbraco/Licenses | Lowercase `u` and uppercase `L` |
| /config | Lowercase `c` |

If you create a custom section/tree, Umbraco will build paths based on the name of that section or tree. These folder paths will be case-sensitive.

For example: if you have a custom tree with the `treeAlias`

of `MyCustomTree`

Umbraco will look for files in `App_Plugins\MyPackage\backoffice\MyCustomTree\`.


You should never hardwire a file or folder location into code. Instead, it is recommended to follow either of the options below:

Access files using the ASP.NET Core file providers from

`IHostingEnvironment`

.Use the built-in methods to access well-known locations (see below).


The location of the Umbraco temp folder can be controlled via configuration and cannot be assumed. Use the `IHostingEnvironment.LocalTempPath`

variable to locate the temp folder.

If you require the path of a folder relative to the site root, you can use the `IHostingEnvironment`

method to map a path:

It is not recommended to assume things about the folder structure of a site or use direct I/O commands to access the file system. Access to the disk within an ASP.NET Core site is usually managed with File Providers. You can access the file providers from the `IWebHostEnvironment`

class.

Example: If you want to read `robots.txt`

from the `wwwroot`

folder, use `WebRootFileProvider`

in a controller to get to the root of the site and read the file:

This is the preferred method for file I/O. Not all files served up by a site are placed in the `wwwroot`

folder when you expect them to be. This is especially true if the site is using Razor Class Library projects to insert static files.

Building folder path strings manually can cause problems when swapping between file systems. Windows uses the backslash character ('\') to separate folders and files while Linux uses the forward slash ('/').

On Windows, a file might be located at `d:\website\robots.txt`

while on Linux this might look like `/home/website/robots.txt`

instead.

You should use the .NET `Path`

methods wherever possible when building paths to ensure that the correct path is built:

If you need to build a path manually, use `Path.DirectorySeparatorChar`

instead to get the correct separator for the file system.

Most packages will require some settings to be stored for the users to control in order to change the behavior of the package. Where you store these settings will depend a lot on the nature of the package.

Property Editors should store their settings as part of their Data Type in Umbraco. This is the standard way property editor behavior is controlled while it is familiar to users and supported by deployment tools.

You should not alter `appsettings.json`

via code.

Settings in ASP.NET Core are merged from a number of different locations at runtime. You cannot guarantee that `appsettings.json`

is the location that a setting is read from and your users may not want certain settings in that file. You can read settings from the configuration, but you cannot assume they have come from `appsettings.json`.


There are many options for where you might save your settings and a lot will depend on the nature of your package.

Below you can find pros and cons for different places where you might save the settings for your package.

Settings can be saved to the database. Settings can be stored in the database using the Umbraco `IKeyValueService`

, and for more complex settings you can use a custom database table.

Pros:

Settings will be accessible directly from the database, and not dependent on deployed files on disk.


Cons:

Setup is required to create the database tables for the settings to live in.

The settings will only be available to the specific instance of the site, and any settings will not be deployed between a local, development, or staging site.



You can choose to save the settings to disk. As an example, the settings can be saved in the `/config`

folder at the root of the site.

Pros:

Settings will be accessible to the site and can be included in deployments between sites.


Cons:

You cannot guarantee that the folder or files will be present on a site or that they will be writable.

Using your own config means your users cannot harness the power of the .NET Core configuration system and move settings to environment variables or other key/value stores. This means that sensitive information may end up on disk.



You could choose to provide your users with a snippet they can copy into their `appsettings.json`

file. This will ensure that the settings are stored in the correct location.

Pro: Allows your users to fully control how and where the settings are stored (eg. secure key/value stores).

Con: Requires the user to edit files on disk to get the settings in place.


Last updated

Was this helpful?

---

## Installing and Uninstalling Packages | CMS

The process of installing and, in turn, uninstalling packages in your Umbraco CMS website.

This article will cover the process of installing as well as uninstalling packages from your Umbraco CMS website.

In the Umbraco Backoffice, you will find a **Packages** section that displays the . From here you can browse all community-made as well as official Umbraco packages for the Umbraco CMS.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f14549ef229e55991723d8b0c44d6f623b81fec2%252Fbackoffice-packages-section.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=41074124&sv=2)

Navigating to a specific package in the section will present you with an overview of the package, as well as an install snippet for NuGet CLI.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c31ad8034781bae8ad4d4fc5d47c533d30cc524c%252Fbackoffice-packages-section-package.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3c1be737&sv=2)

The packages can be installed by using:

**NuGet Package Manager**in Visual Studio**Package Manager Console**in Visual Studio.NET CLI (usually accessible from the terminal/command prompt of your system)


For example, to install the StarterKit package for the Umbraco CMS the command would be:

`dotnet add package Umbraco.TheStarterKit`


Navigating to the NuGet Package Manager in Visual Studio is more visual, and gives you an overview of already installed packages.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-95d91944f82b7c89ed65482941f79d90b9046110%252Fnuget-installing-options.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5fbde2fd&sv=2)

The Package Manager has an integrated search function that allows you to find any public NuGet package and install it on the project.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d5e1b3b80a51cbc68d50cac8cadb03eb7f135d71%252Fnuget-package-in-manager.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e9227260&sv=2)

Once the package has been installed, it will show up under the **Packages** section in the backoffice, under **Installed** tab.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-74651ae2ada6088d39c4a981f9951a2558c13078%252Fbackoffice-installed-packages.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c7c485f5&sv=2)

Uninstalling packages is not always as straightforward as installing them.

In this section, we will provide two examples of uninstalling a package - the StarterKit package and the SEOChecker package.

Keep in mind that this particular guide targets a specific package. There are many packages out there, and each one is different. The exact steps presented here might not work the exact same way for all the packages, though the general approach should still apply.

The Starter Kit provides you with a boilerplate website solution to build upon. The package installs Document Types, Templates, media, content, and everything else needed to set up a small website. There is little custom code/functionality involved which is usually the case for such starter kit or sample-site packages.

To uninstall a package, either run a command or use the NuGet Package Manager in Visual Studio.

`dotnet remove package Umbraco.TheStarterKit`


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b63cc056930545ac457bf540403bbac90472dece%252Funinstalling-via-nuget-package-manager.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=21ecc3f2&sv=2)

It is recommended to clean the solution after removing any package. This can be done by right-clicking the project in Visual Studio and choosing the *Clean* option, or using the `dotnet clean`

command.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-435e2505b065bec324bda14b419b98bde6bf9cb8%252Fvs-cleaning-solution.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=669a3a9b&sv=2)

With packages like the StarterKit, the process does not end there. While the package is gone, content - and everything else needed for the website - is still available in the backoffice. To fully remove this kind of package, additional steps are needed.

### Remove content provided by the package

There is no universal way to tell what content comes from a package, and what content is custom-made. In the Content section, delete individual nodes accordingly. If the goal is to fully remove the package and clean the site, all the content can be removed (and the recycle bin emptied).

![Backoffice - removing content](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-3fa0db3b6ade4248ad6eca2ccec56533bd6d30b6%252Fremoving-content.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=4897e6ee&sv=2)


### Remove media provided by the package

Similar to content, media also might have to be removed.

![Backoffice - removing media](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-160ccfac9f626757133c5e7f62dcc79e18b3902c%252Fremoving-media.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=f0dedd1e&sv=2)


### Remove Document Types

Document Types can be removed from the **Settings** section. If fully removing the package, all Document Types can be deleted, as there are no default Document Types in a clean-slate Umbraco installation.

![Backoffice - removing document types](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-40d0ad2a49dc4902205d46de18e532169959f7d7%252Fremoving-document-types.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=d980e24c&sv=2)


### Removing Data Types

As opposed to Document Types, there are some Data Types that are available out of the box when Umbraco is installed. It is not recommended to remove them. The safe approach is to delete any item that starts with a Document Type prefix and includes multiple dashes. That is the default naming convention for new configurations of Data Types (Example: "Blog - How many posts should be shown - Slider")

![Backoffice - removing data types](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7cd36ad62eb0389a2534a0ff02b1f15504d730a9%252Fremoving-datatypes.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=a90381fd&sv=2)


### Removing Templates

No Templates are available out of the box in a new installation. If cleaning up after a package, it would be okay to delete all that are present

![Backoffice - removing templates](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-08beb8e2c15080b93eb9f23d707d4ac8481b63b7%252Fremoving-templates.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=67edbb83&sv=2)


### Removing Partial Views

Out of the box, there are a few views available in the `blocklist`

and `grid`

folders. Everything else can theoretically be removed.

![Backoffice - removing partial views](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1fc93d8ccaa66b1bea6322d24903d837a13f1a96%252Fremoving-partials.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=4dd72a9&sv=2)


### Cleaning leftover files on disk

Some packages might reference other items. For example, installing the StarterKit also adds `Bergmania.OpenStreetMap`

to your project. That component will show up as installed in the backoffice even after uninstalling the NuGet package.

![Backoffice - Packages section - leftover dependency](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-48ee681032083c03d19ae29af292a5293381b095%252Finstalled-package-leftovers-backoffice.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=5b63e499&sv=2)


In many cases, custom dashboards, editors, and scripts are left in the `App_Plugins`

folder after a package has been uninstalled via NuGet. These files also have to be deleted manually.

![Visual Studio - App Plugins leftover files](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f69d24e28df3347051cd4dad7565036bfabe7b50%252Fapp-plugins-starterkit.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=61623168&sv=2)


Keep in mind that this particular guide targets a specific package. There are many packages out there, and each one is different. The exact steps presented here might not work the exact same way for all the packages, though the general approach should still apply.

More advanced packages that add functionality on top of Umbraco, usually rely on providing custom, compiled code. That being said, many of such packages also implement custom Sections, Dashboards, editors, and views.

In this example, we will be using the SEOChecker package. This package allows developers of the site to add custom properties to Document Types used to track search engine optimization practices.

An example use case of the SEOChecker property on a Document Type, as presented in the Content section:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5c83b0d11e64ac92893bdd38a8e3df0d166c4557%252Fseochecker-content-section.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=38738f05&sv=2)

To uninstall the SEOChecker from a website, the first step is to remove the package via a `dotnet`

command or use the NuGet Package Manager.

The following command can be used for uninstalling the package:

`dotnet remove package SEOChecker`


After that, cleaning the solution is recommended.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-435e2505b065bec324bda14b419b98bde6bf9cb8%252Fvs-cleaning-solution.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=669a3a9b&sv=2)

### Cleaning leftover files on disk

While uninstalling the package would remove most of the custom code, the `App_Plugins`

folder has to be cleaned manually.

![SEOChecker files in App Plugins](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b2b2ec0b92c61de8604c1ef3b6253b4f59eda29d%252Fseochecker-app-plugins.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=6eb2ce69&sv=2)


Removing *seochecker* folder from `App_Plugins`

will clean up the leftover backoffice section and dashboards.

If content on the website relies on having a custom Property Editor or a data source installed, those properties will default to a `label`

Data Type. All previously saved content in the property will in turn be converted to a string.

In the case of the SEOChecker, the custom property added from the package would look like this after all the package files have been removed:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9eb77e233095cb3f32571f92c3b656f2a54c0c5a%252Fseochecker-after-removal.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=20d71f2a&sv=2)

Depending on the packages and the implementation, rendering of content from custom editors, or any frontend functionality dependent on external code, might not work correctly. It is always recommended to inspect the frontend of the site after removing any packages.

Last updated

Was this helpful?

---

## Language file for packages | CMS

Information on how to use language files to make your Umbraco package UI support multiple languages

```
{...
  "name": "MyPackage",
  "extensions": [
    {
      "type": "localization",
      "alias": "MyPackage.Localize.En",
      "name": "English",
      "meta": {
        "culture": "en"
      },
      "js": "/App_Plugins/MyPackage/Localization/en-us.js"
    }
  ]
}
```

[Previous Creating a Package chevron-left](/umbraco-cms/extending/packages/creating-a-package)

[Next Listing a Package on the Umbraco Marketplace chevron-right](/umbraco-cms/extending/packages/listing-on-marketplace)

Last updated

Was this helpful?

---

## Listing a Package on the Umbraco Marketplace | CMS

Information on how to list your package on the Umbraco Marketplace.

Last updated

Was this helpful?

Information on how to list your package on the Umbraco Marketplace.

The is a website built and maintained by Umbraco HQ to support searching and reviewing packages.

It lists all commercial and open-source packages that the community has made available on NuGet.

More information, including details of the steps for listing, are available at the dedicated .

Last updated

Was this helpful?

Was this helpful?

---

## Maintaining packages | CMS

Once you've created and published your package, here is what's involved in it's ongoing maintenance

Updating with new Umbraco major versions

Referencing Umbraco dependencies

```
<PackageReference Include="Umbraco.Cms.Web.BackOffice" Version="10.0.0" />
```

```
<PackageReference Include="Umbraco.Cms.Web.BackOffice" Version="[10.0.0, 13)" />
```

Manage feature requests and issues

Package no longer required?

Last updated

Was this helpful?

---

## Packages on Umbraco Cloud | CMS

Things to consider for package development and usage in Umbraco Cloud

If you want to use or develop packages for Umbraco Cloud there are a few things to consider and be aware of. The two most important things to know about are

When developing a package you will sometimes store data, this can be data in many forms - Umbraco schema / content, package settings, etc.

When you develop a package for Umbraco Cloud there are a few things to be aware of when storing data, mainly whether you want that data to be specific to 1 environment or more.

Let's take a look at the most common ways of storing data in packages - and what to watch out for on Cloud.

A [migration](/umbraco-cms/extending/database) is some code that you run as part of a migration plan. That migration plan has an ID that is stored in the database (in the KeyValue table). This means that when you add new migrations Umbraco will only execute the ones that came after the one with the stored ID. The most important difference between a migration and a package action is when they are initialized. A package action runs on package install and uninstall, whereas a migration will run whenever you want it to run, see below for common examples.

As migration runs are stored in the database of the site it also means that they will run on each environment you trigger them on. The most common way to trigger a migration is to include them in a [composer](/umbraco-cms/implementation/composing), which will ensure they run on site startup. This means any commands you have in your migration will automatically run when the site starts up. When your package code is pushed to a new environment it will run them from the beginning on that environment as no ID is saved in the database.

This is normally a good thing. However if you generate any Umbraco schema then Umbraco Deploy will automatically create based on that schema, and commit them to source control. This means that when you deploy all your files to the next environment the migration will run again, create duplicates and generate duplicate UDA files, which could end up causing a lot of issues.

You could consider creating Umbraco schema only during a package action, and then running things like creating database tables in migrations. Another good workaround could be to not run the migrations in a composer, but rather create a dashboard for the package where the user can choose which migrations to run themselves. The has an example of this.

You may sometimes choose to save data in a file. Could be a separate config file for your package or a to add an app setting to the web.config. If you do this be aware of two things:

If these files are generated on a Cloud environment they will not be stored in source control, and will be overwritten on next deployment. They need to be installed locally, committed to source control and then pushed up to the Cloud environments. We have an

[existing feature request](/umbraco-cms/reference/mapping)on allowing package creators to commit their files directly on Cloud, and it is possible to do so currently but not in a supported way, and it may change suddenly.If you need the content of the files to be different on the different environments you will need to use environment specific .


A value connector is an extension to Umbraco Deploy that allows you to transform data when you deploy content of any kind between environments. When it comes to packages, one reason you need to consider these if you are supporting deploying content properties that rely on integer IDs. Content and other Umbraco data has two identifiers - an integer and a GUID. The GUID is consistent between environments but the integer ID is not. As such, if transferring content between environments and relying on integer IDs, you'll need to include a value connector to transform the value.

They also manage dependencies for property data. If you save an ID of an image in your property editor, you can make sure the related image media item is transferred too.

You can read more about value connectors and other extensions to Umbraco Deploy .

Last updated

Was this helpful?

---
