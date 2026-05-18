# Reference — Part 6: Querying → Response Caching | CMS

## Querying

### Contents

- [IMemberManager | CMS](#imembermanager-cms)
- [Ipublishedcontent](#ipublishedcontent)
- [IPublishedContentQuery | CMS](#ipublishedcontentquery-cms)
- [ITagQuery | CMS](#itagquery-cms)
- [UDI Identifiers | CMS](#udi-identifiers-cms)
- [UmbracoContext helper | CMS](#umbracocontext-helper-cms)
- [UmbracoHelper | CMS](#umbracohelper-cms)

---

### IMemberManager | CMS

Using the IMemberManager

How to reference IMemberManager

Dependency Injection

```
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Core.Security;

namespace UmbracoDocs.Samples;

public class MemberAuthenticationController : Controller
{
    private readonly IMemberManager _memberManager;

    public MemberAuthenticationController(IMemberManager memberManager)
        => _memberManager = memberManager;
}
```

Views

Examples

Finding members

FindByIdAsync(string)

Find member by

`Udi`

Find member by

`Guid`

FindByEmailAsync(string)

FindByNameAsync(string)

AsPublishedMember(MemberIdentityUser)

GetCurrentMemberAsync()

GetUserIdAsync()

IsLoggedIn()

IsMemberAuthorizedAsync(IEnumerable memberTypes, IEnumerable memberGroups, IEnumerable memberIds)

IsProtectedAsync()

MemberHasAccessAsync(string)

ValidateCredentialsAsync(string username, string password)

Last updated

Was this helpful?

---

### Ipublishedcontent

#### Contents

- [IPublishedContent Collections | CMS](#ipublishedcontent-collections-cms)
- [IPublishedContent IsHelpers | CMS](#ipublishedcontent-ishelpers-cms)
- [IPublishedContent Property Access & Extension Methods | CMS](#ipublishedcontent-property-access-extension-methods-cms)

---

#### IPublishedContent Collections | CMS

Collections

.Children

```
<ul>
    @foreach(var item in Model.Children)
    {
        <li><a href="@item.Url()">@item.Name</a></li>
    }
</ul>
```

.ChildrenForAllCultures

```
<ul>
    @foreach(var item in Model.ChildrenForAllCultures)
    {
        <li><a href="@item.Url()">@item.Name</a></li>
    }
</ul>
```

.Children(string culture = null)

.Ancestors()

.Ancestor()

.AncestorsOrSelf()

.Descendants()

.DescendantsOrSelf()

.OfTypes

Filtering, Ordering & Extensions

.Where

.OrderBy

.GroupBy

.Take(int)

.Skip(int)

.Count()

.Any()

Filtering Conventions

.IsVisible()

Last updated

Was this helpful?

---

#### IPublishedContent IsHelpers | CMS

How to use

```
@{
if(item.IsVisible())
{
<a href="@item.Url()">@item.Name</a>
}
}
```

IsHelper Methods

IsComposedOf(string alias)

IsAllowedTemplate(int templateId)

IsAllowedTemplate(string templateAlias)

.IsEqual(IPublishedContent otherNode[,string valueIfTrue][,string valueIfFalse])

.IsNotEqual(IPublishedContent otherNode[,string valueIfTrue][,string valueIfFalse])

.IsDescendant(IPublishedContent otherNode[,string valueIfTrue][,string valueIfFalse])

.IsDescendantOrSelf(IPublishedContent otherNode[,string valueIfTrue][,string valueIfFalse])

.IsAncestor(IPublishedContent otherNode[,string valueIfTrue][,string valueIfFalse])

.IsAncestorOrSelf(IPublishedContent otherNode[,string valueIfTrue][,string valueIfFalse])

[Previous IPublishedContent Collections chevron-left](/umbraco-cms/reference/querying/ipublishedcontent/collections)

[Next IPublishedContent Property Access & Extension Methods chevron-right](/umbraco-cms/reference/querying/ipublishedcontent/properties)

Last updated

Was this helpful?

---

#### IPublishedContent Property Access & Extension Methods | CMS

```
@* gets the current page Url *@
@Model.Url(PublishedUrlProvider)

@* gets the Creation date, and formats it to a short date *@
@Model.CreateDate.ToString("D")

@* Outputs the name of the parent if it exists *@
@if(Model.Parent != null){
    <h1>@Model.Parent.Name</h1>
}
```

```
@Model.Id
```

Last updated

Was this helpful?

Umbraco Properties

Built-in properties, which exists on all content objects by default

Common Examples

```
@* gets the current page Url *@
@Model.Url(PublishedUrlProvider)

@* gets the Creation date, and formats it to a short date *@
@Model.CreateDate.ToString("D")

@* Outputs the name of the parent if it exists *@
@if(Model.Parent != null){
    <h1>@Model.Parent.Name</h1>
}
```

.Id

Returns the unique Id for the current content item

```
@Model.Id
```

.Name

Returns the Name of the current content item in the current culture

.Name(IVariationContextAccessor, string culture = null)

Returns the Name of the current content item in the specified culture, null falls back to the current culture

.ContentType

Returns a strongly typed 'PublishedContentType' object representing the content type the IPublishedContent item is based on, that gives access to the alias

.GetCultureFromDomains(IUmbracoContextAccessor, ISiteDomainHelper, Uri current = null)

Returns a culture from a configured domain in the content tree.

.Parent

Returns the parent content item

.Path

Returns a comma delimited string of Node Ids that represent the path of content items back to root.

.Level

Returns the Level (depth) this content item is in its tree path

.TemplateId

Returns the id of the default Template object used with this content item.

There are extension methods to retrieve template alias (Model.GetTemplateAlias())

.SortOrder

Returns the index the page is on, compared to its siblings

.Url(PublishedUrlProvider, culture = null, UrlMode mode = UrlMode.Default) - (Extension method)

Returns the Url to the page.

**Example:** Getting a Danish Url for a site where a Danish language has been set up.

**Example:** Getting an Absolute Danish Url for a site where a Danish language has been set up.

.UrlSegment

Returns the Url encoded name of the page (slug) of the current culture

.UrlSegment(IVariationContextAccessor, string culture = null)

Returns the Url encoded name of the page (slug) of the specified culture

.WriterId

Returns the id of the Umbraco backoffice user that performed the last update operation on the content item.

.WriterName(IUserService)

Returns the name of the Umbraco backoffice user that initially created the content item.

.CreatorId

Returns the id of the Umbraco backoffice user that initially created the content item

.CreatorName(IUserService)

Returns the name of the Umbraco backoffice user that initially created the content item.

.CreateDate

Returns the DateTime the page was created

.UpdateDate

Returns the DateTime the page was modified

Custom properties

All content and media items contain a reference to all the data defined by their Document Type. Custom property access is achieved using variations of the method: `Value`


Model.Value(IPublishedValueFallback, string)

Returns the property value for the specified property alias

The type returned of this property value is `object`

. This is fine in most cases since when using the above syntax, Razor will automatically execute a `ToString()`

on the result value.

See `Model.Value<T>(string)`

for how to return a strongly typed object for the property

Model.Value<T>(string)

Returns the property value for the specified property alias converted to 'T' - the requested output type of the property value.

For example, to return the `string`

result of "siteName":

Fallbacks

If the current content item doesn't have the requested value, use an alternative 'fallback' value in its place.

Each of the examples below make use of an injected PublishedValueFallback. This is achieved by adding the following at the top of your Razor file:

This parameter is optional, but can make unit testing easier.

Fallback to Default Value

If a content page has a 'title' property, to fallback to use the 'Name' of the content item if the 'title' is not populated. Set the Fallback type to be Fallback.ToDefaultValue, and set the DefaultValue accordingly:

or to a specific value

Fallback to Ancestors

Look for a property value on the current page. If it doesn't exist look for the property value on the parent page. Then the parent's parent page and so on. This approach allows specifying 'global property values' all the way up the content tree. These values can be overridden in different sections or individual pages.

Fallback to Language

If working with variants - fallback to a different language value - if perhaps the value hasn't been populated yet for the current language:

Combining the Fallback options

Use Fallback.To() to 'combine' Fallback options.

The following would first look for a 'title' property on all ancestors, before defaulting to the current page's name:

Property Methods

**There are a few helpful methods to help check if a property exists, has a value or is null.**

.HasProperty(string propertyAlias)

Returns a boolean value representing if the IPublishedContent has a property with the specified alias.

.HasValue(string propertyAlias)

Returns a boolean value representing if the IPublishedContent property has had a value set.

It's possible to use 'Fallbacks' with HasValue:

Last updated

Was this helpful?

Umbraco Properties.Id.Name.Name(IVariationContextAccessor, string culture = null).ContentType.GetCultureFromDomains(IUmbracoContextAccessor, ISiteDomainHelper, Uri current = null).Parent.Path.Level.TemplateId.SortOrder.Url(PublishedUrlProvider, culture = null, UrlMode mode = UrlMode.Default) - (Extension method).UrlSegment.UrlSegment(IVariationContextAccessor, string culture = null).WriterId.WriterName(IUserService).CreatorId.CreatorName(IUserService).CreateDate.UpdateDateCustom propertiesModel.Value(IPublishedValueFallback, string)Model.Value<T>(string)FallbacksFallback to Default ValueFallback to AncestorsFallback to LanguageCombining the Fallback optionsProperty Methods.HasProperty(string propertyAlias).HasValue(string propertyAlias)

Was this helpful?

```
@Model.Name
```

```
@Model.Name(VariationContextAccessor, "dk-dk")
```

```
@Model.ContentType
@Model.ContentType.Alias
```

```
@Model.GetCultureFromDomains(ContextAccessor, DomainHelper)
```

```
@Model.Parent
@Model.Parent.Name
```

```
@Model.Path
```

```
@Model.Level
```

```
@Model.TemplateId
```

```
@Model.SortOrder
```

```
@Model.Url(PublishedUrlProvider)
```

```
@Model.Url(PublishedUrlProvider, "dk")
```

```
@Model.Url(PublishedUrlProvider, "dk", UrlMode.Absolute)
```

```
@Model.UrlSegment
```

```
@Model.UrlSegment(VariationContextAccessor)
```

```
@Model.WriterId
```

```
@Model.WriterName(UserService)
```

```
@Model.CreatorId
```

```
@Model.CreatorName(UserService)
```

```
@Model.CreateDate
@* gets the Creation date, and formats it to a short date *@
@Model.CreateDate.ToString("D")
```

```
@Model.UpdateDate
@* gets the Update/Modified date, and formats it to a short date *@
@Model.UpdateDate.ToString("D")
```

```
@*Get the property with alias: "siteName" from the current page  *@
@Model.Value(PublishedValueFallback, "siteName")
```

```
@(Model.Value<string>(PublishedValueFallback, "siteName"))
```

```
var mediaItems = Model.Value<IEnumerable<IPublishedContent>>(PublishedValueFallback, "mediaIds");
```

```
@inject IPublishedValueFallback PublishedValueFallback
```

```
@(Model.Value<string>(PublishedValueFallback, "title", fallback: Fallback.ToDefaultValue, defaultValue: Model.Name));
```

```
@(Model.Value<string>(PublishedValueFallback, "author", fallback: Fallback.ToDefaultValue, defaultValue: "Team Reporter"));
```

```
@(Model.Value(PublishedValueFallback, "propertyAlias", fallback: Fallback.ToAncestors))
```

```
@(Model.Value(PublishedValueFallback, "pageTitle", "fr", fallback: Fallback.ToLanguage))
```

```
@Model.Value(PublishedValueFallback, "title", fallback: Fallback.To(Fallback.Ancestors, Fallback.DefaultValue), defaultValue: Model.Name)
```

```
bool hasPageTitleSetSomewhere = Model.HasValue(PublishedValueFallback, "pageTitle", fallback: Fallback.ToAncestors);
```

---

---

### IPublishedContentQuery | CMS

Querying in views with IPublishedContentQuery in Umbraco

How to inject IPublishedContentQuery

```
using Umbraco.Cms.Core;

namespace Umbraco.Docs.Samples.Web.Services;

public class SearchService
{
    private readonly IPublishedContentQuery _publishedContentQuery;

    public SearchService(IPublishedContentQuery publishedContentQuery)
    {
        _publishedContentQuery = publishedContentQuery;
    }
}
```

Accessing the Published Content Cache via

`IPublishedContentQuery`

Examples

.Search(string term)

.Search(string term, int skip, int take, out long totalRecords)

.Search(IQueryExecutor queryExecutor)

Last updated

Was this helpful?

---

### ITagQuery | CMS

Working with tags in Umbraco

How to reference ITagQuery

```
@inject ITagQuery _tagQuery;
```

```
using System.Collections.Generic;
using System.Linq;
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Core.PublishedCache;

namespace UmbracoHelperDocs.Controllers;

[ApiController]
[Route("/umbraco/api/tags")]
public class TagApiController : Controller
{
 private readonly ITagQuery _tagQuery;

 public TagApiController(ITagQuery tagQuery)
 {
  _tagQuery = tagQuery;
 }

 [HttpGet("getmediatags")]
 public ActionResult<IEnumerable<string>> GetMediaTags()
 {
  return _tagQuery.GetAllMediaTags().Select(tag => tag.Text).ToList();
 }
}
```

Examples

GetAllContentTags([string tagGroup])

GetAllMediaTags([string tagGroup])

GetAllMemberTags([string tagGroup])

GetAllTags([string tagGroup])

GetContentByTag(string tag, [string tagGroup])

GetContentByTagGroup(string tagGroup)

GetMediaByTag(string tag, [string tagGroup])

GetMediaByTagGroup(string tag, [string tagGroup])

GetTagsForEntity(int contentId, [string tagGroup])

GetTagsForProperty(int contentId, string propertyTypeAlias, [string tagGroup])

Last updated

Was this helpful?

---

### UDI Identifiers | CMS

```
umb://document/4fed18d8c5e34d5e88cfff3a5b457bf2.
```

Format

Usage

Retrieving Content by UDI

```
using Umbraco.Cms.Core.Services;
using Umbraco.Cms.Core.Models

@inject IContentService contentService

@{
   // Define the UDI string here
    var udiString = "umb://document/334cadfa62dd49049aad86b6e4c02aac"; // Example UDI string

   if (udiString.StartsWith("umb://document/"))
    {
        // Extract the GUID from the UDI string
        var guidString = udiString.Replace("umb://document/", "");
        if (Guid.TryParse(guidString, out var guid))
        {
            // Retrieve the content by GUID
            var content = contentService.GetById(guid);
            if (content != null)
            {
                // Access the body text field
                var bodyText = content.GetValue<string>("bodyText"); // Replace 'bodyText' with the alias of your body text field
                <p>@bodyText</p>  // Output the body text
            }
        else
            {
                <p>Content not found.</p>
            }
        }
        else
        {
            <p>Invalid GUID in the UDI string.</p>
        }
    }
}
```

UDI Types

GUID UDI

String UDI

Last updated

Was this helpful?

Umbraco uses Unique Document Identifiers (UDIs) to reference most object types, such as content, media, and members. A UDI contains all the metadata needed to retrieve an Umbraco object and is readable within text.

Example:

```
umb://document/4fed18d8c5e34d5e88cfff3a5b457bf2.
```

UDIs are commonly used in Umbraco’s querying and management APIs.

Format

A UDI consists of three parts:

Scheme:

`umb://`

– Identifies as an Umbraco UDI.Type:

`document`

– Specifies the object type (for example, media, member, Data Type, and so on).GUID Identifier:

`4fed18d8c5e34d5e88cfff3a5b457bf2`

– A unique identifier for the object (a GUID without dashes).

Usage

UDIs are useful for retrieving content, media, or other Umbraco objects through the API. Below are examples of how to use a UDI in C# to get content or media.

Retrieving Content by UDI

You can retrieve a content item using `IContentService`:


```
using Umbraco.Cms.Core.Services;
using Umbraco.Cms.Core.Models

@inject IContentService contentService

@{
   // Define the UDI string here
    var udiString = "umb://document/334cadfa62dd49049aad86b6e4c02aac"; // Example UDI string

   if (udiString.StartsWith("umb://document/"))
    {
        // Extract the GUID from the UDI string
        var guidString = udiString.Replace("umb://document/", "");
        if (Guid.TryParse(guidString, out var guid))
        {
            // Retrieve the content by GUID
            var content = contentService.GetById(guid);
            if (content != null)
            {
                // Access the body text field
                var bodyText = content.GetValue<string>("bodyText"); // Replace 'bodyText' with the alias of your body text field
                <p>@bodyText</p>  // Output the body text
            }
        else
            {
                <p>Content not found.</p>
            }
        }
        else
        {
            <p>Invalid GUID in the UDI string.</p>
        }
    }
}
```

UDI Types

There are two types of UDIs in Umbraco:

GUID UDI

Used for objects that have a GUID identifier, such as content and media.

String UDI

Used for objects that are not GUID-based, such as dictionary items.

Last updated

Was this helpful?

Was this helpful?

---

### UmbracoContext helper | CMS

The UmbracoContext is a helpful service provided on each request to the website.

Last updated

Was this helpful?

The UmbracoContext is a helpful service provided on each request to the website.

The UmbracoContext is the simplified way to work with the current request on your website.

You can use UmbracoContext to access the content and media cache. Other useful properties are the original and cleaned URLs of the current request. You can also check if the current request is running in "preview" mode.

How to reference UmbracoContext

If you are using Views you can reference the UmbracoContext with the syntax: `@UmbracoContext`.


If you need an `UmbracoContext`

in your own controllers, you need to inject an `IUmbracoContextAccessor`.


The following is an example of how to get access to the `UmbracoContext`

in a controller:

```
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Core;
using Umbraco.Cms.Core.Web;

namespace MyProject.Controllers.Api;

[ApiController]
[Route("/umbraco/api/people")]
public class PeopleController : Controller
{
    private readonly IUmbracoContextAccessor _umbracoContextAccessor;
    private readonly IPublishedContentQuery _publishedContentQuery;

    public PeopleController(
        IUmbracoContextAccessor umbracoContextAccessor,
        IPublishedContentQuery publishedContentQuery)
    {
        _umbracoContextAccessor = umbracoContextAccessor;
        _publishedContentQuery = publishedContentQuery;
    }

    [HttpGet("getall")]
    public ActionResult<IEnumerable<string>> GetAll()
    {
        // Try to get the UmbracoContext
        if (_umbracoContextAccessor.TryGetUmbracoContext(out IUmbracoContext? context) == false)
        {
            return Problem("Unable to get UmbracoContext");
        }

        // Check if we're in preview mode using UmbracoContext
        if (context.InPreviewMode)
        {
            // In preview mode, you might want to show draft content or additional info
            return Ok(new
            {
                message = "Preview mode active",
                isPreview = true
            });
        }

        if (context.Content == null)
        {
            return Problem("Content Cache is null");
        }

        // Use IPublishedContentQuery to get root content
        var rootNodes = _publishedContentQuery.ContentAtRoot();

        if (!rootNodes.Any())
        {
            return Problem("No content found at root");
        }

        // Find a specific parent node (for example, "People" section)
        var peopleNode = rootNodes
            .FirstOrDefault()?
            .Children()
            .FirstOrDefault(c => c.ContentType.Alias == "people");

        if (peopleNode == null)
        {
            return Problem("People node not found");
        }

        // Get only the direct children of the People node
        var personNodes = peopleNode.Children()
            .Where(c => c.ContentType.Alias == "person")
            .Select(p => p.Name);

        // Return results with UmbracoContext information
        return Ok(new
        {
            people = personNodes,
            // Include UmbracoContext properties in the response
            contextInfo = new
            {
                isPreview = context.InPreviewMode,
                currentUrl = context.CleanedUmbracoUrl?.ToString()
            }
        });
    }
}
```

For content querying scenarios, use `IPublishedContentQuery.ContentAtRoot()`.


For advanced navigation, multi-site setups, or culture-specific root detection, use `IDocumentNavigationQueryService.TryGetRootKeys()`

, which returns GUID keys representing the structure of the content tree.

UmbracoContext is registered with a scoped lifetime. See the for more information. A service scope is created for each request, which means you can resolve an instance directly in a controller.

Last updated

Was this helpful?

Was this helpful?

---

### UmbracoHelper | CMS

Using the Umbraco Helper

How to reference UmbracoHelper

```
using System.Linq;
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Web.Common;
using Umbraco.Cms.Web.Common.Controllers;

namespace UmbracoHelperDocs.Controllers;

[Route("customcontent/[action]")]
public class CustomContentController : Controller
{
    private readonly UmbracoHelper _umbracoHelper;

    public CustomContentController(UmbracoHelper umbracoHelper)
        => _umbracoHelper = umbracoHelper;

    public IActionResult GetHomeNodeName()
    {
        IPublishedContent rootNode = _umbracoHelper
            .ContentAtRoot()
            .FirstOrDefault();

        if (rootNode is null)
        {
            return NotFound();
        }

        return Ok(rootNode.Name);
    }
}
```

IPublishedContent

Working with Content

.Content(Guid id)

.ContentAtRoot()

Working with Media

.Media(Guid id)

.MediaAtRoot()

Working with Tags

Working with Members

Searching

Fetching Dictionary Values

.GetDictionaryValue(string key)

.GetDictionaryValueOrDefault(string key, string altText)

Last updated

Was this helpful?

---

---


## Response Caching | CMS

Modify the

`Cache-Control`

header for Static Files```
using System.IO;
using System;
using System.Collections.Generic;

using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Options;
using Microsoft.AspNetCore.Http.Headers;
using Microsoft.Net.Http.Headers;

using Umbraco.Cms.Core.Configuration.Models;
using Umbraco.Cms.Core.Hosting;
using IHostingEnvironment = Umbraco.Cms.Core.Hosting.IHostingEnvironment;

namespace Umbraco.Docs.Samples.Web.Tutorials;

public class ConfigureStaticFileOptions : IConfigureOptions<StaticFileOptions>
{
    // These are the extensions of the file types we want to cache (add and remove as you see fit)
    private static readonly HashSet<string> _cachedFileExtensions = new(StringComparer.OrdinalIgnoreCase)
    {
        ".ico",
        ".css",
        ".js",
        ".svg",
        ".woff2",
        ".jpg"
    };

    private readonly string _backOfficePath;

    public ConfigureStaticFileOptions(IOptions<GlobalSettings> globalSettings, IHostingEnvironment hostingEnvironment)
        => _backOfficePath = hostingEnvironment.GetBackOfficePath();

    public void Configure(StaticFileOptions options)
        => options.OnPrepareResponse = ctx =>
        {
            // Exclude Umbraco backoffice assets
            if (ctx.Context.Request.Path.StartsWithSegments(_backOfficePath))
            {
                return;
            }

            // Set headers for specific file extensions
            var fileExtension = Path.GetExtension(ctx.File.Name);
            if (_cachedFileExtensions.Contains(fileExtension))
            {
                ResponseHeaders headers = ctx.Context.Response.GetTypedHeaders();

                // Update or set Cache-Control header
                CacheControlHeaderValue cacheControl = headers.CacheControl ?? new CacheControlHeaderValue();
                cacheControl.Public = true;
                cacheControl.MaxAge = TimeSpan.FromDays(365);
                headers.CacheControl = cacheControl;
            }
        };
}
```

Modify the

`Cache-Control`

header for ImageSharp.WebAdd the

`Cache-Control`

header for rendering using the Last updated

Was this helpful?

---
