# Reference — Part 1: Contents → Common Pitfalls & Anti-Patterns | CMS

## Contents

- [Adding Additional Languages | CMS](#adding-additional-languages-cms)
- [API Documentation | CMS](#api-documentation-cms)
- [API versioning and OpenAPI | CMS](#api-versioning-and-openapi-cms)
- [Cache](#cache)
- [Common Pitfalls & Anti-Patterns | CMS](#common-pitfalls-anti-patterns-cms)
- [Configuration](#configuration)
- [Content Delivery Api](#content-delivery-api)
- [Content Type Filters | CMS](#content-type-filters-cms)
- [Custom Swagger API | CMS](#custom-swagger-api-cms)
- [Database Availability Checks | CMS](#database-availability-checks-cms)
- [Debugging with SourceLink | CMS](#debugging-with-sourcelink-cms)
- [Distributed Locks | CMS](#distributed-locks-cms)
- [Dive into the code | CMS](#dive-into-the-code-cms)
- [JSON Serialization | CMS](#json-serialization-cms)
- [Language Variation | CMS](#language-variation-cms)
- [Management Api](#management-api)
- [Management | CMS](#management-cms)
- [UmbracoMapper | CMS](#umbracomapper-cms)
- [Markdown to HTML Conversion | CMS](#markdown-to-html-conversion-cms)
- [Notifications](#notifications)
- [Plugins](#plugins)
- [Property Editor UIs | CMS](#property-editor-uis-cms)
- [Querying](#querying)
- [Response Caching | CMS](#response-caching-cms)
- [Routing](#routing)
- [Scheduling | CMS](#scheduling-cms)
- [Searching | CMS](#searching-cms)
- [Security](#security)
- [Service Registration | CMS](#service-registration-cms)
- [Templating](#templating)
- [Umbraco Flavored Markdown | CMS](#umbraco-flavored-markdown-cms)
- [Inversion of Control / Dependency injection | CMS](#inversion-of-control-dependency-injection-cms)
- [Webhooks | CMS](#webhooks-cms)
- [Website Output Caching | CMS](#website-output-caching-cms)

---


## Adding Additional Languages | CMS

Learn how to make additional language cultures available in Umbraco when they do not appear in the backoffice language dropdown.

When adding a new language in the Umbraco backoffice, you may find that a language culture you need is not listed in the dropdown. This article explains why some cultures are missing and how to make them available.

From version 9 onward, Umbraco runs on .NET (Core) and uses [app-local ICU (International Components for Unicode) arrow-up-right](https://learn.microsoft.com/en-us/dotnet/core/extensions/globalization-icu#app-local-icu)

The app-local ICU data contains fewer culture codes than the Windows NLS (National Language Support) data that .NET Framework used. If you are migrating from Umbraco 8 or earlier, you may notice that some cultures you previously used are no longer listed.

In addition, Umbraco's default `IIsoCodeValidator`

filters out cultures flagged as `UserCustomCulture`

. This ensures the available languages are consistent across all platforms and hosting environments. Under app-local ICU, some valid BCP (Best Current Practice) 47 locale codes (such as `zh-HK`

) are classified as custom cultures even though they are standard cultures.

These two factors combined mean certain languages will not appear in the backoffice language dropdown by default.

You can make additional cultures available by replacing Umbraco's default `IIsoCodeValidator`

and `ICultureService`

implementations using a [composer](/umbraco-cms/implementation/composing).

The custom `IIsoCodeValidator`

allows the additional ISO codes to pass validation. The custom `ICultureService`

ensures those cultures appear in the backoffice dropdown list.

The `IIsoCodeValidator`

is used when saving or updating language ISO codes and backoffice user cultures. Changes to the validator affect all culture validation in Umbraco, not only the language selection dropdown.

Add the following code to your project, updating the `_additionalIsoCodes`

array with the culture codes you need:

```
using System.Globalization;
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.Services;

namespace MySite.Composers;

/// <summary>
/// Replaces the default <see cref="IIsoCodeValidator"/> and <see cref="ICultureService"/>
/// to allow specific cultures that are valid BCP 47 locales but get incorrectly flagged as
/// <see cref="CultureTypes.UserCustomCulture"/> on .NET with app-local ICU, or are not
/// enumerated by <see cref="CultureInfo.GetCultures"/> despite being resolvable.
/// </summary>
public class AllowAdditionalCulturesComposer : IComposer
{
    private static readonly string[] _additionalIsoCodes = ["zh-HK"];

    public void Compose(IUmbracoBuilder builder)
    {
        builder.Services.AddUnique<IIsoCodeValidator>(
            new AllowAdditionalCulturesIsoCodeValidator(_additionalIsoCodes));
        builder.Services.AddUnique<ICultureService>(provider =>
            new AllowAdditionalCulturesCultureService(
                provider.GetRequiredService<IIsoCodeValidator>(),
                _additionalIsoCodes));
    }
}

internal class AllowAdditionalCulturesIsoCodeValidator : IIsoCodeValidator
{
    private readonly IsoCodeValidator _inner = new();
    private readonly HashSet<string> _additionalIsoCodes;

    public AllowAdditionalCulturesIsoCodeValidator(params string[] additionalIsoCodes)
        => _additionalIsoCodes = new HashSet<string>(additionalIsoCodes, StringComparer.OrdinalIgnoreCase);

    public bool IsValid(CultureInfo culture)
        => _inner.IsValid(culture) || _additionalIsoCodes.Contains(culture.Name);
}

internal class AllowAdditionalCulturesCultureService : ICultureService
{
    private readonly CultureService _inner;
    private readonly string[] _additionalIsoCodes;

    public AllowAdditionalCulturesCultureService(
        IIsoCodeValidator isoCodeValidator,
        string[] additionalIsoCodes)
    {
        _inner = new CultureService(isoCodeValidator);
        _additionalIsoCodes = additionalIsoCodes;
    }

    public CultureInfo[] GetValidCultureInfos()
    {
        CultureInfo[] baseCultures = _inner.GetValidCultureInfos();

        // Resolve and append any additional cultures not already in the list.
        var existing = new HashSet<string>(baseCultures.Select(c => c.Name), StringComparer.OrdinalIgnoreCase);

        IEnumerable<CultureInfo> extra = _additionalIsoCodes
            .Where(code => !existing.Contains(code))
            .Select(code =>
            {
                try { return CultureInfo.GetCultureInfo(code); }
                catch (CultureNotFoundException) { return null; }
            })
            .Where(c => c is not null)
            .Cast<CultureInfo>();

        return baseCultures
            .Concat(extra)
            .OrderBy(c => c.EnglishName)
            .ToArray();
    }
}
```

Replace `"zh-HK"`

in the `_additionalIsoCodes`

array with the culture codes you need. You can add multiple codes, for example: `["zh-HK", "zh-MO"]`.


When the application starts, the composer will automatically register the custom implementations. The additional cultures will then appear in the backoffice language dropdown.

Last updated

Was this helpful?

---


## API Documentation | CMS

Information on Umbraco API Documentation

C# API Documentation

Backoffice UI Documentation

Last updated

Was this helpful?

Information on Umbraco API Documentation

A library of API Reference documentation is auto-generated from the comments within the Umbraco Source Code.

C# API Documentation

C# API references for the Umbraco Core, Infrastructure, Extensions, and Web libraries.

Opens a documentation browser that is different from the documentation section you're viewing now.

Backoffice UI Documentation

You can find all reference documentation for the Backoffice UI in the [UI Library](/umbraco-cms/customizing/ui-library) article.

Last updated

Was this helpful?

Was this helpful?

---


## API versioning and OpenAPI | CMS

How to use API versioning and OpenAPI (Swagger) for your own APIs.

Umbraco ships with Swagger to document the Content Delivery API. Swagger and the Swagger UI is available at `{yourdomain}/umbraco/swagger`

. For security reasons, both are disabled in production environments.

Due to the way OpenAPI works within ASP.NET Core, we have to apply some configurations in a global scope. If your Umbraco site used Swagger previous to Umbraco 12, these global configurations may interfere with your setup.

In this article we'll explore concrete solutions to overcome challenges with the global configurations.

Umbraco uses to handle Swagger and the Swagger UI.

If you have been using previous to Umbraco 12, chances are your Swagger setup will continue to work in Umbraco 12+ without any changes. Swashbuckle.AspNetCore and NSwag can coexist within the same site, as long as there are no conflicting routes between the two.

That being said, it would be sensible to consider migrating your API documentation to Swashbuckle.AspNetCore. This way you can avoid having multiple dependencies that perform the same tasks.

The Umbraco APIs rely on having the requested API version as part of the URL. If you prefer a different versioning for your own APIs, you can setup alternatives while still preserving the functionality of the Umbraco API.

The following code sample illustrates how you can use a custom header to pass the requested API version to your own APIs.

```
using Asp.Versioning;
using Microsoft.Extensions.Options;

namespace My.Custom.Swagger;

public class MyConfigureApiVersioningOptions : IConfigureOptions<ApiVersioningOptions>
{
    public void Configure(ApiVersioningOptions options)
        => options.ApiVersionReader = ApiVersionReader.Combine(
            // the URL segment version reader is required for the Umbraco APIs
            new UrlSegmentApiVersionReader(),
            // here you can add additional version readers to suit your needs
            new HeaderApiVersionReader("my-api-version"));
}

public static class MyConfigureApiVersioningUmbracoBuilderExtensions
{
    // call this from Program.cs, i.e.:
    //     builder.CreateUmbracoBuilder()
    //         ...
    //         .ConfigureMyApiVersioning()
    //         .Build();
    public static IUmbracoBuilder ConfigureMyApiVersioning(this IUmbracoBuilder builder)
    {
        builder.Services.ConfigureOptions<MyConfigureApiVersioningOptions>();
        return builder;
    }
}
```

As mentioned in the beginning of this article, Umbraco exposes Swagger and the Swagger UI at `{yourdomain}/umbraco/swagger`

. Both are disabled when the site is in production mode.

The code sample below shows how to change the Swagger route and availability.

Custom operation IDs can be a great way to make your API easier to use. Especially for consumers that generate API contracts from your Swagger documents.

The Umbraco APIs use custom operation IDs for that exact reason. In order to remain as un-intrusive as possible, these custom operation IDs are not applied to your APIs.

If you want to apply custom operation IDs to your APIs, you must ensure that the Umbraco APIs retain their custom operation IDs. The following code sample illustrates how this can be done.

Custom schema IDs can also make it easier for your API consumers to understand and work with your APIs. To that same end, Umbraco applies custom schema IDs to the Umbraco APIs - but not to your APIs.

If you want to create custom schema IDs for your APIs, you must ensure that the Umbraco APIs retain their custom schema IDs. The following code sample illustrates how that can be done.

Umbraco automatically adds a "default" Swagger document to contain all APIs that are not explicitly mapped to a named Swagger document. This means that your custom APIs will automatically appear in the "default" Swagger document.

If you want to exercise more control over where your APIs show up in Swagger, you can do so by adding your own Swagger documents.

Umbraco imposes no limitations on adding Swagger documents, and the code below is a simplistic example.

In the you will find comprehensive documentation for Swagger documents.

A common use case for this is when you maintain multiple versions of the same API. Often you want to have separate Swagger documents for each version. The following code sample creates two Swagger documents - "My API v1" and "My API v2".

With these Swagger documents in place, you can now assign the different versions of your API controllers to their respective documents using the `MapToApi`

annotation.

Last updated

Was this helpful?

---


## Cache

### Contents

- [Accessing the cache | CMS](#accessing-the-cache-cms)
- [Cache Seeding | CMS](#cache-seeding-cms)
- [Examples | CMS](#examples-cms)
- [ICacheRefresher | CMS](#icacherefresher-cms)
- [IMemberPartialViewCacheInvalidator | CMS](#imemberpartialviewcacheinvalidator-cms)
- [IServerMessenger | CMS](#iservermessenger-cms)
- [Getting/Adding/Updating/Inserting Into Cache | CMS](#gettingaddingupdatinginserting-into-cache-cms)

---

### Accessing the cache | CMS

Last updated

Was this helpful?

You should always be doing this consistently with the best practices listed below. You shouldn't be using HttpRuntime.Cache or HttpContext.Current.Cache directly. Instead, you should always be accessing it via the AppCaches cache helper (`Umbraco.Cms.Core.Cache`

).

Cache types

The `AppCaches`

which can be found in namespace `Umbraco.Cms.Core.Cache`

contains types of cache: Runtime Cache, Request Cache and Isolated Caches.

**Runtime Cache** is the most commonly used and is synonymous with HttpRuntime.Cache.**Request cache** is cache that exists only for the current request. This is synonymous with HttpContext.Current.Items and **isolated caches**. These are used by for example repositories, to ensure that each cached entity type has its own cache. When they have their own cache, lookups are fast and the repository does not need to search through all keys on a global scale.

Getting the AppCaches

If you wish to use the AppCaches in a class, you need to use Dependency Injection (DI) in your constructor:

```
public class MyClass
{
    private readonly IRelationService _relationService;

    private readonly IAppPolicyCache _runtimeCache;
    private readonly IAppCache _requestCache;
    private readonly IsolatedCaches _isolatedCaches;
    
    public MyClass(AppCaches appCaches, IRelationService relationService)
    {
        _relationService = relationService;
        _runtimeCache = appCaches.RuntimeCache;
        _requestCache = appCaches.RequestCache;
        _isolatedCaches = appCaches.IsolatedCaches;
    }

    // One example would be to get relations based on a node id. The RelationService hits the database each time and is not something you should call fx from a view that could get hit many times.
    // To get around that limitation you can wrap it in the cache so it only has to retrieve the value from the db once every minute (or whatever you set the timespan to).
    public void DocsService(int nodeId)
    {
        // Gets child relations from the cache if it exists, otherwise gets them and caches them for 1 min.
        var relations = _runtimeCache.GetCacheItem(
            $"ChildRelations_{nodeId}",
            () => _relationService.GetByChildId(nodeId, "umbDocument"), 
            TimeSpan.FromMinutes(1));
    }
}
```

Last updated

Was this helpful?

Was this helpful?

---

### Cache Seeding | CMS

Information about cache seeding

Umbraco uses a lazy loaded cache, meaning content is loaded into the cache on an as-needed basis. Whenever a piece of content is shown on the website for the first time it first needs to be loaded into the cache.

Loading the content into the cache causes a delay. This delay is dependent on the latency between your server and your database, but is generally minimal. For certain pages, like the front page, you may not want this delay to be there. The role of cache seeding is meant to solve this issue.

Cache seeding is based on the concept of an `ISeedKeyProvider`

. The role of the seed key provider is to specify what keys need to be seeded.

There are two types of seed key providers: an `IDocumentSeedKeyProvider`

specifying which document should be seeded, and an `IMediaSeedKeyProvider`

specifying which media should be seeded.

During startup, all the `ISeedKeyProviders`

are run, and the keys they return are seeded into their respective caches, `IPublishedContentCache`

for documents, and `IPublishedMediaCache`

for media. Additionally, whenever a document or media is changed, the cache will immediately be updated with the changed content. This ensures that the content is always present in the cache.

Whenever a piece of content is changed, the seeded keys must be checked, to see if the updated content was seeded. Because of the need the check all seeded keys, Umbraco caches the keys themselves during startup. This means that if you have a dynamic seed key provider, any newly added content will not be considered seeded until the server restarts. For instance, when seeding by Document Type any new content using the specified Document Type will not be seeded until the server is restarted.

By default, Umbraco ships with two seed key providers for documents, and one for media.

For documents, the `ContentTypeSeedKeyProvider`

seeds all documents of the given Document Types specified in the `appSettings.json`

file.

For documents and media, the `BreadthFirstKeyProvider`

does a breadth-first traversal of the content and media tree respectively. This will seed N number of content specified in the `appSettings.json`

file.

The default seed key provider configuration can be found in the [cache settings section.](/umbraco-cms/reference/configuration/cache-settings).

It is also possible to implement custom seed key providers. These are run alongside the default seed key providers on startup.

The returned keys of all the seed key providers are unioned into a single set. This means there will be no duplicates.

As mentioned above the provided keys are cached. Only the keys returned at startup will be considered seeded until the server restarts and the provider is rerun.

For a specific example of implementing a custom seed key provider, see [Creating a Custom Seed Key Provider](/umbraco-cms/extending/creating-custom-seed-key-provider).

Last updated

Was this helpful?

---

### Examples | CMS

Umbraco Documentation

file-lines Docs Overview

folder-grid CMS

Setting up caching on the tags property.

Previous Getting/Adding/Updating/Inserting Into Cache chevron-left

Next Working with caching chevron-right

Last updated 7 months ago

Was this helpful?

#### Working with caching | CMS

Information on how to insert and delete from the runtime cache

This article will show you how to insert and delete from the runtime cache.

For this example we're working with tags. On my site I have two tag properties:

One on every page using the tag group

`default`

One on my blog posts using the tag group

`blog`


We're going to expose an endpoint that allows us to get the tags from each group.

The tags from the `default`

should be cached for a minute. The `blog`

tags will be cached until site restart or if you publish a blog post node in the Backoffice.

Why work with tags? Because they're not cached by default.. which makes them ideal for demo purposes :)

First we want to create our `CacheTagService`

. In this example it's a basic class with one method (`GetAll`

) that wraps Umbraco's `TagQuery.GetAllTags()`.


```
using System;
using System.Collections.Generic;
using Umbraco.Cms.Core.Cache;
using Umbraco.Cms.Core.Models;
using Umbraco.Cms.Core.PublishedCache;
using Umbraco.Extensions;

namespace Doccers.Core.Services.Implement;

public class CacheTagService : ICacheTagService
{
    private readonly ITagQuery _tagQuery;
    private readonly IAppPolicyCache _runtimeCache;

    public CacheTagService(ITagQuery tagQuery, AppCaches appCaches)
    {
        _tagQuery = tagQuery;
        // Get the RuntimeCache from appCaches
        // and assign to our private field.
        _runtimeCache = appCaches.RuntimeCache;
    }

    public IEnumerable<TagModel> GetAll(
        string group,
        string cacheKey,
        TimeSpan? timeout = null)
    {
        // GetCacheItem will automatically insert the object
        // into cache if it doesn't exist.
        return _runtimeCache.GetCacheItem(cacheKey, () =>
        {
            return _tagQuery.GetAllTags(group);
        }, timeout);
    }
}
```

As you can see we inherit from the `ICacheTagService`

interface. All that has is:

The interface was created to better register it so we can use dependency injection. You can register your own classes like so:

Now you can inject `ICacheTagService`

in any constructor in your project - wohooo!

Now that we have our service it's time to create an endpoint where we can fetch the (cached) tags.

`/umbraco/api/tags/getblogtags`


`/umbraco/api/tags/getdefaulttags`


Everything should now work as expected when it comes to getting tags. However, if I go to my Backoffice and add a new tag to the `blog`

group the changes aren't shown on the endpoint. Let's fix that.

To clear the cache we need a notification handler in which we register to the `ContentPublishedNotification`

event on the `ContentService`

. This allows us to run a piece of code whenever you publish a node.

Now that we have our notification we also need to register it. Add `builder.AddNotificationHandler<ContentPublishedNotification, Notification>();`

to the `Compose`

method in the `Composer`

class so it becomes:

Awesome! Now we have set up caching on our tags - making the site a bit faster.

Last updated

Was this helpful?

---

### ICacheRefresher | CMS

What is an ICacheRefresher

Last updated

Was this helpful?

*This section describes what ICacheRefresher and ICacheRefresher<T> are and how to use them to invalidate your cache correctly including load balanced environments*

What is an ICacheRefresher

This interface has been in the Umbraco core for a significant period. However, it has really only been used to ensure that content cache is refreshed among all server nodes participating in a load balanced scenario.

An `ICacheRefresher`

is the primary method that invalidates *any* cache needing refreshment or removal. This applies regardless of a load balanced environment.

There are now a few different types of `ICacheRefreshers`

in the Umbraco core. It is important to understand the differences between them and how cache invalidation works across multiple server nodes.

Last updated

Was this helpful?

Was this helpful?

---

### IMemberPartialViewCacheInvalidator | CMS

What is an IMemberPartialViewCacheInvalidator?

Why do we need to partially invalidate the partial view cache?

Where is it used?

Details of the default implementation

Customizing the implementation

Last updated

Was this helpful?

---

### IServerMessenger | CMS

[Previous IMemberPartialViewCacheInvalidator chevron-left](/umbraco-cms/reference/cache/imemberpartialviewcacheinvalidator)

[Next Getting/Adding/Updating/Inserting Into Cache chevron-right](/umbraco-cms/reference/cache/updating-cache)

Last updated

Was this helpful?

Broadcasts distributed cache notifications to all servers of a load balanced environment. Also ensures that the notification is processed on the local environment.

For a specified [ICacheRefresher](/umbraco-cms/reference/cache/icacherefresher), the implemented methods will:

Notify the distributed cache

Invalidate specified items

Notify all servers of specified items removal

Notify all servers of invalidation of a object

Notify all servers of a global invalidation (clear the complete cache)


[Previous IMemberPartialViewCacheInvalidator chevron-left](/umbraco-cms/reference/cache/imemberpartialviewcacheinvalidator)

[Next Getting/Adding/Updating/Inserting Into Cache chevron-right](/umbraco-cms/reference/cache/updating-cache)

Last updated

Was this helpful?

Was this helpful?

---

### Getting/Adding/Updating/Inserting Into Cache | CMS

Adding and retrieving items in the cache

```
MyObject cachedItem = _appCaches.RuntimeCache.GetCacheItem<MyObject>("MyCacheKey", () => new MyObject());
```

Retrieving an item from the cache without a callback

```
MyObject cachedItem = _appCaches.RuntimeCache.GetCacheItem<MyObject>("MyCacheKey");
```

Inserting an item into the cache without retrieval

Last updated

Was this helpful?

---

---


## Common Pitfalls & Anti-Patterns | CMS

Information on common Pitfalls and Anti-Patterns in Umbraco

This section highlights common pitfalls that developers often encounter. Some of the anti-patterns discussed here can lead to memory leaks, instability, or poor performance on your site. Reading this section could save your site.

Generally speaking, if you are writing software these days you should be using Dependency Injection (DI) principles. If you do this, you probably are not using or , and for the most part you should not be.

Since Umbraco comes with dependency injection out of the box, there really is no reason to use singletons or statics. It makes your code difficult to test and hard to manage. Furthermore, the APIs become leaky and you will end up with more problems than when you started.

Dependency injection is available everywhere, and you can register your own services as well. Additionally, some resources are available through properties on certain base classes. For example, all Razor views that Umbraco creates expose an `UmbracoHelper`

property you can access through `@Umbraco`

. The other base classes expose some things you might need like `UmbracoContext`

, and things like `SurfaceController`

. Even here the services are initially obtained through DI, and you can inject further Umbraco and custom services that you might need.

For more information about consuming and registering your own dependencies have a look at the [Dependency Injection](/umbraco-cms/reference/using-ioc) documentation.

```
public class ContactFormSurfaceController : SurfaceController
{
    // The services are injected with DI and passed to the parent class
    public ContactFormSurfaceController(
        IUmbracoContextAccessor umbracoContextAccessor,
        IUmbracoDatabaseFactory databaseFactory,
        ServiceContext services,
        AppCaches appCaches,
        IProfilingLogger profilingLogger,
        IPublishedUrlProvider publishedUrlProvider)
        : base(umbracoContextAccessor, databaseFactory, services, appCaches, profilingLogger, publishedUrlProvider)
    {
    }

    [HttpPost]
    public IActionResult SubmitForm(ContactFormModel model)
    {
        // All normal form processing logic is left out of this example for brevity.
        // You can access all of these properties because they are properties of the base class. 
        // If you need something else you can inject it in the constructor.
        
        //Profiling logger
        using (ProfilingLogger.TraceDuration<ContactFormSurfaceController>("Start", "stop"))
        {
            // UmbracoContext
            UmbracoContext.Content.GetById(1234);
        }

        return Ok();
    }
}
```

`UmbracoHelper`

This practice can cause memory leaks along with inconsistent data results when using this `_umbracoHelper`

instance.

It is important to understand the difference between an object with Request-based scope and Singleton/Application-based scope.

**Application scope**: If an object has a singleton/application scope, that single object instance will exist for the lifetime of the application. The single instance will be shared by every thread that accesses it. Static variables will always exist for the lifespan of the application.**Request scope**: The web world is made up of requests and each request has its own thread. When an object is in the scope of a Request it only survives as long as the web request survives. At the end of the web request, the object may either be disposed of or cleared from memory by the garbage collector. Request scoped object instances are not accessed by every other thread in the application unless you do something like the above.

An example of a request-scoped instance is the `HttpContext`

. This object exists for a single request and it cannot be shared between other threads, especially not other request threads. This is because the object's thread is where the security information for a given user is handled. The `UmbracoContext`

is also a request-scoped object. In fact, it relies directly on an instance of `HttpContext`

. The `UmbracoHelper`

is request-scoped as well.

In the example above, the `UmbracoHelper`

, which has a request-scoped lifetime, will be statically assigned to a variable. This request-scoped object is now bound to an Application-scope lifetime and will exist after the request has ended. This could mean that under certain circumstances an entire Umbraco cache copy is stuck in memory. It could also mean that the `Security`

property of the context will be accessed by multiple threads. These threads may now contain the security information for a user from another request.

Additionally there is never really any reason to use static references. Instead, you should always inject your required resources, and let the DI container handle the lifetimes of the objects.

When using queries like this, you need to understand the implications. Here is a particularly bad scenario:

You have 10,000 content items in your tree and your tree structure is something like this:

You create a menu on your Home page like:

The query above renders out: *Root, Home, Blog, Office Locations, About Us, Contact Us*

This is going to iterate over every single node in Umbraco, all 10,000 of them. This will have a negative effect on the site's general performance.

Instead of using the snippet above, something similar to the snippet below can be used:

In many cases, you might know that there is only ever going to be a small number of Descendants. If so, using Descendants or DescendantsOrSelf will not have a negative effect on the site's performance. It is important to always be aware of the implications of what you are writing.

Querying and traversing content is not free. Anytime you make a query or resolve a property value there is overhead involved. Think about every query you make as an SQL call; too many requests can have a negative effect on the site's performance.

Here is a common pitfall in relation to this:

Following the example above, the menu is going to be rendered using the current page's root node:

The `@Model.Root()`

syntax is shorthand for doing this: `Model.AncestorOrSelf(1)`

. This will traverse up the tree until it reaches an ancestor node with a level of one. As mentioned above, traversing costs resources and in this example, there are 3x traversals being done for the same value.

Consider writing something similar to the example below:

The Services layer of Umbraco is for manipulating the business logic of Umbraco directly to/from the database. None of these methods should be used within your views and can have a negative impact on the performance and stability of your application.

Your views should rely only on the read-only data services such as `UmbracoHelper`

, `ITagQuery`

and `IMemberManager`

and the properties and methods they expose. This ensures that the data being queried comes from the cache and that you are not inadvertently making database changes.

For example, when retrieving a content item in your views:

If you are using services in your views, you should figure out why this is being done and, in most cases, remove this logic.

This is one of the anti-patterns that could have the most negative impact on your site's performance.

Umbraco content should not be used for volatile data. The Umbraco APIs, and the way Umbraco data is persisted, was not designed for this. When you need to store, write or track data that changes a lot, use a custom database table or another service. Do not use Umbraco content nodes for this.

Some examples of what not to do, and what to do instead:

| What not to do | Alternative |
|---|---|
| Hit counters to track the number of times your page has been viewed. | Use something like Google Analytics or a custom database table instead. |
| Creating new nodes for form submissions. | This should be stored in a custom database table. |
| Importing lots of data into Umbraco content nodes. | Import the data into custom database tables instead. |

Umbraco allows you to run some initialization code during startup by using `UmbracoApplicationStartingNotification`

. This code can have a negative impact on the application startup process. This is especially true for Package developers as your code could end up impacting many websites.

In many cases, [initialization code can be done lazily instead of eagerly arrow-up-right](https://msdn.microsoft.com/en-us/library/dd997286(v=vs.110).aspx)

Using and putting the initialization logic in its callback.

Putting logic in a property getter with a lock and setting a flag when it is processed.

Putting logic in a method with a lock and setting a flag when it is processed.


It is important to ensure that the initialization logic executes only once for the lifetime of the application, even when your app domain is restarted. If your initialization logic creates a database table that should only be executed one time, set a persistence flag. A persistence flag will indicate to your own logic that the initialization code has already been executed and does not need to be done again.

Rebuilding examine indexes can have a negative effect of the sites performance and is not a recommended practice. It is recommeded to ensure you are running the latest Umbraco and Examine versions if you are having trouble with out-of-sync index data.

The primary reasons your data will become out of sync are:

Old version of Umbraco.

Rebuilding indexes and restarting your app domain at the same time.


It is not recommended to rebuild your indexes unless you absolutely need to. If you need to do this often then it is advised to determine why and to try to resolve the underlying problem.

There are a couple of well-known Examine events: `TransformingIndexValues`

and `DocumentWriting`

. Both of these events allow the developer to modify the data that is going into the Lucene index. We often see developers performing service lookups in these methods. For example, using `IContentService.GetById(e.NodeId)`

inside of these events could cause an `N + 1`

problem. This is because these events are executed for every single document being indexed. If you are rebuilding an index, this will mean that this logic will fire for every single document and media item going into each index. That could mean a large number of lookups, which can negatively impact on the site's performance.

Similarly, if you are executing inefficient logic in these events, anytime you save or publish content or media that logic will slow the process down. If you rebuild an index, any slow code running in these events will cause the indexing to go even slower.

The API method called `RenderTemplateAsync`

allows you to render a particular content item's template and get a `IHtmlEncodedString`

in response. This could be useful if you want to send an email based on a content item and its template. However, you must be careful not to use this for purposes it is not meant to be used for.

Do not use this method for rendering content as this could cause severe performance problems. For you are rendering normal content of module type data from another content item, you should use Partial Views instead.

Constructors should generally not perform any logic. They should set parameter values, perform null checks and perhaps validate data.

There are a few reasons why this can become a performance problem:

The consumer of an API does not expect that by creating an object they should be worried about performance.

Creating an object can inadvertently happen many times, especially when using Language Integrated Query (LINQ).


Here is an example of how this can go wrong.

Your tree structure is something like this:

You have a custom model that looks like this:

You run the following code to show the favorites:

To show the top 10 voted recipes, this code will end up doing the following:

Iterate over all 5000 Recipes.

Create and allocate 5000 instances of

`RecipeModel`

.For each

`RecipeModel`

created, it will traverse upwards, iterate all 5000 recipes then resolve property data for 2 properties.

This means that there is now an additional 5,000 new objects created and allocated in memory. The number of traversals/visits to each of these objects is now `5000 x 5000 = 25,000,000`.


The other problem is that the logic used to lookup related recipes is inefficient. Instead, each recipe should have a picker to choose its related recipes, and then each of those can be looked up by their ID.

The above example could be rewritten like this:

The code will still iterate over all Recipes meaning that the number of traversals/visits to each of these objects will be 5000.

There really is not much reason to create a `RecipeModel`

. Instead, it could be written like:

Based on the above two points, you can see that iterating content with the traversal APIs ends up being expensive in terms of performance.

How to solve performance issues will always depend on the specific scenario. One thing to consider is to cache the IDs of the content you need in your critical code. Then you could retrieve the content from the cache by ID.

When you need to render the same four pieces of content for your navigation, we recommend caching, or hardcoding, the IDs of those content items. You can retrieve the content from their IDs using `Umbraco.Content`

. This will always be faster than trying to traverse your content tree and finding the content programmatically. It will do a direct lookup in the cache, meaning that your code does not have to do many traversals to get your content.

When memory is used, for instance creating 5,000 recipe models with a `Select`

statement, needs to occur. This turnover can cause performance problems. The more objects created, the more items allocated in memory, the harder the job is for the Garbage Collector, resulting in more performance problems.

Even worse is when you allocate a lot of large items in memory. These items will remain in memory for a long time, ending up in "" which the Garbage Collector ignores for as long as possible. It does so because it knows it is going to take a lot of resources to clean up.

Extending models should be used to add stateless, local features to models. It should not be used to transform content models into view models or manage trees of content.
You can read more about this in the [Understanding and Extending Models Builder documentation](/umbraco-cms/reference/templating/modelsbuilder/understand-and-extend)

Last updated

Was this helpful?

---
