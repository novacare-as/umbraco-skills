# Reference — Part 4: Content Type Filters | CMS → Management | CMS

## Content Type Filters | CMS

Describes how to use Content Type Filters to restrict the allowed content options available to editors.

Filtering Allowed Content Types

Implementing a Content Type Filter

Example Use Case

```
internal class OneHomePageOnlyContentTypeFilter : IContentTypeFilter
{
    private readonly IContentService _contentService;

    public OneHomePageOnlyContentTypeFilter(IContentService contentService) => _contentService = contentService;

    public Task<IEnumerable<TItem>> FilterAllowedAtRootAsync<TItem>(IEnumerable<TItem> contentTypes)
        where TItem : IContentTypeComposition
    {
        var docTypeAliasesToExclude = new List<string>();

        const string HomePageDocTypeAlias = "homePage";
        var docTypeAliasesAtRoot = _contentService.GetRootContent()
            .Select(x => x.ContentType.Alias)
            .Distinct()
            .ToList();
        if (docTypeAliasesAtRoot.Contains(HomePageDocTypeAlias))
        {
            docTypeAliasesToExclude.Add(HomePageDocTypeAlias);
        }

        return Task.FromResult(contentTypes
            .Where(x => docTypeAliasesToExclude.Contains(x.Alias) is false));
    }

    public Task<IEnumerable<ContentTypeSort>> FilterAllowedChildrenAsync(
        IEnumerable<ContentTypeSort> contentTypes,
        Guid parentContentTypeKey,
        Guid? parentContentKey)
        => Task.FromResult(contentTypes);
}
```

Last updated

Was this helpful?

---


## Custom Swagger API | CMS

Example of a Custom API with Authorization and Swagger

```

using Microsoft.Extensions.Options;
using Microsoft.OpenApi.Models;
using Swashbuckle.AspNetCore.SwaggerGen;
using Umbraco.Cms.Api.Management.OpenApi;
using Umbraco.Cms.Core.Composing;

namespace Umbraco.Cms.Web.UI.New.Custom;

//Necessary code for the new API to show in the Swagger documentation and Swagger UI
public class MyBackOfficeSecurityRequirementsOperationFilter : BackOfficeSecurityRequirementsOperationFilterBase
{
    protected override string ApiName => "my-api-v1";
}

public class MyConfigureSwaggerGenOptions : IConfigureOptions<SwaggerGenOptions>
{
    public void Configure(SwaggerGenOptions options)
    {
        options.SwaggerDoc("my-api-v1", new OpenApiInfo { Title = "My API v1", Version = "1.0" });
        options.OperationFilter<MyBackOfficeSecurityRequirementsOperationFilter>();
    }
}

public class MyComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
        => builder.Services.ConfigureOptions<MyConfigureSwaggerGenOptions>();
}
```

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-466ab1bb8c4f8bb6fca47e7bbbfaeb895ea8ac00%252Fcustom-api-swagger-example.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c7e31de3&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-76664f2786f29909a76155bdedb99542d93af3f4%252Fcustom-api-swagger-example-response.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f5532959&sv=2)

Last updated

Was this helpful?

Example of a Custom API with Authorization and Swagger

This article covers how to create a Custom API controller protected by the backoffice authorization policies. It also shows how to enable the authorization UI in Swagger docs.

Before proceeding, make sure to read the [Management API](/umbraco-cms/reference/management-api) article. It provides information about the Swagger documentation and Authorization used in this article.

This example can be a starting point for creating a secure custom API with automatic Swagger documentation. You can find other examples in the [API versioning and OpenAPI](/umbraco-cms/reference/api-versioning-and-openapi) article.

Create a new

`.cs`

file called`MyBackOfficeSecurityRequirementsOperationFilter`

in your Umbraco project.Add the following code so that the new API shows in the Swagger documentation and Swagger UI:


MyBackOfficeSecurityRequirementsOperationFilter.cs

```

using Microsoft.Extensions.Options;
using Microsoft.OpenApi.Models;
using Swashbuckle.AspNetCore.SwaggerGen;
using Umbraco.Cms.Api.Management.OpenApi;
using Umbraco.Cms.Core.Composing;

namespace Umbraco.Cms.Web.UI.New.Custom;

//Necessary code for the new API to show in the Swagger documentation and Swagger UI
public class MyBackOfficeSecurityRequirementsOperationFilter : BackOfficeSecurityRequirementsOperationFilterBase
{
    protected override string ApiName => "my-api-v1";
}

public class MyConfigureSwaggerGenOptions : IConfigureOptions<SwaggerGenOptions>
{
    public void Configure(SwaggerGenOptions options)
    {
        options.SwaggerDoc("my-api-v1", new OpenApiInfo { Title = "My API v1", Version = "1.0" });
        options.OperationFilter<MyBackOfficeSecurityRequirementsOperationFilter>();
    }
}

public class MyComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
        => builder.Services.ConfigureOptions<MyConfigureSwaggerGenOptions>();
}
```

Our filter inherits from

`BackOfficeSecurityRequirementsOperationFilterBase`

. This marks our API as supporting authorization via Swagger.`MyConfigureSwaggerGenOptions`

configures our API swagger docs with our filter applied.`MyComposer`

makes sure the swagger generator knows about our API docs configuration at runtime.

Add the ApiController to setup the logic behind the endpoint:


Run the project and navigate to

`{yourdomain}/umbraco/swagger`

.Choose the swagger documentation we created with the code above named

**My API v1**from**Select a definition**.

Here, we can find the endpoint that we created:

Click on the

**Authorize**button to authenticate.Try out the endpoint using the

**Try it out**button.Click on

**Execute**.

We now get the response we have setup using the code: `"Hello, {{userName}}"`.


Last updated

Was this helpful?

Was this helpful?

MyBackOfficeSecurityRequirementsOperationFilter.cs

```

using Umbraco.Cms.Api.Common.Attributes;
using Umbraco.Cms.Api.Common.Filters;
using Umbraco.Cms.Core;
using Umbraco.Cms.Core.Models.Membership;
using Umbraco.Cms.Core.Security;
using Umbraco.Cms.Web.Common.Authorization;
using Asp.Versioning;
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;...

//Creating the Controller
[ApiController]
[ApiVersion("1.0")] 
[MapToApi("my-api-v1")] 
[Authorize(Policy = AuthorizationPolicies.BackOfficeAccess)] 
[JsonOptionsName(Constants.JsonOptionsNames.BackOffice)]
[Route("api/v{version:apiVersion}/my")]
public class MyApiController : Controller
{
    private readonly IBackOfficeSecurityAccessor _backOfficeSecurityAccessor;

    public MyApiController(IBackOfficeSecurityAccessor backOfficeSecurityAccessor)
        => _backOfficeSecurityAccessor = backOfficeSecurityAccessor;

    [HttpGet("say-hello")]
    [MapToApiVersion("1.0")]
    [ProducesResponseType(typeof(string), StatusCodes.Status200OK)]
    public IActionResult SayHello()
    {
        IUser currentUser = _backOfficeSecurityAccessor.BackOfficeSecurity?.CurrentUser
                            ?? throw new InvalidOperationException("No backoffice user found");
        return Ok($"Hello, {currentUser.Name}");
    }
}
```

