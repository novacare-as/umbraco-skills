# Implementation

## Contents

- [Composing | CMS](#composing-cms)
- [Controllers | CMS](#controllers-cms)
- [Custom Routing | CMS](#custom-routing-cms)
- [Data Persistence (CRUD) | CMS](#data-persistence-crud-cms)
- [Default Routing](#default-routing)
- [Integration Testing | CMS](#integration-testing-cms)
- [Learn how Umbraco works | CMS](#learn-how-umbraco-works-cms)
- [Nullable Reference Types | CMS](#nullable-reference-types-cms)
- [Services and Helpers | CMS](#services-and-helpers-cms)
- [Unit Testing | CMS](#unit-testing-cms)

---

## Composing | CMS

This article covers the topic of composing in Umbraco.

Overview

Example - Creating a Composer to listen for ContentSavingNotification

```
using System.Linq;
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.DependencyInjection;
using Umbraco.Cms.Core.Events;
using Umbraco.Cms.Core.Notifications;
using Umbraco.Extensions;

namespace My.Website;

public class SubscribeToContentServiceSavingComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.AddNotificationHandler<ContentSavingNotification, CustomContentSavingNotificationHandler>();
    }
}

public class CustomContentSavingNotificationHandler : INotificationHandler<ContentSavingNotification>
{
    public void Handle(ContentSavingNotification notification)
    {
        foreach (var content in notification.SavedEntities
            // Check if the content item type has a specific alias
            .Where(c => c.ContentType.Alias.InvariantEquals("MyContentType")))
        {
            // Do something if the content is using the MyContentType doctype
        }
    }
}
```

Example - Explicitly Registering a new custom OEmbedProvider

ComponentComposer

Collections

| Collection | Type | Registration |
|---|---|---|
| Actions | Lazy | Type scanned for `IAction` |
| BackOfficeAssets | Ordered | Explicit Registration - Empty by default |
| CacheRefreshers | Lazy | Type scanned for `ICacheRefresher` |
| Components | Ordered | Explicit Registration |
| ContentApps | Ordered | Package.manifest & Explicit Registration |
| ContentFinders | Ordered | Explicit Registration |
| ContentIndexHandlers | Lazy | Type scanned for `IContentIndexHandler` |
| Dashboards | Weighted | Package.manifest & Explicit Registration |
| DataEditors | Lazy | Type scanned for `IDataEditor` |
| DataValueReferenceFactories | Ordered | Explicit Registration - Empty by default |
| EditorValidators | Lazy | Type scanned for `IEditorValidator` |
| EmbedProviders | Ordered | Explicit Registration |
| FilterHandlers | Lazy | Type scanned for `IFilterHandler` |
| HealthChecks | Lazy | Type scanned for `HealthCheck` |
| HealthCheckNotificationMethods | Lazy | Type scanned for `IHealthCheckNotificationMethod` |
| ManifestFilters | Ordered | Explicit Registration - Empty by default |
| ManifestValueValidators | Set | Explicit Registration |
| MapDefinitions | Set | Explicit Registration |
| Mappers | Set | Explicit Registration |
| MediaUrlGenerators | Set | Explicit Registration |
| MediaUrlProviders | Ordered | Explicit Registration |
| NPocoMappers | Set | Explicit Registration |
| PackageMigrationPlans | Lazy | Type scanned for `PackageMigrationPlan` |
| PartialViewSnippets | Lazy | Explicit Registration. Reads .cshtml files from `Umbraco.Cms.Core.EmbeddedResources.Snippets` assembly |
| PropertyValueConverters | Ordered | Type scanned for `IPropertyValueConverter` |
| RuntimeModeValidators | Set | Explicit Registration |
| Sections | Ordered | Package.manifest & Explicit Registration |
| SelectorHandlers | Lazy | Type scanned for `ISelectorHandler` |
| SortHandlers | Lazy | Type scanned for `ISortHandler` |
| TourFilters | Base | Empty collection |
| Trees | Base | Type scanned. Must inherit `TreeControllerBase` & use `[Tree]` |
| UrlProviders | Ordered | Explicit Registration |
| UrlSegmentProviders | Ordered | Explicit Registration |
| Validators | Lazy | Explicit Registration |

Types of Collections

| Method | Notes | |
|---|---|---|
| Set | `SetCollectionBuilderBase` | The base class for collection builders that do not order their items explicitly. |
| Ordered | `OrderedCollectionBuilderBase` | The base class for collection builders that order their items explicitly. |
| Weighted | `WeightedCollectionBuilder` | The base class for collection builders that order their items by the `[Weight]` attribute. |
| Lazy | `LazyCollectionBuilderBase` | The base class for collection builders that resolve the types at the last moment, only when the collection is required. |

Example - Modifying Collections

Attributes

ComposeBefore and ComposeAfter

Weight

HideFromTypeFinder

DisableComposer & Disable

Runtime Levels

| Level | Description |
|---|---|
| `BootFailed` | The runtime has failed to boot and cannot run. |
| `Unknown` | The level is unknown. |
| `Boot` | The runtime is booting. |
| `Install` | The runtime has detected that Umbraco is not installed at all, ie. there is no database, and is currently installing Umbraco. |
| `Upgrade` | The runtime has detected an Umbraco install that needed to be upgraded and is currently upgrading Umbraco. |
| `Run` | The runtime has detected an up-to-date Umbraco install and is running. |

Example of using Ordered Collections and adding types explicitly

Example of using Lazy Collections with Type Scanning

Last updated

Was this helpful?

---

## Controllers | CMS

An Umbraco API Controller is an ASP.NET WebApi controller that is used for creating REST services.

Render MVC Controllers

Surface Controllers

Public API Controllers

Backoffice API Controllers

Last updated

Was this helpful?

An Umbraco API Controller is an ASP.NET WebApi controller that is used for creating REST services.

Umbraco contains different types of controllers to perform different tasks:

Render MVC Controllers

When you make a page request to the MVC application, a controller is responsible for returning the response to that request. The controller can perform one or more actions.

By default, all front-end requests to an Umbraco site are auto-routed via the *Index* action of a core Controller: `Umbraco.Cms.Web.Common.Controllers.RenderController`.


For details on using Render MVC Controllers, see the [Controller & Action Selection](/umbraco-cms/implementation/default-routing/controller-selection) article.

Surface Controllers

A SurfaceController is an MVC controller that interacts with the front-end rendering of an UmbracoPage. They can be used for rendering view components and for handling Form data submissions. SurfaceControllers are auto-routed which means you don't have to add/create your own routes for these controllers to work.

All implementations of Surface Controllers inherit from the base class: `Umbraco.Cms.Web.Website.Controllers.SurfaceController`.


For details on using Surface Controllers, see the [Surface Controllers](/umbraco-cms/reference/routing/surface-controllers) article.

Public API Controllers

A public API Controller is an ASP.NET Core API controller that is used for creating publicly available REST services. For details on implementing public API Controllers, see the [Umbraco API Controllers](/umbraco-cms/reference/routing/umbraco-api-controllers) article.

Backoffice API Controllers

For a comprehensive guide to writing APIs for the Management API, read the [Creating a Backoffice API article](/umbraco-cms/tutorials/creating-a-backoffice-api).

The Umbraco Backoffice API is also known as the Management API. Thus, a Backoffice API Controller is often referred to as a Management API Controller.

Umbraco HQ offers a training course covering everything you need to know about working with MVC in an Umbraco context. The course targets anyone who's interested in learning how to utilize Umbraco´s built-in features and basic functionality with standard MVC.

to learn more about the topics covered and how it can enhance your Umbraco development skills.

Last updated

Was this helpful?

Was this helpful?

---

## Custom Routing | CMS

Learn everything you need to know about custom routing in Umbraco CMS.

Customizing the inbound pipeline

IContentFinder

Last Chance IContentFinder

```
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.DependencyInjection;
using Umbraco.Extensions;

namespace My.Website;

public class UpdateContentFindersComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        //set the last chance content finder
        builder.SetContentLastChanceFinder<My404ContentFinder>();
    }
}
```

Custom MVC routes

RoutingRequestNotification

Related articles

Last updated

Was this helpful?

### Adding a hub with SignalR and Umbraco | CMS

Umbraco ships with signalR installed, find out how to add your own hub(s) to the existing setup

Create a hub and its interface

```
public interface ITestHubEvents
{
    // Define the events the clients can listen to
    public Task Pong();
}
```

```
using Microsoft.AspNetCore.SignalR;

public class TestHub : Hub<ITestHubEvents>
{
    // when a client sends us a ping
    public async Task Ping()
    {
        // we trigger the pong event on all clients
        await Clients.All.Pong();
    }
}
```

Add the routing to the Umbraco Composer

Add the route in appsettings.json file

Test the setup

Last updated

Was this helpful?

---

## Data Persistence (CRUD) | CMS

Dependency injection

Constructors in classes

```
    public class MyClass
    {
        private readonly IContentService _contentService;

        public MyClass(IContentService contentService)
        {
            _contentService = contentService;
        }
    }
```

Constructors in views

```
    @inject IContentService ContentService
```

Services

Last updated

Was this helpful?

*The Umbraco Services layer is used to query and manipulate Umbraco stored in the database*.

Dependency injection

All services are available using their interfaces in the dependency injection container. ASP.NET Core supports dependency injection in almost every scenario.

Constructors in classes

```
    public class MyClass
    {
        private readonly IContentService _contentService;

        public MyClass(IContentService contentService)
        {
            _contentService = contentService;
        }
    }
```

Constructors in views

```
    @inject IContentService ContentService
```

Services

There is a service for each type of data in Umbraco.

[See here For a full list of services available (external) arrow-up-right](https://apidocs.umbraco.com/v17/csharp/api/Umbraco.Cms.Core.Services.html)

Last updated

Was this helpful?

Was this helpful?

---

## Default Routing

### Contents

- [Controller & Action Selection | CMS](#controller-action-selection-cms)
- [Execute Request | CMS](#execute-request-cms)
- [Request Pipeline | CMS](#request-pipeline-cms)

---

### Controller & Action Selection | CMS

Default Controller Action

```
using Umbraco.Cms.Web.Common.Controllers;
using Microsoft.Extensions.Logging;
using Microsoft.AspNetCore.Mvc.ViewEngines;
using Umbraco.Cms.Core.Web;
using Microsoft.AspNetCore.Mvc;

namespace UmbracoProject.Controller;

public class HomePageController : RenderController
{

    public HomePageController(ILogger<RenderController> logger, ICompositeViewEngine compositeViewEngine, IUmbracoContextAccessor umbracoContextAccessor)
    : base(logger, compositeViewEngine, umbracoContextAccessor)
    {
    }
    public override IActionResult Index()
    {
        return CurrentTemplate(CurrentPage);
    }

    public IActionResult HomePage()
    {
        return CurrentTemplate(CurrentPage);
    }
}
```

Change the Default Controllers

Custom Controller Selection

Last updated

Was this helpful?

When you make a page request to the MVC application, a controller is responsible for returning the response to that request. The controller can perform one or more actions. The controller action can return different types of action results based on the request.

Default Controller Action

By default, Umbraco will execute every request via it's built-in default controller: `Umbraco.Cms.Web.Common.Controllers.RenderController`

. Umbraco site automatically routes all the front-end requests via the `Index`

action of the `RenderController`.


```
using Umbraco.Cms.Web.Common.Controllers;
using Microsoft.Extensions.Logging;
using Microsoft.AspNetCore.Mvc.ViewEngines;
using Umbraco.Cms.Core.Web;
using Microsoft.AspNetCore.Mvc;

namespace UmbracoProject.Controller;

public class HomePageController : RenderController
{

    public HomePageController(ILogger<RenderController> logger, ICompositeViewEngine compositeViewEngine, IUmbracoContextAccessor umbracoContextAccessor)
    : base(logger, compositeViewEngine, umbracoContextAccessor)
    {
    }
    public override IActionResult Index()
    {
        return CurrentTemplate(CurrentPage);
    }

    public IActionResult HomePage()
    {
        return CurrentTemplate(CurrentPage);
    }
}
```

Change the Default Controllers

It is possible to implement a custom Controller to replace the default implementation to give complete control during the Umbraco request pipeline execution. You can configure Umbraco to use your implementation in a class. For example:

Ensure that the controller inherits from the base controller `Umbraco.Cms.Web.Common.Controllers.RenderController`

. You can override the `Index`

method to perform any customizations of your choice.

Custom Controller Selection

You can create Custom controllers for different Document Types and Templates. This is termed 'Hijacking Umbraco Routes'. For details on how this process works, see the [Custom MVC Controllers (Umbraco Route Hijacking)](/umbraco-cms/reference/routing/custom-controllers) article.

Last updated

Was this helpful?

Was this helpful?

MyRenderController.cs

```
using Microsoft.AspNetCore.Mvc.ViewEngines;
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.Web;
using Umbraco.Cms.Web.Common.Controllers;
using Umbraco.Cms.Web.Website.Controllers;

namespace YourProjectNamespace;

public class MyRenderController : RenderController
{
 public MyRenderController(
  ILogger<MyRenderController> logger,
  ICompositeViewEngine compositeViewEngine,
  IUmbracoContextAccessor umbracoContextAccessor)
  : base(logger, compositeViewEngine, umbracoContextAccessor)
 {
 }

 public override IActionResult Index() => Ok("MyRenderController Index method hit with CurrentPage.Name set to: " + CurrentPage?.Name);
}

public class MyComposer : IComposer
{
 public void Compose(IUmbracoBuilder builder)
 {
  builder.Services.Configure<UmbracoRenderingDefaultsOptions>(renderOptions
   => renderOptions.DefaultControllerType = typeof(MyRenderController));
 }
}
```

---

### Execute Request | CMS

*During the Umbraco request execution, an MVC Action is called which executes a Razor view to render content to the end-user*,

Whenever a content item is rendered on the front-end, it is based on a model of type `IPublishedContent`

. This model contains all of the information about the content item associated with the current request.

If you are working in a custom MVC Controller's action, a model of type `ContentModel`

will be provided in the Action's method parameters. This model contains an instance of `IPublishedContent`

which you can use.

When you are working in a View of type `UmbracoViewPage`

(which is the default view type), the Model provided to that view will be `IPublishedContent`

. For example, to render the current content model's name you could do:

```
@Model.Name
```

All Umbraco view page types inherit from `UmbracoViewPage<TModel>`

. A neat trick is that if you want your view Model to be `IPublishedContent`

you can change your view type to `UmbracoViewPage`

and the view will still render without issue even though the controller is passing it a model of type ContentModel.

IPublishedContent is a strongly typed model used for all published content, media, and members. It is used to render content in your views for your website.

UmbracoHelper is the unified way to work with published content/media on your website. Whether you are using MVC or WebForms you will be able to use UmbracoHelper to query/traverse Umbraco published data.

IMemberManager is an user manager interface for accessing member data in the form of IPublishedContent. IMemberManager has a variety of methods that are useful in views, controllers, and webforms classes.

Last updated

Was this helpful?

---

### Request Pipeline | CMS

Umbraco's request pipeline is the process of building up a URL, resolving the requests, and returning correct content.

The inbound process is triggered by `UmbracoRouteValueTransformer`

and then handled with the Published router. The [Published Content Request Preparation](/umbraco-cms/reference/routing/request-pipeline/published-content-request-preparation) process kicks in and creates a `PublishedRequestBuilder`

which will be used to create a `PublishedContentRequest`.


What it does:

It ensures Umbraco is ready, and the request is a document request.

Ensures there's content in the published cache, if there isn't it routes to the

`RenderNoContentController`

which displays the no content page you see when running a fresh install.Creates a published request builder.

Routes the request with the request builder using the

`PublishedRouter.RouteRequestAsync(…)`

.This will handle redirects, find domain, template, published content and so on.

Build the final

`IPublishedRequest`.


Sets the routed request in the Umbraco context, so it will be available to the controller.

Create the route values with the

`UmbracoRouteValuesFactory`

.This is what routes your request to the correct controller and action, and allows you to hijack routes.


Set the route values to the http context.

Handles posted form data.

Returns the route values to netcore so it routes your request correctly.


When finding published content the will first check if the already has content, if it doesn't the content finders will kick in. For more information, see the [Find published content](/umbraco-cms/reference/routing/request-pipeline/published-content-request-preparation#find-published-content) section in the [Published Content Request Preparation](/umbraco-cms/reference/routing/request-pipeline/published-content-request-preparation) article.

This information is also used during the [Controller & Action selection](/umbraco-cms/implementation/default-routing/controller-selection) process.

Last updated

Was this helpful?

---

---

## Integration Testing | CMS

A guide to getting started with integration testing in Umbraco

These examples are for Umbraco 14. They use as the testing framework. Leveraging providing base classes.

The Umbraco.Tests.Integration project uses version `3.14.0`

of the NUnit NuGet package. It is essential to use this version to ensure compatibility. You can check the current package versions used by the `Umbraco.Tests.Integration`

project .

First you have to create a new UnitTest project based on NUnit and install the package into the project.

```
//Create project
dotnet new nunit
//Install Umbraco.Tests.Integration package
dotnet add package Umbraco.Cms.Tests.Integration
```

After the project is created and the package is added we have to create a JSON file, named `appsettings.Tests.Local.json`

and a `GlobalSetup`

class.

The package already created an `appsettings.Tests.json`

file. For both files make sure to go to "properties" and set "Copy to output directory" to "always" or "copy if newer".

The GlobalSetup is necessary to call the `GlobalSetupTeardown`

class present in the package. This class makes sure that configuration is read and everything is setup as needed. Here is a sample that can be used:

```
[SetUpFixture]
public class CustomGlobalSetupTeardown
{
    private static GlobalSetupTeardown _setupTearDown;

    [OneTimeSetUp]
    public void SetUp()
    {
        _setupTearDown = new GlobalSetupTeardown();
        _setupTearDown.SetUp();
    }

    [OneTimeTearDown]
    public void TearDown()
    {
        _setupTearDown.TearDown();
    }
}
```

The class should not have a namespace.

To create a test you have to create a new class in your project. This class has to be derived from `UmbracoIntegrationTest`

. This gives you access to some helper methods that you can use.

Second is the `[UmbracoTest]`

- attribute that has to be set on the class. This attribute is responsible to set which type of database setup you want to use in your test class.

The available options are:

None

NewEmptyPerFixture

NewEmptyPerTest

NewSchemaPerFixture

NewSchemaPerTest


Basic sample:

Start by making a NotificationHandler, this example will be of one canceling overwrites on content named "Root", so if you have some content named "Root" published, you cannot change it.

Then we can make an integration test, we do have to register our notification in the test like you would do with a composer, we can do this by overriding the `CustomTestSetupMethod`

and adding the notification. After this, we can build our ContentType and Content with their respective builders. When we are saving both the ContentType & Content, we need the services to do so, so we use the `GetRequiredService<IService>`

method that can get the services we need. We can then use `Assert.Multiple()`

to do multiple asserts.

So one of the awesome things about integration tests, is that you can set up a site, download the package for it, and we can run this state for every test. This means that you do not have to go through and set up your tests with data like we do in the above example with the builder pattern.

To start with we decorate our class with the `[UmbracoTest]`

attribute with your preferred database setup and we again derive from `UmbracoIntegrationTest`

. Then what you wanna do is set up your Umbraco site, go to the packages section and create your own package. Download the package and place the XML file next to your testing class. You want to have the build action of that XML file to be `EmbeddedResource`

and you can set that again in the file's "properties".

Now we're almost ready to start testing! The last thing we wanna do is have a SetUp method to install the package on your site.

Now you're all set to start testing with your own site! Let's try and see how that would look! Here's an example test, where we test that content is deleted, if you delete the Document Types, as you can see, this time we do not have to use builder patterns to set up our site!

Sometimes we want to test from a controller action and down to the database. In this case, we use the built-in concept of a test server. All you need to do is to use the base class `UmbracoTestServerTestBase`

. Let’s take an example:

In this example you have to note three things:

You still need the

`CustomGlobalSetupTeardown`

class.Use the

`GetManagementApiUrl`

to get the URL of an Action and ensure all services use this URL information when requested.The

`Client`

is a standard`HttpClient`

, but the base URL points to the test server that is set up for each test.

You can still use `GetRequiredService`

to get the services required to seed data.

Keep in mind that integration tests require a lot of setup before the test executes. So execution time will be many times longer compared to a unit test.

Last updated

Was this helpful?

---

## Learn how Umbraco works | CMS

Get to know the Umbraco codebase.

Last updated

Was this helpful?

Get to know the Umbraco codebase.

Developing an application requires knowledge about the tool you are working with. This section will give you an introduction to the underlying structure of Umbraco CMS.

**Routing**

The process from front-end user requests to content delivery.

**Custom routing**

Learn how to work with custom URLs and custom MVC routes.

**Controllers**

Everything you need to know about the different types of controllers.

**Data persistence**

Learn how to create, read, update, and delete data in the Umbraco database.

**Composing**

Customize the behavior of an Umbraco application at 'start up'.

**Services and Helpers**

Learn how to use the core Services and Helpers when extending Umbraco.

Test your application

This section also includes documentation on different ways to run tests on your code and implementations.

Last updated

Was this helpful?

Was this helpful?

---

## Nullable Reference Types | CMS

In this article we describe what Nullable reference types is.

Last updated

Was this helpful?

In this article we describe what Nullable reference types is.

From Umbraco version 10, Nullable Reference Types is enabled by default in Umbraco.

Nullable reference types is a group of features introduced in C# 8.0. These features can be used to minimize the likelihood that your code causes the runtime to throw `System.NullReferenceException`.


Nullable reference types includes three features that help you avoid these exceptions, including the ability to explicitly mark a reference type as nullable:

Improved static flow analysis that determines if a variable may be null before dereferencing it.

Attributes that annotate APIs so that the flow analysis determines null-state.

Variable annotations that developers use to explicitly declare the intended null-state for a variable.


To learn more about Nullable Reference Types, refer to the

Last updated

Was this helpful?

Was this helpful?

---

## Services and Helpers | CMS

Umbraco has a range of 'Core' Services and Helpers that act as a 'gateway' to Umbraco data and functionality to use when extending or implementing an Umbraco site.

Umbraco has a range of 'Core' Services and Helpers that act as a 'gateway' to Umbraco data and functionality to use when extending or implementing an Umbraco site.

The general rule of thumb is that management Services provide access to allow the modification of Umbraco data (and therefore aren't optimised for displaying data). Helpers on the other hand provide access to readonly data with performance of displaying data taken into consideration.

Although there is a management Service named the `IContentService`

- only use this to modify content - do not use the `IContentService`

in a View/Template to pull back data to display, this will make requests to the database and be slow - here instead inject the `IPublishedContentQueryAccessor`

interface and get the `IPublishedContentQuery`

that operate against a cache of published content items, and are significantly quicker.

The management Services and Helpers are all registered with Umbraco's underlying DI framework. This article aims to show examples of gaining access to utilise these resources in multiple different scenarios. There are subtle differences to be aware of depending on what part of Umbraco is being extended.

This article will also suggest how to follow a similar pattern to encapsulate custom 'site specific' implementation logic, in similar services and helpers, registered with the underlying DI contain. This would be to avoid repetition and promote consistency and readability within an Umbraco site solution.

Inside a view/template or partial view, access is also provided by the DI framework, by using the `@inject`

keyword.

```
@inherits Umbraco.Cms.Web.Common.Views.UmbracoViewPage<ContentModels.Root>
@using ContentModels = Umbraco.Cms.Web.Common.PublishedModels;
@using Umbraco.Cms.Core.Services;
@using Umbraco.Cms.Web.Common;

@* it is really 'unlikely' to need to use a management Service in a view: *@
@inject IRelationService RelationService
@inject UmbracoHelper Umbraco

@{
    Layout = null;

    // retrieve an item from Umbraco's published cache with id 123
    IPublishedContent publishedContentItem = Umbraco.Content(123);
}
```

Inside a [custom Controller](/umbraco-cms/reference/routing/custom-controllers) access is provided to Services via the `Services`

property ([ServiceContext](/umbraco-cms/reference/management)) and the `UmbracoHelper`

via the `Umbraco`

property ([UmbracoHelper](/umbraco-cms/reference/querying/umbracohelper)).

Controllers and Views can access an `IUmbracoContext`

by injecting the `IUmbracoContextAccessor`

, however this is not always the case 'everywhere in Umbraco', for example common extension points: Components,ContentFinders or Custom C# Classes.

IUmbracoContext, UmbracoHelper, IPublishedContentQuery - are all based on an HttpRequest - their lifetime is controlled by an HttpRequest. So if you are not operating within an actual request, you cannot inject these parameters and if you try to ... Umbraco will report an error on startup.

It's possible to inject management Services that do not rely on the `UmbracoContext`

into the constructor of a component. This example shows injecting the `IMediaService`

in a Notification Handler to create a corresponding Media Folder for every 'landing page' that is saved in the Content Section, by subscribing to the 'Content Saved' notification.

See documentation on [Composing](/umbraco-cms/implementation/composing) for further examples and information on Components and Composition.

Trying to inject types that are based on an Http Request such as `UmbracoHelper`

or `IPublishedContentQuery`

into classes that are not based on an Http Request will trigger an error. However, there is a technique that allows the querying of the Umbraco Published Content, using the `UmbracoContextFactory`

and calling `EnsureUmbracoContext()`.


In this example, when a page is unpublished, instead of a 404 occurring for the content when the url is requested in the future, we might want to serve a 410 'page gone' status code instead. We handle the Unpublishing notification of the ContentService, access the Published Content Cache, determine it's 'published url' and then store for later use in any 'serving the 410' mechanism.

An [IContentFinder](/umbraco-cms/reference/routing/request-pipeline/icontentfinder) could be placed in the ContentFinder ordered collection, right before a 404 is served. This could be done to lookup the incoming request against the stored location of 410 urls, and serve the 410 status request code if a match is found for the previously published item.

When fetching multiple content items by ID, using `UmbracoContext.Content`

is limited because it only allows retrieving one item at a time. To query multiple items efficiently, you can use `IPublishedContentQuery`

. For more details, see the [IPublishedContentQuery](/umbraco-cms/reference/querying/ipublishedcontentquery) article.

Inside a ContentFinder access to the content cache is possible by injecting `IUmbracoContextAccessor`

into the constructor and provided via the PublishedRequest object:

And inside an `IPublishedUrlProvider`

injection of `IUmbracoContextAccessor`

into the constructor is also possible.

It is still possible to inject services into IContentFinder's. IContentFinders are singletons, but the example is showing you do not 'need to' in order to access the Published Content Cache.

When implementing an Umbraco site, it is likely to have to execute similar code that accesses or operates on Umbraco data, in multiple places, perhaps using the core management Services or Umbraco Helpers.

For example; Getting a list of the latest News Articles, or building a link to the site's News Section or Contact Us page. Repeating this kind of logic in multiple places, Views, Partial Views / Controllers etc, is possible, but it's generally considered good practice to consolidate this logic into a single place.

One option is to add 'Extension Methods' to the `UmbracoHelper`

class or `IPublishedContentQuery`

interface.

Anywhere there is reference to the `UmbracoHelper`

or `IPublishedContentQuery`

and a reference is added to the namespace the extension belongs to, it is possible to call the method by writing `_publishedContentQuery.GetNewsSection()`.


Another option, is to make use of the underlying DI framework, and create custom Services and Helpers, that in turn can have the 'core' management Services and Umbraco Helpers injected into them.

This approach enables the grouping together of similar methods within a suitably named service, and promotes the possibility of testing this custom logic outside of Controllers and Views.

Depending on where the custom service will be utilised, we will dictate the best practice approach to accessing the 'Published Content Cache'. If it is 100% guaranteed that the service will only be called from a place with an UmbracoContext, eg a controller or view, then it is safe to inject `IPublishedContentQuery`

etc for simplicity. However if the custom service is called in a location without UmbracoContext (eg an notification handler) it will fail. Therefore the approach of accessing the Published Content Cache via injecting IUmbracoContextFactory and calling `EnsureUmbracoContext()`

will provide consistency across any custom services no matter where they are utilised.

In this example, we create a custom service, that's responsible for finding key pages within a site, eg the News Section or the Contact Us page. These methods will commonly be called in different places throughout the site, and it's great to encapsulate the logic to retrieve them in a single place - we'll call this service `SiteService`.


Create an interface to define the service:

Create the concrete service class that implements the interface:

Register the custom service with Umbraco's underlying DI container using an `IComposer`:


**"Transient"** services can be injected into "Transient" and below ⤵. (i.e. "Transient" services can be injected anywhere)

"Transient" means that anytime this type is needed a brand new instance of this type will be created.


**"Scope"** services can be injected into "Request"/"Scope" based lifetimes only

"Scope" means that a single instance of this type will be created for the duration of the current HttpRequest. The instance will be disposed of at the end of the current HttpRequest.


**"Singleton"** services can be injected into "Singletons" and below ⤵.

"Singleton" means that only a single instance of this type will ever be created for the lifetime of the application.


**1 - The service will ONLY be used during a request like in a Controller or View**

You can avoid repeating common implementation logic in multiple controllers and views. This is done by consolidating these implementations into a custom service. If you are very familiar with IPublishedContentQuery injecting this into the custom service is straight forward, but the caveat is you can only use this service in a controller/view.

For example, locating the 'special' pages in the site using the familiar syntax of the `IPublishedContentQuery`:


**2 - The service can be used within or outside of a web request**

In order to replicate `ContentAtRoot`

outside of a web request, you can inject `IDocumentNavigationQueryService`

(or `IMediaNavigationQueryService`

for media). This service provides access to an in-memory store of unique keys for all root nodes within the Umbraco Content or Media trees.

This replaces the `PublishedContentCache`

(or PublishedMediaCache) `GetAtRoot()`

method.

The second approach can seem 'different' or more complex at first glance, but it is the syntax and method names that are slightly different... it enables the registering of the service in Singleton Scope, and its use outside of controllers and views.

Occasionally, you may face a situation where Umbraco fails to boot, due to a circular dependency on `IUmbracoContextFactory`

. This can happen if your service interacts with third party code that also depends on an `IUmbracoContextFactory`

instance (e.g. an Umbraco package).

See the [Circular Dependencies](/umbraco-cms/implementation/services/circular-dependencies) article for an example on how to get around this.

**Aside: What is the IUmbracoContextAccessor then?**

The `IUmbracoContextFactory`

will obtain an `UmbracoContext`

by first checking to see if one exists on the current thread using the `IUmbracoContextAccessor`

. This is a singleton that can be injected anywhere and whose function is to provide access to the current UmbracoContext. On a 'non request' thread the IUmbracoContextAccessor's TryGetUmbracoContext method will return false and the IUmbracoContextFactory will create a new instance of the UmbracoContext.

If you need to know whether the UmbracoContext has been obtained from an existing thread, or whether it has been freshly created, you can 'inject' `IUmbracoContextAccessor`

yourself. This will check if the UmbracoContext is null using the TryGetUmbracoContext method, indicating whether you are in a 'non request' thread or not. You will still need to inject and use an IUmbracoContextFactory if you subsequently want to obtain an UmbracoContext in a non-request thread.

NB: With the `IUmbracoContextAccessor`

and `IUmbracoContextFactory`

you should NEVER have to inject the UmbracoContext itself directly into any of your constructors.

Because we've registered the SiteService with Umbraco's underlying DI framework we can inject the service into our controller's constructor, in the same way as 'core' Services and Helpers.

You can generate this ctor in Visual Studio by using either ctrl + . or alt + enter when your cursor is on the base class:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-edf5db7a78ced90e6efdc453d40ed484a5c5c573%252Fvs-di-constructor-generation-tip.gif%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8a464ac3&sv=2)

If strictly following the paradigm of MVC, calling custom Services from Views might feel like an anti-pattern. However there isn't necessarily one single 'best practice' approach to working with Umbraco. A lot depends on circumstance, expertise and pragmatism. Allowing Umbraco to handle the flow of incoming requests to a particular page + template, and writing implementation logic in Views/Templates, is still a very common approach. There are circumstances, where the custom implementation logic shared is very 'View' specific. Custom logic for constructing 'Alternative Text' for images or different crop urls for img srcsets can be neatly handled in a custom Helper/Service without having to create a hijacked MVC route for the request and build a complex ViewModel. Custom Services called from Views, can help separate the concerns, even if the 'plumbing' isn't pure MVC.

To access the service directly from the view you would need to use the Razor `@inject`

keyword to get a reference to the concrete implementation of the service registered with DI:

Sometimes you might want to request, for example "/sitemap.xml" from your server. Since this has a file extension it will be treated as a client-side request and will not work. You can configure routes to be handled as server-side requests in your program.cs.

**For a single route:**

**For multiple routes:**

Last updated

Was this helpful?

### Circular Dependencies | CMS

```
public class SiteService : ISiteService
{
    private readonly Lazy<IUmbracoContextFactory> _umbracoContextFactory;
    public SiteService(Lazy<IUmbracoContextFactory> umbracoContextFactory)
    {
        _umbracoContextFactory = umbracoContextFactory;
    }
     public IPublishedContent GetNewsSection()
    {
         using (UmbracoContextReference umbracoContextReference = _umbracoContextFactory.Value.EnsureUmbracoContext())
         {
             // Do your thing
         }
    }
}
```

Last updated

Was this helpful?

In some cases you might experience that a circular dependency is preventing your Umbraco installing from starting up.

An example of this, could be a circular dependency on `IUmbracoContextFactory`

, which would happen if your service interacts with third party code that also depends on an `IUmbracoContextFactory`

instance.

In this situation, you can request a lazy version of the dependency so it won't evaluate during boot, and would only be evaluated when accessed:

```
public class SiteService : ISiteService
{
    private readonly Lazy<IUmbracoContextFactory> _umbracoContextFactory;
    public SiteService(Lazy<IUmbracoContextFactory> umbracoContextFactory)
    {
        _umbracoContextFactory = umbracoContextFactory;
    }
     public IPublishedContent GetNewsSection()
    {
         using (UmbracoContextReference umbracoContextReference = _umbracoContextFactory.Value.EnsureUmbracoContext())
         {
             // Do your thing
         }
    }
}
```

Last updated

Was this helpful?

Was this helpful?

---

## Unit Testing | CMS

A guide to getting started with unit testing in Umbraco

Mocking

Testing a ContentModel

```
public class PageViewModel : ContentModel
{
    public PageViewModel(IPublishedContent content) : base(content) { }

    public string Heading => (string)this.Content.GetProperty(nameof(Heading)).GetValue();
}

public class PageViewModelTests
{
    [Test, AutoData]
    public void Given_PublishedContent_When_GetHeading_Then_ReturnPageViewModelWithHeading(string value, Mock<IPublishedContent> content)
    {
        SetupPropertyValue(content, nameof(PageViewModel.Heading), value);

        var viewModel = new PageViewModel(content.Object);

        Assert.AreEqual(value, viewModel.Heading);
    }

    public void SetupPropertyValue(Mock<IPublishedContent> content, string propertyAlias, string propertyValue, string culture = null)
    {
        var property = new Mock<IPublishedProperty>();
        property.Setup(x => x.Alias).Returns(nameof(PageViewModel.Heading));
        property.Setup(x => x.GetValue(culture, null)).Returns(propertyValue);
        content.Setup(x => x.GetProperty(propertyAlias)).Returns(property.Object);
    }
}
```

Testing a RenderController

Testing a SurfaceController

Testing a Controller

Testing ICultureDictionary using the UmbracoHelper

Last updated

Was this helpful?

---
