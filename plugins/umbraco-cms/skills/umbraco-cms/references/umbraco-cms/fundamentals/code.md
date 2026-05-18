# Code

## Contents

- [Creating Forms | CMS](#creating-forms-cms)
- [Debugging | CMS](#debugging-cms)
- [Source Control | CMS](#source-control-cms)
- [Subscribing To Notifications | CMS](#subscribing-to-notifications-cms)
- [Service APIs | CMS](#service-apis-cms)

---

## Creating Forms | CMS

Information on creating forms in Umbraco

Creating the view model

```
namespace MyFirstForm.Models;

public class ContactFormViewModel 
{
    public string Name { get; set; }
    public string Email { get; set; }
    public string Message { get; set; }
}
```

Creating the view

Adding the controller

Adding the form to a template

More information

Last updated

Was this helpful?

Information on creating forms in Umbraco

Creating forms requires that you know your way around .NET Core MVC. So if you are familiar with adding view models, views and controllers you are ready to make your first form.

You can also use . It lets you and/or your editors create and handle forms in the backoffice. This includes setting up validation, redirecting and storing and sending form data. Great UI, extendable and supported by Umbraco HQ.

In this example we'll create a basic contact form containing a name, email and message field.

Creating the view model

First, we're going to create the model for the contact form by adding a new class to the `/Models`

folder. If the folder doesn't already exist, create it at the root of your website. Let's call it `ContactFormViewModel.cs`


```
namespace MyFirstForm.Models;

public class ContactFormViewModel 
{
    public string Name { get; set; }
    public string Email { get; set; }
    public string Message { get; set; }
}
```

Build your solution after adding the model.

Creating the view

Next, we add the view for the form to the `/View/Partials`

folder. Because we've added the model and built the solution we can add it as a strongly typed view.

Name your view "ContactForm".

The view can be built with standard MVC helpers:

Adding the controller

Finally, we're going to add the controller. Create a new empty class in the `/Controllers`

folder (if the folder doesn't already exist, create it at the root of the website). Name it `ContactFormController`

and make it inherit from `SurfaceController`

. Inheriting from `SurfaceController`

requires that you call its base constructor. If you are using an IDE: Integrated Development Environment, this can be done automatically.

If the model state is invalid, `CurrentUmbracoPage()`

will send the user back to the form. If valid, you can work with the form data, for example, sending an email to site admin and then `RedirectToCurrentUmbracoPage();`.


Adding the form to a template

You can add the form to a template by rendering the partial view:

More information

Last updated

Was this helpful?

Was this helpful?

```
@using MyFirstForm.Controllers
@model MyFirstForm.Models.ContactFormViewModel

@using (Html.BeginUmbracoForm<ContactFormController>(nameof(ContactFormController.Submit)))
{
    <div class="input-group">
        <label asp-for="Name"></label>
        <input asp-for="Name" />
    </div>
    <div>
        <label asp-for="Email"></label>
        <input asp-for="Email" />
    </div>
    <div>
        <label asp-for="Message"></label>
        <textarea asp-for="Message"></textarea>
    </div>
    <br/>
    <input type="submit" name="Submit" value="Submit" />
}
```

```
using Microsoft.AspNetCore.Mvc;
using MyFirstForm.Models;
using Umbraco.Cms.Core.Cache;
using Umbraco.Cms.Core.Logging; 
using Umbraco.Cms.Core.Routing;
using Umbraco.Cms.Core.Services;
using Umbraco.Cms.Core.Web;
using Umbraco.Cms.Infrastructure.Persistence;
using Umbraco.Cms.Web.Website.Controllers;

namespace MyFirstForm.Controllers;

public class ContactFormController : SurfaceController
{
    public ContactFormController(
        IUmbracoContextAccessor umbracoContextAccessor,
        IUmbracoDatabaseFactory databaseFactory,
        ServiceContext services,
        AppCaches appCaches,
        IProfilingLogger profilingLogger,
        IPublishedUrlProvider publishedUrlProvider) 
        : base(umbracoContextAccessor, databaseFactory, services, appCaches, profilingLogger, publishedUrlProvider)
    {}

    [HttpPost]
    public IActionResult Submit(ContactFormViewModel model)
    {
        if (!ModelState.IsValid)
        {
            return CurrentUmbracoPage();
        }
        
        // Work with form data here

        return RedirectToCurrentUmbracoPage();
    }
}
```

```
@using MyFirstForm.Models;

@{
    Html.RenderPartial("~/Views/Partials/ContactForm.cshtml", new ContactFormViewModel());
}
```

---

## Debugging | CMS

```
{
  "Umbraco": {
    "CMS": {
      "Hosting": {
        "Debug": true
      }
    }
  }
}
```

Tracing

Enabling Trace Logging

MiniProfiler

Displaying the MiniProfiler

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-db39a3caab102f81e600a1707b012681bb0f5f09%252Fv8-miniprofiler-view.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=908512b4&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7b36e615056c799fe8001d68c5a408a8e706cb13%252Fv8-miniprofiler-trivial.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=2f702dcd&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ea1a4c208c187cf27558bf2083b1e66e1150b166%252Fv8-miniprofiler-sql-trigger.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=78d69b6c&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9535949c1e3293ab18b97ac1842fc29c13c5b228%252Fv8-miniprofiler-sql-details.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=bc5158e4&sv=2)

Writing to the MiniProfiler

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-cd40b9f107cf4aa8deb1f84205297aee253c52aa%252Fv8-miniprofiler-write.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ee968ea9&sv=2)

Umbraco Productivity Tool - Chrome Extension

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-922074898af98704af5260847f33da828a5a5e36%252Fchrome-tool.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=20d73426&sv=2)

Last updated

Was this helpful?

During the development of your Umbraco site you can debug and profile the code you have written to analyse and discover bottlenecks in your code.

To perform proper debugging on your site you need to set your application to have debug enabled. This can be done by setting `Umbraco:CMS:Hosting:Debug="true"`

for example in the `appsettings.json`

file:

```
{
  "Umbraco": {
    "CMS": {
      "Hosting": {
        "Debug": true
      }
    }
  }
}
```

Debug should always be set to false in production.

Tracing

Tracing and trace logging are two names for the same technique. You need to configure which log messages you want to log.

Enabling Trace Logging

Do not enable trace logging in your production environment! It reveals an awful lot of (sensitive) information about your production environment.

We recommend at least logging the following namespace at minimum (Verbose) level to enable valuable trace logging. Thereby you will have information about all endpoints that have been executed.

The logged messages can as always be monitored in the log viewer in backoffice

MiniProfiler

Umbraco includes the Mini Profiler project in its core (see for more details). The MiniProfiler profiles your code method calls, giving you a greater insight into code duration and query time for (for example) underlying SQL queries. It's great for tracking down performance issues in your site's implementation.

Displaying the MiniProfiler

To display the profiler on the front end of your site:

Set

`Umbraco:CMS:Hosting:Debug`

to`true`

in`appsettings.json`

.Sign in to the backoffice as a user who has access to the

**Settings**section.Add

`?umbDebug=true`

to the request query string.

If you click 'Show Trivial' you can seen the kind of detail the MiniProfiler makes available to you about the execution path of your page:

and any underlying SQL Statements that are being executed for a part of the execution:

Writing to the MiniProfiler

If you feel like a part of your application is slow you can use the MiniProfiler in your code to test the speed of it.

All you have to do is inject the IProfiler interface and add a step around your logic:

and now in the profiler you can see:

Umbraco Productivity Tool - Chrome Extension

If you are using the Google Chrome browser you can install this .

This will allow you to quickly switch between debugging with the MiniProfiler, Trace viewer and normal mode.

Learn how Umbraco writes log files and how you can write to them.

Last updated

Was this helpful?

Was this helpful?

```
{
  "Serilog": {
    "MinimumLevel": {
      "Override": {
        "Microsoft.AspNetCore.Mvc": "Verbose"
      }
    }
  }
}
```

```
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.ViewEngines;
using Microsoft.Extensions.Logging;
using Umbraco.Cms.Core.Logging;
using Umbraco.Cms.Core.Web;
using Umbraco.Cms.Web.Common.Controllers;

namespace MyCustomUmbracoProject;

public class RootController : RenderController
{
    private readonly IProfiler _profiler;

    public RootController(
        IProfiler profiler,
        ILogger<RenderController> logger,
        ICompositeViewEngine compositeViewEngine,
        IUmbracoContextAccessor umbracoContextAccessor)
        : base(logger, compositeViewEngine, umbracoContextAccessor)
    {
        _profiler = profiler;
    }

    public override IActionResult Index()
    {
        // Perform a step
        using (_profiler.Step("Sleep"))
        {
            System.Threading.Thread.Sleep(1000);
        }

        return base.Index();
    }
}
```

### Logging | CMS

In Umbraco we use the underlying logging framework of .

Out of the box, we write a JSON log file that contains a more detailed logfile. This allows tools to perform searches and correlations on log patterns more efficiently.

The default location of this file is written to `umbraco/Logs`

and contains the Machine name, along with the date too:

`umbraco/Logs/UmbracoTraceLog.DELLBOOK.20210809.json`


Serilog is a logging framework that allows us to do structured logging or write log messages using the message template format. This allows us to have a more detailed log message, rather than the traditional text message in a long txt file.

```
2021-08-10 09:33:23,677 [P25776/D1/T22] INFO   Umbraco.Cms.Core.Services.Implement.ContentService - Document Home (id=1062) has been published.
```

Here is an example of the same log message represented as JSON. More information is available and allows you to search and filter logs based on these properties with an appropriate logging system.

```
{
  "@t":"2021-08-10T08:33:23.6778640Z",
  "@mt":"Document {ContentName} (id={ContentId}) has been published.",
  "ContentName":"Home",
  "ContentId":1062,
  "SourceContext":"Umbraco.Cms.Core.Services.Implement.ContentService",
  "ActionId":"7726d745-d502-4b2d-b55e-97731308041b",
  "ActionName":"Umbraco.Cms.Web.BackOffice.Controllers.ContentController.PostSave (Umbraco.Web.BackOffice)",
  "RequestId":"8000000c-0012-fb00-b63f-84710c7967bb",
  "RequestPath":"/umbraco/backoffice/umbracoapi/content/PostSave",
  "ProcessId":25776,
  "ProcessName":"iisexpress",
  "ThreadId":22,
  "AppDomainId":1,
  "AppDomainAppId":"2f4961977e5c252fa708f7d83915c269b53a620c",
  "MachineName":"DELLBOOK",
  "Log4NetLevel":"INFO ",
  "HttpRequestId":"318b6dd4-b127-4da3-8339-37701f4d1416",
  "HttpRequestNumber":4,
  "HttpSessionId":"0cea7395-ba29-e6c6-93ee-7c08a2fd7219"
}
```

To learn more about structured logging and message templates you can read more about it over on the website. Alternatively watch this video from the Serilog creator -

Umbraco writes log messages, but you are also able to use the Umbraco logger to write the log file as needed. This allows you to gain further insights and details about your implementation.

Here is an example of using the logger to write an Information message to the log. It will contain one property, **Name**, which will output the name variable that is passed into the method.

If you are Logging and using the MiniProfiler, you can inject `IProfilingLogger`

that has a reference to both ILogger and IProfiler.

The incorrect way to log the message would be use string interpolation or string concatenation such as

The bad examples above will write to the log file, but we will not get a separate property logged with the message. This means we can't find them by searching for log messages that use the message template `We are saying hello to {Name}`


Serilog uses levels as the primary means for assigning importance to log events. The levels in increasing order of importance are:

**Verbose**- tracing information and debugging minutiae; generally only switched on in unusual situations**Debug**- internal control flow and diagnostic state dumps to facilitate pinpointing of recognised problems**Information**- events of interest or that have relevance to outside observers; the default enabled minimum logging level**Warning**- indicators of possible issues or service/functionality degradation**Error**- indicating a failure within the application or connected system**Fatal**- critical errors causing complete failure of the application

Serilog can be configured and extended by using the .NET Core configuration such as the AppSetting.json files or environment variables. For more information, see the [Serilog config](/umbraco-cms/reference/configuration/serilog) article.

Serilog uses the concept of Sinks to output the log messages to different places. Umbraco ships with a custom sink configuration called UmbracoFile that uses the sink. This will save the logs to a rolling file on disk. You can disable this sink by setting its Enabled configuration flag to false, see [Serilog config](/umbraco-cms/reference/configuration/serilog) for more information.

Learn more about the [logviewer dashboard](/umbraco-cms/fundamentals/backoffice/logviewer) in the backoffice and how it can be extended.

This is a tool for viewing & querying JSON log files from disk in the same way as the built in log viewer dashboard.

Umbraco ships with the following Serilog projects, where you can find further information & details with the GitHub readme files as needed.

If you are interested in learning more then the following resources will beneficial:

This is

**free**for a single machine such as your own local development computer

Last updated

Was this helpful?

---

## Source Control | CMS

In this article you can learn more about how to effectively source control your Umbraco site.

When you are running your site on Umbraco Cloud, source control is a part of the experience. Have a look at the ['Technical overview of an Umbraco Cloud Environment' arrow-up-right](/umbraco-cloud/getting-started/environments)

If you are hosting your Umbraco implementation outside of Umbraco Cloud, it's generally considered good practice to set up source/version control for your site implementation files. This is especially a good idea when you are working with a team as it can help you track changes and manage conflicts with other developer's work.

So if you've made the decision to try to attempt to source/version control your Umbraco implementation work, perhaps setting up a - then a frequently asked question is:

**exclude**from my source control repository?

There are lots of different possible variations within your working environment that will affect the best way to set up version control. It depends on whether you are:

Working with a team of developers.

How your development environment is set up.

Source control repository.

And also how you intend to build and deploy your solution to your target production environment (build servers, Web Deploy or good old File Transfer Protocol (FTP), etc).


However, Umbraco ships with a `.gitignore`

file with a custom Umbraco section, which will make git ignore the files for you. The Umbraco specific section looks like this:

```
##
### Umbraco CMS
##

# JSON schema file for appsettings.json
appsettings-schema.json

# Packages created from the backoffice (package.xml/package.zip)
/umbraco/Data/CreatedPackages/

# Temp folder containing Examine indexes, MediaCache, etc.
/umbraco/Data/TEMP/

# SQLite database files
/umbraco/Data/*.sqlite.db
/umbraco/Data/*.sqlite.db-shm
/umbraco/Data/*.sqlite.db-wal

# Log files
/umbraco/Logs/

# Media files
/wwwroot/media/
```

For most projects, this gitignore will be enough, and this article will not be an exhaustive list of how to version control Umbraco in all possible scenarios.

However, we will go through the different files in order to give you an insight into the anatomy of an Umbraco website and therefore which parts to include in version control and which parts not to.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-afc7495f8a7a47840c9233fe0709722ae791ff73%252Ffile-structure-v10.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=eab16109&sv=2)

The main folder where the Umbraco CMS resides is the `/umbraco`

one inside your project.

Most of the files and folders within the Umbraco folder, is already added to the default gitignore file. As most of the Umbraco CMS core files are embedded, the `/umbraco`

folder contains primarily temporary files and log files, which are all added as Umbraco is installed.

We recommend that you follow the structure of the default gitignore file, and do not include any temporary files, log files or cache files to git.

Below are a set of general recommendations regarding the files within the `/umbraco`

folder.

`/umbraco/data/TEMP`

- This folder contains examine indexes, NuCache files, and so on, these are temporary and should not be committed.`/umbraco/Logs`

- Umbraco currently uses*Serilog*, and a file will be generated in this folder containing trace logs of your application, one JSON file for each day.`/umbraco/mediacache`

-*ImageSharp*ships with Umbraco and when an image is requested via the processor, for example, to be resized or cropped, a cached version of the transformed image will be stored in this folder. (The[Imaging settings section](/umbraco-cms/reference/configuration/imagingsettings)allows you to determine where this cache is stored)

The strategy here will depend a little on which mode ['Umbraco Models Builder'](/umbraco-cms/reference/templating/modelsbuilder) you have opted to work with.

**InMemoryAuto**(default), The models are generated in memory, no source control is required.**SourceCodeManual**and**SourceCodeAuto**, The models are generated in the`/umbraco/models`

folder of your project (or can be configured to be in a different folder or project), allowing you to track changes to the models in source/version control.

The Media section of Umbraco (unless configured otherwise) stores files in the `/wwwroot/media`

folder. These can be updated by editors, in the Umbraco backoffice, so generally speaking, you would not source control these files.

These are by default ignored by git.

The **App_Plugins** folder is the home for all third-party packages installed on your site.

Depending on how you installed the plugin it will affect how you choose to version control a particular third-party plugin:

Since plugins are installed via NuGet the installed files for individual plugins shouldn't need to be source controlled (and your deployment process should pull the packages implementation files from NuGet during the build and deployment process).

Each plugin could be different depending on its implementation and functionality. It may contain files that it would be useful to track via Source control, and also files that should be ignored: check with the plugin's supporting website/developer for more information.

**include**in my source control repository?

A lot depends on how you maintain the front-end build of your website, e.g. are you using CSS preprocessors such as Sassy Cascading Style Sheets (SCSS)/ Leaner CSS (LESS) etc - gulp/grunt tasks to combine and minify script resources.

But generally, you will need to source control all your website's static assets: JavaScript, CSS, Fonts, Page Furniture Images, etc.

Umbraco site templates/views can be edited via the Umbraco Backoffice. They also reside in the `/Views`

folder on disk. As these views/templates often include code, it can make a lot of sense to have their changes tracked under source/version control.

However, this can pose a problem if the templates are updated via the backoffice outside of source control on the production environment.

This is not an advisable approach since often this will cause breaking changes to your website.

You would need to manually merge these files before considering a deployment.

Umbraco Cloud is a good solution in these scenarios, as changes via the backoffice are tracked in a Git repository automatically.

Any supporting custom code for your application should be in version control, eg any of the following files

C# implementation,

Surface Controllers

API Controllers

ViewModels

Helpers / Extension Methods

Services etc.


Supporting class library projects,

Models generated by Modelsbuilder in SourceCodeManual or SourceCodeAuto mode.


Your site's `appsettings.json`

and `appsettings.Development.json`

files contain the configuration for your Umbraco site.

In general, it is recommended to add these to source control. When you do this, be sure that the file(s) doesn't contain any secrets, like API keys and connection strings. These can be added as needed, but omitted from any commits made to source control.

When you create and edit eg. Document Types, Media Types, and Data Types in the Umbraco Backoffice these values are stored in the Umbraco Database, making them difficult to source control in a 'file based' version control system.

There are a series of add-on packages that can help add source control to these structure changes:

- which can be configured to serialize these changes to files on disk, in a folder called /uSync - enabling you to source/version control these changes and synchronise them to other environments.

- an extension to uSync, for taking 'before' and 'after' snapshots of an Umbraco site, for managing a release of a 'set of changes' between environments.

- the on premise version of the package used by Umbraco Cloud.


Last updated

Was this helpful?

---

## Subscribing To Notifications | CMS

Subscribing to notifications allows you to listen to specific events and run custom code in response.

Create a Notification Handler

```
using Umbraco.Cms.Core.Events;
using Umbraco.Cms.Core.Notifications;
```


```
using Umbraco.Cms.Core.Events;
using Umbraco.Cms.Core.Notifications;

namespace MyProject;

public class LogWhenPublishedHandler : INotificationHandler<ContentPublishedNotification>
{
    // Here we will handle a notification.
}
```

Implement the Handle Method

Inject a Logger for Logging

Log the Content Publication

Register the Notification Handler

Publishing Content and Verifying Custom Log Messages

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c0724c980d027a5c586f574f68e125471c146411%252Flog-viewer-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f05d1422&sv=2)

Log Viewer

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b1d6432573655e77a0f60775fc2ed6d60027a8e8%252Flog-messages-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=59b6588d&sv=2)