MyBackOfficeSecurityRequirementsOperationFilter.cs

```
using Asp.Versioning;
using Microsoft.AspNetCore.Authorization;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Options;
using Microsoft.OpenApi.Models;
using Swashbuckle.AspNetCore.SwaggerGen;
using Umbraco.Cms.Api.Common.Attributes;
using Umbraco.Cms.Api.Common.Filters;
using Umbraco.Cms.Api.Management.OpenApi;
using Umbraco.Cms.Core;
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.Models.Membership;
using Umbraco.Cms.Core.Security;
using Umbraco.Cms.Web.Common.Authorization;

namespace Umbraco.Cms.Web.UI.New.Custom;

//Necessary code for the new API to show in the Swagger documentation and Swagger UI
public class MyBackOfficeSecurityRequirementsOperationFilter : BackOfficeSecurityRequirementsOperationFilterBase
{
    protected override string ApiName => "my-api-v1";
}

public class MyConfigureSwaggerGenOptions : IConfigureOptions<SwaggerGenOptions>
{
    public void Configure(SwaggerGenOptions options)
    {
        options.SwaggerDoc("my-api-v1", new OpenApiInfo { Title = "My API v1", Version = "1.0" });
        options.OperationFilter<MyBackOfficeSecurityRequirementsOperationFilter>();
    }
}

public class MyComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
        => builder.Services.ConfigureOptions<MyConfigureSwaggerGenOptions>();
}

//Creating the Controller
[ApiController]
[ApiVersion("1.0")] 
[MapToApi("my-api-v1")] 
[Authorize(Policy = AuthorizationPolicies.BackOfficeAccess)] 
[JsonOptionsName(Constants.JsonOptionsNames.BackOffice)]
[Route("api/v{version:apiVersion}/my")]
public class MyApiController : Controller
{
    private readonly IBackOfficeSecurityAccessor _backOfficeSecurityAccessor;

    public MyApiController(IBackOfficeSecurityAccessor backOfficeSecurityAccessor)
        => _backOfficeSecurityAccessor = backOfficeSecurityAccessor;

    [HttpGet("say-hello")]
    [MapToApiVersion("1.0")]
    [ProducesResponseType(typeof(string), StatusCodes.Status200OK)]
    public IActionResult SayHello()
    {
        IUser currentUser = _backOfficeSecurityAccessor.BackOfficeSecurity?.CurrentUser
                            ?? throw new InvalidOperationException("No backoffice user found");
        return Ok($"Hello, {currentUser.Name}");
    }
}
```

```
GET /api/v1/my/say-hello
```

---


## Database Availability Checks | CMS

Describes the checks Umbraco will do on startup to determine the availability of the database, and how this behavior can be customized.

Last updated

Was this helpful?

Describes the checks Umbraco will do on startup to determine the availability of the database, and how this behavior can be customized.

When Umbraco boots it will check for a configured database and, if found, verify that a connection can be made.

The default behavior is to check five times with a one second delay between attempts. If, after that, a connection cannot be established, Umbraco will fail with a `BootFailedException`.


Implementing Custom Behavior

For projects in development with the potential for misconfigured database settings, this is likely a reasonable approach to take.

In production, when you have stable configuration, you may prefer to override the behavior to better handle cases where your hosting infrastructure might restart.

We support this by abstracting the default behavior behind the `IDatabaseAvailabilityCheck`

interface found in the `Umbraco.Cms.Infrastructure.Persistence`

namespace.

You can implement your own version of this interface and register it via a composer. This is shown in the following, stub example:

```
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Infrastructure.Persistence;

public class MyDatabaseAvailabilityCheckComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.Services.AddUnique<IDatabaseAvailabilityCheck, MyDatabaseAvailabilityCheck>();
    }
}

internal class MyDatabaseAvailabilityCheck : IDatabaseAvailabilityCheck
{
    public bool IsDatabaseAvailable(IUmbracoDatabaseFactory databaseFactory)
    {
        // Provide your custom logic to check database availability, wait as required, and return true once a connection is established.
        return true;
    }
}
```

For reference and inspiration, the default implementation can be found .

Last updated

Was this helpful?

Was this helpful?

---


## Debugging with SourceLink | CMS

Information on SourceLink and how to use it to debug the Umbraco CMS source code

Enabling SourceLink in Visual Studio 2017 & 2019

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9fb55917f99acbe25d8b6ba356e7a71577a865c9%252FVS19-enable-sourcelink.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ef78b879&sv=2)

Visual Studio 2019 Debug Settings for SourceLink

What is SourceLink?

Working with SourceLink

Example Code Snippet to try with SourceLink

Last updated

Was this helpful?

---


## Distributed Locks | CMS

```
 using (var scope = _scopeProvider.CreateScope())
{
    scope.WriteLock(Constants.Locks.Domains);

    // Carry out save operation.

    scope.Complete();
}
```

| Id | Name | Used By |
|---|---|---|
| -1000 | MainDom | Umbraco CMS |
| -331 to -340 | Various | Umbraco CMS |
| -800 | DeployTransferQueue | Umbraco Deploy |

Last updated

Was this helpful?

During save operations, Umbraco will generally take a database lock to avoid concurrency issues.

Access to this feature is via the `IScope`

interface, for example:

```
 using (var scope = _scopeProvider.CreateScope())
{
    scope.WriteLock(Constants.Locks.Domains);

    // Carry out save operation.

    scope.Complete();
}
```

Each lockable entity is represented by an integer Id, stored along with the state of the lock in the `umbracoLock`

database table.

Packages or custom solutions working with custom data via the `IScope`

interface can introduce their own records to this table. However it's important to not clash with either core identifiers or those introduced by other packages.

A reference is maintained here of known identifiers:

| Id | Name | Used By |
|---|---|---|
| -1000 | MainDom | Umbraco CMS |
| -331 to -340 | Various | Umbraco CMS |
| -800 | DeployTransferQueue | Umbraco Deploy |

Last updated

Was this helpful?

Was this helpful?

---


## Dive into the code | CMS

Learn more about what you can find in this section, which is referred to as the "Developers Reference".

![Cover](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-35d43482ffd23f75ecaf7d98480e6b64418be390%252FDocumentations%2520Icons_Umbraco_CMS_Reference_Configuration.png%3Falt%3Dmedia&width=490&dpr=3&quality=100&sign=23e96d08&sv=2)

![Cover](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-94df11bb19a8298aa0a8bde6fed48dc8fe9502ff%252FDocumentations%2520Icons_Umbraco_CMS_Reference_Templating.png%3Falt%3Dmedia&width=490&dpr=3&quality=100&sign=ed2e92b9&sv=2)

