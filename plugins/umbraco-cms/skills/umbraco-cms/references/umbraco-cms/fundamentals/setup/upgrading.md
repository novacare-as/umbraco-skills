# Upgrading

## Contents

- [Downgrades and Re-running Migrations | CMS](#downgrades-and-re-running-migrations-cms)
- [Upgrade Details | CMS](#upgrade-details-cms)
- [Upgrades in Umbraco | CMS](#upgrades-in-umbraco-cms)
- [Upgrade Unattended | CMS](#upgrade-unattended-cms)
- [Version Specific](#version-specific)

---

## Downgrades and Re-running Migrations | CMS

Discusses the possibility of downgrading to a previous version, along with the related topic of re-running the migrations that have occurred during an upgrade

Downgrades are not a supported feature of the Umbraco product.

The primary reason for this is that the Umbraco migration scheme only supports upward migrations.

When updating to a new version, often there are migrations to run that will make changes to the Umbraco schema and data. This is being done to bring the database to a state that will support the functionality of the version being upgraded to.

There isn't an equivalent downward migration that will undo these changes.

Given that, it can't be guaranteed that a database from a later version will work with an earlier one.

If you wish to downgrade to an earlier version of Umbraco, it's best to also revert to a compatible database backup. You will need one from the version you are downgrading to.

Other factors that may preclude downgrading include packages you may be using. They may not be compatible with the lower version or support downgrades themselves.

That said, between some versions, a downgrade may be possible and perfectly safe. There may be no migrations that run between them. Or, as is often the case, migrations are backward compatible (for example, adding a new, nullable field to a database table).

You will need to determine this for yourself, likely via reviewing the changes and migrations between versions and testing.

Once you have done that, this article will explain how to proceed with downgrading.

Downgrading the Umbraco application itself is straightforward. In the same way as when upgrading, you update the dependency on Umbraco in your project, you do the same when downgrading:

`dotnet add package Umbraco.Cms --version <VERSION>`


If you try to start Umbraco, it's likely you will find an exception thrown on boot indicating a problem with the migration state. This is because the version of Umbraco you are running now doesn't recognize the state stored by the higher version you were running previously.

To resolve this, you need to query the Umbraco database.

There are two migration states stored for the CMS - for the core migrations and the pre-migrations (which run at different times on start-up).

You can find the current state of these via:

You then need to find the latest state for the version of Umbraco you want to downgrade to.

To find the earlier states you have to look in the source code, specifically and .

Each migration is commented with the version it was added, so you can read off the latest one for the version you wish to run.

Having found the state you need, you set it via a query of the form:

Then restart Umbraco.

A related topic is if you want to re-run the migrations from a prior version to the version you are on.

This isn't something that should be needed in normal usage of Umbraco. Umbraco handles running the necessary migrations on start-up and keeps track of its state. However, if investigating an upgrade-related issue or testing an upgrade before running it in production, it's useful to know how to do this.

Again you need to manipulate the migration state stored in the database.

You can update these values to an earlier state, and on start-up Umbraco will recognize that it's not at the latest. It will re-run the migrations from the earlier state to the current one.

For example, let's say you are running 16.2, and want to re-run the core migrations for 15 and 16. Here you would set the core migration state to the latest one from 14, via:

And then restart Umbraco.

Migrations are written to be idempotent, so they can be run multiple times. If the change the migration is making is already detected to be there, it should skip without throwing an exception.

Last updated

Was this helpful?

---

## Upgrade Details | CMS

Describes how to upgrade existing installations to new versions.

In this article, you will find everything you need to upgrade your Umbraco CMS project.

If you are new to upgrades, be sure to read the [upgrade introduction article](/umbraco-cms/fundamentals/setup/upgrading/upgrade-introduction) first.

You can upgrade to a new major version of Umbraco CMS directly by using NuGet.

You must upgrade to the closest version before upgrading to the latest version. For Umbraco 10, the closest long-term support version is Umbraco 13. Once the project is on Umbraco 13, you can move on to Umbraco 14.

Switching to a new major version of Umbraco CMS also means switching to a new .NET version. Ensure that any packages used on your site are compatible with this version before upgrading.

The package compatibility can be checked on the package's download page. Locate the **Project compatibility** area and select **View details** to check version-specific compatibility.

Use the table below to determine which .NET version to upgrade to when going through the steps below.

| CMS version | .NET version |
|---|---|
| 17 | 10.0 |
| 16 | 9.0 |
| 15 | 9.0 |
| 14 | 8.0 |
| 13 | 8.0 |
| 12 | 7.0 |
| 11 | 7.0 |
| 10 | 6.0.5 |

If you are upgrading a Cloud project locally from version 14 to 15, remove the `Umbraco.Cloud.Cms.PublicAccess`

and `Umbraco.Cloud.Identity.Cms`

packages. For more details, see [Step 3: Upgrade the project locally using Visual Studio arrow-up-right](/umbraco-cloud/product-upgrades/major-upgrades#step-3-upgrade-the-project-locally-using-visual-studio)

It's recommended that you upgrade the site offline and test the upgrade fully before deploying it to the production environment.

Stop your site in IIS to prevent any changes from being made while you are upgrading.

Open your Umbraco project in Visual Studio.

Right-click on the project name in the Solution Explorer and select

**Properties**.Select the

**.NET**version from the**Target Framework**drop-down.Go to

**Tools**>**NuGet Package Manager**>**Manage NuGet Packages for Solution...**Go to the

**Installed**tab in the NuGet Package Manager.Upgrade

**Umbraco.Cms**.a. Select the correct version from the

**Version**drop-down.b. Click

**Install**to upgrade your project.

If you have other packages like Umbraco Forms installed, upgrade them before upgrading **Umbraco.CMS**. Consult the [version-specific upgrade notes for Umbraco Forms arrow-up-right](/umbraco-forms/upgrading/version-specific)

Make sure that your connection string has

`TrustServerCertificate=True`

to complete the upgrade successfully:

Restart your site in IIS, then build and run your project to finish the installation.


Umbraco 13 and later versions use the .

If you have added custom code to the `startup.cs`

file, it is recommended to move that code into a Composer after upgrading.

If your database experiences timeout issues after an upgrade, it might be due to the `startupTimeLimit`

configuration.

To fix the issue, try increasing the in the `web.config`

file. Additionally, you can set the value in the in the `appsettings.json`

file.

It is necessary to run the upgrade installer on each environment of your Umbraco site. This wil occur on first boot of an upgraded project as it is deployed into a new environment.

If you receive an error that **a deploy license is missing** even though you have a valid license, follow the guide below.

Google Chrome has aggressive caching, so when experiencing startup issues, clear the cache and cookies thoroughly. Ideally, this should be done for other browsers as well.

Nudge the cache in Chrome following these steps:

Open the developer tools (F12).

Go to the settings (Cog icon).

Ensure that "Disable cache (while DevTools is open)" is checked.

Refresh the page, and the cache will be invalidated.

Right-click the "reload" button next to your address bar and choose "Empty cache and hard reload".


All caches and cookies have now been cleared from your Google Chrome browser. Generally, it is a good thing to do occasionally.

NuGet installs the latest version of the package when you use the `dotnet add package`

command unless you specify a package version:

`dotnet add package Umbraco.Cms --version <VERSION>`


Add a package reference to your project by executing the `dotnet add package Umbraco.Cms`

command in the directory that contains your project file.

Run `dotnet restore`

to install the package.

**For Umbraco 9**
If you are using SQL CE in your project, you need to run `dotnet add package Umbraco.Cms.SqlCe --version <VERSION>`

before the `dotnet restore`

command. From Umbraco 10, SQL CE has been replaced with SQLite, so a `dotnet restore`

should be sufficient. If this is not working, then you need to run `dotnet add package Umbraco.Cms.Persistence.Sqlite --version <VERSION>`

, and then `dotnet restore`.


When the command completes, open the `.csproj`

file to make sure the package reference was updated:

The steps outlined in this article apply to Umbraco version 10 and later versions.

Are you upgrading to a minor version for Umbraco 6, 7, or 8? You can find the appropriate guide below:

Last updated

Was this helpful?

---

## Upgrades in Umbraco | CMS

Introduces upgrades in Umbraco, describing what to consider when planning an upgrade.

When upgrading to a new version of Umbraco, there are four key aspects of the migration to be aware of.

Firstly there's the update of your Umbraco database's schema and how the content is stored. On occasion changes are necessary to support a new feature. This might be adding new tables or columns, or updating the stored data. This is something Umbraco takes care of for you. When Umbraco starts up and is running a newer version, the necessary changes will be detected and applied.

As a developer responsible for the Umbraco website, there's nothing specific you need to do here. We will communicate key migrations that will happen on major version upgrades. As if you have a large site and significant amounts of data need to be updated, the migration could take some time to complete.

Minor or patch versions may contain schema and content updates too, but they won't be extensive.

Secondly you should review your use of property editors to ensure that they are available on the new version. It's rare for these to be removed, but it can happen when better alternatives are available. These are only removed in major versions and with plenty of notice on the . Property editors for retirement will also have been indicated as legacy on earlier versions.

The third aspect is determining and verifying that your own code customizations are compatible with the new version. This includes C# server-side functionality, Razor templates and JavaScript backoffice extensions.

Extensive efforts are made to avoid breaking changes that would cause issues for these types of customization other than in a major version update.

Finally you should consider the packages you are using on your project. You will need to verify that the package will work with the new version of Umbraco. Or that a compatible upgrade of the package is available or planned.

As above, breaking changes that would prevent packages from working other than in a major version update are avoided.

For the reasons described, projects always need to be considered case by case when upgrading to new versions.

Umbraco communicates about the breaking changes in release blog posts and on the documented [version specific upgrade details](/umbraco-cms/fundamentals/setup/upgrading/version-specific). There will be extended release candidate periods to ensure upgrades can be tested and to help package developers support new major versions.

Breaking changes are minimized but there will be cases when such updates are needed. How straightforward the upgrade will be depends on the breaking changes included in the major and whether your project(s) are impacted by them.

The following lists a few things to be aware of before initiating an upgrade of your Umbraco CMS project.

Sometimes, there are exceptions to general upgrade guidelines. These are listed in the

[version-specific guide](/umbraco-cms/fundamentals/setup/upgrading/version-specific). Be sure to read this article before moving on.Ensure your setup meets the

[requirements](/umbraco-cms/fundamentals/setup/requirements)for the new versions you will be upgrading your project to.Things may go wrong for different reasons. Be sure to

**always**keep a backup of both your site's files and the database. This way, you can always return to a version that you know works.Before upgrading to a new major version, check if the packages you're using are compatible with the version you're upgrading to. On the package's page on the , check the "Umbraco versions" field.


Last updated

Was this helpful?

---

## Upgrade Unattended | CMS

Learn how to enable unattended upgrades, allowing your project to upgrade without your interference.

Enable the unattended upgrade feature

```
{
    "Umbraco": {
        "CMS": {
            "Unattended": {
                "UpgradeUnattended": true
            }
        }
    }
}
```

Run the upgrade

Boot order

HTTP behavior during upgrade

| Surface | Behavior |
|---|---|
| Frontend | HTTP 503 with `Upgrading.cshtml` view |
| Surface controllers | HTTP 503 with `Upgrading.cshtml` view |
| Backoffice | Upgrade-in-progress screen |
| Management API | HTTP 503 JSON ProblemDetails |
| Delivery API | HTTP 503 JSON ProblemDetails |

Unattended upgrades in a load-balanced setup

Last updated

Was this helpful?

---

## Version Specific

### Contents

- [Migrate content to Umbraco 15 | CMS](#migrate-content-to-umbraco-15-cms)
- [Migrate content to Umbraco 8 | CMS](#migrate-content-to-umbraco-8-cms)
- [Migrate custom Property Editors to Umbraco version 14 and later | CMS](#migrate-custom-property-editors-to-umbraco-version-14-and-later-cms)
- [Minor upgrades for Umbraco 7 | CMS](#minor-upgrades-for-umbraco-7-cms)
- [Minor upgrades for Umbraco 8 | CMS](#minor-upgrades-for-umbraco-8-cms)
- [Upgrade from Umbraco 8 to the latest version | CMS](#upgrade-from-umbraco-8-to-the-latest-version-cms)
- [Upgrade to Umbraco 7 | CMS](#upgrade-to-umbraco-7-cms)

---

### Migrate content to Umbraco 15 | CMS

This article will help you migrate content to Umbraco 15, and outline options to skip this content migration

Parallelizing the content migration

```
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Infrastructure.Migrations.Upgrade.V_15_0_0;

namespace UmbracoDocs.Samples;

public class DisableBlockEditorMigrationComposer : IComposer
{
    [Obsolete]
    public void Compose(IUmbracoBuilder builder)
        => builder.Services.Configure<ConvertBlockEditorPropertiesOptions>(options =>
        {
            // setting this to true will parallelize the migration of all Block Editors
            options.ParallelizeMigration = true;
        });
}
```

Opting out of the content migration

[Previous Upgrade from Umbraco 8 to the latest version chevron-left](/umbraco-cms/fundamentals/setup/upgrading/version-specific/upgrade-from-8-to-latest)

[Next Migrate custom Property Editors to Umbraco version 14 and later chevron-right](/umbraco-cms/fundamentals/setup/upgrading/version-specific/migrate-custom-property-editors-to-umbraco-14)

Last updated

Was this helpful?

---

### Migrate content to Umbraco 8 | CMS

This guide will show you how to migrate the content from your Umbraco 7 site to a site running Umbraco 8.

Umbraco 8 contains a lot of breaking changes and a lot of code has been cleaned up compared to Umbraco 7. Due to this, it will not be possible to do a direct upgrade from Umbraco 7 to Umbraco 8. You need to **migrate your content** from your Umbraco 7 site into your Umbraco 8 site and then recreate the rest in the new version.

A content migration tool has been implemented in Umbraco 8.1.0, to help you with the transition.

In this guide you can read more about the tool, its limitations, and how to use it in practice.

**Migrating Umbraco Cloud sites**

Follow the [steps outlined in the Umbraco Cloud documentation arrow-up-right](/umbraco-cloud/upgrades/migrate-from-umbraco-7-to-8)

In the following section, you can learn more about the limitations of migrating content from Umbraco 7 to Umbraco 8.

The content migration tool is a database migration, which is made for the database schema of Umbraco 7.14+. This means that in order to do the migration you need to ensure your Umbraco 7 site is running at least Umbraco 7.14.

Umbraco 8 does not support MySQL databases. This means that the migration will not work when moving from an Umbraco 7 site using MySQL to Umbraco 8 on SQL Server

The database types that are supported are SQL Server and SQL CE.

Feedback from user testing has shown that some databases are harder to migrate than others.

We are collecting [a list of these known issues on our GitHub Issue Tracker arrow-up-right](https://github.com/umbraco/Umbraco-CMS/issues?utf8=%E2%9C%93&q=label%3Acategory%2Fcontent-migration+)

A migration was introduced in Umbraco 8.6 which can break the migration process. See for more details.

There are two ways to work around this issue:

Migrate to version 8.5 as a first step and then post-migration, carry out a normal Umbraco upgrade to the latest version of Umbraco 8, or

Install the following community Nuget Package: into your Umbraco 8 project before running the migration (no configuration required). This package was created by Umbraco Gold Partner and patches the migration process so you can migrate directly from the latest Umbraco 7 to Umbraco 8.6+ without encountering the above issue.


.[Learn more about the package and the migration process on Prowork's blog arrow-up-right](https://www.proworks.com/blog/archive/how-to-upgrade-umbraco-version-7-to-version-8)

The migration will transform the data stored in third party editors as well. However, it will be stored as it was in Umbraco 7. If the structure has changed or the property editor doesn't exist, you will still be able to find the data in the database. It will, however, not be available in the backoffice.

#### Learn more about that in the Data Types Migrations

**Migrating data types**

When migrating content from Umbraco 7 to Umbraco 8, the Data Type 'pre-value' structure has changed. In Umbraco 8, the term 'pre-values' no longer exists and is instead referred to as `property editor configuration`.


In Umbraco 8, property editor configuration is a strongly typed object. There are plenty of examples in the .

This configuration is stored differently in Umbraco 8 than it was in Umbraco 7. In Umbraco 7, each pre-value property was stored as a different row in a different database table. In Umbraco 8 this is simplified and property editor configuration is stored as the JSON serialized version of the strongly typed configuration object.

When upgrading from Umbraco 7 to Umbraco 8, Umbraco has no way of knowing how custom property editors have intended to structure their configuration data. During the upgrade, Umbraco will convert the key/value pairs from the old pre-value database table into a serialized JSON version of those values. There is a reasonable chance that the end result of this data conversion is not compatible with the custom property editor.

There are 3 options that a developer can choose to do to work around this automatic data conversion:

**1: Implement a custom ****IPreValueMigrator**

This option requires you to create a custom C# migrator for each of your custom property editors that store custom configuration data. It will also require that you implement these migrators before you run the Umbraco 8 content migration.

To do this, you will create an implementation of `IPreValueMigrator`

or inherit from the base class .

There are plenty of examples of this in the .

You will then need to register them in a composer:

When running the migrations and encountering a custom configuration, Umbraco will utilize the `PreValueMigrator`

when converting the old pre-values into the new JSON format.

**2: Update your Angular configuration (pre-value) and property editor**

This option means that you will choose to use the automatically converted JSON data format. In this case, it will mean updating your pre-value and property editors to use the new JSON configuration data. The converted data won't be much different than the original/intended data format so this might not be too much work.

**3: Update the Angular configuration (pre-value) editor**

With this option the configuration/pre-value editor needs to be updated to transform the JSON converted data into the data structure you want. When this is done and when the Data Type is saved again, the JSON data structure will be saved back to the database. Your property editor will then continue to work.

This will require you to update and save all custom pre-value editors to transform the converted structures back to your intended data structure.

When the migrations are running, Umbraco will go through your entire Umbraco 7 database and update it to the format required for Umbraco 8. The schema will be remodeled and transformed into the correct format and your existing compatible data will be transformed to fit with Umbraco 8.

These migrations will be running directly on your database. They are transforming schema and data - not transferring. Therefore always ensure that you have a backup before attempting to do this. In case something goes wrong, you will be able to rollback and try again.

It is highly recommended to clean up your site before running this as it will be quicker.

Empty Content recycle bin

Empty Media recycle bin

Clean up the database version history (can be done with a script or a package like )


In the following guide we will migrate the content of an Umbraco 7.13.1 site to Umbraco 8.1.0.

Before the content migration can start the site has to run Umbraco 7.14+. Make sure to **always take a backup of the database** before doing an upgrade, and then check the [version specific upgrade instructions](/umbraco-cms/fundamentals/setup/upgrading/version-specific).

The site in this example is an Umbraco 7.13.1 site, and we will use Nuget to update it.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-350e15dc720959beab1badedd1fefe86c9332442%252Fv7-content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=780a1394&sv=2)

Following the [general upgrade instructions](/umbraco-cms/fundamentals/setup/upgrading) we will now upgrade via Nuget until we get to this point:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-af0b40c8db719ac3b8ea861d06fc29e0c9dcd02b%252Fupgrading-7_14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9fa3c539&sv=2)

When upgrading an old website, check if you are using obsolete properties in your Data Types. These should be changed to their updated counterparts. The migration **will fail if you are still using obsolete properties.**

The updated properties are:

Content Picker

Media Picker

Member Picker

Multinode Treepicker

Nested Content

Folder Browser

Related Links


You can see if your site is using the obsolete properties from the `(Obsolete)`

prefix in their name.

Install the , and run it health check from the Developer section of the backoffice. This is done to identify and resolve some common database schema issues before migration.

Once it is upgraded and you have verified everything is working, move on to the next step.

The first thing to do is to spin up a fresh new Umbraco 8.1+ site. Make sure everything works and that no content is there.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7914e6644d3734dc95ec23f1c112b0a764fa91ec%252Ffresh-8_1-site.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6e57479e&sv=2)

If you have customized the `UsersMembershipProvider`

on your Umbraco 7 site you need to copy that over to the 8.1 `web.config`

as well. Additionally you need to update the `type`

attribute to be `type="Umbraco.Web.Security.Providers.UsersMembershipProvider, Umbraco.Web"`.


This also includes the attribute `useLegacyEncoding`

value. Make sure that this setting is copied into your new Umbraco 8 site, as it is needed in order to log in.

Take a backup of your database from the **Umbraco 7.14 site**. Take the information for the backup database and add that to the connectionstring for the **Umbraco 8.1 site**. If you are running SQL CE, you will have to copy the database over to the new site as well.

Once the connectionstring is set, the final step is to change the Umbraco version number in the `web.config`

on the **Umbraco 8.1 site**. Chang it to `7.14.0`

. This will indicate that there is an upgrade pending and it needs to run the migration.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c0dae2344e2ddab82ba2dae44f7ce00499209f3e%252Fset-umbraco-version.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ba6e7c19&sv=2)

The version will be set to 8.1.0, and you need to change it to the version you are currently migrating from.

When you start the site it will ask you to login and then show you this screen:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8104fa8537132c5e71ba2fce329368889c706594%252Fupgrade-to-8_1.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a3df0743&sv=2)

From here, the automatic migration will take over, and after a little bit you can log in and see your content:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1d8efa9c29de746c32ffb61643202783cf0e6bf0%252Fcontent-on-8_1.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c7e319bb&sv=2)

Please be aware that this is a **content migration**. If you go to the frontend after following these steps, it will throw errors.

At this point you will have the content but nothing else.

Before moving on to this step, make sure that the Umbraco 8 project is no longer running.

The following files/folders need to be copied into the Umbraco 8 project:

`~/Views`

- do**not**overwrite the default Macro and Partial View Macro files, unless changes have been made to these.`~/Media`

Any files/folders related to Stylesheets and JavaScripts.

Any custom files/folders the Umbraco 7 project uses, that aren't in the

`~/Config`

or`~/bin`

.`~/App_Data/UmbracoForms`

- in the case Umbraco Forms was used on the Umbraco 7 site.

**Merge the configuration files carefully** to ensure any custom settings are migrated while none of the default configurations for Umbraco 8 is overwritten.

You'll have to revisit all templates and custom implementations to get the site up and running, as all markup is still Umbraco 7-specific.

Are you planning on continuing the migration to the latest version on Umbraco CMS?

Then you can skip the step to revisit the template files and custom implementation. We highly recommend waiting with this step until you've reached the latest version.

If you're stopping at Umbraco 8, you can learn more about .

As you are updating your template files and custom implementation, you should also verify your configuration files and settings.

Umbraco 8 contains a few changes regarding the Sections in the Umbraco Backoffice. Because of this, you should also check your User Groups and make sure they have access to the appropriate sections.

Learn more about the Section in the [Sections article](/umbraco-cms/fundamentals/backoffice/sections)

Last updated

Was this helpful?

---

### Migrate custom Property Editors to Umbraco version 14 and later | CMS

This article helps you migrate custom Property Editors to Umbraco 14 and later

Migration impact for Property Editors

Manifest based Property Editors

Property Editor `valueType` | Resulting `EditorAlias` |
`BIGINT` | `Umbraco.Plain.Integer` |
`DATE` | `Umbraco.Plain.DateTime` |
`DATETIME` | `Umbraco.Plain.DateTime` |
`DECIMAL` | `Umbraco.Plain.Decimal` |
`JSON` | `Umbraco.Plain.Json` |
`INT` | `Umbraco.Plain.Integer` |
`STRING` | `Umbraco.Plain.String` |
`TEXT` | `Umbraco.Plain.String` |
`TIME` | `Umbraco.Plain.Time` |
`XML` | `Umbraco.Plain.String` |

Code based editors

Migration impact for porting Property Editor UIs

Alternatives

Last updated

Was this helpful?

---

### Minor upgrades for Umbraco 7 | CMS

This article provides details on how to upgrade to the next minor version when using Umbraco 7.

Sometimes there are exceptions to these guidelines, which are listed in the [version-specific guide](/umbraco-cms/fundamentals/setup/upgrading/version-specific).

It is necessary to run the upgrade installer on each environment of your Umbraco site. If you want to update your staging and live site then you need to repeat the steps below and make sure that you click through the install screens to complete the upgrade.

In this article you will find instructions for 2 different ways of upgrading:

Open up the

**Package Console**and type:`Update-Package UmbracoCms`

Choose

**"No to All"**by pressing the**"L"**when prompted.If there are any specific configuration changes required for the version you are upgrading to then they will be noted in the

[version-specific guide](/umbraco-cms/fundamentals/setup/upgrading/version-specific).


Alternatively, you can use the Visual Studio **NuGet Package Manager** to upgrade:

Open the

**NuGet Package Manager**and select the**Updates**pane to get a list of available updates.Choose the package called

**UmbracoCms**and select update.

The upgrade will run through all the files and make sure you have the latest changes while leaving the files you have updated.

If you're not upgrading to 7.2.0 or higher then you should follow these extra instructions. If you are upgrading to 7.2.0+ then you can skip this and go to [Merge UI.xml and language](/umbraco-cms/fundamentals/setup/upgrading/version-specific/minor-upgrades-for-umbraco-7#merge-uixml-and-language).

You will be asked to overwrite your web.config file and the files in /config, make sure to answer **No** to those questions.

For some inexplicable reason, the installation will fail if you click "No to All" (in the GUI) or answer "L" (in the package manager console) to the question: "File 'Web.config' already exists in project 'MySite'. Do you want to overwrite it?" So make sure to only answer "**No**" (in the GUI) or "**N**" (in the package manager console).

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9b8dd02ba5485314347262620477b752fa28d258%252Fnuget-overwrite-dialog%2520%281%29%2520%281%29%2520%281%29.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=92288526&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-dbf7db39535659dcf7be1fb3261b3e9f71863712%252Fnuget-upgrade-overwrite%2520%281%29%2520%281%29%2520%281%29.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=dbd8f22c&sv=2)

We will overwrite the `web.config`

file. We'll back it up so don't worry. You can find the backup in `App_Data\NuGetBackup\20140320-165450\`

. The `20140320-165450`

bit is the date and time when the backup occurred, which varies. You can then merge your config files and make sure they're up to date.

Download the .zip file for the new version you are upgrading to from

Copy the following folders from inside the .zip file over the existing folders in your site:

`/bin`

`/Umbraco`

`/Umbraco_Client`


There are hosting providers (we know of one: RackSpace Cloud) that require proper casing of file and folder names. Generally, on Windows, this is not a problem. Is your hosting provider forcing proper casing? You'll then need to verify that folders and files are named in the same casing as the version you're upgrading to.

You can expect some changes to the following configuration files:

Any file in the

`/Config`

folderThe

`/Global.asax`

fileThe

`web.config`

file in the root of your site**(Important: make sure to copy back the version number, and the connection string as they were.)**In rare cases, the

`web.config`

file in the Views folder

Use a tool like to check changes between all of the config files. Depending on when you last did this there may have been updates to a few of them.

There's also the possibility that files in the `/Config`

folder are new or have been removed(we note this in the release notes). WinMerge (and other diff tools) is able to compare folders as well so you can spot these differences.

Up until version 6.0.0 it was necessary to change the version number in `ClientDependency.config`

. This was to clear the cached HTML/CSS/JS files in the backoffice. Change the current version number to one that's higher than that. Make sure not to skip this step as you might get strange behavior in the backoffice otherwise.

Some packages (like Contour and Umbraco Forms) add dialogs to the `UI.xml`

. Make sure to merge those changes back in from your backup during the upgrade so that the packages continue to work. This file can be found in: `/Umbraco/Config/Create/UI.xml`.


Packages like Contour, Umbraco Forms, and Courier also make changes to the language files located in: `/Umbraco/Config/Lang/*.xml`

(typically `en.xml`

).

After copying the files and making the config changes, you can open your site. You should see the installer which will guide you through the upgrade.

The installer will do two things:

Update the version number in the

`web.config`

Upgrade your database in case there are any changes


We are aware that, currently, the installer is asking you for the database details of a **blank database** while upgrading. In the near future this will be pre-filled with your existing details and the wording will be updated. So no need to be scared. Enter the details of your existing database and Umbraco will upgrade it to the latest version when necessary.

One important recommendation is to always remove the `install`

folder immediately after upgrading Umbraco and never to upload it to a live server.

Google Chrome has notoriously aggressive caching. If something doesn't seem to work well in the backoffice, make sure to clear cache and cookies thoroughly (for other browsers as well). Normally the browser cache problem is automatically handled in an Umbraco upgrade by modifying the config/ClientDependency.config version number. If you wish to re-force this update you can increment this version number. This will ensure that any server-side cache of JavaScript and stylesheets gets cleared as well.

One way to nudge the cache in Chrome is to open the developer tools (F12) and go to the settings (the cog icon). There will be a checkbox that says "Disable cache (while DevTools is open)". Once this checkbox is on you can refresh the page and the cache should be invalidated. To force it even more, the "reload" button next to your address bar now has extra options when you right-click it. It should have "Normal reload", "Hard reload" and "Empty cache and hard reload" now. The last option is the most thorough and you might want to try that.

Last updated

Was this helpful?

---

### Minor upgrades for Umbraco 8 | CMS

This article provides details on how to upgrade to the next minor version when using Umbraco 8.

Sometimes there are exceptions to these guidelines, which are listed in the [version-specific guide](/umbraco-cms/fundamentals/setup/upgrading/version-specific).

It is necessary to run the upgrade installer on each environment of your Umbraco site. If you want to update your staging and live site you need to repeat the steps below. Make sure you click through the install screens so that your upgrade is complete.

In this article you will find instructions for 3 different ways of upgrading:

Open up the

**Package Console**and type:`Update-Package UmbracoCms`

Choose

**"No to All"**by pressing the**"L"**when prompted.If there are any specific configuration changes required for the version you are upgrading to then they will be noted in the

[version-specific guide](/umbraco-cms/fundamentals/setup/upgrading/version-specific).


Alternatively, you can use the Visual Studio **NuGet Package Manager** to upgrade:

Open the

**NuGet Package Manager**and select the**Updates**pane to get a list of available updates.Choose the package called

**UmbracoCms**and select update.

The upgrade will run through all the files and make sure you have the latest changes while leaving files you have updated.

Download the `.zip`

file for the new version you are upgrading to from

Copy the following folders from inside the `.zip`

file over the existing folders in your site:

`/bin`

`/Umbraco`


There are hosting providers (we know of one: RackSpace Cloud) that require proper casing of file and folder names. Normally on Windows this is not a problem. If your hosting provider however forces proper casing, you will need to verify that the folder and file names are in the same casing as in the newest version you're upgrading to.

You can expect some changes to the following configuration files:

Any file in the

`/Config`

folderThe

`/Global.asax`

fileThe

`web.config`

file in the root of your site**(Important: make sure to copy back the version number, and the connection string as they were.)**In rare cases, the

`web.config`

file in the`/Views`

folder

Use a tool like to check changes between all of the config files. Depending on when you last did this there may have been updates to few of them.

There's also the possibility that some files in the `/Config`

folder are new or some have been removed (we do make a note of this in the release notes). WinMerge (and other diff tools) can compare folders as well so you can spot these differences.

Some packages like Umbraco Forms add dialogs to the `UI.xml`

. Make sure to merge those changes back in from your backup during the upgrade so that the packages continue to work. This file can be found in: `/Umbraco/Config/Create/UI.xml`.


Packages like Umbraco Forms and Courier also make changes to the language files located in: `/Umbraco/Config/Lang/*.xml`

(typically `en.xml`

).

After copying the files and making the config changes, you can open your site. You should see the installer which will guide you through the upgrade.

The installer will do two things:

Update the version number in the

`web.config`

Upgrade your database in case there are any changes


We are aware that, currently, the installer is asking you for the database details of a **blank database** while upgrading. In the near future this will be pre-filled with your existing details and the wording will be updated. So no need to be scared. Enter the details of your existing database and Umbraco will upgrade it to the latest version when necessary.

When upgrading your Umbraco project to Umbraco v8.12+ it is possible to enable the upgrade to run unattended. This means that you will not need to run through the installation wizard when upgrading.

Below you will find the steps you need to take in order to upgrade your project unattended.

Are you running a load balanced setup with multiple servers and environments?

Check out the section about [Unattended upgrades in a load balanced setup](/umbraco-cms/fundamentals/setup/upgrading/upgrade-unattended#unattended-upgrades-in-a-load-balanced-setup).

Add the

`Umbraco.Core.RuntimeState.UpgradeUnattended`

key to`appSettings`

in your web.config file.Set the value of the key to

`true`.


`ConfigurationStatus`

In order to trigger the actual upgrade, the correct version number needs to be set.

It is important to use the version number of the version that you are upgrading to. If this is not set, the upgrade will not run even if the `UpgradeUnattended`

key has been set to `true`.


Locate the

`ConfigurationStatus`

key in the`appSettings`

section in your web.config file.Update the value to match the Umbraco version that you are upgrading to.


With the correct configuration applied, the project will be upgraded on the next boot.

While the upgrade processes are running, any requests made to the site will be "put on hold", meaning that no content will be returned before the upgrade is complete.

The Runtime level will use `Run`

instead of `Upgrade`

in order to allow the website to continue to boot up directly after the migration is run, instead of initiating the otherwise required restart.

The upgrade is run after Composers but before Components. This is because the migration requires services that are registered in Composers and Components requires that Umbraco and the database is ready.

Follow the steps outlined below to use run unattended upgrades in a load balanced setup.

Upgrade Umbraco via NuGet in Visual Studio. Make sure the

`Umbraco.Core.ConfigurationStatus`

key in`appSetting`

in the`web.config`

file is updated to match the**target version**.Deploy to all environments, including the updated

`appSetting`

for`Umbraco.Core.ConfigurationStatus`

.Set the

`Umbraco.Core.RuntimeState.UpgradeUnattended`

key in`appSetting`

in the`web.config`

to`true`

for**the Main server only**.Request a page on the Main server and the upgrade will run automatically.

Wait for the upgrade to complete.

Browse the Read-Only servers and make sure they do not show the “upgrade required” screen.


One important recommendation is to always remove the `install`

folder immediately after upgrading Umbraco and never to upload it to a live server.

Google Chrome has notoriously aggressive caching, so if something doesn't seem to work well in the backoffice, make sure to clear cache and cookies thoroughly (for other browsers as well). Normally the browser cache problem is automatically handled in an Umbraco upgrade by modifying the config/ClientDependency.config version number. If you however wish to re-force this update you can increment this version number which will ensure that any server-side cache of JavaScript and stylesheets gets cleared as well.

One way to nudge the cache in Chrome is to open the developer tools (F12) and go to the settings (the cog icon). There will be a checkbox that says "Disable cache (while DevTools is open)". Once this checkbox is on you can refresh the page and the cache should be invalidated. To force it even more, the "reload" button next to your address bar now has extra options when you right-click it. It should have "Normal reload", "Hard reload" and "Empty cache and hard reload" now. The last option is the most thorough and you might want to try that.

Last updated

Was this helpful?

---

### Upgrade from Umbraco 8 to the latest version | CMS

Learn how to upgrade your Umbraco 8 project to Umbraco 10.

It is currently not possible to upgrade directly from **Umbraco 8 to the latest version**.

The recommended approach for upgrading from version 8 to the latest version is to use this guide to upgrade from *Umbraco 8 to Umbraco 10*. Umbraco 10 contains the that must be upgraded from Umbraco 8. You can then use the [Upgrading to Major](/umbraco-cms/fundamentals/setup/upgrading#upgrade-to-a-new-major) steps to upgrade from *Umbraco 10 to the latest version*.

Since the underlying framework going from Umbraco 8 to the latest version has changed, there is no direct upgrade path. That said, it is possible to re-use the database from your Umbraco 8 project on your new project in order to maintain the content.

It is not possible to migrate the custom code as the underlying web framework has been updated from ASP.NET to ASP.NET Core. All templates and custom code will need to be reimplemented.

You also need to make sure that the packages you are using are available on the latest version.

A Umbraco 8 project running

**the latest version of Umbraco 8**.A backup of your Umbraco 8 project database.

A clean installation of the latest version of Umbraco.


If you use Umbraco Forms, then on the clean installation of Umbraco, you will need to install `Umbraco.Forms`

package as well.

The video below shows how to complete the upgrade on an Umbraco Cloud project. While the overall process is the same, you must update to the latest supported version on Cloud locally before continuing on Cloud.

Learn more about supported versions in the article.

If you use Umbraco Forms, make sure to have to `True`

before **step 1**.

Create a backup of the database from your Umbraco 8 project (after you have upgraded to the latest version of v8). For this, you can use the .

Import the database backup into SQL Server Management Studio.

Update the connection string in the new projects

`appsettings.json`

file so that it connects to the Umbraco 8 database:

You can also add the connection details if you spin up a clean installation.

Run the new project and login to authorize the upgrade.

Select "Upgrade" when the upgrade wizard appears.

Once the upgrade has been completed, it's recommended to login to the backoffice to verify if your project is upgraded to new version.


This is **only content migration** and the database will be migrated.

You need to manually update the view files and custom code implementation. For more information, see Step 3 of this guide.

The following files/folders need to be copied from the Umbraco 8 project into the new project:

`~/Views`

-**Do not**overwrite the default Macro and Partial View Macro files unless changes have been made to these.`~/Media`

- Media folder from v8 needs to be copied over into the`wwwroot - media`

folderAny files/folders related to Stylesheets and JavaScript.


Migrate custom configuration from the Umbraco 8 configuration files (

`.config`

) into the`appsettings.json`

file on the new project.As of Umbraco version 9, the configuration no longer lives in the

`Web.Config`

file and has been replaced by the`appsettings.json`

file. Learn more about this in the[Configuration](/umbraco-cms/reference/configuration)article.

, if relevant.

As of Umbraco Forms version 9, it is only possible to store Forms data in the database. If Umbraco Forms was used on the Umbraco 8 project, the files need to be migrated to the database.


Run the new project.

It

**will**give you an error screen on the frontend as none of the Template files have been updated. Follow**Step 3**to resolve the errors.


The latest version of Umbraco is different from Umbraco 8 in many ways. With all the files and data migrated it is now time to rewrite and re-implement all custom code and templates.

One of the changes is how published content is rendered through Template files. Due to this, it will be necessary to update **all** the Template files (`.cshtml`

) to reflect these changes.

Read more about these changes in the [IPublishedContent](/umbraco-cms/reference/querying/ipublishedcontent) section of the Umbraco CMS documentation.

Template files need to inherit from

`Umbraco.Cms.Web.Common.Views.UmbracoViewPage<ContentModels.HomePage>`

instead of`Umbraco.Web.Mvc.UmbracoViewPage<ContentModels.HomePage>`

Template files need to use

`ContentModels = Umbraco.Cms.Web.Common.PublishedModels`

instead of`ContentModels = Umbraco.Web.PublishedModels`


For more information on the correct namespaces or custom code, you can find the references in the [API Documentation](/umbraco-cms/reference/api-documentation) article.

Depending on the extent of the project and the amount of custom code and implementations, this step is going to require a lot of work.

Once the new project runs without errors on a local setup it is time to deploy the website to production.

This concludes this tutorial. Find related information and further reading in the section below.

Last updated

Was this helpful?

---

### Upgrade to Umbraco 7 | CMS

This document should be used as a reference, not a step by step guide. Upgrading will largely depend on what version of Umbraco you are currently running, what packages you have installed and the many

The [standard upgrade instructions](/umbraco-cms/fundamentals/setup/upgrading) still apply to this process as well.

It is critical that you back up your website and database before upgrading. There are database changes made during installation and you cannot revert an Umbraco 7 database to an Umbraco 6 database.

Umbraco 7 is built on .Net 4.5 and your development environment will require this version installed in order to operate. Visual Studio users may require 2012 or higher.

Umbraco 7 requires browsers with proper HTML 5 support, these include Chrome, Firefox, IE10+

Before you upgrade be sure to read the list of breaking changes. This is especially recommended if you have removed or modified code in the core or if one of these breaking changes directly affects your installation.

for more details.

It is recommended to rebuild all Examine indexes after completing the upgrade.

You should re-generate the XML cache. This can be done by following the prompts when visiting the following URL:

`your-domain.com/umbraco/dialogs/republish.aspx?xml=true`


It is recommended that you use a Diff tool to compare the configuration file changes with your own current configuration files.

`/web.config`

updatesDetails are listed here:

You will need to compare the new Umbraco 7

`web.config`

with your current`web.config`

. Here is a quick reference of what needs to change:Remove the

`section name="BaseRestExtensions"`

sectionRemove the

`section name="FileSystemProviders"`

sectionRemove the

`sectionGroup name="system.web.webPages.razor"`

sectionRemove the

`<FileSystemProviders>`

elementRemove the

`BaseRestExtensions`

elementRemove the

`add key="umbracoUseMediumTrust"`

elementRemove the

`system.web.extensions`

elementRemoves the

`xhtmlConformance`

elementRemove the

`system.codedom`

elementRemove the

`compilation`

assemblies,`/compilation`

Remove the

`system.web.webPages.razor`

elementNew:

`sectionGroup name="umbracoConfiguration"`

sectionNew:

`umbracoConfiguration`

elementEnsure that the

`targetFramework="4.5"`

is added to the`httpRuntime`

elementAdd

`add key="ValidationSettings:UnobtrusiveValidationMode" value="None"`

to the`appSettings`

element


`/config/clientdependency.config`

changesremove

`add name="CanvasProvider"`

element

`/views/web.config`

updatesNew

`macroscripts/web.config`

`config/umbracoSettings.config`

Umbraco is now shipped with minimal settings but the are still available

`umbracoSettings`

is now a true ASP.NET configuration sectionRemove the

`EnableCanvasEditing`

elementRemove the

`webservices`

element

Removed

`xsltExtensions.config`

`/config/applications.config`

and`/config/trees.config`

have some icon paths and names updated. You need to merge the new changes into your existing config files.`/config/tinyMceConfig.config`

The

`inlinepopups`

is compatible and supported in Umbraco 7. You need to remove these elements:`plugin loadOnFrontend="true"`

,`inlinepopups/plugin`

;The plugins element that is shipped with Umbraco 7 looks like this:

You need to merge the changes from the new

`tinyMceConfig`

file into yours. The`command`

elements that have changed are:`JustifyCenter`

,`JustifyLeft`

,`JustifyRight`

,`JustifyFull`

,`umbracomacro`

,`umbracoembed`

,`mceImage`

,`subscript`

,`superscript`

,`styleselect`

Remove the command:

`mceSpellCheck`



`/config/dashboard.config`

You need to merge the changes from the new

`dashboard.config`

into yours. Some of the original dashboard entries that were shipped with Umbraco 6 have been replaced or removed.


Umbraco 7+ will no longer support medium trust environments. There are now some assemblies used in the core that do not support medium trust but are used extensively. Plugin scanning now also allows for scanning Umbraco's internal types which requires full trust.

Content, Media, Members, and Data Type trees will no longer raise the legacy tree events (based on BaseTree). It is recommended to change all tree event handlers to use the new tree events that fire for every tree in Umbraco including legacy trees. The new tree events are static events and are found in the class `Umbraco.Web.Trees.TreeControllerBase`:


`MenuRendering`

`RootNodeRendering`

`TreeNodesRendering`


The Content, Media, Member, and Data Type editors have been re-created and are solely using the new Umbraco Services data layer. This means that operations performed in the backoffice will no longer raise the legacy business logic events (for example, events based on `umbraco.cms.businesslogic.web.Document`

). It is recommended to change your event handlers to subscribe to the new Services data layer events. These are static events and are found in the services. For example: `Umbraco.Core.Services.ContentService.Saved`.


Legacy property editors (pre-Umbraco 7) will not work with Umbraco 7. During the upgrade installation process, Umbraco will generate a report showing you which legacy property editors are installed. These will all be converted to a `readonly`

Label property editor. No data loss will occur but you'll need to re-assign your existing data types to use a new compatible Umbraco 7 property editor.

Most Umbraco core property editors shipped will be mapped to their equivalent Umbraco 7 editors. The Image cropper editor has not been completed for v7.0.

Since the Related Links property is an advanced property editor, the data format has changed from XML to JSON. This should not have any effect when retrieving the data from razor. If you are outputting Related Links data with XSLT you will need to update your XSLT snippet. Making use of the new library method `umbraco.library:JsonToXml`

and taking into account that the xml structure has also slightly changed.

One of the database changes made in Umbraco 7 is the change of referencing a property editor from a GUID to a string alias. In order to map a legacy property editor to a new Umbraco 7 version you can add your custom "GUID -> Alias" map during application startup. To do this you would add your map using this method: `Umbraco.Core.PropertyEditors.LegacyPropertyEditorIdToAliasConverter.CreateMap`


Legacy parameter editors (pre-Umbraco 7) will not work with Umbraco 7. If Umbraco detects legacy parameter editor aliases that do not map to a Umbraco 7 parameter editor it will render a textbox in its place. You will need to update your macros to use a compatible Umbraco 7 parameter editor as those that aren't supported.

Previously, parameter editors were registered in an Umbraco database table: `cmsMacroPropertyType`

which no longer exists. Parameter editors in Umbraco 7 are plugins like property editors. During the Umbraco 7 upgrade installation process it will update the new `cmsMacroProperty.editorAlias`

column with the previous parameter editor alias. During this process it will look into the `Umbraco.Core.PropertyEditors.LegacyParameterEditorAliasConverter`

for a map between a legacy alias to a new Umbraco 7 alias.

Custom legacy parameters can be mapped to new Umbraco 7 parameter editor aliases during installation. This can be done by modifying the mapping during application startup using this method: `Umbraco.Core.PropertyEditors.LegacyParameterEditorAliasConverter.CreateMap`.


All database changes will be taken care of during the upgrade installation process.

For database change details see (including all child tasks):

See above for the database updates made for better tag support.

Tags can now be assigned to a nodes property and not only a node

Multiple tag controls can exist on one page with different data

The legacy API does

**not**support this, the legacy API will effectively, add/update/remove tags for the first property found for the document that is assigned a tag property editor.

There is a new ITagService that can be used to query tags

Querying for tags in a view (front-end) can be done via the new TagQuery class which is exposed from the UmbracoHelper. For example:

`@Umbraco.TagQuery.GetTagsForProperty`



You should check with the package creator for all installed packages to ensure they are compatible with Umbraco 7.

We see common errors that we cannot fix for you, but we do have recommendations you can follow to fix them:

The TypeFinder has been deprecated since 4.10 and is now found under `Umbraco.Core.TypeFinder`.


While you need to have JavaScript inside menu actions to trigger a response, it is highly recommended that you use the recommended `UmbClientMgr`

methods. You should not try to override `parent.right.document`

and similar tricks to get to the right-hand frame.

If you have a webforms page, it is recommended to use the built-in ASP.NET controls to render panels, properties and so on. If you use the raw HTML or try to style it to match the backoffice, you will get out of sync. Follow the guidelines set by Umbraco's internal editors and use the ASP.NET custom controls for UI.

Last updated

Was this helpful?

---

---