Additional Notes

More Information

Last updated

Was this helpful?

---

## Service APIs | CMS

*Whenever you need to modify an entity that Umbraco stores in the database, there are service APIs available to help you. This means that you can create, update and delete any of the core Umbraco entities directly from your custom code.*

Services are typically defined using interfaces. Umbraco has them in the `Umbraco.Cms.Core.Services`

namespace, while the specific implementations can be found under the `Umbraco.Cms.Core.Services.Implement`

namespace. To use the service APIs you must first access them. Owing to the built-in dependency injection (DI) in ASP.NET Core, configured services are made available throughout Umbraco's codebase. This can be achieved via injecting the specific service you require - the service type or an interface.

If you are accessing Umbraco services inside your own controller class, you can add the Umbraco services that you need as constructor parameters. An instance of every service will be provided at runtime from the service container. By saving each one to a local field, you can make use of them within the scope of your class:

```
public class CustomController
{
    private readonly IContentService _contentService;


    public ContentController(IContentService contentService)
    {
        _contentService = contentService;
    }


    public ActionResult PerformAction()
    {
        var someContent = _contentService.GetById(1234);
    }
}
```

Inside a Razor View template, you can make use of a service injection into a view using the `@inject`

directive. It works similarly to adding a property to the view, and populating the property using DI:

If we wish to subscribe to notifications on one of the services, we'd create a Composer C# class, where you will add a custom `NotificationHandler`

. In this custom `NotificationHandler`

we would inject the service we need into the public constructor of the class and Umbraco's. The underlying dependency injection framework will do the rest.

In this example we will wire up to the ContentService 'Saved' event. We will create a new folder in the Media section whenever a new LandingPage is created in the content section to store associated media. Therefore we will need the MediaService available to create the new folder.

When you're creating your own class, in order to make use of the dependency injection framework, you need register the `ICustomNewsArticleService`

service with the type `CustomNewsArticleService`

. The `AddScoped()`

method registers the service with the lifetime of a single request.

There are different ways that you can achieve the same outcome:

Register directly into the **Program.cs** class.

Another approach is to create an extension method to `IUmbracoBuilder`

and add it to the startup pipeline.

When creating Umbraco packages you don't have access to the Startup class, therefore it's recommended to use a `IComposer`

instead. A Composer gives you access to the `IUmbracoBuilder`.


If you don't have access to the Startup class

Then your custom class eg. `CustomNewsArticleService`

can take advantage of the same injection to access services eg:

Last updated

Was this helpful?

---