![Cover](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-61b11658050545835b088a11aa14556286f27f4d%252FDocumentations%2520Icons_Umbraco_CMS_Reference_Querying_and_Models.png%3Falt%3Dmedia&width=490&dpr=3&quality=100&sign=511e5811&sv=2)

![Cover](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8529aae789f4fa66c7280a478c7f60601ce1b40f%252FDocumentations%2520Icons_Umbraco_CMS_Reference_Routing_and_Controllers.png%3Falt%3Dmedia&width=490&dpr=3&quality=100&sign=3fd0e152&sv=2)

![Cover](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a9bbebbbea0e853a660a43135b6027bb6a4b6822%252FDocumentations%2520Icons_Umbraco_CMS_Reference_Security.png%3Falt%3Dmedia&width=490&dpr=3&quality=100&sign=e703962e&sv=2)

![Cover](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-36feaf257198335a3fd1df1f572a909f7dab7cfd%252FDocumentations%2520Icons_Umbraco_CMS_Reference_Searching.png%3Falt%3Dmedia&width=490&dpr=3&quality=100&sign=7660c09&sv=2)

![Cover](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5790d353ba3b10ed39fd0b249180ed2318c17ce1%252FDocumentations%2520Icons_Umbraco_CMS_Reference_Notifications.png%3Falt%3Dmedia&width=490&dpr=3&quality=100&sign=334712c9&sv=2)

![Cover](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-41b02fe3c4aec3ca063548403a6d79bd5ab75c56%252FDocumentations%2520Icons_Umbraco_CMS_Reference_Caching.png%3Falt%3Dmedia&width=490&dpr=3&quality=100&sign=c7c84487&sv=2)

![Cover](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7164d6542f9212e75cea5b8b88cc91f8d94e6f2a%252FDocumentations%2520Icons_Umbraco_CMS_Reference_API_Documentation.png%3Falt%3Dmedia&width=490&dpr=3&quality=100&sign=f7e1de62&sv=2)

Also in this section

[Inversion of Control / Dependency injection chevron-right](/umbraco-cms/reference/using-ioc)

[Response Caching chevron-right](/umbraco-cms/reference/response-caching)

[Common Pitfalls & Anti-Patterns chevron-right](/umbraco-cms/reference/common-pitfalls)

Last updated

Was this helpful?

---


## JSON Serialization | CMS

Describes how the JSON serialization within Umbraco can be customized.

Last updated

Was this helpful?

Describes how the JSON serialization within Umbraco can be customized.

Umbraco uses JSON as a format to serialize information to the database and for output. For example, the configuration of data types and the property values of complex editors are serialized to JSON for persistence.

The serializers within Umbraco uses a `JavascriptEncoder`

which only considers basic latin characters as unnecessary to encode.

Implementing Custom Behavior

For projects making use of non-Latin characters you may want to amend this behavior. By doing so you can reduce the space the serialized information takes up in the database.

We support this by abstracting the default behavior behind the `IJsonSerializerEncoderFactory`

interface found in the `Umbraco.Cms.Core.Serialization`

namespace.

You can implement your own version of this interface and register it via a composer. This is shown in the following example that marks Cyrillic characters as excluded for encoding:

```
using System.Text.Encodings.Web;
using System.Text.Unicode;
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.Serialization;
using Umbraco.Cms.Infrastructure.Serialization;

namespace Umbraco.Cms.Web.UI.Custom.SystemTextConfigurationEditor;

public class SystemTextConfigurationEditorComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.Services.AddUnique<IJsonSerializerEncoderFactory, MyConfigurationEditorJsonSerializerEncoderFactory>();
    }
}

internal class MyConfigurationEditorJsonSerializerEncoderFactory : IJsonSerializerEncoderFactory
{
    public JavaScriptEncoder CreateEncoder<TSerializer>()
        where TSerializer : IJsonSerializer
    {
        return JavaScriptEncoder.Create(UnicodeRanges.BasicLatin, UnicodeRanges.Cyrillic);
    }
}
```

For reference, the default implementation can be found .

Last updated

Was this helpful?

Was this helpful?

---


## Language Variation | CMS

Language variants allow you to have different variations of content based on the language culture. Learn how to use them in this section.

```
@Model.Value("pageTitle", "fr", fallback: Fallback.ToLanguage)
```

```
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Core.Cache;
using Umbraco.Cms.Core.Logging;
using Umbraco.Cms.Core.Routing;
using Umbraco.Cms.Core.Services;
using Umbraco.Cms.Core.Web;
using Umbraco.Cms.Infrastructure.Persistence;
using Umbraco.Cms.Web.Website.Controllers;
using Umbraco.Extensions;

namespace TestStuff;

public class TestController : SurfaceController
{

    public TestController(
        IUmbracoContextAccessor umbracoContextAccessor, 
        IUmbracoDatabaseFactory databaseFactory, 
        ServiceContext services, 
        AppCaches appCaches, 
        IProfilingLogger profilingLogger, 
        IPublishedUrlProvider publishedUrlProvider) 
        : base(umbracoContextAccessor, databaseFactory, services, appCaches, profilingLogger, publishedUrlProvider)
    {
    }

    public IActionResult Index()
    {
        var culturedRootNode = CurrentPage.Root();
        TempData.Add("CulturedRootNode", culturedRootNode);

        return View();
    }
}
```

Last updated

Was this helpful?

Language variants allow you to have different variations of content based on the language culture. Learn how to use them in this section.

Language Variation allows you to have different variations of content based on a language culture. In the documentation there are other useful articles about the feature:

[ IPublishedContent](/umbraco-cms/reference/querying/ipublishedcontent) contains all language variations of a node, and when rendering it out it will then use the Culture you are currently on. This can then be overridden on an individual property level if you want, like this:

```
@Model.Value("pageTitle", "fr", fallback: Fallback.ToLanguage)
```

Here we would attempt to render the `pageTitle`

property in the French variant. We want to fallback to the current culture language if it can't find it in French.

The challenge arises when trying to display all values of an IPublishedContent model in a specific culture from a "current culture"-less context, like a [ SurfaceController](/umbraco-cms/reference/routing/surface-controllers).

If you do something like this:

```
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Core.Cache;
using Umbraco.Cms.Core.Logging;
using Umbraco.Cms.Core.Routing;
using Umbraco.Cms.Core.Services;
using Umbraco.Cms.Core.Web;
using Umbraco.Cms.Infrastructure.Persistence;
using Umbraco.Cms.Web.Website.Controllers;
using Umbraco.Extensions;

namespace TestStuff;

public class TestController : SurfaceController
{

    public TestController(
        IUmbracoContextAccessor umbracoContextAccessor, 
        IUmbracoDatabaseFactory databaseFactory, 
        ServiceContext services, 
        AppCaches appCaches, 
        IProfilingLogger profilingLogger, 
        IPublishedUrlProvider publishedUrlProvider) 
        : base(umbracoContextAccessor, databaseFactory, services, appCaches, profilingLogger, publishedUrlProvider)
    {
    }

    public IActionResult Index()
    {
        var culturedRootNode = CurrentPage.Root();
        TempData.Add("CulturedRootNode", culturedRootNode);

        return View();
    }
}
```

