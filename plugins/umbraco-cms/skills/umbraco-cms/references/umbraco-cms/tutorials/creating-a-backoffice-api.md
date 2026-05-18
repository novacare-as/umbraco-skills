# Creating A Backoffice Api

## Contents

- [Access policies | CMS](#access-policies-cms)
- [Adding a custom Swagger document | CMS](#adding-a-custom-swagger-document-cms)
- [Documenting your controllers | CMS](#documenting-your-controllers-cms)
- [Polymorphic output in the Management API | CMS](#polymorphic-output-in-the-management-api-cms)
- [Umbraco schema and operation IDs | CMS](#umbraco-schema-and-operation-ids-cms)
- [Versioning your API | CMS](#versioning-your-api-cms)

---

## Access policies | CMS

How to apply access policies for Management APIs

Built-in access policies

```
using Umbraco.Cms.Web.Common.Authorization;...

[Authorize(AuthorizationPolicies.SectionAccessContent)]
public class MyItemApiController : ManagementApiControllerBase
```

Custom access policies

```
public class SampleCustomPolicyComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
        => builder.Services.AddAuthorization(options =>
            options.AddPolicy(SiteConstants.CustomPolicyName, policy =>
            {
                policy.AuthenticationSchemes.Add(OpenIddictValidationAspNetCoreDefaults.AuthenticationScheme);
                policy.RequireRole(SiteConstants.CustomGroupAlias);
                policy.RequireRole(Constants.Security.AdminGroupAlias);
            })
        );
}
```

Last updated

Was this helpful?

How to apply access policies for Management APIs

A Management API is by default available to any authorized Umbraco backoffice user.

To further restrict access we can apply access policies using the `[Authorize]`

attribute.

Built-in access policies

Umbraco maintains a set of built-in access policies we can leverage in our own APIs. The policy names are defined in `Umbraco.Cms.Web.Common.Authorization.AuthorizationPolicies`.


For example, the following makes the API accessible only to users with Content section access:

MyItemApiController.cs

```
using Umbraco.Cms.Web.Common.Authorization;...

[Authorize(AuthorizationPolicies.SectionAccessContent)]
public class MyItemApiController : ManagementApiControllerBase
```

Custom access policies

We can also define our own access policies. Custom access policies are a great way of keeping access control in sync across multiple endpoints, as projects evolve over time.

A custom access policy is defined by means of composition.

The following access policy definition requires the user to be a member of both the Umbraco Administrators group and a custom defined group:

SampleCustomPolicyComposer.cs

```
public class SampleCustomPolicyComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
        => builder.Services.AddAuthorization(options =>
            options.AddPolicy(SiteConstants.CustomPolicyName, policy =>
            {
                policy.AuthenticationSchemes.Add(OpenIddictValidationAspNetCoreDefaults.AuthenticationScheme);
                policy.RequireRole(SiteConstants.CustomGroupAlias);
                policy.RequireRole(Constants.Security.AdminGroupAlias);
            })
        );
}
```

With the policy defined, we can apply it to the API controller:

Last updated

Was this helpful?

Was this helpful?

SiteConstants.cs

```
public static class SiteConstants
{
    public const string CustomPolicyName = "Site.CustomPolicy";

    public const string CustomGroupAlias = "customGroup";
}
```

MyItemApiController.cs

```
[Authorize(SiteConstants.CustomPolicyName)]
public class MyItemApiController : ManagementApiControllerBase
```

---

## Adding a custom Swagger document | CMS

Adding a custom Swagger document for a custom Management API

```
using Microsoft.Extensions.Options;
using Microsoft.OpenApi.Models;
using Swashbuckle.AspNetCore.SwaggerGen;
using Umbraco.Cms.Api.Management.OpenApi;
using Umbraco.Cms.Core.Composing;

namespace UmbracoDocs.Samples;

public class MyItemApiComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.Services.ConfigureOptions<MyItemApiSwaggerGenOptions>();
    }
}

public class MyItemApiSwaggerGenOptions : IConfigureOptions<SwaggerGenOptions>
{
    public void Configure(SwaggerGenOptions options)
    {
        // register the custom Swagger document "my-item-api"
        options.SwaggerDoc(
            "my-item-api",
            new OpenApiInfo { Title = "My item API", Version = "1.0" }
        );

        // enable Umbraco authentication for the "my-item-api" Swagger document
        options.OperationFilter<MyItemApiOperationSecurityFilter>();
    }
}

public class MyItemApiOperationSecurityFilter : BackOfficeSecurityRequirementsOperationFilterBase
{
    protected override string ApiName => "my-item-api";
}
```

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7926fe84e622f94b94bee44d6b738d9ce822d8a7%252Fmy-item-api-swagger-ui.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fdcc90df&sv=2)

Last updated

Was this helpful?

Adding a custom Swagger document for a custom Management API

By default, all controllers based on ManagementApiControllerBase will be included in the default Management API Swagger document.

When building custom Management API controllers, sometimes it's preferable to have a dedicated Swagger document for them. Doing so is a three-step process:

Register the Swagger document with Swagger UI.

Instruct Swagger UI to utilize Umbraco authentication for the Swagger document.

Move the controllers to the Swagger document.


The following code exemplifies how to achieve the first two steps;

MyItemApiComposer.cs

```
using Microsoft.Extensions.Options;
using Microsoft.OpenApi.Models;
using Swashbuckle.AspNetCore.SwaggerGen;
using Umbraco.Cms.Api.Management.OpenApi;
using Umbraco.Cms.Core.Composing;

namespace UmbracoDocs.Samples;

public class MyItemApiComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.Services.ConfigureOptions<MyItemApiSwaggerGenOptions>();
    }
}

public class MyItemApiSwaggerGenOptions : IConfigureOptions<SwaggerGenOptions>
{
    public void Configure(SwaggerGenOptions options)
    {
        // register the custom Swagger document "my-item-api"
        options.SwaggerDoc(
            "my-item-api",
            new OpenApiInfo { Title = "My item API", Version = "1.0" }
        );

        // enable Umbraco authentication for the "my-item-api" Swagger document
        options.OperationFilter<MyItemApiOperationSecurityFilter>();
    }
}

public class MyItemApiOperationSecurityFilter : BackOfficeSecurityRequirementsOperationFilterBase
{
    protected override string ApiName => "my-item-api";
}
```

With this in place, the last step is to annotate the relevant API controllers with the MapToApi attribute:

Now when we visit the Swagger UI, "My item API" has its own Swagger document:

Swagger UI sometimes has persistent caching, which can prevent the new definition from appearing immediately. If this happens, disable caching in the **Network** tab of your browser's developer tools.

Last updated

Was this helpful?

Was this helpful?

MyItemApiController.cs

```
[MapToApi("my-item-api")]
public class MyItemApiController : ManagementApiControllerBase
```

---

## Documenting your controllers | CMS

ApiExplorerSettings

```
[ApiExplorerSettings(GroupName = "My item API")]
public class MyItemApiController : ManagementApiControllerBase
```

ProducesResponseType Attribute

```
[HttpGet("{id:guid}")]
[ProducesResponseType<MyItem>(StatusCodes.Status200OK)]
[ProducesResponseType<ProblemDetails>(StatusCodes.Status404NotFound)]
public IActionResult GetItem(Guid id)
{
// Method implementation
}
```

Example Documentation for Each Controller Method

GetAllItems

GetItem

CreateItem

UpdateItem

DeleteItem

Verifying the changes

Last updated

Was this helpful?

---

## Polymorphic output in the Management API | CMS

How to support polymorphic outputs from custom Management APIs

Polymorphism by interface

```
public interface IMyItem
{
    Guid Id { get; }

    string Value { get; set; }
}
```

```
public class MyItem(string value) : IMyItem
{
    public Guid Id { get; } = Guid.NewGuid();

    public string Value { get; set; } = value;
}
```

```
public class MyOtherItem(string value, int otherValue) : IMyItem
{
    public Guid Id { get; } = Guid.NewGuid();

    public string Value { get; set; } = value;

    public int OtherValue { get; } = otherValue;
}
```

Polymorphism by annotation

Last updated

Was this helpful?

---

## Umbraco schema and operation IDs | CMS

How to apply the Umbraco schema and operation IDs for custom Management APIs

Last updated

Was this helpful?

How to apply the Umbraco schema and operation IDs for custom Management APIs

All core Management APIs have a custom scheme for their generated OpenAPI schema and operation IDs.

This scheme is strictly opt-in to avoid affecting custom APIs by default. In this article, we'll see how to opt-in to the scheme.

If you are happy with your APIs' default schema and operation IDs, nothing is likely gained by using the Umbraco ones.

Schema IDs

Schema IDs are handled by `ISchemaIdHandler`

implementations. To opt-in to the Umbraco schema IDs, we base our implementation on the core handler:

SampleSchemaIdHandler.cs

```
using Umbraco.Cms.Api.Common.OpenApi;

namespace UmbracoDocs.Samples;

// this schema ID handler extends the Umbraco schema IDs
// to all types in the UmbracoDocs.Samples namespace
public class SampleSchemaIdHandler : SchemaIdHandler
{
    public override bool CanHandle(Type type)
        => type.Namespace == "UmbracoDocs.Samples";
}
```

Then, we implement a composer to register the new schema ID handler:

SampleSchemaIdComposer.cs

```
using Umbraco.Cms.Api.Common.OpenApi;
using Umbraco.Cms.Core.Composing;

namespace UmbracoDocs.Samples;

public class SampleSchemaIdComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
        =>  builder.Services.AddSingleton<ISchemaIdHandler, SampleSchemaIdHandler>();
}
```

Operation IDs

Operation IDs follow the same pattern as schema IDs. The only difference is that the `IOperationIdHandler`

operates at the API level, not at the type level.

Again, to opt-in to the Umbraco operation IDs, we base our implementation on the core handler:

Then, we implement a composer to register the new operation ID handler:

Last updated

Was this helpful?

Was this helpful?

SampleOperationIdHandler.cs

```
using Asp.Versioning;
using Microsoft.AspNetCore.Mvc.ApiExplorer;
using Microsoft.AspNetCore.Mvc.Controllers;
using Microsoft.Extensions.Options;
using Umbraco.Cms.Api.Common.OpenApi;

namespace UmbracoDocs.Samples;

// this operation ID handler extends the Umbraco operation IDs
// to all API controllers in the UmbracoDocs.Samples namespace
public class SampleOperationIdHandler : OperationIdHandler
{
    public SampleOperationIdHandler(IOptions<ApiVersioningOptions> apiVersioningOptions)
        : base(apiVersioningOptions)
    {
    }

    protected override bool CanHandle(ApiDescription apiDescription, ControllerActionDescriptor controllerActionDescriptor)
        => controllerActionDescriptor.ControllerTypeInfo.Namespace == "UmbracoDocs.Samples";
}
```

SampleOperationIdComposer.cs

```
using Umbraco.Cms.Api.Common.OpenApi;
using Umbraco.Cms.Core.Composing;

namespace UmbracoDocs.Samples;

public class SampleOperationIdComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
        =>  builder.Services.AddSingleton<IOperationIdHandler, SampleOperationIdHandler>();
}
```

---

## Versioning your API | CMS

Adding new versions of custom Management APIs

All APIs register as version 1.0 by default, which means their endpoints are routed under `/umbraco/management/api/v1/`.


As projects evolve, adding new versions of your APIs sometimes becomes necessary. Multiple versions of the same API can co-exist to retain backward compatibility.

APIs are versioned using attribute annotation:

`[ApiVersion]`

attributes on the API controllers.`[MapToApiVersion]`

attributes on the API controller actions.

It is recommended to annotate *all* API controller actions, as well as the version 1.0 actions.

Using the API controller from the [Creating your own API article](/umbraco-cms/tutorials/creating-a-backoffice-api) as an example, we can add version 2.0 implementations of select actions:

```
[ApiVersion("1.0")]
[ApiVersion("2.0")]
public class MyItemApiController : ManagementApiControllerBase
{
    [HttpGet]
    [MapToApiVersion("1.0")]
    public IActionResult GetAllItems(int skip = 0, int take = 10)
    {
        // ...
    }

    [HttpGet("{id:guid}")]
    [MapToApiVersion("1.0")]
    public IActionResult GetItem(Guid id)
    {
        // ...
    }

    [HttpPost]
    [MapToApiVersion("1.0")]
    public IActionResult CreateItem(string value)
    {
        // ...
    }

    [HttpPut("{id:guid}")]
    [MapToApiVersion("1.0")]
    public IActionResult UpdateItem(Guid id, string value)
    {
        // ...
    }

    [HttpDelete("{id:guid}")]
    [MapToApiVersion("1.0")]
    public IActionResult DeleteItem(Guid id)
    {
        // ...
    }

    [HttpGet("{id:guid}")]
    [MapToApiVersion("2.0")]
    public IActionResult GetItemV2(Guid id)
    {
        MyItem? item = AllItems.FirstOrDefault(item => item.Id == id);

        return item is not null
            ? Ok(item)
            : OperationStatusResult(
                MyItemOperationStatus.NotFound,
                builder => NotFound(
                    builder
                        .WithTitle("The item was not found")
                        .WithDetail("The item with the given ID did not exist.")
                        .Build()
                )
            );
    }

    [HttpPost]
    [MapToApiVersion("2.0")]
    public IActionResult CreateItemV2(string value)
    {
        var newItem = new MyItem(value);
        AllItems.Add(newItem);
        return CreatedAtId<MyItemApiController>(
            ctrl => nameof(ctrl.GetItemV2),
            newItem.Id
        );
    }
}
```

Version 2.0 of the "get" and "create" endpoints - `GetItemV2`

and `CreateItemV2`

respectively, are added with the code above. The rest of the endpoints remain version 1.0 only.

The version 2.0 endpoints are routed under `/umbraco/management/api/v2/`.


In the example above, the version 2.0 actions are added to the same API controller as their version 1.0 counterparts. If you prefer, they can be added to a new API controller instead. This will leave you with separate API controllers, one for each version of the API. See the examples below:

With the version 1.0 actions added in a controller sampled above, the version 2.0 actions are added in a new controller, as shown below.

While perhaps tempting, do *not* name your API controller `V2`

- e.g. `MyItemApiVersionV2`

. Due to an upstream issue in the API versioning system, this will currently cause routing issues in certain scenarios.

Last updated

Was this helpful?

---
