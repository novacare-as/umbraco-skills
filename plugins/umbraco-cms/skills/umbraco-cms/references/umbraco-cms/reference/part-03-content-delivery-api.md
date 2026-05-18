# Content Delivery Api

## Content Delivery Api

### Contents

- [Additional preview environments support | CMS](#additional-preview-environments-support-cms)
- [Custom Delivery API endpoints | CMS](#custom-delivery-api-endpoints-cms)
- [Custom property editors support | CMS](#custom-property-editors-support-cms)
- [Extension API for querying | CMS](#extension-api-for-querying-cms)
- [Media Delivery API | CMS](#media-delivery-api-cms)
- [Output caching | CMS](#output-caching-cms)
- [Property expansion and limiting | CMS](#property-expansion-and-limiting-cms)
- [Protected content in the Delivery API | CMS](#protected-content-in-the-delivery-api-cms)

---

### Additional preview environments support | CMS

Configure custom preview URLs to provide editors with seamless access to external preview environments for the Content Delivery API data.

Server-side implementation

```
using Umbraco.Cms.Core.Models;
using Umbraco.Cms.Core.Models.PublishedContent;
using Umbraco.Cms.Core.Routing;

namespace My.Site;

public class MyUrlProvider : IUrlProvider
{
    public string Alias => "MyUrlProvider";

    public UrlInfo? GetUrl(IPublishedContent content, UrlMode mode, string? culture, Uri current)
        => null;

    public IEnumerable<UrlInfo> GetOtherUrls(int id, Uri current)
        => [];

    public async Task<UrlInfo?> GetPreviewUrlAsync(IContent content, string? culture, string? segment)
    {
        var token = await GetPreviewTokenAsync();
        return new UrlInfo(
                url: new Uri($"https://my.preview.environment/?id={content.Key}&culture={culture}&token={token}"),
                provider: Alias,
                culture: culture,
                message: null,
                isExternal: true);
    }

    private async Task<string> GetPreviewTokenAsync()
    {
        // this is where you'll perform auth against the external preview environment and return an auth token
    }
}
```

Client-side implementation

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7843053e0aa6847b926a2e5ca30a10ac7f1da64e%252Fexternal-preview-option.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7ec9eaa0&sv=2)

Last updated

Was this helpful?

---

### Custom Delivery API endpoints | CMS

Implementing custom Delivery API endpoints.

Sometimes it can be useful to extend the Delivery API with custom endpoints.

At its core, a custom Delivery API endpoint is no different from an ordinary an API controller. However, there are a few tricks that can make your own endpoints feel more like part of the native Delivery API. These include:

Consistent JSON serialization.

Matching routing schemes.

Swagger documentation.

Authentication.

Respecting the configured Delivery API access rules.


In this article you'll find snippets and examples to get you started.

Here is a basic example of a Delivery API endpoint:

```
using Asp.Versioning;
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Api.Delivery.Controllers;
using Umbraco.Cms.Api.Delivery.Filters;
using Umbraco.Cms.Api.Delivery.Routing;

namespace Umbraco.Docs;

[ApiVersion("2.0")]
[VersionedDeliveryApiRoute("custom")]
[ApiExplorerSettings(GroupName = "Custom")]
[DeliveryApiAccess]
public class BasicDeliveryApiController : DeliveryApiControllerBase
{
    [HttpGet("basic-api")]
    [MapToApiVersion("2.0")]
    [ProducesResponseType(typeof(int), StatusCodes.Status200OK)]
    [ProducesResponseType(StatusCodes.Status401Unauthorized)]
    [ProducesResponseType(StatusCodes.Status403Forbidden)]
    public IActionResult Get() => Ok(123);
}
```

Since a lot is happening above, you can explore the following sections to understand the implementations and attributes.

Implementing the `DeliveryApiControllerBase`

ensures that:

The endpoint is automatically included in the Swagger documentation for the Delivery API.

The endpoint respects the JSON serialization scheme for the entire Delivery API.


There are also a few attributes applied to the endpoint:

The

`ApiVersion`

and`MapToApiVersion`

attributes match the endpoint version to the current Delivery API version.The

`VersionedDeliveryApiRoute`

attribute ensures that the endpoint routing matches that of the Delivery API.The

`ApiExplorerSettings`

attribute adds the endpoint to a custom group in the Swagger documentation.The

`DeliveryApiAccess`

attribute ensures that this endpoint can only be invoked if the Content Delivery API is[enabled](/umbraco-cms/reference/content-delivery-api#enable-the-content-delivery-api).The

`ProducesResponseType`

attributes help the Swagger documentation understand the endpoint.

`DeliveryApiAccess`

also comes in a specific version for the [Media Delivery API](/umbraco-cms/reference/content-delivery-api/media-delivery-api) - the `DeliveryApiMediaAccess`

attribute.

If your custom Delivery API endpoint outputs content, you will likely find `ContentApiControllerBase`

a better fit as a base class. Here is an example of how to use it:

This endpoint does not require the `DeliveryApiAccess`

attribute, because it is already defined on the base class.

The `ContentApiControllerBase`

adds a lot of functionality to your custom endpoint, including:

Basic request validation.

Variance context for requests.

Delivery API

[output caching](/umbraco-cms/reference/content-delivery-api/output-caching), including the appropriate`Vary`

response headers.Comprehensive Swagger documentation for .


The base class also gives convenient access to:

The

`IApiPublishedContentCache`

, a specialized content cache tailored for the Delivery API. Among other things, it enforces the configuration of[(dis)allowed output types](/umbraco-cms/reference/content-delivery-api#additional-configuration).The

`IApiContentResponseBuilder`

for generating a content response format that conforms with the Delivery API. This includes support for property expansion and limiting.

Similarly to content, a base class also exists for media endpoints; the `MediaApiControllerBase`

. This base class provides much of the same functionality as the corresponding base class for content.

Here's an example of how to use the `MediaApiControllerBase`:


Last updated

Was this helpful?

---

### Custom property editors support | CMS

Customize the Content Delivery API's response for custom property editors.

Out of the box, the Delivery API supports custom property editors, ensuring they are rendered alongside the built-in ones in Umbraco. However, if the output generated by a property editor isn't optimal for a headless context, developers can customize the API response. This customization won't impact the Razor rendering, allowing developers to tailor the Content Delivery API response according to their specific requirements.

This article discusses how to work with the `IDeliveryApiPropertyValueConverter`

interface and implement custom [property expansion](/umbraco-cms/reference/content-delivery-api/property-expansion-and-limiting) for custom property editors.

The examples in this article revolve around the fictional `My.Custom.Picker`

property editor. This property editor stores the key of a single content item and is backed by a property value converter.

This article will not dive into the details of creating a custom property editor for Umbraco. Guidance on that can be found in these articles: [Creating a Property Editor](/umbraco-cms/tutorials/creating-a-property-editor) and [Property Value Converters](/umbraco-cms/customizing/property-editors/property-value-converters).

To customize the output of a property value editor in the Delivery API, opt-in by implementing the `IDeliveryApiPropertyValueConverter`

interface.

The code example below showcases the implementation of this interface in the property value converter for `My.Custom.Picker`

. These code samples focus on the methods provided by the `IDeliveryApiPropertyValueConverter`

, which are responsible for customizing the Delivery API response.

Response model classes can be found near the end of this article.

The `IsConverter()`

and `GetPropertyValueType()`

methods are inherited from the `PropertyValueConverterBase`

class, which is covered in the [Property Value Converters](/umbraco-cms/customizing/property-editors/property-value-converters) article.

```
using Umbraco.Cms.Core.DeliveryApi;
using Umbraco.Cms.Core.Models.DeliveryApi;
using Umbraco.Cms.Core.Models.PublishedContent;
using Umbraco.Cms.Core.PropertyEditors;
using Umbraco.Cms.Core.PropertyEditors.DeliveryApi;
using Umbraco.Cms.Core.PublishedCache;

public class MyCustomPickerValueConverter(
    IPublishedContentCache publishedContentCache, 
    IApiContentRouteBuilder apiContentRouteBuilder): 
    PropertyValueConverterBase, IDeliveryApiPropertyValueConverter
{
    public override bool IsConverter(IPublishedPropertyType propertyType)
        => propertyType.EditorAlias.Equals("My.Custom.Picker");

    public override Type GetPropertyValueType(IPublishedPropertyType propertyType)
        => typeof(Guid?);

    public PropertyCacheLevel GetDeliveryApiPropertyCacheLevel(IPublishedPropertyType propertyType)
        => PropertyCacheLevel.Elements;

    public PropertyCacheLevel GetDeliveryApiPropertyCacheLevelForExpansion(IPublishedPropertyType propertyType)
        => PropertyCacheLevel.Snapshot;

    public Type GetDeliveryApiPropertyValueType(IPublishedPropertyType propertyType)
        => typeof(DeliveryApiCustomPicker);

    public object? ConvertIntermediateToDeliveryApiObject(
        IPublishedElement owner,
        IPublishedPropertyType propertyType,
        PropertyCacheLevel referenceCacheLevel,
        object? inter,
        bool preview,
        bool expanding)
    {
        if (inter is null)
        {
            return null;
        }

        return BuildDeliveryApiCustomPicker(inter, expanding);
    }

    private DeliveryApiCustomPicker? BuildDeliveryApiCustomPicker(object inter, bool expanding)
    {
        if (!Guid.TryParse(inter as string, out Guid id))
        {
            return null;
        }
        
        var content = publishedContentCache.GetById(id);

        if (content is null)
        {
            return null;
        }
        
        return new DeliveryApiCustomPicker { Id = id };
    }
}
```

Umbraco developers need to inject `IPublishedContentCache`

, `IPublishedMediaCache`

, `IPublishedMemberCache`

, and `IPublishedContentTypeCache`

individually, instead of injecting the `IPublishedSnapshotAccessor`

as in previous versions.

The Implementation of the `IDeliveryApiPropertyValueConverter`

interface can be found in the following methods:

`GetDeliveryApiPropertyCacheLevel()`

: This method specifies the cache level used for our property representation in the Delivery API response.`GetDeliveryApiPropertyCacheLevelForExpansion()`

: This method specifies the cache level used for our property representation in the Delivery API response when[property expansion](/umbraco-cms/reference/content-delivery-api/property-expansion-and-limiting)is applied.`GetDeliveryApiPropertyValueType()`

: This method defines the value type of the custom property output for the Delivery API response.`ConvertIntermediateToDeliveryApiObject()`

: This method converts the value from the property editor to the desired custom object in a headless context.

In the given example, the content key (`Guid`

value) is used when rendering with Razor. This is sufficient because Razor provides full access to the published content within the rendering context. In a headless context, we do not have the same access. To prevent subsequent round-trips to the server, we create a richer output model specifically for the Delivery API.

The following example request shows how our custom implementation is reflected in the resulting API response. In this case, our custom property editor is configured under the alias `"pickedItem"`.


**Sample Request**

**Sample Response**

Property expansion allows developers to conditionally add another level of detail to the Delivery API output. Usually, these additional details are "expensive" to retrieve (for example, requiring database access to populate). By applying property expansion, Umbraco developers provide the option for the caller of the API to opt-in explicitly to this "expensive" operation. From the caller's perspective, the alternative might be an even more expensive additional round-trip to the server.

In this example, property expansion is implemented within `ConvertIntermediateToDeliveryApiObject()`

. By considering the value of the `expanding`

parameter, the `BuildDeliveryApiCustomPicker()`

method can be modified as follows:

If the `expanding`

parameter is `false`

, the method returns the same shallow representation of the referenced content item as before. Otherwise, retrieve the corresponding `IPublishedContent`

and construct the response object accordingly.

To see the expanded output in the API response, add the `expand`

query parameter to the request. This parameter can be applied using either `?expand=properties[$all]`

to expand all properties or `?expand=properties[pickedItem]`

to expand the specific `'pickedItem'`

property.

**Sample Request**

**Sample Response**

The `itemDetails`

property of the `pickedItem`

in the JSON response contains the additional details of the selected content item.

Last updated

Was this helpful?

---

### Extension API for querying | CMS

Learn how to extend the Content Delivery API with custom selecting, filtering, and sorting options for the multi-item-based endpoint.

The Delivery API allows you to retrieve multiple items by utilizing the `/umbraco/delivery/api/v2/content`

endpoint. With the built-in query parameters, you have the flexibility to get any number of content nodes based on your needs. For a comprehensive list of supported query options, refer to the [Endpoints](/umbraco-cms/reference/content-delivery-api#endpoints) section.

For the query endpoint, we have created a new Examine index (*DeliveryApiContentIndex*) that facilitates fast retrieval of the desired content. This index ensures quick indexing and searching of data, with the possibility for future extensions.

In this article, we'll explore creating custom selecting, filtering, and sorting options to enhance the querying capabilities of the Delivery API.

Let's take a look at an example of using the query endpoint with query parameters for `fetch`

, `filter`

, and `sort`

. A request might look like this:

```
GET /umbraco/delivery/api/v2/content?fetch=xxx&filter=yyy&filter=zzz&sort=aaa&sort=bbb
```

The placeholders in the example (`xxx`

, `yyy`

, etc.) represent the values that each query option evaluates in order to determine the suitable query handler.

You can include only one `fetch`

parameter, while multiple `filter`

and `sort`

parameters are allowed. Additionally, the order of the `sort`

parameters influences the sorting behaviour. Refer to the [Query parameters](/umbraco-cms/reference/content-delivery-api#query-parameters) section for the currently supported options.

The implementation of each querying option consists of a class for indexing the data into the *DeliveryApiContentIndex* and another one for handling the query. By implementing the `IContentIndexHandler`

interface, you can control how your relevant data is indexed and made available for querying through our index. And you can customize the querying behaviour to suit your needs by implementing the `ISelectorHandler`

, `IFilterHandler`

, and `ISortHandler`

interfaces.

In the following sections, we will explore the implementation details of creating custom querying functionality for the Delivery API.

Selectors handle the `fetch`

part of a query.

To showcase how to build a custom selector, consider a site structure with a few blog posts. A post is linked to an author, which is another content item.

Authors can be marked as *'Featured'* using a toggle, granting them additional visibility and recognition. We will use this marker as part of the indexing implementation for our selector option.

The following example demonstrates the implementation of an `AuthorSelector`

, which allows you to customize the querying behaviour specifically for finding all featured authors. This class contains both indexing and querying responsibilities. However, keep in mind that it is generally recommended to separate these responsibilities into dedicated classes.

The `AuthorSelector`

class implements the `ISelectorHandler`

and `IContentIndexHandler`

interfaces.

`ISelectorHandler`

allows for handling the `fetch`

value in API queries through the `CanHandle()`

and `BuildSelectorOption()`

methods.

`CanHandle()`

determines if the given`fetch`

query corresponds to the`"featuredAuthors"`

value.`BuildSelectorOption()`

constructs the selector option to search for authors with a positive value (for example,`"y"`

) in a`"featured"`

index field.

The `GetFields()`

and `GetFieldValues()`

methods each play a role in defining how the data should be indexed and made searchable.

`GetFields()`

defines the behaviour of fields that are added to the index. In this example, the`"featured"`

field is added as a "raw" string for efficient and accurate searching.`GetFieldValues()`

is responsible for retrieving the values of the defined index fields. In this case, the`"featured"`

field of content items of type`"author"`

. It creates an`IndexFieldValue`

with the appropriate field value (`"y"`

for featured,`"n"`

otherwise), which will be added to the index.

Since our custom query option modifies the index structure, we will need to rebuild the *DeliveryApiContentIndex*. You can find it by navigating to the "Examine Management" dashboard in the "Settings" section. Once rebuilt, we can make a request to the Delivery API query endpoint as follows:

**Request**

**Response**

Filters handle the `filter`

part of a query.

Staying within the topic of blog posts and their authors, we will create a custom filter to find posts by specific author(s).

This filter allows specifying the desired author(s) by their key (`Guid`

) in an `author:`

filter option. Multiple authors can be included by listing their keys as comma-separated-values, like:

**Request**

The response will include the blog posts associated with the provided authors, enabling us to retrieve only the relevant results from the API.

**Response**

Our filter implementation follows a similar structure to the custom selector we discussed earlier. We continue to utilize the `IContentIndexHandler`

interface, but this time we introduce the `IFilterHandler`

. This combination gives us flexibility and control over the filtering behaviour.

The procedure remains the same - we store and query the author key in a new `"authorId"`

field within the index. Consequently, we will need to rebuild the index to reflect the changes.

To illustrate the implementation, consider the following code example:

The principal difference from the selector is that the filter implements `BuildFilterOption()`

instead of `BuildSelectorOption()`

. Here, the filter performs an exact match for any specified `Guid`

in the query. Efficiently, this makes the filter perform an `OR`

operation against the index.

Since we need to perform an exact match, the index field (`authorId`

) is once again defined as a "raw" string. Other options include "analyzed" and "sortable" strings. These support "contains" searches and alpha-numeric sorting, respectively.

When implementing a filter, you can use the following operators: `Is`

, `IsNot`

, `Contains`

, `DoesNotContain`

, `GreaterThan`

, `GreaterThanOrEqual`

, `LessThan`

and `LessThanOrEqual`.


The range operators (*the latter four*) only work with number and date fields - `FieldType.Number`

and `FieldType.Date`

respectively.

It is possible to pass multiple values to each operator, and these values will be treated inclusively as an **or** operator. For example, if `tag1`

and `tag2`

were passed into a filter using the `Is`

operator, *any* document containing **either** `tag1`

**or** `tag2`

would return. The request for this might look like this:

If you require this functionality to be restrictive i.e. `tag1`

**and** `tag2`

, then the current approach would be to chain the custom filter. The request would change to look more like this:

Finally, we can also add custom handling for the `sort`

part of the query.

We'll add a custom sort handler that allows us to sort blog posts based on a custom `"publishDate"`

Date Picker property. The implementation will allow for sorting the posts in ascending or descending order.

This sorting should only be used with query results that have a published date to ensure accurate results.

To demonstrate this, consider the following implementation example:

The implementation follows the same structure as the other examples, defined by the `IContentIndexHandler`

and `ISortHandler`

interfaces.

One point to highlight is that we store the `"publishDate"`

value as a "date" field in the index, which allows for correct date sorting.

Once more, when adding fields to the index, we need to rebuild it to reflect the changes.

In the following example request, we also apply the author filter to retrieve only `"blogpost"`

content nodes, which we know have the `"publishDate"`

field.

**Request**

**Response**

Last updated

Was this helpful?

---

### Media Delivery API | CMS

Using the Media Delivery API.

Getting Started

```
{
    "Umbraco": {
        "CMS": {
            "DeliveryApi": {
                "Enabled": true,
                "PublicAccess": true,
                "Media": {
                    "Enabled": true,
                    "PublicAccess": false
                }
            }
        }
    }
}
```

Endpoints

Gets a media item by id

Path Parameters

| Name | Type | Description |
|---|---|---|
| id* | String | GUID of the media item |

Query Parameters

| Name | Type | Description |
|---|---|---|
| expand | String | Which properties to expand in the response |
| fields | String | Which properties to include in the response (by default all properties are included) |

Headers

| Name | Type | Description |
|---|---|---|
| Api-Key | String | Access token |

Gets a media item by path

Path Parameters

| Name | Type | Description |
|---|---|---|
| path* | String | Path of the media item. The path is composed by the names of any ancestor folders and the name of the media item itself, separated by`/` . |

Query Parameters

| Name | Type | Description |
|---|---|---|
| expand | String | Which properties to expand in the response |
| fields | String | Which properties to include in the response (by default all properties are included) |

Headers

| Name | Type | Description |
|---|---|---|
| Api-Key | String | Access token |

Gets media item(s) by id

Query Parameters

| Name | Type | Description |
|---|---|---|
| id* | String Array | GUIDs of the media items |
| expand | String | Which properties to expand in the response |
| fields | String | Which properties to include in the response (by default all properties are included) |

Headers

| Name | Type | Description |
|---|---|---|
| Api-Key | String | Access token |

Gets media item(s) from a query

Query Parameters

| Name | Type | Description |
|---|---|---|
| fetch* | String | Structural query string option (e.g. `ancestors` , `children` , `descendants` ).Note: The default API implementation only supports `children` . |
| filter | String Array | Filtering query string options (e.g. `mediaType` , `name` ) |
| sort | String Array | Sorting query string options (e.g. `createDate` , `name` , `sortOrder` , `updateDate` ) |
| skip | Integer | Amount of items to skip |
| take | Integer | Amount of items to take. Type: Integer. Default: 10. Limits: No limits. Accepts 0. |
| expand | String | Which properties to expand in the response |
| fields | String | Which properties to include in the response (by default all properties are included) |

Headers

| Name | Type | Description |
|---|---|---|
| Api-Key | String | Access token |

Request samples

Media item JSON structure

Last updated

Was this helpful?

---

### Output caching | CMS

Boosting Delivery API performance with output caching.

Umbraco provides opt-in output caching for Delivery API responses. When enabled, the server caches API responses and serves them for subsequent requests. The API pipeline is not re-executed until the cache expires or is evicted.

Under the hood, the Delivery API uses the built-in to handle the cache.

This article covers output caching for the Content Delivery API. For output caching of server-side rendered (Razor) pages, see the [Website Output Caching](/umbraco-cms/reference/website-output-caching) article.

Output caching is designed to increase performance. While the Delivery API is performant on its own, output caching takes the performance to another level.

Another aspect to consider is the overall server load. Uncached requests require more processing time than cached requests. For high-traffic sites, even a short-lived output cache makes a significant difference in the server load. This can result in a lesser need to scale instances, and thus a greener footprint for the site.

However, output caching does come with trade-offs:

The cache consumes additional server memory.

Editors may experience a short delay between publishing and the updated response appearing. Active eviction on publish keeps this minimal.


*not*to use output caching

Output caching can be a poor fit in some cases:

Responses where editors require guaranteed zero delay between publishing and the update appearing.

When using personalization in the API output.

If a custom property editor requires re-rendering for every request. For example, if a property value converter outputs the current time.


Output caching is **disabled by default**. Enabling it is an opt-in decision.

Enable output caching by adding the `OutputCache`

section to the `DeliveryApi`

configuration in `appsettings.json`:


| Property | Type | Default | Description |
|---|---|---|---|
| `Enabled` | `bool` | `false` | Enables or disables Delivery API output caching. |
| `ContentDuration` | `TimeSpan` | `00:00:10` (10 seconds) | Cache duration for Content Delivery API responses. |
| `MediaDuration` | `TimeSpan` | `00:00:10` (10 seconds) | Cache duration for Media Delivery API responses. |

The following requests are excluded from caching by default:

**Preview mode**requests.Requests without

**public access**to the Delivery API.

Cached responses are automatically evicted when content changes. This works through a tagging system. When a response is cached, it is tagged with identifiers. When content changes, the relevant tags are targeted for eviction.

Each cached content response is automatically tagged with:

Its own

**content key**.The keys of all its

**ancestors**in the content tree.Its

**content type**alias.

Each cached media response is tagged with its own **media key**.

These tags enable eviction at multiple levels:

**By content item**: When a content item is published, unpublished, moved, or deleted, cached responses for that item are evicted via its content key tag.**By branch**: Branch operations evict all descendants via the ancestor tags.**By relations**: When content, media, or a member is saved, responses for content that references the changed item via picker properties are evicted.**Global**: A full content cache refresh evicts all cached responses.

The Delivery API's output caching supports the same two approaches available for the website rendering pipeline:

**Per-instance in-memory cache (the default)**: each server maintains its own cache, with eviction notifications distributed across the cluster so cached responses stay consistent.**Shared distributed cache**: a single cache shared across all servers, typically backed by via the

package.[Microsoft.AspNetCore.OutputCaching.StackExchangeRedis arrow-up-right](https://www.nuget.org/packages/Microsoft.AspNetCore.OutputCaching.StackExchangeRedis)

The trade-offs and the guidance on when to choose one over the other are the same as for website rendering. For a full discussion, see [Load balancing considerations](/umbraco-cms/reference/website-output-caching#load-balancing-considerations) in the Website Output Caching article.

The feature provides extension points for customizing caching behavior. Each is registered through dependency injection.

**Interface:** `IDeliveryApiOutputCacheRequestFilter`

**Registration:** Single — replace the default with `builder.Services.AddUnique<IDeliveryApiOutputCacheRequestFilter, YourFilter>()`.


Controls whether a request is eligible for output caching. The interface has two methods:

`IsCacheable(HttpContext)`

— called before the controller runs, for request-level decisions.`IsCacheable(HttpContext, IPublishedContent)`

— called after the controller resolves content, for content-aware decisions.

The default implementation (`DefaultDeliveryApiOutputCacheRequestFilter`

) returns `false`

for preview mode requests and requests without public access. It exposes `virtual`

methods for each check, so you can inherit and override individual concerns.

**Example — skip caching when a query parameter is present:**

Register the filter in a composer:

**Example — skip caching for a specific content type:**

**Interfaces:** `IDeliveryApiOutputCacheTagProvider`

and `IDeliveryApiOutputCacheEvictionProvider`

. **Registration:** Multiple — add with `builder.Services.AddSingleton<>()`

. Multiple providers of each type are additive.

These two interfaces work as a pair to support cross-content eviction scenarios:

`IDeliveryApiOutputCacheTagProvider`

adds custom tags to cached responses when they are stored.`IDeliveryApiOutputCacheEvictionProvider`

returns tags to evict when a content change occurs.

Tags can also be targeted from custom code using `IDeliveryApiOutputCacheManager.EvictByTagAsync()`.


**Example — evict a blog category response when one of its blog posts is published:**

In this example, a blog site has two Document Types: `blogCategory`

and `blogPost`

. Each blog post has a content picker property with the alias `blogCategory`

that references its category. When a blog post is published, the selected category response is evicted so it reflects the change.

The tag provider tags each category response with a tag that includes the category content key. The eviction provider checks whether the changed content is a blog post. If so, it reads the picker value to return the tag for the selected category.

Register both providers in a composer:

**Interface:** `IDeliveryApiOutputCacheManager`

**Usage:** Inject via dependency injection. All methods are no-ops when output caching is not enabled.

Evict cache entries from custom code. This is useful when external data changes that affect Delivery API responses.

Available methods:

`EvictContentAsync(Guid contentKey)`

— evicts the cached response for a specific content item.`EvictMediaAsync(Guid mediaKey)`

— evicts the cached response for a specific media item.`EvictByTagAsync(string tag)`

— evicts all cached responses with a specific tag.`EvictAllContentAsync()`

— evicts all cached content responses.`EvictAllMediaAsync()`

— evicts all cached media responses.`EvictAllAsync()`

— evicts all cached Delivery API responses (content and media).

**Interface:** `IDeliveryApiOutputCacheVaryByProvider`

**Registration:** Multiple — add with `builder.Services.AddSingleton<IDeliveryApiOutputCacheVaryByProvider, YourProvider>()`

. Multiple providers are additive.

Control which request dimensions produce separate cache entries. Each provider receives the `HttpContext`

and the ASP.NET Core `CacheVaryByRules`

object.

By default, content responses vary by `Accept-Language`

, `Accept-Segment`

, and `Start-Item`

headers. Media responses vary by `Start-Item`

only.

**Example — vary by a custom header:**

With this provider registered, requests with `X-Test-Variant: A`

and `X-Test-Variant: B`

produce separate cache entries.

The output cache policy logs all cache decisions at `Debug`

level. Enable debug logging for the caching namespace:

Log messages include why caching was skipped (preview mode, public access, content-aware filter). When caching is applied, the logs show the tag count and duration.

The `Age`

response header on cached responses indicates how long the response has been served from cache.

While output caching is a great way to boost performance, it should never be used as a band-aid to solve poor uncached performance. The Delivery API is generally performant without caching.

If you experience performance issues while querying the Delivery API, your first step should be to diagnose and fix the root cause. This could be any number of things, like:

Un-performant value converters.

Overly complex queries.

An inexpedient content architecture.

...or something else entirely.


Hiding such problems behind output caching should only ever be considered as a short-term solution. In the long run, it will not be a sustainable fix.

Last updated

Was this helpful?

---

### Property expansion and limiting | CMS

Using property expansion and limiting to shape the Delivery API output

This article explains the mechanics of property expansion and limiting in depth. If you haven't already, read the article first - in particular the "Concepts" section.

Property expansion and limiting applies only to select property editors. The following built-in property editors in Umbraco support expansion and limiting:

Picker editors

Content Picker

Media Picker

Media Picker (legacy)

Multinode Treepicker


Block-based editors

Block List

Block Grid

Rich Text Editor (with blocks)



When working with property expansion and limiting in API queries, there are two rules of thumb to keep in mind:

Expandable properties are

*not*expanded by default. They must be expanded explicitly.All properties are included in the API output by default. We can apply limiting to limit the included properties.


In the following examples, we will be querying a content tree with blog posts and blog authors:

All blog posts are located under a root content item called "Posts".

All authors are located under a root content item called "Authors".


The blog post content type (`post`

) contains two properties that support expansion and limiting:

`author`

: A content picker for picking the author of the post.`coverImage`

: A media picker for picking an image for the post.

The author content type (`author`

) contains a single property that supports expansion and limiting:

`picture`

: A media picker for picking a picture of the author.

When fetching a blog post, the `author`

and `coverImage`

properties are returned in their un-expanded representation by default. This representation does not contain any property data; the `properties`

collections of `author`

and `coverImage`

are empty:

**Request**

**Response**

If we want to show the author's picture when rendering the blog post, we need to *expand* the `author`

property. By expanding the property, the author properties (including `picture`

) are included in the output. We can achieve this by appending the `expand`

parameter to our request.

The `expand`

parameter syntax is as follows:

`expand=properties[propertyAlias1,propertyAlias2,propertyAlias3]`


Within the `properties`

part of the `expand`

parameter we can list the aliases of the properties we wish to expand. If we want to expand all expandable properties, we can use the operator `$all`

instead:

`expand=properties[$all]`


**Request**

**Response**

Now we have the `picture`

data in the `properties`

collection of `author`

. However, the rest of the author's properties (`biography`

and `dateOfBirth`

) are also present in our output, so we are slightly over-fetching. We will take care of that later.

First, we need to get the alt texts of our images (the blog post `coverImage`

and the author `picture`

). The alt text in this case is a text string property (`altText`

) on the media type. Fetching the alt texts is possible because property expansion can be performed both across multiple properties and in a nested fashion.

For nested property expansion, the `expand`

parameter syntax is as follows:

`expand=properties[propertyAlias[properties[nestedPropertyAlias1,nestedPropertyAlias2]]]`


Nested property expansion can also be combined with the `$all`

operator:

`expand=properties[$all[properties[nestedPropertyAlias1,nestedPropertyAlias2]]]`


There is no API limit to how "deep" the nesting can go. Eventually though, the total length of the request URL may become a hard limit to the size of the query.

Let's amend the `expand`

parameter to accommodate expansion of the images:

**Request**

**Response**

As mentioned above we are slightly over-fetching. We don't need all the author data - we are only interested in the author's `picture`

. To fix this we can apply property limiting by adding the `fields`

parameter to our request.

The `fields`

parameter allows us to limit the properties in the output to only those specified. The parameter uses the same syntax as the `expand`

parameter.

Our ideal blog post output contains:

All the properties of the blog post, including the

`altText`

of the post`coverImage`

.Only the

`picture`

property of`author`

, including the`altText`

of the author`picture`.


As with property expansion, we can use the `$all`

operator in the `fields`

parameter. This will include everything at any given query level. We'll use this to include all the blog post properties in the output without having to specify each property explicitly:

**Request**

**Response**

Now the API output contains only the properties we need to render the blog post.

Property limiting is particularly useful when querying multiple items. For example, if we were building a condensed list of blog posts, we likely wouldn't need the author data nor the blog post content. By applying limiting to a filtered query, we can tailor the API output specifically to this scenario:

**Request**

**Response**

If you are not familiar with block-based editors, refer to the .

In the API output, a block has little value without its contained properties. Therefore, the content and settings properties of blocks are always included in the output. However, these properties are not expanded. As such, we can apply expansion and limiting to the contained properties.

In the following examples we'll request different types of articles, all of which are located under a root content item called "Articles":

An article with a Block List property (

`blockList`

).An article with a Block Grid property (

`blockGrid`

).An article with a Rich Text Editor property (

`richText`

).

All these properties are configured with a "Featured Post" block which consists of:

A content model (

`featuredPost`

) that contains:`title`

: A text string property.`post`

: A content picker property that allows for picking a blog post.

A settings model (

`featuredPostSettings`

) that contains:`backgroundColor`

: An approved color property.`showTags`

: A toggle property.


The goal is once again to build a condensed list of blog posts. But this time we'll build the list from the "Featured Post" blocks within each block editor.

To build the list we need the block `title`

, the `coverImage`

and `excerpt`

from the picked post, and the `backgroundColor`

from the block settings. Thus, we need to:

Expand the

`post`

property to retrieve the`altText`

of the post`coverImage`

.Limit both the block-level properties and the nested

`post`

properties, as to only output the properties relevant for building the condensed list.

For comparison, the samples show both the default output and the output with expansion and limiting applied. Notice that:

The

`expand`

and`fields`

parameter syntax is the same for all editors, even though their rendered output is structurally different.The

`expand`

and`fields`

parameters target both the content and settings parts of each block.

Default output without expansion and limiting:

**Request**

**Response**

Output with property expansion and limiting:

**Request**

**Response**

Default output without expansion and limiting:

**Request**

**Response**

Output with property expansion and limiting:

**Request**

**Response**

**Request**

**Response**

Output with property expansion and limiting:

**Request**

**Response**

Property expansion and limiting is a powerful feature that can boost our application performance. With this, we can prevent additional requests to obtain data for linked items, and we can tailor the output to specific use cases.

However, it is also a complex feature. The query syntax quickly gets complicated, particularly when targeting block editors. You will likely need to experiment to get the query exactly right. Hopefully, the examples in this article will guide you in applying expansion and limiting to your own content.

Last updated

Was this helpful?

---

### Protected content in the Delivery API | CMS

How to use member authorization with the Delivery API to access protected content.

Umbraco allows for restricting access to content. Using the "Public access" feature, specific content items can be protected and made accessible only for authorized members. The same is possible in the Delivery API. By default, protected content is ignored by the Delivery API, and is never exposed through any API endpoints. However, by enabling member authorization in the Delivery API, protected content can be accessed by means of access tokens.

If you are not familiar with members in Umbraco, read the [Members](/umbraco-cms/fundamentals/data/members) article.

This article describes how to access protected content in a client-to-server context, using an interactive authorization flow.
If you are looking to achieve server-to-server access to protected content, refer to [server-to-server access article](/umbraco-cms/reference/content-delivery-api/protected-content-in-the-delivery-api/server-to-server-access) instead.

Member authentication and authorization in the Delivery API is performed using the OpenId Connect flow *Authorization Code Flow + Proof Key of Code Exchange (PKCE)*. This is a complex authorization flow, and it is beyond the scope of this article to explain it. Many articles can be found online that explain the flow in detail.
Most programming languages have OpenId Connect client libraries to handle the complexity for us. is a great example of such a library. In ASP.NET Core, OpenId Connect support is built into the framework.

It is no longer recommended to use public OpenID Connect (OAuth) clients for web applications. If you want to use protected content from the Delivery API in a web application, consider adding additional layers of security.

For more details, see [Microsoft’s guide on configuring OpenID Connect for web authentication arrow-up-right](https://learn.microsoft.com/en-us/aspnet/core/security/authentication/configure-oidc-web-authentication)

Member authorization is an opt-in feature of the Delivery API. To enable it, configure `MemberAuthorization:AuthorizationCodeFlow`

in the `DeliveryApi`

section of `appsettings.json`:


`Enabled`

must be`true`

.One or more

`LoginRedirectUrls`

must be configured. These specify where the server is allowed to redirect the client after a successful authorization.Optionally one or more

`LogoutRedirectUrls`

must be configured. These specify where the server is allowed to redirect the client after successfully terminating a session.These are only necessary if logout is implemented in the client.



All redirect URLs must be absolute and contain the full path to the expected resource. It is not possible to use wildcards or to allow all paths under a given domain.

```
{
    "Umbraco": {
        "CMS": {
            "DeliveryApi": {
                "Enabled": true,
                "MemberAuthorization": {
                    "AuthorizationCodeFlow": {
                        "Enabled": true,
                        "LoginRedirectUrls": [
                            "https://absolute.redirect.url/path/after/login"
                        ],
                        "LogoutRedirectUrls": [
                            "https://absolute.redirect.url/path/after/logout"
                        ]
                    }
                }
            }
        }
    }
}
```

When changing the `MemberAuthorization`

configuration, Umbraco must be restarted to pick up on the changes.

When enabling or disabling member authentication, the `DeliveryApiContentIndex`

must be rebuilt to correctly reflect the existing content protection state.
The index can be rebuilt from the [Examine Management dashboard](/umbraco-cms/reference/searching/examine/examine-management).

Many client libraries support automatic discovery of the server OpenId endpoints. This is also supported by the Delivery API, so likely we do not have to worry about the server endpoints.
If automatic discovery is not applicable, the server endpoints must be configured manually. The server endpoints can be found at `https://{server-host}/.well-known/openid-configuration`.


Keep in mind that the API versions can change over time, which might affect the configuration.

To connect the client and the server, we need to apply some configuration details to the connection:

The

`client_id`

must be`umbraco-member`

.The

`response_type`

must be`code`

.The

`redirect_uri`

must be one of the configured`LoginRedirectUrls`

.The

`scope`

must either be empty, or be`openid`

and/or`offline_access`

.*PKCE*must be enabled.

For inspiration, the [samples section](/umbraco-cms/reference/content-delivery-api/protected-content-in-the-delivery-api#basic-client-configuration) at the end of this article shows how to configure an ASP.NET Core client.

*Authorization Code Flow + Proof Key of Code Exchange (PKCE)* requires the authentication service (identity provider) to be separate from the client application. This is to ensure that credentials are never exposed directly to the client application.
As an authentication service, we can use both Umbraco's built-in member authentication and external identity providers. By default the Delivery API attempts to use the built-in member authentication.

First and foremost we need a login page. By ASP.NET Core defaults, this page should be located at `/Account/Login`

. However, we can change the default path by adding the following piece of code:

To invoke this code, we need to call `SetCustomMemberLoginPath()`

in `Program.cs`:


No matter the path to the login page, we still need a page to render the login screen. Create a content item located at the login page path, and use this template to render it:

With all this in place, it's time to test the setup. Use a browser to perform a request to `https://{server-host}/umbraco/delivery/api/v1/security/member/authorize`

with these query string parameters:

`client_id=umbraco-member`

`redirect_uri=https://absolute.redirect.url/path/after/login`

(replace the value with one of the configured login redirect URLs)`response_type=code`

`code_challenge=WZRHGrsBESr8wYFZ9sx0tPURuZgG2lmzyvWpwXPKz8U`

`code_challenge_method=S256`


If everything works as expected, the request will yield a redirect to the login page. Completing the login form will cause a redirect to the specified redirect URL with a `code`

query string parameter. The `code`

can subsequently be exchanged for an access token, which can be used to access protected content.

Do not worry about the URL construction and subsequent handling of the `code`

parameter. This complexity is what the OpenId Connect client libraries handle for us.

For more inspiration on using the built-in member authentication, check the [Members Registration and Login](/umbraco-cms/tutorials/members-registration-and-login) article. Here you will also learn how to create member sign-up functionality.

Umbraco allows adding external identity providers for both backoffice users and members. The process is documented in detail in the [External Login Providers](/umbraco-cms/reference/security/external-login-providers) article.

The Delivery API supports the same functionality. In the following we'll be using GitHub to test this.

First, we need to create an OAuth App in GitHub. This is done in the . Use `https://{server-host}/umbraco/signin-github`

as authorization callback URL in the App.

Once the App is created, generate a new client secret within the App. Make sure to copy both the client ID of your App and the generated secret.

Now we need to connect Umbraco members with the App:

Add the NuGet package

`AspNet.Security.OAuth.GitHub`

to your Umbraco project.Add the code below to configure the connection to the App. Remember to update the OAuth client ID and secret.


Finally, we need to invoke the connection configuration by calling `AddGitHubAuthentication()`

in `Program.cs`.


There are multiple ways of registering extensions and dependencies like these in your Umbraco project. Which method to use depends on your implementation and preferred way of working.
Learn more about this in the [Dependency Injection](/umbraco-cms/reference/using-ioc) article.

Now we can test the setup. We'll be calling `https://{server-host}/umbraco/delivery/api/v1/security/member/authorize`

as described previously, but we need to add one more query string parameter:

`identity_provider=UmbracoMembers.GitHub`


If the setup is correct, the request will yield a redirect to the GitHub login page. Here we need to authorize the GitHub OAuth App we created earlier, in order to complete the login. Upon completion, a series of redirects will once more take us to the specified redirect URL with a `code`

query string parameter.

Different client libraries have different ways of declaring the `identity_provider`

in the authorization request. The [samples section](/umbraco-cms/reference/content-delivery-api/protected-content-in-the-delivery-api#using-a-named-identity-provider) shows how to configure this in an ASP.NET Core client.

We can also add the external identity providers to the member authentication login screen. This way the end user can decide whether to log in as a registered member, or use an external identity provider.

The features an implementation of this combined login experience.

When the authorization flow completes we'll obtain an access token. This token can be used as a bearer token to access protected content for the logged-in member:

Access tokens expire after one hour. Once expired, a new access token must be obtained to continue accessing protected content.

Refresh tokens provide a means to obtain a new access token without having to go through the authentication flow. A refresh token is issued automatically by the Delivery API when the `offline_access`

scope is specified in the authorization request.

Refresh tokens are subject to certain limitations and can result in security issues if not applied correctly. All this is beyond the scope of this article to explain in detail. Familiarize yourself with the inner workings of refresh tokens before applying them in a solution.

The member authorization is tied to the access and refresh tokens obtained in the authorization flow. Discarding these tokens efficiently terminates the access to protected content.

However, the tokens are still valid and can be reapplied until they expire. Depending on your scenario, it might be prudent to revoke the tokens and maybe even terminate the session on the server.

Access and refresh tokens can be revoked by performing a `POST`

request containing the token:

When terminating a session on the server, the member is logged out of Umbraco. This means any subsequent authorization attempt will require an explicit login.

To terminate the active session for any given member, you must redirect the browser to the signout endpoint. The request must contain one of the white-listed `LogoutRedirectUrls`

from the `appsettings.json`:


The "user info" endpoint is part of the .

This implementation returns a few of the , all of which are subject of availability:

`sub`

(required claim)`name`

(if available)`email`

(if available)

On top of this, the member groups (if any) are returned in the role claim.

The implementation is build to be extendable, so custom claims can be added to these claims - and the core claims can be removed, too.

The Delivery API Swagger document can be configured to support member authentication.

Before we can do that, we need two things in place:

We have to implement a login page

[as described above](/umbraco-cms/reference/content-delivery-api/protected-content-in-the-delivery-api#logging-in-members).We must add

`https://{server-host}/umbraco/swagger/oauth2-redirect.html`

to the configured`LoginRedirectUrls`.


With these in place, we can enable member authentication in Swagger for the Delivery API by adding the following to `Program.cs`:


The Swagger UI will now feature authorization.

Remember to use `umbraco-member`

as `client_id`

when authorizing. `client_secret`

can be omitted, as it is not used by the authorization flow.

The following samples show how to configure an ASP.NET Core client to utilize member authorization in the Delivery API. To put these samples into context, refer to the article above.

When using external identity providers, Umbraco still allows for performing local two-factor authentication for members. This feature is not available in the Delivery API. Instead, two-factor authentication should be performed at the identity provider.

Last updated

Was this helpful?

#### Server to server access | CMS

How to fetch protected content from the Delivery API with a server-to-server approach.

Configuration

```
{
    "Umbraco": {
        "CMS": {
            "DeliveryApi": {
                "Enabled": true,
                "MemberAuthorization": {
                    "ClientCredentialsFlow": {
                        "Enabled": true,
                        "AssociatedMembers": [
                            {
                                "ClientId": "my-client",
                                "ClientSecret": "my-client-secret",
                                "UserName": "member@local"
                            }
                        ]
                    }
                }
            }
        }
    }
}
```

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-62925be5ec625251767547f95c170089c0e51a49%252Fapi-member.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fee314e3&sv=2)

Authorizing and consuming the Delivery API

Last updated

Was this helpful?

How to fetch protected content from the Delivery API with a server-to-server approach.

If protected content is consumed from the Delivery API in a server-to-server context, the [interactive authorization flow](/umbraco-cms/reference/content-delivery-api/protected-content-in-the-delivery-api) won't work. Instead, we have to utilize the OpenId Connect Client Credentials flow, which is configured in the application settings.

Configuration

In the Delivery API, Client Credentials map known Members to client IDs and secrets. These Members are known as API Members. When an API consumer uses the Client Credentials of an API Member, the consumer efficiently assumes the identity of this API Member.

An API Member works the same as a regular Member, with the added option of authorizing with Client Credentials.

In the following configuration example, the Member "member@local" is mapped to a set of Client Credentials:

appsettings.json

```
{
    "Umbraco": {
        "CMS": {
            "DeliveryApi": {
                "Enabled": true,
                "MemberAuthorization": {
                    "ClientCredentialsFlow": {
                        "Enabled": true,
                        "AssociatedMembers": [
                            {
                                "ClientId": "my-client",
                                "ClientSecret": "my-client-secret",
                                "UserName": "member@local"
                            }
                        ]
                    }
                }
            }
        }
    }
}
```

After restarting the site, the backoffice will list "member@local" as an API Member:

Authorizing and consuming the Delivery API

The configured Client Credentials can be exchanged for an access token using the Delivery API token endpoint. Subsequently, the access token can be used as a Bearer token to retrieve protected content from the Delivery API.

The following code sample illustrates how this can be done.

This sample requires the NuGet packages and to run.

You should *always* reuse access tokens for the duration of their lifetime. This will increase performance both for your Delivery API consumer and for the Delivery API itself.

The code sample handles token reuse in the `ApiAccessTokenService`

service. It must be registered as a singleton service to work.

In the code sample, the token endpoint is hardcoded in the token exchange request. The Delivery API also supports OpenId Connect Discovery for API Members, if you prefer that.

Last updated

Was this helpful?

Was this helpful?

Program.cs

```
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using System.Net.Http.Json;
using IdentityModel.Client;

var builder = Host.CreateApplicationBuilder(args);
builder.Services.AddSingleton<ApiAccessTokenService>();
builder.Services.AddTransient<ApiConsumerService>();

using IHost host = builder.Build();
var consumer = host.Services.GetRequiredService<ApiConsumerService>();
await consumer.ExecuteAsync();

public static class Constants
{
    // the base URL of the Umbraco site - change this to fit your custom setup
    public static string Host => "https://localhost:44391";
}

// This is the API consumer, which will be listing the first few available content items - including protected ones.
public class ApiConsumerService
{
    private readonly ApiAccessTokenService _apiAccessTokenService;

    public ApiConsumerService(ApiAccessTokenService apiAccessTokenService)
        => _apiAccessTokenService = apiAccessTokenService;

    public async Task ExecuteAsync()
    {
        // get an access token from the access token service.
        var accessToken = _apiAccessTokenService.GetAccessToken();
        if (accessToken is null)
        {
            Console.WriteLine("Could not get an access token, aborting.");
            return;
        }

        var client = new HttpClient();
        client.SetBearerToken(accessToken);

        // fetch [pageSize] content items from the "all content" Delivery API endpoint.
        const int pageSize = 5;
        var apiResponse = await client.GetAsync($"{Constants.Host}/umbraco/delivery/api/v2/content?take={pageSize}");
        var apiContentResponse = await apiResponse
            .EnsureSuccessStatusCode()
            .Content
            .ReadFromJsonAsync<ApiContentResponse>();

        if (apiContentResponse is null)
        {
            Console.WriteLine("Could not parse content from the API response.");
            return;
        }

        Console.WriteLine($"There are {apiContentResponse.Total} items in total - listing the first {pageSize} items.");
        foreach (var item in apiContentResponse.Items)
        {
            Console.WriteLine($"- {item.Name} ({item.Id})");
        }
    }
}

// This service ensures the reuse of access tokens for the duration of their lifetime.
// It must be registered as a singleton service to work properly.
public class ApiAccessTokenService
{
    private readonly Lock _lock = new();

    private string? _accessToken;
    private DateTime _accessTokenExpiry = DateTime.MinValue;

    public string? GetAccessToken()
    {
        if (_accessTokenExpiry > DateTime.UtcNow)
        {
            // we already have a token, reuse it.
            return _accessToken;
        }

        using (_lock.EnterScope())
        {
            if (_accessTokenExpiry > DateTime.UtcNow)
            {
                // another thread fetched a new token before this thread entered the lock, reuse it.
                return _accessToken;
            }

            var client = new HttpClient();
            var tokenResponse = client.RequestClientCredentialsTokenAsync(
                    new ClientCredentialsTokenRequest
                    {
                        Address = $"{Constants.Host}/umbraco/delivery/api/v1/security/member/token",
                        ClientId = "umbraco-member-my-client",
                        ClientSecret = "my-client-secret"
                    }
                )
                // cannot await inside a using.
                .GetAwaiter().GetResult();

            if (tokenResponse.IsError || tokenResponse.AccessToken is null)
            {
                Console.WriteLine($"Error obtaining a token: {tokenResponse.ErrorDescription}");
                return null;
            }

            _accessToken = tokenResponse.AccessToken;
            _accessTokenExpiry = DateTime.UtcNow.AddSeconds(tokenResponse.ExpiresIn - 20);
            return tokenResponse.AccessToken;
        }
    }
}

public class ApiContentResponse
{
    public required int Total { get; set; }

    public required ApiContentItemResponse[] Items { get; set; }
}

public class ApiContentItemResponse
{
    public required Guid Id { get; set; }

    public required string Name { get; set; }
}
```

---

---