You will get the root node in the default culture. However you can set a new `VariationContext`

like this:

So we access the `IVariationContextAccessor.VariationContext`

and set it to a new one with our own specified culture (remember `using Umbraco.Core.Models.PublishedContent;`

at the top to get access to it).

The elements you get afterward will be in the culture you have specified.

Last updated

Was this helpful?

Was this helpful?

```
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Core.Cache;
using Umbraco.Cms.Core.Logging;
using Umbraco.Cms.Core.Models.PublishedContent;
using Umbraco.Cms.Core.Routing;
using Umbraco.Cms.Core.Services;
using Umbraco.Cms.Core.Web;
using Umbraco.Cms.Infrastructure.Persistence;
using Umbraco.Cms.Web.Website.Controllers;
using Umbraco.Extensions;

namespace TestStuff;

public class TestController : SurfaceController
{
    private readonly IVariationContextAccessor _variationContextAccessor;

    public TestController(
        IUmbracoContextAccessor umbracoContextAccessor, 
        IUmbracoDatabaseFactory databaseFactory, 
        ServiceContext services, 
        AppCaches appCaches, 
        IProfilingLogger profilingLogger, 
        IPublishedUrlProvider publishedUrlProvider, 
        IVariationContextAccessor variationContextAccessor) 
        : base(umbracoContextAccessor, databaseFactory, services, appCaches, profilingLogger, publishedUrlProvider)
    {
        _variationContextAccessor = variationContextAccessor;
    }

    public IActionResult Index()
    {
        const string culture = "af"; // Afrikaans

        // This is how the culture is set for the context we are in
        _variationContextAccessor.VariationContext = new VariationContext(culture);

        var culturedRootNode = CurrentPage.Root();
        TempData.Add("CulturedRootNode", culturedRootNode);

        return View();
    }
}
```

---


## Management Api

### Contents

