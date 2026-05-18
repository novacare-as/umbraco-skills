# Configuration

## Configuration

### Contents

- [Basic Authentication Settings | CMS](#basic-authentication-settings-cms)
- [Cache Settings | CMS](#cache-settings-cms)
- [Connection strings settings | CMS](#connection-strings-settings-cms)
- [Content Settings | CMS](#content-settings-cms)
- [Data Types Settings | CMS](#data-types-settings-cms)
- [Debug settings | CMS](#debug-settings-cms)
- [Dictionary | CMS](#dictionary-cms)
- [Distributed jobs settings | CMS](#distributed-jobs-settings-cms)
- [Examine settings | CMS](#examine-settings-cms)
- [Exception filter settings | CMS](#exception-filter-settings-cms)
- [FileSystemProviders Configuration | CMS](#filesystemproviders-configuration-cms)
- [Global Settings | CMS](#global-settings-cms)
- [Health checks | CMS](#health-checks-cms)
- [Hosting settings | CMS](#hosting-settings-cms)
- [Imaging settings | CMS](#imaging-settings-cms)
- [Indexing settings | CMS](#indexing-settings-cms)
- [Install Default Data Settings | CMS](#install-default-data-settings-cms)
- [Logging settings | CMS](#logging-settings-cms)
- [Maximum Upload Size Settings | CMS](#maximum-upload-size-settings-cms)
- [Models builder settings | CMS](#models-builder-settings-cms)
- [Package Migration | CMS](#package-migration-cms)
- [Plugins settings | CMS](#plugins-settings-cms)
- [Request handler settings | CMS](#request-handler-settings-cms)
- [Runtime settings | CMS](#runtime-settings-cms)
- [Security Settings | CMS](#security-settings-cms)
- [Serilog settings | CMS](#serilog-settings-cms)
- [Type finder settings | CMS](#type-finder-settings-cms)
- [Unattended | CMS](#unattended-cms)
- [Web routing | CMS](#web-routing-cms)

---

### Basic Authentication Settings | CMS

Configuration reference for the Umbraco basic authentication settings section in appsettings.json.

```
"Umbraco": {
  "CMS": {
    "BasicAuth": {
      "AllowedIPs": [],
      "Enabled": false,
      "RedirectToLoginPage": false,
      "SharedSecret": {
        "HeaderName": "X-Authentication-Shared-Secret",
        "Value": null
      },
      "LoginViewPath": "/umbraco/BasicAuthLogin/Login.cshtml",
      "TwoFactorViewPath": "/umbraco/BasicAuthLogin/TwoFactor.cshtml"
    }
  }
}
```

AllowedIPs

Enabled

RedirectToLoginPage

SharedSecret

HeaderName

Value

LoginViewPath

TwoFactorViewPath

Last updated

Was this helpful?

---

### Cache Settings | CMS

Information on the Cache settings section

Are you looking for the **NuCache Settings**?

While most cache configurations are under the `Umbraco:CMS:Cache`

settings node, a few remain under `Umbraco:CMS:NuCache`

. [Learn more about this at the bottom of this article](/umbraco-cms/reference/configuration/cache-settings#nucache-settings).

Umbraco's cache is implemented using Microsofts `HybridCache`

, which also has its own settings. For more information .

One `HybridCache`

setting of particular interest is the `MaximumPayloadBytes`

setting. This setting specifies the maximum size of a cache entry in bytes and replaces the `BTreeBlockSize`

setting from NuCache. The default from Microsoft is 1MB. However, this limit could quickly be reached, especially when using multiple languages or property editors like the block grid. To avoid this Umbraco overrides the setting to 100MB by default. You can also configure this manually using a composer:

```
using Microsoft.Extensions.Caching.Hybrid;
using Umbraco.Cms.Core.Composing;

namespace MySite.Caching;

public class ConfigureCacheComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.Services.AddOptions<HybridCacheOptions>().Configure(x =>
        {
            x.MaximumPayloadBytes = 1024 * 1024 * 10; // 10MB
        });
    }
}
```

The Seeding settings allow you to specify which content should be seeded into your cache. For more information on cache seeding see the [Cache Seeding.](/umbraco-cms/reference/cache/cache-seeding) article.

The `ContentTypeKeys`

setting specifies which Document Types should be seeded into the cache. The setting is a comma-separated list of Document Type keys.

The `DocumentBreadthFirstSeedCount`

setting specifies how many documents should be seeded into the cache when doing a breadth-first traversal. `MediaBreadthFirstSeedCount`

provides the same for media. The default value for both is 100.

When populating the cache on startup the content keys defined by the seeding strategy are processed in batches. The batch size for documents and media can be modified via the `DocumentSeedBatchSize`

and `MediaSeedBatchSize`

respectively. The default value for both is 100.

The Entry settings allow you to specify how long cache entries should be kept. The cache entry settings are identical for documents and media.

Specifies the duration for which cache entries should be kept in the local memory cache. The default value is 24 hours.

Specifies the duration that cache entries should be kept in the remote cache, second level cache. This setting is only relevant if a second-level cache is configured. The default value is 1 year.

Specifies the duration for which seeded cache entries should be kept in the cache. The default value is 1 year.

When you save a content type with structural changes, Umbraco rebuilds the database cache for every affected content item. Structural changes include removing a property, changing a property alias, or changing the variation mode.

By default, this rebuild runs during the save operation and blocks it until every content item of the affected types has been re-serialized. On sites with many content items per type, or when multiple related content types are saved in succession, the save can be slow.

The `ContentTypeRebuildMode`

setting controls whether the database cache rebuild runs immediately or is deferred to a background task. It accepts two values:

`Immediate`

(default): the database cache rebuild runs during the save operation.`Deferred`

: the database cache rebuild is queued to a background task. The save returns without waiting for the rebuild to complete.

When `Deferred`

is set, the content cache is still evicted immediately during the save. The next request reads the previously serialized data from the database. Once the background rebuild completes, the content cache is evicted again, and subsequent requests pick up the fresh data. Content continues to be served throughout the rebuild without errors, but may be temporarily stale.

If multiple content types are saved in quick succession, the affected content type IDs are accumulated and processed together in a single batch. This avoids overlapping rebuild work between related types.

The same setting also controls the deferral of search re-indexing triggered by content type changes.

The `ContentTypeRebuildMode`

setting is available from Umbraco 17.4.

For backward compatibility reasons, certain settings are under the `Umbraco:CMS:NuCache`

settings node.

When `UsePagedSqlQuery`

is set to `False`

, the `Fetch`

method is used instead of the `QueryPaged`

method for rebuilding the NuCache files. This will increase performance on larger Umbraco websites with a lot of content when rebuilding the NuCache.

Specifying the `SqlPageSize`

will change the size of the paged SQL queries. The default value is 1000.

The `NuCacheSerializerType`

setting allows developers to specify the serialization format for cached content.

The fastest and most compact format `MessagePack`

is used by default.

An alternate `JSON`

option was provided for backward compatibility for the Umbraco cache implementation used from Umbraco 8 to 14 (NuCache).

It is no longer supported with the cache implementation from Umbraco 15+ based on .NET's Hybrid cache.

The option is kept available only for a more readable format suitable for testing purposes.

Last updated

Was this helpful?

---

### Connection strings settings | CMS

Information on the connection strings settings section

Last updated

Was this helpful?

Information on the connection strings settings section

The connection strings settings section contains the connection string to the database Umbraco will connect to. This section is similar to what is used by default in .NET Core. The important thing is that the key for the connection string Umbraco will use is `"umbracoDbDSN"`

. It is also important to know that this section is outside the `Umbraco.CMS`

section, and is therefore in the root of the config.

The connection strings config can look like this:

```
{
  "ConnectionStrings": {
    "umbracoDbDSN": "Data Source=|DataDirectory|/Umbraco.sqlite.db;Cache=Shared;Foreign Keys=True;Pooling=True",
    "umbracoDbDSN_ProviderName": "Microsoft.Data.Sqlite"
  }
}
```

It is recommended to use shared cache for SQLite when using Umbraco. It provides better performance and consistency when multiple connections may access the database simultaneously.

The connection string used here is an SQLite connection string, that will connect to a data in the file `Umbraco.sqlite.db`

located in `/umbraco/Data`.


Umbraco currently supports using either a Microsoft SQL Server or a SQLite database. Both of these options will have different connection strings. For more information about the specific connection strings, see:

If you're using Umbraco 9 is supported instead of SQLite.

Provider name

Because Umbraco cannot determine the provider name from the connection string in all cases. Umbraco follows for provider names, which involves specifying it as a postfix in the connection string name.

Last updated

Was this helpful?

Was this helpful?

---

### Content Settings | CMS

Information on the content settings section

Content settings contains a handful of settings related to the content in the CMS. It includes settings such as allowed upload files, image settings, and much more. All the values in the content settings has default values, so all configuration is optional.

The following snippet will give an overview of the keys and values in the content section including the default values:

```
"Umbraco": {
  "CMS": {
    "Content": {
      "ContentVersionCleanupPolicy": {
        "EnableCleanup": false,
        "KeepAllVersionsNewerThanDays": 7,
        "KeepLatestVersionPerDayForDays": 90
      },
      "AllowEditInvariantFromNonDefault": false,
      "AllowedMediaHosts":  [],
      "AllowedUploadedFileExtensions": [],
      "DisableDeleteWhenReferenced": false,
      "DisableUnpublishWhenReferenced": false,
      "DisallowedUploadedFileExtensions": ["ashx", "aspx", "ascx", "config", "cshtml", "vbhtml", "asmx", "air", "axd", "xamlx"],
      "Error404Collection": [],
      "BackOfficeLogo": "../media/qyci4xti/logo.png",
      "HideBackOfficeLogo": false,
      "Imaging": {
        "ImageFileTypes": ["jpeg", "jpg", "gif", "bmp", "png", "tiff", "tif"],
        "AutoFillImageProperties": [
          {
            "Alias": "umbracoFile",
            "ExtensionFieldAlias": "umbracoExtension",
            "HeightFieldAlias": "umbracoHeight",
            "LengthFieldAlias": "umbracoBytes",
            "WidthFieldAlias": "umbracoWidth"
          }
        ]
      },
      "LoginBackgroundImage": "login/login.jpg",
      "LoginLogoImage": "login/logo_light.svg",
      "LoginLogoImageAlternative": "login/logo_dark.svg",
      "Notifications": {
        "DisableHtmlEmail": false,
        "Email": null
      },
      "PreviewBadge": "<![CDATA[<b>My HTML here</b>]]>",
      "ResolveUrlsFromTextString": false,
      "ShowDeprecatedPropertyEditors": false,
      "ShowDomainWarnings": true,
      "ShowUnroutableContentWarnings": true,
      "EnableMediaRecycleBinProtection": false
    }
  }
}
```

In the root level section, that is those without a separate sub section like Imaging, you can configure:

Invariant properties are properties on a multilingual site that are not varied by culture. This means that they share the same value across all languages added to the website.

When the `AllowEditInvariantFromNonDefault`

setting is set to `false`

(default) the invariant properties can only be edited and published from the default language. This means you need access to the default language in order to edit the property. You will also need to publish the default language to see changes in the invariant property on your website.

When set to `true`

the invariant properties can be edited and published from any language.

If greater control is required than available from the `DisallowedUploadedFileExtensions`

setting, this setting can be used to store a list of file extensions. If provided, only files with these extensions can be uploaded via the backoffice.

By default, only relative URLs are allowed when getting URLs for resized images or thumbnails using the ImagesController. If you need absolute URLs you will have to add the allowed hosts to this list. The value could be `["umbraco.com", "www.umbraco.com", "our.umbraco.com"]`.


This setting allows you to specify whether a user can delete content or media items that depend on other items. This also includes any descendants that have dependencies. Setting this to **true** will remove or disable the *Delete* button.

This setting allows you to specify whether or not users can unpublish content items that depend on other items or have descendants that have dependencies. Setting this to **true** will disable the *Unpublish* button.

This setting consists of a list of file extensions that editors shouldn't be allowed to upload via the backoffice.

In case of a 404 error (page not found) Umbraco can return a default page instead. This is set here. Notice you can also set a different error page, based on the current culture so a 404 page can be returned in the correct language.

The above example shows what you need to do if you only have a single site that needs to show a custom 404 page. You specify which node that should be shown when a request for a non-existing page is being made. You can specify the node in three ways:

Enter the nodes

**id**(`"ContentId": 1`

)Enter the node's

**GUID**(`"ContentKey": "4f96ffdd-b969-46a8-949e-7935c41fabc0"`

)Use

[IContentLastChanceFinder](/umbraco-cms/tutorials/custom-error-page#set-a-custom-404-page-using-icontentlastchancefinder)to find the node.

Ids are usually local to the specific solution (so won't point to the same node in two different environments if you're using Umbraco Cloud).

GUIDs are universal and will point to the same node on different environments, provided the content was created in one environment and deployed to the other(s).


If you have multiple sites, with different cultures, setup in your tree then you will need to setup the errors section like below:

If you have more than two sites and forget to add a 404 page and a culture, the default page will act as fallback. Same happens if you for some reason forget to define a hostname on a site.

This setting can be used to set a custom image path to replace the Umbraco logo in the backoffice.

This setting can be used to hide the Umbraco logo in backoffice.

You can specify your own background image for the login screen here. The image will automatically get an overlay to match backoffice colors. This path is relative to the `wwwroot/umbraco`

path. The default location is: `wwwroot/umbraco/login/login.jpg`.


You can specify your own image for the small logo in the top left corner of the login screen. This path is relative to the `wwwroot/umbraco`

path. The default location is: `wwwroot/umbraco/login/logo_light.svg`.


You can specify your own alternative image for the small logo in the top left corner of the login screen. The alternative image is shown on light backgrounds (for example for mobile resolutions). This path is relative to the `wwwroot/umbraco`

path. The default location is: `wwwroot/umbraco/login/logo_dark.svg`.


This allows you to customize the preview badge being shown when you're previewing a node.

This setting is used when you're running Umbraco in virtual directories. Setting this to true can increase render time for pages with a large number of links. However, this is required if Umbraco is running in a virtual directory.

This setting is used for controlling whether or not the Data Types marked as obsolete should be visible in the dropdown when creating new Data Types.

By default this is set to `false`

. To make the obsolete data types visible in the dropdown change the value to `true`.


If you do not configure Domains for each language in a multilingual site then every time you publish your content you get this warning:

`Content published: Domains are not configured for multilingual site, please contact an administrator, see log for more information.`


If you have a use case for not setting the domains, you can set this setting **ShowDomainWarnings** to `false`

to stop the warning from displaying.

If your routing setup leads to more than one document having the same URL, on publish a warning will be displayed:

`Content published: The document does not have a URL, possibly due to a naming collision with another document. More details can be found under Info.`


To suppress these warnings, set this option to `false`.


By default, when media is moved to the recycle bin, the files are still accessible at their previous public URL. They will only be unavailable once the recycle bin is emptied or the media item is fully deleted.

If this is a concern, setting `EnableMediaRecycleBinProtection`

to `true`

will avoid this. On moving a media item to the recycle bin, the file extension will be changed. The change will be reverted if the media item is restored to its original location.

Separately, a middleware component will be enabled to prevent access to these renamed files if the user is not logged into the backoffice.

When enabling this option, ensure that the media recycle bin is initially empty.

This option may be enabled by default from Umbraco version 18.

The global settings for the scheduled job which cleans historic content versions. These settings can be overridden per Document Type.

Current draft and published versions will never be removed, nor will individual content versions which have been marked as "preventCleanup".

See [Content Version Cleanup](/umbraco-cms/fundamentals/data/content-version-cleanup) for more details on overriding configuration and preventing cleanup of specific versions.

If you don't wish to retain any content versions except for the current draft and currently published you can set both of the "keep" settings values to 0. After doing this, the next time the scheduled job runs (hourly) all non-current versions (except those marked "prevent cleanup") will be removed.

When `true`

a scheduled job will delete historic content versions that are not kept according to the policy every hour.

When `false`

, the scheduled job will never delete any content versions regardless of overridden settings for a Document Type.

This defaults to `false`

when not set in the configuration which will be the case for those upgrading from v9.0.0. However, the dotnet new template will supply an `appsettings.json`

with the value set to true for all sites starting from Umbraco 9.1.0.

All versions that fall in this period will be kept.

For content versions that fall in this period, the most recent version for each day is kept. All previous versions for that day are removed unless marked as preventCleanup.

This variable is independent of `KeepAllVersionsNewerThanDays`

, if both were set to the same value `KeepLatestVersionPerDayForDays`

would never apply as `KeepAllVersionsNewerThanDays`

is considered first.

This setting controls how many content versions are processed in a single cleanup run. When more eligible versions exist than this limit, the remainder will be cleaned up in subsequent hourly runs. This allows large version histories to be cleaned incrementally without overwhelming the database.

Set to 0 to disable the limit and process all eligible versions in a single run.

This section is used for managing how Umbraco handles images, allowed attributes and, which properties of an image that should be automatically updated on upload.

Let's break it down.

This is a separated list of accepted image formats

You can define what properties should be automatically updated when an image is being uploaded. This means that if you decide to rename the default **umbracoWidth** and **umbracoHeight** properties the values in

and **"WidthFieldAlias"**

need to be updated. This needs to happen in order to automatically populate the values when the image is being uploaded.**"HeightFieldAlias"**

If you need to create a custom Media Type to handle images you need to add another object using the custom Media Type alias. Like below. Keep in mind that the width and height attributes have also been changed in this example.

Umbraco can send out email notifications, set the sender email address for the notifications emails here. To set the SMTP server used to send the emails, edit the standard Simple Mail Transfer Protocol (SMTP) section in the global section, see [global settings](/umbraco-cms/reference/configuration/globalsettings) for more information.

Last updated

Was this helpful?

---

### Data Types Settings | CMS

Information on the data types settings section

Last updated

Was this helpful?

Information on the data types settings section

Allows you to configure the behavior of data types.

```
{
  "Umbraco": {
    "CMS": {
      "DataTypes": {
        "CanBeChanged": "True"
      }
    }
  }
}
```

CanBeChanged

Gets or sets a value indicating if data types can be changed after they've been used.

Valid values:

`"True"`

Allows data types to be changed after creation. This can lead to data on content is not valid on the Data Type.


`"False"`

Disallow Data Type changes. (Recommended value, unless you really know what you are doing)


`"FalseWithHelpText"`

Disallow Data Type changes, but show the users a help text so they understand why.



Last updated

Was this helpful?

Was this helpful?

---

### Debug settings | CMS

Information on debug settings section

Last updated

Was this helpful?

Information on debug settings section

This section contains configurations regarding debugging, and should therefore only be used in development.

The debug section has two settings you can configure, `"LogIncompletedScopes"`

and `"DumpOnTimeoutThreadAbort"`

, both of these are false by default:

```
"Umbraco": {
  "CMS": {
    "Debug": {
      "DumpOnTimeoutThreadAbort": false,
      "LogIncompletedScopes": false
    }
  }
}
```

Log incompleted scopes

If this value is set to true, any scope that gets disposed without first being completed will trigger a log entry containing the stacktrace.

DumpOnTimeoutThreadAbort

If this value is set to true, a memory dump will be taken if a thread aborts due to a timeout. This dump will be saved to `/umbraco/Data/MiniDump`.


Last updated

Was this helpful?

Was this helpful?

---

### Dictionary | CMS

Information on the dictionary settings section.

Last updated

Was this helpful?

Information on the dictionary settings section.

Dictionary settings allow you to configure how dictionary items are searched in the Umbraco backoffice.

The following snippet contains all the available options with their default values:

```
{
  "Umbraco": {
    "CMS": {
      "Dictionary": {
        "EnableValueSearch": false
      }
    }
  }
}
```

EnableValueSearch

Key: `UseDictionaryValueSearch`


Type: `bool`

(default: `false`

)

Enables searching dictionary items by their **translation values** in addition to **keys** in the backoffice.

When set to `false`

(default), only dictionary keys are searched using prefix matching.

When set to `true`

, both dictionary keys and translation values are searched. Keys use prefix matching while values use substring matching, allowing editors to find dictionary items by their translated content.

This feature is **disabled by default** to preserve backward compatibility and performance. It is recommended to enable the setting only when your editors need to search by translation values.

Related Links

Last updated

Was this helpful?

Was this helpful?

---

### Distributed jobs settings | CMS

Configuration

```
"Umbraco": {
  "CMS": {
    "DistributedJobs": {
      "Period": "00:00:05",
      "Delay": "00:01:00",
      "MaximumExecutionTime": "00:05:00"
    }
  }
}
```

Settings

Period

Delay

MaximumExecutionTime

Last updated

Was this helpful?

The distributed jobs settings allow you to configure how Umbraco handles distributed background jobs in a load-balanced environment.

Configuration

```
"Umbraco": {
  "CMS": {
    "DistributedJobs": {
      "Period": "00:00:05",
      "Delay": "00:01:00",
      "MaximumExecutionTime": "00:05:00"
    }
  }
}
```

Settings

Period

**Default:** `00:00:05`

(5 seconds)

Specifies how frequently each server checks for distributed background jobs that need to be run.

A shorter period means jobs are picked up more quickly, but increases the frequency of database queries. A longer period reduces overhead but may introduce delays in job execution.

Delay

**Default:** `00:01:00`

(1 minute)

Specifies how long the server should wait after initial startup before beginning to check for and run distributed background jobs. This startup delay ensures that the application is fully initialized and stable before participating in distributed job processing.

MaximumExecutionTime

**Default:** `00:05:00`

(5 minutes)

Specifies the maximum time a distributed job can run before it is considered stale. Jobs that are currently being executed by one server are not picked up by other servers, preventing duplicate execution. However, if a job exceeds this time threshold, it is considered abandoned and can be picked up by another server for recovery.

This setting is useful for handling scenarios where a server crashes or becomes unresponsive while processing a job. By setting an appropriate maximum execution time, the system can automatically recover and reassign stale jobs to healthy servers.

Last updated

Was this helpful?

Was this helpful?

---

### Examine settings | CMS

Information on the Examine settings section

```
"Umbraco": {
  "CMS": {
    "Examine": {
      "LuceneDirectoryFactory": "Default"
    }
  }
}
```

Last updated

Was this helpful?

Information on the Examine settings section

Since the majority of Examine configuration takes place in code, this section is small and contains only one setting to change: `LuceneDirectoryFactory`

. This setting allows you to change the behavior of the `ExamineIndexes`

directory.

This section has a default value, and does not need to be configured, configuring Examine might look something like this:

```
"Umbraco": {
  "CMS": {
    "Examine": {
      "LuceneDirectoryFactory": "Default"
    }
  }
}
```

This is how Examine is configured by default. There is three different types of Lucene directory factories:

`Default`

- The index will operate from the default location:`umbraco/Data/TEMP/ExamineIndexes`

`SyncedTempFileSystemDirectoryFactory`

- The index will operate on a local index created in the processes %temp% location and will replicate back to main storage in`umbraco/Data/TEMP/ExamineIndexes`

`TempFileSystemDirectoryFactory`

- The index will operate only in the processes %temp% directory location

Last updated

Was this helpful?

Was this helpful?

---

### Exception filter settings | CMS

Information on the exception filter settings section

```
"Umbraco": {
  "CMS": {
    "ExceptionFilter": {
      "Disabled": true
    }
  }
}
```

Last updated

Was this helpful?

Information on the exception filter settings section

This section allows you to disable the `ModelBindingExceptionFilter`

, this filter is only enable if the models builder mode is set to `InMemoryAuto`

. This filter will return a redirect to the page being loaded after one second, if a `ModelsBindingException`

or `InvalidCastException`

occurs. The reason for this filter is that a page might be requested at the same time as the content type has been changed. If this occurs, the new model might not have been generated and loaded yet. This filter will take care of this.
By default this filter is enabled, but will be ignored if the mode is not `InMemoryAuto`

. To manually disable the filter add the `"ExceptionFilter"`

section to your config with the `"Disabled"`

key set to `true`

like so:

```
"Umbraco": {
  "CMS": {
    "ExceptionFilter": {
      "Disabled": true
    }
  }
}
```

Last updated

Was this helpful?

Was this helpful?

---

### FileSystemProviders Configuration | CMS

Information on FileSystemProviders and how to configure them in Umbraco

Filesystem providers are configured via code, you can either configure it in a composer, or in the `Program.cs`

file.

```
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.IO;
using Umbraco.Cms.Infrastructure.DependencyInjection;
using IHostingEnvironment = Umbraco.Cms.Core.Hosting.IHostingEnvironment;

namespace FilesystemProviders;

public class FilesystemComposer : IComposer
{
 public void Compose(IUmbracoBuilder builder) =>
  builder.SetMediaFileSystem(factory =>
  {
   IHostingEnvironment hostingEnvironment = factory.GetRequiredService<IHostingEnvironment>();
   IWebHostEnvironment webHostEnvironment = factory.GetRequiredService<IWebHostEnvironment>();
   var folderLocation = "~/CustomMediaFolder";
   var rootPath = webHostEnvironment.MapPathWebRoot(folderLocation);
   var rootUrl = hostingEnvironment.ToAbsolute(folderLocation);

   return new PhysicalFileSystem(
    factory.GetRequiredService<IIOHelper>(),
    hostingEnvironment,
    factory.GetRequiredService<ILogger<PhysicalFileSystem>>(),
    rootPath,
    rootUrl);
  });
}
```

By default Umbraco will save Media in a folder called `/media`

within the webroot on the Physical file system. The code snippet above will change the location to instead save the media in a folder called `/CustomMediaFolder`

within the webroot.

The media provider can be of many types, for example in case you want to store media on Azure, Amazon or even DB. But the provider that comes by default with the installation of Umbraco is the `PhysicalFileSystem`

provider.

The physical file system provider manages the interaction of Umbraco with the local file system. It can be configured for two different scenarios:

Media files stored inside a virtual folder of the site

Media files stored somewhere else outside of the site and accessed via a custom URL


To configure the PhysicalFileSystem for a virtual folder, create a new filesystem with a root path and URL within the wwwroot folder. Refer to the example above and [Extending FileSystemProviders](/umbraco-cms/extending/filesystemproviders) for more information.

There are a few more steps involved if you want to store the media files in a separate folder outside the webroot.

First you must register the folder as a static file provider in your `Program.cs`

file like so:

Now you can register the folder as the media filesystem

This is much the same as when you register it within the wwwroot with a virtual folder. The only difference is that now you provide an absolute root path and root URL to the physical filesystem.

`rootPath`

is the full filesystem path where you want media files to be stored. It has to be rooted, must use directory separators (`\`

) and must not end with a separator. For example,`Z:`

or`C:\path\to\folder`

or`\\servername\path`

.`rootUrl`

is the URL where the files will be accessible from. It must use URL separators (`/`

) and must not end with a separator. It can either be a folder, like`/UmbracoMedia`

, in which case it will considered as subfolder of the main domain (`example.com/UmbracoMedia`

) or can be a fully qualified URL, with also domain name and protocol (for ex`http://media.example.com/media`

).

For more information see [Extending FileSystemProviders](/umbraco-cms/extending/filesystemproviders).

To store media files in different systems, the type of provider must be changed. You can learn [how to build a custom filesystem provider](/umbraco-cms/extending/filesystemproviders#custom-file-systems-ifilesystem) in the Extending Umbraco section.

At the moment when a file is saved, its full URL is stored as node property. This means that a configuration change will not apply to pre-existing media files but only to the ones saved after that.

If you want all your media files in the same location, you have to copy all pre-existing files to the new path. Additionally, you need to update the path property of the media item to the new URL. This can be either directly inside the database or by using the `MediaService`.


The recommended approach to obtain a file's content as a stream is to utilize the `MediaFileManager`

. It is advised to avoid reading the file directly from the server using methods like `Server.MapPath`

. This will ensure that, regardless of the file system provider, the stream will be returned correctly. This example demonstrates using MediaFileManager to validate file existence and stream it back from a controller.

Last updated

Was this helpful?

---

### Global Settings | CMS

Information on the global settings section

Global settings contains at set of global settings for the CMS such as default UI language, reserved urls, and much more. All settings except Simple Mail Transfer Protocol (SMTP) use default values. Configuration is optional unless you want to send emails from your site.

The following snippet contains all the available options, with default values, and some example values for the required keys `From`

, `Host`

, and `Port`

keys of the SMTP settings:

```
"Umbraco": {
  "CMS": {
    "Global": {
      "ReservedUrls": "~/.well-known,",
      "ReservedPaths": "~/app_plugins/,~/install/,~/mini-profiler-resources/,~/umbraco/,",
      "TimeOut": "00:20:00",
      "DefaultUILanguage": "en-US",
      "HideTopLevelNodeFromPath": true,
      "UseHttps": true,
      "VersionCheckPeriod": 7,
      "IconsPath": "~/umbraco/assets/icons",
      "UmbracoCssPath": "~/css",
      "UmbracoScriptsPath": "~/scripts",
      "UmbracoMediaPath": "~/media",
      "UmbracoMediaPhysicalRootPath": "X:/Shared/Media",
      "InstallMissingDatabase": false,
      "DisableElectionForSingleServer": false,
      "DatabaseFactoryServerVersion": "SqlServer.V2019",
      "MainDomLock": "FileSystemMainDomLock",
      "MainDomKeyDiscriminator": "",
      "Id": "184a8175-bc0b-43dd-8267-d99871eaec3d",
      "NoNodesViewPath": "~/umbraco/UmbracoWebsite/NoNodes.cshtml",
      "UpgradingViewPath": "~/umbraco/UmbracoWebsite/Upgrading.cshtml",
      "Smtp": {
        "From": "[email protected]",
        "Host": "localhost",
        "Port": 25,
        "SecureSocketOptions": "Auto",
        "DeliveryMethod": "Network",
        "PickupDirectoryLocation": "",
        "Username": "[email protected]",
        "Password": "SuperSecretPassword",
        "EmailExpiration": null,
      },
      "DatabaseServerRegistrar": {
        "WaitTimeBetweenCalls": "00:01:00",
        "StaleServerTimeout": "00:02:00"
      },
      "DatabaseServerMessenger": {
        "MaxProcessingInstructionCount": 1000,
        "TimeToRetainInstructions": "2.00:00:00",
        "TimeBetweenSyncOperations": "00:00:05",
        "TimeBetweenPruneOperations": "00:01:00"
      },
      "DistributedLockingMechanism": "",
      "DistributedLockingReadLockDefaultTimeout": "00:01:00",
      "DistributedLockingWriteLockDefaultTimeout": "00:00:05",
      "MainDomAcquisitionTimeout": "00:00:40"
    }
  }
}
```

In the root level section, that is those without a separate sub section like SMTP, you can configure.

Key: `ReservedUrls`

Type: `string`

(default: `~/.well-known,`

)

A comma-separated list of files to be left alone by Umbraco, these files will be served, and the Umbraco request pipeline will not be triggered.

Key: `ReservedPaths`

Type: `string`

(default: `~/app_plugins/,~/install/,~/mini-profiler-resources/,~/umbraco/,`

)

A comma-separated list of all the folders in your directory to be left alone by Umbraco. If you have folders with custom files, add them to this setting to make sure Umbraco leaves them alone.

Adding additional values to the Reserved URLs and Reserved Paths will overwrite the default values. You should make sure to include these values as well as any additional ones you provide.

Key: `TimeOut`

Type: `string`

(default: `00:20:00`

)

Configure the session timeout to determine how much time without a request being made can pass before the user is required to log in again. The session timeout format needs to be set as `HH:MM:SS`

. Any activity within the backoffice will reset the timer.

Long session timeouts raise data exposure and unauthorized access risks. Thus, it's vital to establish a reasonable timeout to mitigate security risks.

Key: `DefaultUILanguage`

Type: `string`

(default: `en-US`

)

The default language to use in the backoffice if a user isn't explicitly assigned one.

Key: `HideTopLevelNodeFromPath`

Type: `bool`

(default: `true`

)

If you are running multiple sites, you don't want the top level node in your URL and can disable it with this setting.

Key: `UseHttps`

Type: `bool`

(default: `true`

)

Makes sure that all of the requests in the backoffice are called over HTTPS instead of HTTP when set to true.

Key: `VersionCheckPeriod`

Type: `int`

(default: `7`

)

When this value is set above 0, the backoffice will check for a new version of Umbraco every 'x' number of days where 'x' is the value defined for this setting. Set this value to 0 to never check for a new version.

Key: `IconsPath`

Type: `string`

(default: `umbraco/assets/icons`

)

By adding this value you can specify a new/different folder for storing your icon resources. It's important to be aware of .NET Core's limitations regarding serving static file content. By default, static content will only be served from the `wwwroot`

folder.

Key: `UmbracoCssPath`

Type: `string`

(default: `~/css`

)

By adding this, you can store CSS files in a different folder and still edit them in Umbraco. .NET Core only serves static files from the `wwwroot`

folder by default. For more info see [Extending filesystem](/umbraco-cms/extending/filesystemproviders).

Key: `UmbracoScriptsPath`

Type: `string`

(default: `~/scripts`

)

By adding this, you can store script/JavaScript files in a different folder and still edit them in Umbraco. .NET Core only serves static files from the `wwwroot`

folder by default. For more info see [Extending filesystem](/umbraco-cms/extending/filesystemproviders).

Key: `UmbracoMediaPath`

Type: `string`

(default: `~/media`

)

By adding this, you can store media files in a different folder and still edit them in Umbraco. .NET Core only serves static files from the `wwwroot`

folder by default. For more info see [Extending filesystem](/umbraco-cms/extending/filesystemproviders).

Key: `UmbracoMediaPhysicalRootPath`

Type: `string`

(default: `~/media`

)

By adding this you can specify a new/different folder for storing your media files elsewhere on the server. Unlike `UmbracoMediaPath`

, this does not change the relative path that media is served from (e.g. /media) but allows for files to be stored **outside** of the wwwroot folder. Both relative paths (../../Shared/Media) and absolute server paths (X:/Shared/Media) are supported. For more info see [Extending filesystem](/umbraco-cms/extending/filesystemproviders).

Key: `InstallMissingDatabase`

Type: `bool`

(default: `false`

)

This is not a setting that commonly needs to be configured.

If enabled Umbraco will try to automatically install the database when it's missing. This is primarily used in conjunction with unattended installs.

Key: `DisableElectionForSingleServer`

Type: `bool`

(default: `false`

)

This is not a setting that commonly needs to be configured.

This value is primarily used on Umbraco Cloud for a small startup performance optimization. When this is true, the website instance will automatically be configured to not support load balancing and the website instance will be configured to be the 'primary' server for scheduling so no [primary election](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/file-system-replication) occurs. This will save 1 database call during startup.

Key: `DatabaseFactoryServerVersion`

Type: `bool`

(default: `false`

)

This is not a setting that commonly needs to be configured.

This setting is used to specify which sql server version that the database is running, this setting is only required if you use SqlServer 2008, if this is the case set the setting to `"SqlServer.V2008"`.


Key: `MainDomLock`

Type: `string`


Specifies the implementation of IMainDomLock to be used.

`IMainDomLock`

is used to synchronize access to resources like the Lucene indexes.

Available options:

`"FileSystemMainDomLock"`

- Available cross-platform, uses lock files written to LocalTempPath to control acquisition of MainDom status.`"MainDomSemaphoreLock"`

- Windows only, uses a named system Semaphore with a`maximumCount`

of 1 to control acquisition of MainDom status.`"SqlMainDomLock"`

- Available cross-platform, uses the database to control acquisition of MainDom status.

The default implementation unless configured otherwise is `FileSystemMainDomLock`.


Key: `MainDomKeyDiscriminator`

Type: `string`


For advanced use cases e.g. deployment slot swapping on Azure app services.

When using SqlMainDomLock a MainDomKey is used to identify an instance of a running application.

The MainDomKey is by default comprised of the server's machine name & the application id.

This is generally all that is required to control MainDom status as starting a new process for the same application on the same server will result in a matching MainDomKey. This will then require that an existing instance yields MainDom status to the new process.

Deployment slots for a given Azure App Service share the same machine name. Without additional configuration, they will share a MainDomKey and therefore compete for MainDom status. This can be undesirable if attempting to deploy to a deployment slot followed by a swap with the production slot as once traffic has switched to the new instance the old production instance reboots and can re-acquire MainDom status. See .

To prevent this from occurring you can specify a MainDomKeyDiscriminator which should be set as a slot-specific configuration to prevent the slots from competing for MainDom status.

It's worth noting that during the swap operation there is a period where both instances will share the same configuration and at this point, the old instance will yield MainDom status to the new instance.

Key: `MainDomReleaseSignalPollingInterval`

Type: `string`


Gets or sets the duration (in milliseconds) for which the MainDomLock release signal polling task should sleep. The default value is 2000ms.

Key: `Id`

Type: `string`


This setting doesn't need to be configured.

This setting contains a unique ID used to identify your project, and is populated the first time your site runs, you shouldn't change this setting.

Key: `NoNodesViewPath`

Type: `string`

(default: `~/umbraco/UmbracoWebsite/NoNodes.cshtml`

)

This setting specifies what view to render when there is no content on the site.

Key: `UpgradingViewPath`

Type: `string`

(default: `~/umbraco/UmbracoWebsite/Upgrading.cshtml`

)

This setting specifies the view to render when an unattended upgrade is running in the background. Frontend and surface controller requests receive an HTTP 503 response with this view during the upgrade. See [Upgrade Unattended](/umbraco-cms/fundamentals/setup/upgrading/upgrade-unattended) for details on the upgrade process.

By adding this settings to the appsettings.json you will be able to send out emails from your Umbraco installation. This could be notifications emails if you are using content workflow, or you are using Umbraco Forms you also need to specify SMTP settings to be able use the email workflows. The forgot password function from the backoffice also needs a SMTP server to send the email with the reset link.

Specifies the default email address used when sending emails. This can be overridden in some cases, like when inviting a user. The address follows the Request for Comments (RFC) 822 format, allowing a friendly name like: `"Friendly Name <`

.[[email protected]](/cdn-cgi/l/email-protection)>"

Address of the SMTP host used to send the email from.

The port of the SMTP host, port 25 is a common port for SMTP.

The username used to authenticate with the specified SMTP server, when sending an email.

The password used to authenticate with the specified SMTP server, when sending an email.

Allows you to specify what security should be used for the connection sending the email.

The options are:

None - No SSL or TLS encryption should be used.

Auto - Allow the IMailService to decide which SSL or TLS options to use (default). If the server does not support SSL or TLS, then the connection will continue without any encryption.

SslOnConnect - The connection should use SSL or TLS encryption immediately.

StartTls - Elevates the connection to use TLS encryption immediately after reading the greeting and capabilities of the server. If the server does not support the STARTTLS extension, then the connection will fail and a NotSupportedException will be thrown.

StartTlsWhenAvailable - Elevates the connection to use TLS encryption immediately after reading the greeting and capabilities of the server, but only if the server supports the STARTTLS extension.


Specifies what delivery method should be used for emails, most of the time you'd want to use the default `"Network"`

option to send emails over the network. It might be useful during development to use `"SpecifiedPickupDirectory"`

to place the email messages in a folder on disk, instead of trying to send them over the network.

If you're using the `"SpecifiedPickupDirectory"`

option on as the delivery method, this setting allows you to specify what folder the emails should be saved to.

If set to a TimeSpan format, this value will be used to add an `Expires`

heading to emails sent from Umbraco. The configured expiry will be used unless a specific value is provided (for example, password reset and user invites have specific settings and defaults).

It's unlikely that you will have to change these settings unless you're using a load balanced setup.

Key: `DatabaseServerRegistrar.WaitTimeBetweenCalls`

Type: `string`

(default: `00:01:00`

)

Sets a value for the amount of time to wait between calls to the database on the background thread.

Key: `DatabaseServerRegistrar.StaleServerTimeout`

Type: `string`

(default: `00:02:00`

)

Sets a value for the time span to wait before considering a server stale, after it has last been accessed.

It's unlikely that you will have change these settings, unless you're using a load balanced setup. These settings are all about how load balancing instructions from the database are processed and pruned.

Key: `DatabaseServerMessenger.MaxProcessingInstructionCount`

Type: `string`

(default: `1000`

)

Sets a value for the maximum number of instructions that can be processed at startup; otherwise the server cold-boots (rebuilds its caches).

Key: `DatabaseServerMessenger.TimeToRetainInstructions`

Type: `string`

(default: `2.00:00:00`

)

Sets a value for the time to keep instructions in the database; records older than this number will be pruned.

Key: `DatabaseServerMessenger.TimeBetweenSyncOperations`

Type: `string`

(default: `00:00:05`

)

Sets a value for the time to wait between each sync operation.

Key: `DatabaseServerMessenger.TimeBetweenPruneOperations`

Type: `string`

(default: `00:01:00`

)

Sets a value for the time to wait between each prune operation.

Key: `DistributedLockingMechanism`

Type: `string`


This is not a setting that commonly needs to be configured.

Gets or sets a value representing the DistributedLockingMechanism to use.

Valid values:

`"SqlServerDistributedLockingMechanism"`

`"SqliteDistributedLockingMechanism"`


Key: `DistributedLockingReadLockDefaultTimeout`

Type: `string`

(default: `00:01:00`

)

Gets or sets a value representing the maximum time to wait whilst attempting to obtain a distributed read lock.

The default value is 60 seconds.

Key: `DistributedLockingWriteLockDefaultTimeout`

Type: `string`

(default: `00:00:05`

)

Gets or sets a value representing the maximum time to wait whilst attempting to obtain a distributed write lock.

The default value is 5 seconds.

Key: `MainDomAcquisitionTimeout`

Type: `string`

(default: `00:00:40`

)

Gets or sets a value representing the maximum time to wait whilst attempting to acquire MainDom status on startup.

The default value is 40 seconds.

Last updated

Was this helpful?

---

### Health checks | CMS

Information on the health check settings section

The health checks section allows you to disable certain health checks, and configure your own custom notification methods, that will automatically run the health checks every so often, and notify you if any health checks fails.

An example of a HealthChecks settings can look something like this:

```
"Umbraco": {
  "CMS": {
    "HealthChecks": {
      "DisabledChecks": [
        {
          "Id": "D0F7599E-9B2A-4D9E-9883-81C7EDC5616F"
        }
      ],
      "Notification": {
        "Enabled": true,
        "FirstRunTime": "0 4 * * *",
        "Period": "1.00:00:00",
        "NotificationMethods": {
          "email": {
            "Enabled": true,
            "Verbosity": "Detailed",
            "FailureOnly": true,
            "Settings": {
              "RecipientEmail": "[email protected]"
            }
          }
        }
      }
    }
  }
}
```

This config will enable notifications to run the checks and notify via email if a check fails. The checks will run the first time five minutes after the site is booted, and then once every day.

The email notification method is built in, if you want to read more about creating you own notification methods, or see a list of the ID of every built in health check, then see [Extending health checks](/umbraco-cms/extending/health-check)

But let's go through the config one by one

A list of `DisabledHealthCheckSettings`

objects, each of these objects represents a disabled health check. Only the Id key needs to be present and have a value, corresponding to the GUID of the health check to disable.

There is also a `DisabledOn`

key representing the date the health check was disabled and a `DisabledBy`

key containing the ID of the user that disabled the health check, however these values are currently not used.

Settings relating to running the health checks automatically and sending out notifications.

Allows you to disable or enable all notifications methods, if set to false, the health checks will not automatically run.

This will configure when you run the health checks for the first time, if the value is not configured the health checks will run immediately after the site boots for the first time. This value is specified as a string in crontab format, so in this example, the health checks will first run at 4 a.m.

Specifies how often the health checks should run, as a DateTime string, in this example the checks will run every day (every 24 hours).

A dictionary of all the notification methods that should be used.

The key of the dictionary is the alias of the notification method, and the value is a `HealthChecksNotificationMethodSettings`

configuration object, in this case it's the built in `email`

notification method.

Each object allows the following to be configured:

Allows you to enable or disable specific checks.

Configures how verbose the reporting should be, the available options are:

Summary

Detailed


If set to true, the notification method will only run if a check has failed.

Allows you to set custom settings for a given implementation of a notification method, which settings are available depends on the specific implementation.

Last updated

Was this helpful?

---

### Hosting settings | CMS

Information on the hosting settings section

```
"Umbraco": {
  "CMS": {
    "Hosting": {
      "ApplicationVirtualPath": "/",
      "LocalTempStorageLocation": "Default",
      "TemporaryFileUploadLocation"
      "Debug": false,
      "SiteName"
    }
  }
}
```

Setting overview

Application virtual path

Local temp storage location

Temporary file upload location

Debug

Site name

Last updated

Was this helpful?

Information on the hosting settings section

Hosting settings contains settings regarding the hosting of the site, such as application virtual path, local temporary storage location and debug.

A full configuration with default values can be seen here:

```
"Umbraco": {
  "CMS": {
    "Hosting": {
      "ApplicationVirtualPath": "/",
      "LocalTempStorageLocation": "Default",
      "TemporaryFileUploadLocation"
      "Debug": false,
      "SiteName"
    }
  }
}
```

Setting overview

Application virtual path

This setting specified the virtual path of the application, this path must start with a slash.

Local temp storage location

This setting specifies the location of the local temp storage.

Options:

Default

EnvironmentTemp


Temporary file upload location

This setting specifies the location of the temporarily uploaded files, for instance, when uploading files in the media section. The `umbraco/Data/TEMP/TemporaryFile/`

folder is used if not specified.

Debug

This setting allows you to run Umbraco in debug mode, by setting the value to true.

Site name

Gets or sets a value specifying the name of the site. The is used if not specified

Last updated

Was this helpful?

Was this helpful?

---

### Imaging settings | CMS

Information on the imaging settings section

The imaging settings section lets you configure the cache and resize settings for processed images on your project (using as default implementation). If you need to configure allowed image file types or auto fill image properties, you want to use [content settings](/umbraco-cms/reference/configuration/contentsettings) instead.

All these settings contain default values, so nothing needs to be explicitly configured. A complete settings section for imaging can be seen here with all the default values:

```
"Umbraco": {
  "CMS": {
    "Imaging": {
      "Cache": {
        "BrowserMaxAge": "7.00:00:00",
        "CacheMaxAge": "365.00:00:00",
        "CacheFolderDepth": 8,
        "CacheHashLength": 12,
        "CacheFolder": "~/umbraco/Data/TEMP/MediaCache"
      },
      "Resize": {
        "MaxWidth": 5000,
        "MaxHeight": 5000
      },
      "HMACSecretKey": ""
    }
  }
}
```

Contains configuration for browser and server caching. When changing these cache headers, it is recommended to clear your media cache. This is due to the data being stored in the cache and not updated when the configuration is changed.

Specifies how long a requested processed image may be stored in the browser cache by using this value in the `Cache-Control`

response header. The default is 7 days (formatted as a timespan).

Specifies how long a processed image may be used from the server cache before it needs to be re-processed again. The default is one year (365 days, formatted as a timespan).

Gets or sets the depth of the nested cache folders structure to store the images. Defaults to 8.

Gets or sets the length of the filename to use (minus the extension) when storing images in the image cache. Defaults to 12 characters.

Allows you to specify the location of the cached images folder. By default, the cached images are stored in `~/umbraco/Data/TEMP/MediaCache`

. The tilde (`~`

) resolves to the content root of your project/application.

Contains configuration for image resizing.

Specifies the maximum width and height an image can be resized to. If the requested width and height are *both* above the configured maximums, no resizing will be performed. This adds basic security to prevent resizing to big dimensions and using a lot of server CPU/memory to do so.

The maximum width and height settings are enforced by setting the `ImageSharpMiddlewareOptions.OnParseCommandsAsync`

option of ImageSharp to an Umbraco-specific function. If you want to add your own logic without overwriting this behaviour, use the following code:

Specifies the key used to secure image requests by generating an HMAC. This ensures that only valid requests can access or manipulate images.

To enable it, you need to set a secure random key. This key should be kept secret and not shared publicly. The key can be set through the `IOptions`

pattern, or you can insert a base64 encoded key in the `appsettings.json`

file. The key should ideally be 64 bytes long.

The key must be the same across all environments (development, staging, production) to ensure that image requests work for content published across environments.

For new Umbraco installations, a unique key will be automatically created and applied to the configuration.

For projects created on Umbraco 17.2 or earlier, a unique key was not automatically created and applied.

If the `HMACSecretKey`

is not set, image requests are not secured, and any person can request images with any parameters. This may expose your server to abuse, such as excessive resizing requests or unauthorized access to images.

It is recommended to add this key.

A health check is available under *Settings > Health Checks* that verifies the existence of the configured key and warns if it is absent.

The `HMACSecretKey`

should be a secure, random key. For most use cases, a 64-byte (512-bit) key is recommended. If you are using `HMACSHA384`

or `HMACSHA512`

, you may want to use a longer key (for example: 128 bytes).

**appsettings.json**

**Using the ****IOptions**** pattern**

To generate the `HMACSecretKey`

programmatically instead of hardcoding it in configuration files, use the `IOptions`

pattern. The following example demonstrates how to generate a secure random key at runtime:

The `HMACSecretKey`

must be kept secret and never exposed publicly. If the key is exposed, malicious users may generate valid HMACs and exploit server resources.

To verify that your `HMACSecretKey`

is working correctly:

Set the

`HMACSecretKey`

key in the`appsettings.json`

file or via the`IOptions`

pattern.Make a request to an image URL with valid parameters and ensure it works as expected.

Modify the URL parameters or remove the HMAC signature and confirm that the request is rejected.


Last updated

Was this helpful?

---

### Indexing settings | CMS

Information on the indexing section

Last updated

Was this helpful?

Information on the indexing section

This section allows you to configure how content is indexed for Examine.

```
"Umbraco": {
  "CMS": {
    "Indexing": {
      "ExplicitlyIndexEachNestedProperty": true,
      "BatchSize": 10000
    }
  }
}
```

ExplicitlyIndexEachNestedProperty

When indexing content, each property contained within certain complex editors are indexed as separate fields by default. These complex editors include:

Block List

Block Grid


The complex editors are also indexed to their own separate fields, which then contains "the sum" of all properties contained within.

In some cases this yields a lot of fields in the index, which can lead to errors when performing searches. Changing this setting to `false`

can mend that issue. It prevents each contained property from being written to the index in its own field.

BatchSize

For large indexing operations (such as rebuilding an index), content is loaded from the database and indexed in batches.

Depending on the complexity of your content model, lowering the batch size might speed up these operations.

Last updated

Was this helpful?

Was this helpful?

---

### Install Default Data Settings | CMS

Information on configuration allowing for the modification of default data installed in new projects

When Umbraco is installed for the first time, it creates a set of default data. These include a language, some Data Types, and some Media and Member Types.

In certain setups, you may want to take control over what is installed and opt-out of the creation of certain items.

When working in a team and using Umbraco Deploy for schema updates, consider your colleague's local project setup. The default installed data may not always be useful.

For example, if different languages are set up in Umbraco, it's better not to recreate them from the default language (en-US). In other situations, certain Umbraco default Data, Member and Media Types may not be required.

The following example configuration shows how this default data installation can be customized:

```
"Umbraco": {
  "CMS": {
  "InstallDefaultData": {
      "Languages": {
        "InstallData": "Values",
        "Values": [
          "en-US"
        ]
      },
      "DataTypes": {
        "InstallData": "ExceptValues",
        "Values": [
          "0225af17-b302-49cb-9176-b9f35cab9c17"
        ]
      },
      "MediaTypes": {
        "InstallData": "All",
      },
      "MemberTypes": {
        "InstallData": "None"
      }
    }
  }
}
```

Each `InstallData`

setting can be one of the following values:

`All`

- all default data for the type will be installed (this is the default behavior if the configuration is omitted).`Values`

- only the default data specified will be installed. For languages, the values are the ISO codes for the language. For all other types, the Guid for the type should be listed.`ExceptValues`

- all default data except those specified will be installed.`None`

- no default data of the type will be installed.

Be cautious when changing a Data Type configuration, as there are some dependencies between the different types. Make sure to check the reference information in the `info`

tab to ensure they are not referenced somewhere else.

For example, if you check the info tab of the `Label (bigint)`

Data Type, you can see that it is referenced by the `Media Types`:


For `DataTypes`

, `MediaTypes`

and `MemberTypes`

the Guid identifiers for the default data items need to be provided in the `Values`

collection.

For `Languages`

, the `Values`

collection expects the standard language ISO codes to be provided. Given this code is enough to fully specify a language, it's possible to use this collection to install additional default data.

As an example, the following configuration would omit the default "English (United States)" language and instead install the "English (United Kingdom)" and "Italian" languages. As "English (United Kingdom)" is provided first, it would be created as Umbraco's default language for content creation.

The Guid values representing the default Data, Media, and Member Types installed are as follows.

Data types:

Media types:

Member types:

Last updated

Was this helpful?

---

### Logging settings | CMS

Information on the logging settings section.

```
"Umbraco": {
  "CMS": {
    "Logging": {
      "MaxLogAge": "2.00:00:00",
      "Directory": "~/CustomLogFileLocation",
      "FileNameFormat": "UmbracoTraceLog.{0}..json",
      "FileNameFormatArguments": "MachineName"
    }
  }
}
```

MaxLogAge

Directory

FileNameFormat

FileNameFormatArguments

Last updated

Was this helpful?

Information on the logging settings section.

The majority of logging related configuration has been moved to the Serilog configuration see [Serilog settings](/umbraco-cms/reference/configuration/serilog) for more information.

The following configuration is available in the Logging settings:

```
"Umbraco": {
  "CMS": {
    "Logging": {
      "MaxLogAge": "2.00:00:00",
      "Directory": "~/CustomLogFileLocation",
      "FileNameFormat": "UmbracoTraceLog.{0}..json",
      "FileNameFormatArguments": "MachineName"
    }
  }
}
```

MaxLogAge

This setting allows you to configure the maximum log age for the internal audit log scrubbing. The default maximum age for the internal audit log is 24 hours. Change the duration with the `MaxLogAge`

key in the Logging settings.

To increase the maximum age of the entries in the audit log to 48 hours (2 days), set the value to `2.00:00:00`.


Directory

By default, all log files are saved to the `umbraco/Logs`

directory. You can define a custom directory for your log files by using the `Directory`

key in the Logging settings.

Set the value to `~/LogFiles`

to add all log files to a `LogFiles`

directory in the root of the file structure.

FileNameFormat

The default file name format for the Umbraco log file is `UmbracoTraceLog.{0}..json`

. The single argument is replaced at runtime with the server's machine name.

If you want to change the file name or include additional arguments, you can amend the format with the `FileNameFormat`

setting.

FileNameFormatArguments

By default the single argument for the log file format name is the server's machine name.

Other or additional arguments can be provided via the `FileNameFormatArguments`

setting using a comma-delimited string:

`MachineName`

- the server's name.`EnvironmentName`

- the ASP.NET environment name such as "Development" or "Production.

So for example, to provide both supported arguments you would configure `MachineName,EnvironmentName`.


The number of arguments provided should match the placeholders in the configured `FileNameFormat`.


Last updated

Was this helpful?

Was this helpful?

---

### Maximum Upload Size Settings | CMS

Information on how to change the default cap of upload size

Using IIS

```
<?xml version="1.0"?>
<configuration>
  <system.webServer>
    <security>
      <requestFiltering>
        <!-- 2 MB in bytes -->
        <requestLimits maxAllowedContentLength="2000000" />
      </requestFiltering>
    </security>
  </system.webServer>
</configuration>
```

Hosting on Umbraco Cloud

Using Kestrel

![System Information with Maximum Upload Size Settings](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5c363f078df0b433ac71f5ef15918590f3436e63%252Fsysteminformation-tempfileconfig.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b262622e&sv=2)

External Server Configurations

Last updated

Was this helpful?

Information on how to change the default cap of upload size

Learn how to change the upload size limit for your Umbraco site depending on your hosting setup:

By default, Umbraco does not restrict upload size. The limits are controlled by the hosting platform.

It is advisable that you tell Umbraco what the maximum upload size is by setting the `Umbraco:CMS:Runtime:MaxRequestLength`

in the `appsettings.json`

file. The Backoffice will use this value to help guide the users.

Using IIS

The default upload limit in IIS is 30000000 bytes (~28.6 MB). The maximum value allowed is 4 GB.

To increase the upload limit:

Create or update the

`web.config`

file at the root of your project.Add the following configuration:


```
<?xml version="1.0"?>
<configuration>
  <system.webServer>
    <security>
      <requestFiltering>
        <!-- 2 MB in bytes -->
        <requestLimits maxAllowedContentLength="2000000" />
      </requestFiltering>
    </security>
  </system.webServer>
</configuration>
```

`maxAllowedContentLength`

is specified in bytes. For example:

2 MB = 2097152 bytes

100 MB = 104857600 bytes

500 MB = 524288000 bytes

4 GB = 4294967295 (maximum value allowed)


Hosting on Umbraco Cloud

Umbraco Cloud uses IIS for hosting, so you must apply this setting in your `web.config`

file. The maximum permitted upload size on Umbraco Cloud is `500 MB`.


To change the limit, update the `maxAllowedContentLength`

value in your `web.config`

file accordingly.

Using Kestrel

Kestrel’s runtime settings allow you to configure `MaxRequestLength`

. If you want to upload files larger than 50MB, or amend this default, update this value in the `appsettings.json`

file.

Example configuration:

`MaxRequestLength`

is specified in kilobytes. For example:2000 KB = 2 MB

100000 KB = 100 MB



You can check the current configuration by inspecting the "System information" output in the Backoffice. You can access it by clicking the logo and then "System information":

External Server Configurations

Last updated

Was this helpful?

Was this helpful?

```
"Umbraco": {
  "CMS": {
    "Runtime": {
      "MaxRequestLength": 2000
    }
  }
}
```

---

### Models builder settings | CMS

Information on the models builder settings section

This section allows you to configure the Umbraco models builder, a complete section with default values can be seen here:

```
"Umbraco": {
  "CMS": {
    "ModelsBuilder": {
      "ModelsMode": "InMemoryAuto",
      "ModelsNamespace": "Umbraco.Cms.Web.Common.PublishedModels",
      "FlagOutOfDateModels": false,
      "ModelsDirectory": "~/umbraco/models",
      "AcceptUnsafeModelsDirectory": false,
      "DebugLevel": 0,
      "IncludeVersionNumberInGeneratedModels": true,
      "GenerateVirtualProperties": true
    }
  }
}
```

Let's go through them one by one.

Specifies how the models builder will generate models and when to generate them. The options are:

`Nothing`

- The modelsbuilder will not generate any models, this means that all views will use IPublishedContent, instead of strongly typed models.`InMemoryAuto`

- Models will automatically be generated each time a content type change occurs, and will then be compiled, and loaded into memory dynamically. This means that the models are only available in views, however they will be available instantly.`SourceCodeManual`

- Models will be generated as`.cs`

files whenever a user clicks the "Generate models" button on the models builder dashboard - however, the models will not be compiled and loaded into memory dynamically. This means that models are available to edit within the project. The project needs to be recompiled and restarted for the new models, or model changes, to take effect.`SourceCodeAuto`

- This mode behaves the same as`SourceCodeManual`

with one difference, the generation of models happens automatically every time a content type change occurs.

When using Models Builder it is best practice to use the "Nothing" setting for all `appsettings.json`

files. If needed, the models mode can then be set to "SourceCodeManual" or "SourceCodeAuto" In the `appsettings.json`

file used on the local environment.

This setting allows you to customize the namespace of the generated models, for instance you might want to change this to something that aligns better with your project structure, such as `MySite.ContentModels`.


This setting allows you to specify if a model should be flagged as out of date if its content type, or a datatype the content type depends on, are changed. When a model is flagged as out of date you will be able to see that you need to regenerated models in modelsbuilder dashboard.

This setting is only really relevant if you use the `SourceCodeManual`

models mode, since otherwise the models will be automatically regenerated, and will therefore never be out of date.

If you set this setting to true while using an `Auto`

mode, it will automatically be interpreted as false.

Allows you to specify a custom directory for your generated models. By default this settings has to be a virtual directory, that is, it must start with `~/`

, if needed `AcceptUnsafeModelsDirectory`

can be set to true, to allow the path to be outside the website root, be aware though that this is a potential security risk.

If you want to generate models outside the web project you can change the ModelsDirectory path. Suppose you have a data project called My.Website.Data the ModelsDirectory path should be:

`~/../My.Website.Data/Models/`


By setting this to true, you specify that the models directory is allowed to be outside the websites root. This is not allowed by default since it can be a potential security risk.

This setting specifies the logging level for the models builder. By default this is set to 0, which means minimal logging. Anything higher that 0 means increased logging. Be aware that this setting should only be set to something higher than 0 for development use, not on live sites.

When source code options are used, the Umbraco version number written to the generated code for each property of the model. This can be useful for debugging purposes but isn't essential. It causes the generated code to change every time Umbraco is upgraded and models are regenerated. In turn, this leads unnecessary code file changes that need to be checked into source control.

If you prefer to exclude this version number from being written to the generated code, set this value to `false`.


By default, the models will be generated with all properties marked as `virtual`

for extensibility purposes. You can disable `virtual`

properties by setting this to `false`.


does not support changing or adding `virtual`

properties while the application is running.

If you plan to use Hot Reload while developing your Umbraco site, set this value to `false`.


Last updated

Was this helpful?

---

### Package Migration | CMS

Information on the package migration settings section

This settings section provides control over how package migrations are executed in different environments (local, development, live etc.)

Package migrations are defined by package developers allowing them to add functionality to their package that enhances the Umbraco CMS. There can be various types of migrations applied, including creating custom database tables and installing Umbraco schema and content.

They run on start-up, thus ensuring that the functionality of the package has the necessary infrastructure, schema, and content in place when it is used.

Migration steps that are explicitly created by the package developer to make database schema changes will always run in all environments.

Depending on your workflow, for those steps that install Umbraco data - whether schema such as document types, content, or media - you may want them run in all environments, or you may prefer to only do this in certain ones.

The default behavior for Umbraco CMS is for all package migrations to run in all environments.

If using Umbraco Cloud, the default is to run package migrations fully *only in local environments*. By doing this, for schema, `.uda`

files will be generated in the `/umbraco/Deploy/Revision`

folder, which when pushed to a Cloud environment will be used to install the schema and content there. For content and media, the "queue for transfer" operation can be used. With this behavior, we avoid any issues caused by both a package migration and a deployment operation attempting to create schema and content.

If different behavior is required, or if using Umbraco Deploy On-Premises, the following settings can be applied:

```
{
  "$schema": "https://json.schemastore.org/appsettings.json",
  "Umbraco": {
    "CMS": {
      "PackageMigration": {
        "RunSchemaAndContentMigrations": true,
        "AllowComponentOverrideOfRunSchemaAndContentMigrations": true
      }
    }
  }
}
```

If set to `true`

, the default behavior described above for Umbraco CMS on-premises and Umbraco Cloud will be applied. By setting to `false`

, the installation of Umbraco schema and content from a package migration will be skipped. If missing the default value is `true`.


If this is set to the default value of `true`

, Umbraco Cloud (or other deployment tools) can override the configured value of `RunSchemaAndContentMigrations`

as is appropriate for their operation. By setting to `false`

such tools should respect this setting, not make any overrides and use the configured value.

Last updated

Was this helpful?

---

### Plugins settings | CMS

Information on the plugins settings section

```
"Umbraco": {
  "CMS": {
    "Plugins": {
      "BrowsableFileExtensions": [
        ".html",
        ".css",
        ".js",
        ".jpg", ".jpeg", ".gif", ".png", ".svg",
        ".eot", ".ttf", ".woff", ".woff2",
        ".xml", ".json", ".config",
        ".lic"]
    }
  }
}
```

Last updated

Was this helpful?

Information on the plugins settings section

The Plugins settings allow you to configure how Umbraco handles plugins. Currently, you can only configure browsable file extensions, which allows you to customize what file types plugins are allowed to use for the front end. The default configuration looks like this:

```
"Umbraco": {
  "CMS": {
    "Plugins": {
      "BrowsableFileExtensions": [
        ".html",
        ".css",
        ".js",
        ".jpg", ".jpeg", ".gif", ".png", ".svg",
        ".eot", ".ttf", ".woff", ".woff2",
        ".xml", ".json", ".config",
        ".lic"]
    }
  }
}
```

As you can see above, by default, markup, styles, scripts, images, fonts, configurations, and license type are included. If you were to, for example, remove the ".html" entry, then plugins would no longer be allowed to use HTML files.

Last updated

Was this helpful?

Was this helpful?

---

### Request handler settings | CMS

Information on the request handler settings section

```
"Umbraco": {
  "CMS": {
    "RequestHandler": {
      "AddTrailingSlash": true,
      "ConvertUrlsToAscii": "try",
      "ConvertFileNamesToAscii": "false",
      "EnableDefaultCharReplacements": true,
      "UserDefinedCharCollection": [
      {
        "Char": " ",
        "Replacement": "-"
      },
      {
        "Char": "\\",
        "Replacement": ""
      },
      {
        "Char": "'",
        "Replacement": ""
      },
      {
        "Char": "%",
        "Replacement": ""
      },
      {
        "Char": ".",
        "Replacement": ""
      },
      {
        "Char": ";",
        "Replacement": ""
      },
      {
        "Char": "/",
        "Replacement": ""
      },
      {
        "Char": "\\\\",
        "Replacement": ""
      },
      {
        "Char": ":",
        "Replacement": ""
      },
      {
        "Char": "#",
        "Replacement": ""
      },
      {
        "Char": "+",
        "Replacement": "plus"
      },
      {
        "Char": "*",
        "Replacement": "star"
      },
      {
        "Char": "&",
        "Replacement": ""
      },
      {
        "Char": "?",
        "Replacement": ""
      },
      {
        "Char": "æ",
        "Replacement": "ae"
      },
      {
        "Char": "ä",
        "Replacement": "ae"
      },
      {
        "Char": "ø",
        "Replacement": "oe"
      },
      {
        "Char": "ö",
        "Replacement": "oe"
      },
      {
        "Char": "å",
        "Replacement": "aa"
      },
      {
        "Char": "ü",
        "Replacement": "ue"
      },
      {
        "Char": "ß",
        "Replacement": "ss"
      },
      {
        "Char": "|",
        "Replacement": "-"
      },
      {
        "Char": "<",
        "Replacement": ""
      },
      {
        "Char": ">",
        "Replacement": ""
      }
      ]
    }
  }
}
```

Add trailing slash

Convert URLs to ASCII

Convert file names to ASCII

Enable default character replacements

Char collection

Last updated

Was this helpful?

---

### Runtime settings | CMS

Information on the runtime settings section

```
"Umbraco": {
  "CMS": {
    "Runtime": {
      "MaxRequestLength": 2048,
      "Mode": "BackofficeDevelopment",
      "TemporaryFileLifeTime": "1.00:00:00"
    }
  }
}
```

Last updated

Was this helpful?

Information on the runtime settings section

In the Runtime settings you can configure:

Size limits for requests and query strings. Neither of these settings needs to be configured. If nothing is configured, requests and query strings can be any size.

The runtime mode of Umbraco.

The lifetime of temporary file uploads. This is primarily used when uploading images and other media in the backoffice.


An example of a configuration could look something like:

```
"Umbraco": {
  "CMS": {
    "Runtime": {
      "MaxRequestLength": 2048,
      "Mode": "BackofficeDevelopment",
      "TemporaryFileLifeTime": "1.00:00:00"
    }
  }
}
```

`MaxRequestLength`

is specified in kilobytes. Setting this limits the request size, including the size of uploaded files. This only has an effect on the server when hosting with Kestrel, but is also used by the Backoffice to advise users. See the[Maximum Upload Size Settings](/umbraco-cms/reference/configuration/maximumuploadsizesettings)article for more information.`Mode`

can have three values:`BackofficeDevelopment`

(default),`Development`

, and`Production`

. For more information, see the[Runtime modes](/umbraco-cms/fundamentals/setup/server-setup/runtime-modes)article.`TemporaryFileLifeTime`

is specified as a timespan. The default value is one day -`1.00:00:00`.


Last updated

Was this helpful?

Was this helpful?

---

### Security Settings | CMS

Information on the security settings section

```
"Umbraco": {
  "CMS": {
    "Security": {
      "KeepUserLoggedIn": false,
      "HideDisabledUsersInBackOffice": false,
      "AllowPasswordReset": true,
      "AuthCookieName": "UMB_UCONTEXT",
      "AuthCookieDomain": "",
      "UsernameIsEmail": true,
      "MemberRequireUniqueEmail": true,
      "AllowedUserNameCharacters": "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789-._@+\\",
      "BackOfficeHost": "http://your-domain.com",
      "UserPassword": {
        "RequiredLength": 10,
        "RequireNonLetterOrDigit": false,
        "RequireDigit": false,
        "RequireLowercase": false,
        "RequireUppercase": false,
        "HashAlgorithmType": "PBKDF2.ASPNETCORE.V3",
        "MaxFailedAccessAttemptsBeforeLockout": 5
      },
      "MemberPassword": {
        "RequiredLength": 10,
        "RequireNonLetterOrDigit": false,
        "RequireDigit": false,
        "RequireLowercase": false,
        "RequireUppercase": false,
        "HashAlgorithmType": "PBKDF2.ASPNETCORE.V3",
        "MaxFailedAccessAttemptsBeforeLockout": 5
      },
      "UserDefaultLockoutTimeInMinutes": 43200,
      "MemberDefaultLockoutTimeInMinutes": 43200,
      "AllowConcurrentLogins": false,
      "UserAllowConcurrentLogins": null,
      "MemberAllowConcurrentLogins": null,
      "UserDefaultFailedLoginDurationInMilliseconds": 1000,
      "UserMinimumFailedLoginDurationInMilliseconds": 250,
      "PasswordResetEmailExpiry": "01:00:00",
      "UserInviteEmailExpiry": "3.00:00:00",
      "BackOfficeTokenCookie": {
        "SameSite": "Strict",
        "SiteName": ""
      }
    }
  }
}
```

Root level settings

Keep user logged in

Hide disabled users in backoffice

Allow password reset

Auth cookie name

Auth cookie domain

Username is email

Member require unique email

Allowed user name characters

BackOffice Host

User default lockout time

Member default lockout time

Allow concurrent logins

User allow concurrent logins

Member allow concurrent logins

Configuration examples

User login duration

Password reset email expiry

User invite email expiry

User password settings

Required length

Require non letter or digit

Require digit

Require lowercase

Require uppercase

Max failed access attempts before lockout

Hash algorithm type

Member password settings

Backoffice token cookie settings

Same site

Site name

Last updated

Was this helpful?

---

### Serilog settings | CMS

Information on the serilog settings section

Umbraco uses Serilog as its logging library, this means that the configuration of logging is offloaded to Serilog instead of the CMS. This means that logging specific configuration is not in the `Umbraco.Cms`

section, but instead the Serilog section.

We will go through some of the more common logging configurations here, but for more information see the .

When you create a new Umbraco project the following Serilog section will be included by default:

```
"Serilog": {
  "MinimumLevel": {
    "Default": "Information",
    "Override": {
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information",
      "System": "Warning"
    }
  }
}
```

As you can see above, the CMS comes with a default Serilog config that defines the minimum log level with the `"MinimumLevel"`

key.

You can specify the overall minimum log level with the `"Default"`

key. This will apply to all namespaces, however it's also possible to override this log level for specific names spaces with the `"Override"`

key. In the example above, any logging coming from the `Microsoft`

and `System`

namespaces will only log warnings and up, however the `Microsoft.Hosting.Lifetime`

namespace will log information and up.

The possible values, from most verbose to least, is:

Verbose

Debug

Information

Warning

Error

Fatal


For information on what each of these levels means see .

This can be done by updating the appsettings.json configuration file to specify namespaces in which you want to change the log level for.

Serilog has the ability to log to a number of different mechanisms, from console to files, even to Slack or email. This is all configured using what Serilog calls sinks.

An example of this can be seen in the default `appsettings.Development.json`

, where Serilog is configured to log to the console using the Async wrapper sink:

Here you can see that we use the `"WriteTo"`

key to specify a list of sinks the logger should write to. In this case we use the `"Async"`

sink configured to write to the console, this means that we'll log to the console asynchronously.

Now there's too many sinks to cover here, for a full list of all available sinks see . Each of these entries will have their own documentation on how to set up the logging with the particular sink.

By default, Umbraco uses a special Serilog 'sink' that is optimized for performance. To change parameters for only this sink, but not the default. For E.g higher log level for this compared to other sinks you can do it in the following way:

You can also disable this sink if you do not wish to write files to disk.

You may wish to add a log property to all log messages. A good example could be a log property for the `environment`

to determine if the log message came from `development`

or `production`.


This is useful when you could be writing logs from all environments or multiple customer projects into a single logging source, such as Elasticsearch. This would allow you to search and filter for a specific project and its environment to see the log messages. You can also reference your hosting server's environment variables in the property values.

In the `appsettings.json`

configuration file you can add the following lines

Last updated

Was this helpful?

---

### Type finder settings | CMS

Information on the type finder settings section

```
"Umbraco": {
  "CMS": {
    "TypeFinder": {
      "AssembliesAcceptingLoadExceptions": "*",
      "AdditionalAssemblyExclusionEntries": []
    }
  }
}
```

Last updated

Was this helpful?

Information on the type finder settings section

The type finder settings allows you to specify assemblies that accept load exceptions when they are type scanned. For multiple assemblies separate them with a comma (`,`

).
To accept load exceptions for all assemblies use an asterisk (`*`

), like so:

Furthermore it is possible to add additional assemblies to the exclusion filter. Thereby these assemblies will be ignored by Umbraco. This can be useful depending on nuget packages that are not Umbraco packages.

```
"Umbraco": {
  "CMS": {
    "TypeFinder": {
      "AssembliesAcceptingLoadExceptions": "*",
      "AdditionalAssemblyExclusionEntries": []
    }
  }
}
```

Last updated

Was this helpful?

Was this helpful?

---

### Unattended | CMS

Information on the unattended settings section

```
{
  "$schema": "https://json.schemastore.org/appsettings.json",

  "ConnectionStrings": {
    "umbracoDbDSN": "Server=.;Database=DocsSite;Integrated Security=true"
  },
  "Umbraco": {
    "CMS": {
      "Unattended": {
        "InstallUnattended": true,
        "PackageMigrationsUnattended": true,
        "UpgradeUnattended": true,
        "UnattendedUserName": "A.N. Other",
        "UnattendedUserEmail": "[email protected]",
        "UnattendedUserPassword": "APasswordMeetingRequirements",
        "UnattendedTelemetryLevel": "Detailed"
      }
    }
  }
}
```

Install unattended

Upgrade unattended

Unattended user name

Unattended email

Unattended user pass

Unattended telemetry level

Package migrations unattended

Last updated

Was this helpful?

---

### Web routing | CMS

Information on the web routing settings section

This section allows you to configure routing for your solution, all of these settings have either default values, or do not need to be configured. However, you might want to tweak these settings in some scenarios, for instance, if you're running in a load-balanced setup.

An example of a web routing config with default values, and a placeholder for the application URL can be seen here:

```
"Umbraco": {
  "CMS": {
    "WebRouting": {
      "TryMatchingEndpointsForAllPages": false,
      "TrySkipIisCustomErrors": false,
      "InternalRedirectPreservesTemplate": false,
      "DisableAlternativeTemplates": false,
      "ValidateAlternativeTemplates": false,
      "DisableFindContentByIdPath": false,
      "DisableRedirectUrlTracking": false,
      "UrlProviderMode": "Auto",
      "UmbracoApplicationUrl": "http://www.mysite.com/",
      "ApplicationUrlDetection": "None",
      "UseStrictDomainMatching": false
    }
  }
}
```

**Are you on Umbraco Cloud?**

It is not possible to change the `UmbracoApplicationUrl setting`

because the value is overwritten to the default Umbraco URL: `https://[project-alias].[region].umbraco.io/`

on Umbraco Cloud.

The following is an example of how you can use code to get the value for the `UmbracoApplicationUrl`

configuration key:

When set to `true`

Umbraco will check if any routed endpoints match a front-end request. This happens before the Umbraco dynamic router tries to map the request to a Umbraco content item. This setting should not be necessary as long as the Umbraco catch-all route is registered last.

Defines the value of Response.TrySkipIisCustomErrors when an error (404, 400, 500...) is encountered. In order to prevent IIS from displaying its own 404 or 500 pages, set this to `true`

to have your own page displayed.

When true, an internal redirect does not reset the alternative template, if any.

When true, the entire alternative templates feature of Umbraco is disabled.

**validateAlternativeTemplates** will not load the template from the database. If `false`

the template might not exists in the database. Otherwise the template need to exist in the database.

If set to true alternative templates will be validated

When true, content can't be found by their ID meaning that urls such as /1234 do *not* find content with ID 1234.

When you move and rename pages in Umbraco, 301 permanent redirects are automatically created, set this to true if you do not want this behavior.

Will set the URL provider mode, options are:

`Default`

: Indicates that the URL provider should do what it has been configured to do.`Relative`

: Indicates that the URL provider should produce relative URLs exclusively.`Absolute`

: Indicates that the URL provider should produce absolute URLs exclusively.`Auto`

: Indicates that the URL provider should determine automatically whether to return relative or absolute URLs.

Defines the Umbraco application URL that the server should reach itself. This URL is used in features such as password reset links, user invitations, and other email notifications, as well as for some health checks. The format is: `http://www.mysite.com/`

and must contain the scheme (http/https) and complete hostname.

When this setting is provided, it always takes precedence over any value detected through `ApplicationUrlDetection`

. Setting an explicit value is the recommended approach for production environments.

Previously before v9, it was required to specify the **backoffice** path as this was customizable (`/umbraco`

by default). However, from v9+ this is no longer possible, so it's sufficient to use the URL that contains the scheme (http/https) and complete hostname.

Controls how Umbraco determines the application URL when `UmbracoApplicationUrl`

has not been set explicitly. Available options are:

`None`

(default): No auto-detection takes place. The application URL must be set explicitly via`UmbracoApplicationUrl`

. Operations that require it (such as user invitations and password resets) will fail with a`400 Bad Request`

response indicating that the application URL is not configured.`FirstRequest`

: The application URL is set from the first HTTP request received by the server, after which it is locked. Subsequent requests with different`Host`

headers are ignored.`EveryRequest`

: The application URL is set from the first HTTP request and can be overwritten by every subsequent request.

In environments where Umbraco is not behind a reverse proxy that validates the `Host`

header, allowing auto-detection (`FirstRequest`

or `EveryRequest`

) can enable a forged `Host`

header to influence the URL used in email notifications. Explicitly configuring `UmbracoApplicationUrl`

is the recommended approach.

`UmbracoApplicationUrl`

always takes precedence over the value derived through `ApplicationUrlDetection`.


With multi-site setups multiple root nodes will be prepared with assigned domains. When routing a request, the content matched by path below the root node that matches the domain is returned.

A request may be received on an unrecognized domain that otherwise matches by path to a content item. By default Umbraco will route this item.

With `UseStrictDomainMatching`

set to `true`

, the request will only be routed if the domain as well as the path matches.

Why use this? It's possible to receive requests on domains that are configured on web server but aren't setup as domains in Umbraco. The Azure web app default domain is an example of this. By switching this option on, requests that come in on that domain will no longer be routed.

Last updated

Was this helpful?

---

---