- [External Access | CMS](#external-access-cms)
- [Patching](#patching)
- [Setup OAuth using Postman | CMS](#setup-oauth-using-postman-cms)

---

### External Access | CMS

How external applications can consume the Management API.

```
{
  "access_token": "ZnEAKg5YwDc7621y6xZlEdT9kwp_ULGQPc5mnY9cDw0",
  "token_type": "Bearer",
  "expires_in": 299
}
```

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-fd7a06436c0ba16f54bb8d0418731b207b37fc9f%252Fcurrent-user-endpoint.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=90b2d354&sv=2)

Last updated

Was this helpful?

How external applications can consume the Management API.

The Management API can be used directly for integrations between Umbraco and external systems.

When consuming the Management API from an external source, you must use the OpenId Connect Client Credentials flow for authorization. Refer to the [API Users](/umbraco-cms/fundamentals/data/users/api-users) article for details on setting up Client Credentials.

With a set of Client Credentials in place, you can obtain an access token from the Management API token endpoint: `/umbraco/management/api/v1/security/back-office/token`.


The token endpoint response looks like this:

```
{
  "access_token": "ZnEAKg5YwDc7621y6xZlEdT9kwp_ULGQPc5mnY9cDw0",
  "token_type": "Bearer",
  "expires_in": 299
}
```

As shown, the access token should be used as a Bearer token when consuming the Management API.

Also, notice that access tokens have a fixed expiry. While you can keep issuing new tokens for the Client Credentials, reuse tokens within their lifespan. This will be more performant and avoid flooding the Umbraco database with tokens.

The Management API does not support OpenID Connect Discovery. This is reserved for Members accessing protected content via the [Delivery API](/umbraco-cms/reference/content-delivery-api/protected-content-in-the-delivery-api).

The following code sample demonstrates how to consume the Management API by

Obtaining an access token from the token endpoint, and

Fetching data from the "current user" endpoint.


This sample requires the to run.

Last updated

Was this helpful?

Was this helpful?

Program.cs

```
using System.Net.Http.Json;
using Duende.IdentityModel.Client;

// the base URL of the Umbraco site - change this to fit your setup
const string host = "https://localhost:44391";

var client = new HttpClient();

// request a client credentials token from the Management API token endpoint
var tokenResponse = await client.RequestClientCredentialsTokenAsync(
    new ClientCredentialsTokenRequest
    {
        Address = $"{host}/umbraco/management/api/v1/security/back-office/token",
        ClientId = "umbraco-back-office-my-client",
        ClientSecret = "my-client-secret"
    }
);

if (tokenResponse.IsError || tokenResponse.AccessToken is null)
{
    Console.WriteLine($"Error obtaining a token: {tokenResponse.ErrorDescription}");
    return;
}

// use the access token as Bearer token
client.SetBearerToken(tokenResponse.AccessToken);

// fetch user data from the "current user" Management API endpoint
var apiResponse = await client.GetAsync($"{host}/umbraco/management/api/v1/user/current");
var apiUserResponse = await apiResponse
    .EnsureSuccessStatusCode()
    .Content
    .ReadFromJsonAsync<ApiUserResponse>();

if (apiUserResponse is null)
{
    Console.WriteLine("Could not parse a user from the API response.");
    return;
}

Console.WriteLine($"Hello, {apiUserResponse.Name} ({apiUserResponse.Email})");

public class ApiUserResponse
{
    public required Guid Id { get; set; }

    public required string Name { get; set; }

    public required string Email { get; set; }
}
```

---

### Patching

#### Contents

- [Document PATCH endpoint guide | CMS](#document-patch-endpoint-guide-cms)
- [Document PATCH endpoint spec | CMS](#document-patch-endpoint-spec-cms)

---

#### Document PATCH endpoint guide | CMS

What is the PATCH Endpoint

Endpoint

```
PATCH /umbraco/management/api/v1/document/{id}/patch
Content-Type: application/json-patch+json
```

Request Format

```
{
  "operations": [
    {
      "op": "replace",
      "path": "/values[alias=title,culture=en-US,segment=null]/value",
      "value": "New Title"
    }
  ]
}
```

| Field | Required | Description |
|---|---|---|
| `op` | Yes | The operation: `"replace"` , `"add"` , or `"remove"` . |
| `path` | Yes | A path expression pointing to the target location in the document. |
| `value` | For replace/add | The new value to set. |

Operations

Replace

Add

Remove

Response Codes

| Code | Meaning |
|---|---|
| 200 | All operations applied successfully. |
| 400 | Invalid path syntax, missing value for replace/add, or path could not be resolved. |
| 404 | Document not found, or content type not found. |
| 422 | Property type not found on the content type. |

Path Syntax

Building Blocks

| Syntax | What it does | Example |
|---|---|---|
| `/property` | Access a named property on an object. | `/value` , `/name` , `/markup` |
| `[key=value]` | Find an array element where `key` equals `value` . | `[alias=title]` |
| `[k1=v1,k2=v2]` | Find an element matching all conditions. | `[alias=title,culture=en-US,segment=null]` |
| `/0` , `/1` , ... | Access an array element by index (zero-based). | `/contentData/0` |
| `/-` | Target the end of an array (for add/append). | `/contentData/-` |
| `~1` | Escape sequence for `/` in a property name. | `/Umbraco.BlockList` uses no escape since `.` is fine |
| `~0` | Escape sequence for `~` in a property name. | Rarely needed |

Filter Syntax Details

The Document JSON Structure

Root Level

Values Array

Variants Array

Block Editor Values

The Four Arrays

| Array | Purpose |
|---|---|
| Defines the visual order and structure of blocks. Keyed by editor alias (`Umbraco.BlockList` , `Umbraco.BlockGrid` , or `Umbraco.RichText` ). |
| The actual block content. Each item has a `key` (GUID), `contentTypeKey` (element type GUID), and `values` (array of property values). |
| Same structure as `contentData` but for block settings. |
| Controls which blocks are visible for which cultures/segments. Each entry links a `contentKey` to a `culture` and `segment` . |

Layout Items by Editor Type

Block Grid

`contentData`

is FlatNested Block Values Are Expanded

Rich Text Editor Specifics

Common Recipes

Update a Property Value

Update a Variant Name

Update a Culture-Specific Property

Replace a Value Inside a Block List Block

Add a Block to a Block List

Insert a Block at a Specific Position

Remove a Block

Update a Deeply Nested Property

Add a Block to a Rich Text Editor

Tips and Gotchas

Last updated

Was this helpful?

---

#### Document PATCH endpoint spec | CMS

```
PATCH /umbraco/management/api/v1/document/{id:guid}/patch
```

| Parameter | Type | Description |
|---|---|---|
| `id` | GUID (path) | The document key |

| Header | Value |
|---|---|
| `Content-Type` | `application/json-patch+json` |
| `Authorization` | Bearer token or cookie-based auth. |

| Code | Condition |
|---|---|
| 200 | Success |
| 400 | Invalid path syntax, missing value, path resolution failure, invalid culture. |
| 404 | Document not found, content type not found. |
| 422 | Property type not found on content type. |

```
{
  "operations": [
    {
      "op": "replace" | "add" | "remove",
      "path": "<path-expression>",
      "value": <any>           // REQUIRED for replace and add. OMIT for remove.
    }
  ]
}
```

| Type | Syntax | Resolves To | Example |
|---|---|---|---|
| PropertySegment | `/name` | Named property on a JsonObject. | `/value` , `/markup` , `/layout` |
| FilterSegment | `[k=v,k2=v2]` | First element in a JsonArray matching all conditions. | `[alias=title,culture=en-US,segment=null]` |
| IndexSegment | `/0` , `/1` | Element at numeric index in a JsonArray. | `/contentData/0` |
| AppendSegment | `/-` | Past-the-end position in a JsonArray. | `/contentData/-` |

| Target | Behavior |
|---|---|
| Object property | Sets property to new value. |
| Array element (by index or filter) | Replaces element value. |
| Cannot target `/-` | Error |

| Target | Behavior |
|---|---|
| Object property | Sets property (creates if missing). |
| Array with `/-` | Appends to end of array. |
| Array with index `/N` | Inserts at index N, shifts existing elements right. |

| Target | Behavior |
|---|---|
| Object property | Removes the property. |
| Array element (by index or filter) | Removes element, shifts subsequent elements left. |
| Cannot target `/-` | Error |

| Editor | Alias |
|---|---|
| Block List | `Umbraco.BlockList` |
| Block Grid | `Umbraco.BlockGrid` |
| Rich Text | `Umbraco.RichText` |

`contentData`

/ `settingsData`

Entry)`contentData`

)| # | Operation | Path suffix | Value |
|---|---|---|---|
| 1 | `add` | `/contentData/-` | BlockItemData object. |
| 2 | `add` | `/layout/<EditorAlias>/-` | Layout item. |
| 3 | `add` | `/expose/-` | Expose entry (one per culture/segment). |

| # | Operation | Path suffix | Value |
|---|---|---|---|
| 1 | `add` | `/blocks/contentData/-` | BlockItemData object. |
| 2 | `add` | `/blocks/layout/Umbraco.RichText/-` | Layout item. |
| 3 | `add` | `/blocks/expose/-` | Expose entry. |
| 4 | `replace` | `/markup` | Updated HTML with `<umb-rte-block data-content-key="NEW_GUID">` . |

| Segment | Type | Resolves to |
|---|---|---|
| `/values` | Property | Root values array. |
| `[alias=blockList,culture=null,segment=null]` | Filter | The blockList property entry. |
| `/value` | Property | The block list value object. |
| `/contentData` | Property | Content data array. |
| `[key=f32d4827-...]` | Filter | The container block. |
| `/values` | Property | Container block's values array. |
| `[alias=block,culture=null,segment=null]` | Filter | The "block" property (inner block list). |
| `/value` | Property | The inner block list value object. |
| `/contentData` | Property | Inner content data array. |
| `[key=dc9db89c-...]` | Filter | The grid container block. |
| `/values` | Property | Grid container's values array. |
| `[alias=grid,culture=null,segment=null]` | Filter | The "grid" property (block grid). |
| `/value` | Property | The block grid value object. |
| `/contentData` | Property | Grid content data array. |
| `[key=5122504c-...]` | Filter | The text block. |
| `/values` | Property | Text block's values array. |
| `[alias=text,culture=nl,segment=null]` | Filter | The Dutch text value. |
| `/value` | Property | The actual string value. |

| Error | HTTP Code | Cause |
|---|---|---|
| Invalid path syntax | 400 | Path doesn't start with `/` , unclosed bracket, empty filter key, and so on. |
| Missing value | 400 | `replace` or `add` operation has `value: null` . |
| Path resolution failed | 400 | Property not found on object, filter matched no elements, index out of bounds. |
| Invalid culture | 400 | Culture in path doesn't exist in the system. |
| Document not found | 404 | No document with the given ID. |
| Content type not found | 404 | Document's content type was deleted. |
| Property type not found | 422 | Property alias doesn't exist on the content type. |

Last updated

Was this helpful?

---

---

### Setup OAuth using Postman | CMS

Setup OAuth authorization for swagger via Postman

This guide is created by a community member and is not managed by Umbraco HQ. Some attributes may change in the future because of the integration with Postman (third-party tool).

This guide covers how to set up OAuth authorization for the Management API using Postman.

Before proceeding, make sure to read the [Management API](/umbraco-cms/reference/management-api) article. It provides information about Authorization and why it is needed in this article.

This guide covers the following:

Open the swagger UI at

`{yourdomain}/umbraco/swagger`

.Choose

**Umbraco Management API**from**Select a definition**.Open the JSON file, which you can find right underneath the

**Title**:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-463023ea8fe9b2c85195ced201a5c72d651b8c15%252Fpostman-setup-swagger-json-file.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fcac8819&sv=2)

Save the JSON file to disk. The name of the file will be saved by default with the name of

`swagger.json`

.Click to in Postman.

Import the

`swagger.json`

file.Choose

**Postman Collection**when prompted.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-376d417974bcc9c8775ded1ec85d501cac52f019%252Fpostman-setup-swagger-import.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=76b8e3ce&sv=2)

Once imported, you will see a new collection called **Umbraco Management API**.

Click on

**Variables**tab in the**Umbraco Management API**collection.Add a new variable called

`baseUrl`

and in the**Initial**and**Current**values add your URL, which in this example we use the`localhost URL`

(without trailing slashes):

The localhost URL might vary from this example. Make sure to change the URL to the current localhost URL your project is running on.

Save the changes.


To set up authorization values, follow these steps:

Click on

**Authorization**tab in the**Umbraco Management API**collection.Choose

`OAuth 2.0`

from**Type**Check if these attributes are set:


**Add auth data**is set to`Request Headers`

**Auto-refresh token**is`Disabled`


Now let's setup a new token:

Add a

**Token name**called`BackofficeSwagger`

under**Configure New Token**. The token name can be anything.Choose

`Authorization Code (With PKCE)`

from**Grant Type**.Click to enable

`Authorize using browser`

on**Callback URL**.Add the following on

**Auth URL**:

Add the following on

**Access Token URL**:

Add

`umbraco-postman`

on**Client ID**.Choose

`SHA-256`

from**Code Challenge Method**.Choose

`Send Client credentials in body`

from**Client Authentication**.Any other field should either be empty or auto-filled by default.

Click

**Save**.Click on

**Get New Access Token**. A window appears to authenticate into the Backoffice. Follow the given instruction to**Open in Postman**.

You will see a new

**Manage access tokens**window in Postman.

Click

**Use Token**.

Click on

**Authorization**tab in the**Umbraco Management API**collection .Click on

`Clear Cookies`

at the bottom of the page above the**Get New Access Token**.Open your localhost instance of Umbraco in the browser. Example:

`https://localhost:44331`

.Inspect the page, go to

**Application**tab and clear the`UmbracoBackOffice`

cookie.Click on

**Get New Access Token**in Postman andClick on

**Use Token**after authentication.

When trying to obtain a token you might run into an error. If you see the message `Error: localhost request not supported`

in the Postman console, it means the Postman agent is missing. To resolve this issue, you can download the Postman agent from the Postman website and try again.

When requesting a token, you might get an error that reads `Error: unable to verify the first certificate`

in the console.
To resolve this:

Click on the

**Settings**cog wheel in the top right corner next to the**Invite**button.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e15b2156bf8e53e5a2568e470520ae29022e3695%252Fpostman-setup-swagger-cog-wheel.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fb7cf2c8&sv=2)

Click on

**Settings**and disable`SSL certificate verification`.


When making a request for the first time, follow these steps:

Click on the

**Authorization**tab in the**Umbraco Management API**collection.Choose

`Inherit auth from parent`

from**Type**.Disable any parameters you are not using as Postman sets their value to default sometimes.

Click

**Save**

Last updated

Was this helpful?

---

---


## Management | CMS

Details of CRUD operations within Umbraco and how to interact with the data persisted in the database

Last updated

Was this helpful?

Details of CRUD operations within Umbraco and how to interact with the data persisted in the database

The intended audience for these reference pages is .NET developers. It is assumed the reader already knows the basics of Umbraco and knows .NET & C#.

Since the release of Umbraco 14, the documentation for Models and Services has been removed from the documentation.

Find references for the models in the public API. The models include Content, ContentType, Language, Media, and Template classes.

Find references for the services available for performing Create, Read, Update, and Delete (CRUD) operations for the models.

Find a handful of resources for using some of the services available with Umbraco CMS.

Last updated

Was this helpful?

Was this helpful?

### Using Services

### Contents

- [Consent Service | CMS](#consent-service-cms)
- [Content Service | CMS](#content-service-cms)
- [Content Type Service | CMS](#content-type-service-cms)
- [Localization Service | CMS](#localization-service-cms)
- [Media Service | CMS](#media-service-cms)
- [Relation Service | CMS](#relation-service-cms)
- [User Service | CMS](#user-service-cms)

---

### Consent Service | CMS

What is a Consent

Register a new consent

Get the current state

Revoking a consent

Examples

```
// store a new consent
var newConsent = _consentService.RegisterConsent("userId", "Our.Custom.Umbraco.Plugin", "AllowedToEmail", ConsentState.Granted, "some comments");

// lookup a consent
var consents = _consentService.LookupConsent("userId", "Our.Custom.Umbraco.Plugin", "AllowedToEmail", sourceStartsWith : true);
if (consents != null && consents.Any())
{
    var currentConsent = consents.First(c => c.Current == true);
    if(currentConsent.State  == ConsentState.Granted)
    {
        // Do what you need
    }
    else
    {
        // the state is None, Pending or Revoked
    }
}
```

Last updated

Was this helpful?

A service for handling lawful data processing requirements.

What is a Consent

A consent is fully identified by a source (whoever is consenting), a context (for example, an application), and an action (whatever is consented). A consent state registers the state of the consent (granted, revoked...).

Register a new consent

Consent can be given or revoked or changed via the `RegisterConsent`

method, which creates a new `Consent`

entity to track the consent.

Get the current state

Getter methods of this service return the current state of a consent, that is the latest entity that was created.

Revoking a consent

Revoking a consent is performed by registering a revoked consent.

A consent *cannot be deleted*. It can only be revoked by registering a "revoked consent".

Examples

```
// store a new consent
var newConsent = _consentService.RegisterConsent("userId", "Our.Custom.Umbraco.Plugin", "AllowedToEmail", ConsentState.Granted, "some comments");

// lookup a consent
var consents = _consentService.LookupConsent("userId", "Our.Custom.Umbraco.Plugin", "AllowedToEmail", sourceStartsWith : true);
if (consents != null && consents.Any())
{
    var currentConsent = consents.First(c => c.Current == true);
    if(currentConsent.State  == ConsentState.Granted)
    {
        // Do what you need
    }
    else
    {
        // the state is None, Pending or Revoked
    }
}
```

Last updated

Was this helpful?

Was this helpful?

---

### Content Service | CMS

Example on how to create and publish content programmatically using the `IContentService`.

Creating content programmatically

```
using Umbraco.Cms.Core.Models;
using Umbraco.Cms.Core.Services;

namespace Umbraco.Cms.Web.UI.Custom;

public class PublishContentDemo
{
    private readonly IContentService _contentService;

    public PublishContentDemo(IContentService contentService) => _contentService = contentService;

    public void Create()
    {
        // Create a variable for the GUID of the parent page - Catalogue, where you want to add a child item.
        var parentId = Guid.Parse("b6fbbb31-a77f-4f9c-85f7-2dc4835c7f31");

        // Create a new child item of type 'Product'
        var demoProduct = _contentService.Create("Microphone", parentId, "product");

        // Set the value of the property with alias 'category'
        demoProduct.SetValue("category" , "audio");

        // Set the value of the property with alias 'price'
        demoProduct.SetValue("price", "1500");

        // Save content first
        _contentService.Save(demoProduct);

        // Publish content
        var userId = -1; // -1 = system user
        _contentService.Publish(demoProduct, new[] { "*" }, userId); // use "*" for invariant content
    }
}
```

Publishing content programmatically

Last updated

Was this helpful?

Example on how to create and publish content programmatically using the `IContentService`.

Learn how to use the Content Service.

Creating content programmatically

In the example below, a new content item is programmatically created using the content service. It is assumed that there are two document types, namely *Catalogue* and *Product*. A new *Product* node will be created under the *Catalogue* page.

Create a new C# class file (for example, `MyProject/Services/PublishContentDemo.cs`

) inside your web project.

```
using Umbraco.Cms.Core.Models;
using Umbraco.Cms.Core.Services;

namespace Umbraco.Cms.Web.UI.Custom;

public class PublishContentDemo
{
    private readonly IContentService _contentService;

    public PublishContentDemo(IContentService contentService) => _contentService = contentService;

    public void Create()
    {
        // Create a variable for the GUID of the parent page - Catalogue, where you want to add a child item.
        var parentId = Guid.Parse("b6fbbb31-a77f-4f9c-85f7-2dc4835c7f31");

        // Create a new child item of type 'Product'
        var demoProduct = _contentService.Create("Microphone", parentId, "product");

        // Set the value of the property with alias 'category'
        demoProduct.SetValue("category" , "audio");

        // Set the value of the property with alias 'price'
        demoProduct.SetValue("price", "1500");

        // Save content first
        _contentService.Save(demoProduct);

        // Publish content
        var userId = -1; // -1 = system user
        _contentService.Publish(demoProduct, new[] { "*" }, userId); // use "*" for invariant content
    }
}
```

Always call `Save()`

before `Publish()`

, as publishing without saving first will not persist the changes.

In a multi-language setup, it is necessary to set the name of the content item for a specified culture:

For information on how to retrieve multilingual languages, see the [Retrieving languages](/umbraco-cms/reference/management/using-services/localizationservice) article.

Publishing content programmatically

The `IContentService`

is also used for publishing existing content. The following example shows how to publish a page and all its descendants.

Create a new C# class file (for example, `MyProject/Services/PublishBranchContentDemo.cs`

) inside your web project.

The `PublishBranchFilter`

option can include one or more of the following flags:

`Default`

- publishes only nodes with pending changes.`IncludeUnpublished`

- publishes unpublished content and existing nodes with pending changes.`ForceRepublish`

- republishes all nodes, even if unchanged.`All`

- combines`IncludeUnpublished`

and`ForceRepublish`

.For multilingual content, replace

`"*"`

with the array of cultures, for example,`new[] { "en-us", "da" }`.


Last updated

Was this helpful?

Was this helpful?

```
demoProduct.SetCultureName("Microphone", "en-us"); // this will set the english name
demoProduct.SetCultureName("Mikrofon", "da"); // this will set the danish name
```

```
using Umbraco.Cms.Core.Models;
using Umbraco.Cms.Core.Services;

namespace Umbraco.Cms.Web.UI.Custom;

public class PublishBranchContentDemo
{
    private readonly IContentService _contentService;

    public PublishBranchContentDemo(IContentService contentService) => _contentService = contentService;

    public void Publish(Guid key)
    {
        var parentKey = Guid.Parse("b6fbbb31-a77f-4f9c-85f7-2dc4835c7f31");

        var content = _contentService.GetById(key)
            ?? throw new InvalidOperationException($"Could not find content with key: {key}.");

        var userId = -1;
        _contentService.PublishBranch(content, PublishBranchFilter.Default, new[] { "*" }, userId);
    }
}
```

---

### Content Type Service | CMS

Examples on how to retrieve content types and content type containers using the ContentTypeService.

Getting a single content type

```
// Declare the GUID ID
Guid guid = new Guid("796a8d5c-b7bb-46d9-bc57-ab834d0d1248");

// Get a reference to the content type by its GUID ID
IContentType contentType = _contentTypeService.Get(guid);
```

```
// Get a reference to the content type by its numeric ID
IContentType contentType = _contentTypeService.Get(1234);
```

```
// Get a reference to the content type by its alias
IContentType contentType = _contentTypeService.Get("home");
```

Getting a list of content types

```
// Get a collection of all content types
IEnumerable<IContentType> contentTypes = _contentTypeService.GetAll();
```

Check whether a content type has children

Retrieving content type container

Getting a single content type container

Getting a list of content type containers

Last updated

Was this helpful?

---

### Localization Service | CMS

Example on how to retrieve languages using the LocalizationService.

Getting a single language

```
// Get a reference to the language by its ID
ILanguage language1 = _localizationService.GetLanguageById(1);
```

```
// Get a reference to the language by its ISO code
ILanguage language2 = _localizationService.GetLanguageByIsoCode("en-US");
```

Getting all languages

```
// Get a collection of all languages
IEnumerable<ILanguage> languages = _localizationService.GetAllLanguages();

// Iterate over the collection
foreach (ILanguage language in languages)
{
    // Get the .NET culture info
    CultureInfo cultureInfo = language.CultureInfo;

    <pre>ID: @language.Id</pre>
    <pre>Key: @language.Key</pre>
    <pre>Name: @language.CultureName</pre>
    <pre>ISO: @language.IsoCode</pre>
    <pre>Culture info: @cultureInfo</pre>
    <hr />
}
```

Full example

Last updated

Was this helpful?

---

### Media Service | CMS

Examples on how to create a new folder and a new media item from a stream by using the MediaService.

```
using Umbraco.Cms.Core;
using Umbraco.Cms.Core.IO;
using Umbraco.Cms.Core.Models;
using Umbraco.Cms.Core.PropertyEditors;
using Umbraco.Cms.Core.Services;
using Umbraco.Cms.Core.Strings;
using Umbraco.Extensions;
```

Creating a new folder

```
// Initialize a new media at the root of the media archive
IMedia folder = _mediaService.CreateMedia("Samples Media Item Folder", Constants.System.Root, Constants.Conventions.MediaTypes.Folder);

// Save the folder
var result = _mediaService.Save(folder);
```

```
// Initialize a new media at the root of the media archive
IMedia folder = _mediaService.CreateMedia("Samples Media Item Folder", -1, "Folder");

// Save the folder
var result = _mediaService.Save(folder);
```

Creating a new media item from a stream

Last updated

Was this helpful?

---

### Relation Service | CMS

Last updated

Was this helpful?

The `RelationService`

allows creating relations between objects that would otherwise have no obvious connection.

The following examples demonstrate how to use `RelationService`.


Automatically relate to the root node

To perform this task, implement a Notification Handler:

[Read more about composing Umbraco here](/umbraco-cms/implementation/composing).

```
using Umbraco.Cms.Core.Events;
using Umbraco.Cms.Core.Notifications;
using Umbraco.Cms.Core.Services;

namespace Doccers.Core.Components;

public class ContentPublishedNotificationHandler(IContentService contentService, IRelationService relationService) : INotificationHandler<ContentPublishedNotification>
{
    public void Handle(ContentPublishedNotification notification)
    {
        var home = contentService.GetRootContent().FirstOrDefault();
        if (home == null) return;

        // Get the relation type by alias
        var relationType = relationService.GetRelationTypeByAlias("homesick");

        if (relationType == null) return;

        foreach (var entity in notification.PublishedEntities
                     .Where(x => x.Id != home.Id))
        {
            // Check if they are already related
            if (!relationService.AreRelated(home.Id, entity.Id))
            {
                // If not then let us relate the current entity to home
                relationService.Relate(home.Id, entity.Id, relationType);
            }
        }
    }
}
```

To make Umbraco recognize the Notification Handler, register it in a composer:

After saving and publishing the `Products`

node, the following result is displayed:

The next step is to fetch the data from an API.

Note the `x => new Relation()`

expression. The returned data must be serializable, therefore the `Relation`

class is defined as follows:

Browsing `/umbraco/api/relations/getbyrelationtypealias?alias=homesick`

returns the following output:

When implementing similar functionality, consider wrapping a caching layer around it. The `RelationService`

queries the database directly.

Last updated

Was this helpful?

Was this helpful?

```
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.Notifications;

namespace Doccers.Core.Composers;

public class RelationComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.AddNotificationHandler<ContentPublishedNotification, ContentPublishedNotificationHandler>();
    }
}
```

```
using Microsoft.AspNetCore.Mvc;
using System.Runtime.Serialization;
using Umbraco.Cms.Core.Services;
using Umbraco.Cms.Web.Common;

namespace Doccers.Core.Controllers.Http;

[ApiController]
[Route("/umbraco/api/relations")]
public class RelationsController : Controller
{
    private readonly IRelationService _relationService;
    private readonly UmbracoHelper _umbracoHelper;

    public RelationsController(IRelationService relationService, UmbracoHelper umbracoHelper)
    {
        // Alternatively you could also access
        // the service via the service context:
        // _relationService = Services.RelationService;
        _relationService = relationService;
        _umbracoHelper = umbracoHelper;
    }

    [HttpGet("getbyrelationtypealias")]
    public IActionResult GetByRelationTypeAlias(string alias)
    {
        var relationType = _relationService.GetRelationTypeByAlias(alias);
        if (relationType == null)
            return BadRequest("Invalid relation type alias");

        var relations = _relationService.GetAllRelationsByRelationType(relationType.Id);
        var content = relations.Select(x => _umbracoHelper.Content(x.ChildId))
            .Select(x => new Relation()
            {
                Name = x.Name,
                UpdateDate = x.UpdateDate
            });

        return Ok(content);
    }
}
```

```
[DataContract(Name = "relation")]
public class Relation
{
    [DataMember(Name = "name")]
    public string Name { get; set; }

    [DataMember(Name = "updateDate")]
    public DateTime UpdateDate { get; set; }
}
```

---

### User Service | CMS

This will show you how to perform various User management using the Umbraco service layer.

Last updated

Was this helpful?

This will show you how to perform various User management using the Umbraco service layer.

Learn how to use the User Service to manage the users on your Umbraco project.

Assigning a User to a User Group

To assign a User to a User Group, we need both the `IUserService`

and `IUserGroupService`

. As with all Umbraco services, these are obtained using dependency injection.

Start by defining an interface for our implementation:


ISampleUserHandler.cs

```
namespace UmbracoDocs.Samples;

public interface ISampleUserHandler
{
    Task<bool> AssignUserToAdminGroup(string email, Guid performingUserKey);
}
```

Next we implement the interface. This implementation holds the dependency to the Umbraco services:


SampleUserHandler.cs

```
using Umbraco.Cms.Core;
using Umbraco.Cms.Core.Models;
using Umbraco.Cms.Core.Models.Membership;
using Umbraco.Cms.Core.Services;
using Umbraco.Cms.Core.Services.OperationStatus;

namespace UmbracoDocs.Samples;

public class SampleUserHandler : ISampleUserHandler
{
    private readonly IUserService _userService;
    private readonly IUserGroupService _userGroupService;

    public SampleUserHandler(IUserService userService, IUserGroupService userGroupService)
    {
        _userService = userService;
        _userGroupService = userGroupService;
    }

    public async Task<bool> AssignUserToAdminGroup(string email, Guid performingUserKey)
    {
        IUser? user = _userService.GetByEmail(email);
        if (user is null)
        {
            return false;
        }

        Attempt<UserGroupOperationStatus> result = await _userGroupService.AddUsersToUserGroupAsync(
            new UsersToUserGroupManipulationModel(Constants.Security.AdminGroupKey, [user.Key]),
            performingUserKey
        );

        return result.Success;
    }
}
```

Register the implementation in a Composer:


Lastly, we need to put our implementation to use. This could be done in a Management API controller:


Last updated

Was this helpful?

Was this helpful?

SampleUserHandlerComposer.cs

```
using Umbraco.Cms.Core.Composing;

namespace UmbracoDocs.Samples;

public class SampleUserHandlerComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
        => builder.Services.AddSingleton<ISampleUserHandler, SampleUserHandler>();
}
```

SampleUserController.cs

```
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Api.Management.Controllers;
using Umbraco.Cms.Api.Management.Routing;
using Umbraco.Cms.Core.Security;

namespace UmbracoDocs.Samples;

[ApiExplorerSettings(GroupName = "Sample user handler")]
[VersionedApiBackOfficeRoute("sample/user-handler")]
public class SampleUserController : ManagementApiControllerBase
{
    private readonly ISampleUserHandler _sampleUserHandler;
    private readonly IBackOfficeSecurityAccessor _backOfficeSecurityAccessor;

    public SampleUserController(
        ISampleUserHandler sampleUserHandler,
        IBackOfficeSecurityAccessor backOfficeSecurityAccessor)
    {
        _sampleUserHandler = sampleUserHandler;
        _backOfficeSecurityAccessor = backOfficeSecurityAccessor;
    }

    [HttpPut]
    [ProducesResponseType(StatusCodes.Status200OK)]
    [ProducesResponseType(StatusCodes.Status400BadRequest)]
    public async Task<IActionResult> AssignUserToAdminGroup(string email)
        => await _sampleUserHandler.AssignUserToAdminGroup(email, CurrentUserKey(_backOfficeSecurityAccessor))
            ? Ok()
            : BadRequest();
}
```

---

---
