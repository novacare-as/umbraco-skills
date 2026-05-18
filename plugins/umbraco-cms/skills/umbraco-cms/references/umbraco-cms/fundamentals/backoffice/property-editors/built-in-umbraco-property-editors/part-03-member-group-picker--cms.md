# Built In Umbraco Property Editors — Part 3: Member Group Picker | CMS → User Picker | CMS

## Member Group Picker | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a0510029d2fc8d1567c47a18c9212f566e590eaa%252FMember-Picker-DataType.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=deae2a5f&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-33109a95d23767e2061b20a400100d0d08bbe573%252FMember-Group-Picker-Content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=53f50458&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.MemberGroupPicker`


`UI Alias: Umb.PropertyEditorUi.MemberGroupPicker`


`Returns: string`


The Member Group Picker opens a panel to pick one or more member groups from the Member section. The value saved is of type string (comma separated IDs).

Data Type Definition Example

Content Example

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

You can also add multiple groups by creating a comma separated string with the desired member group IDs.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@if (Model.HasValue("memberGroup"))
{
    var memberGroup = Model.Value<string>("memberGroup"); 
    <p>@memberGroup</p>
}
```

```
@if (!string.IsNullOrEmpty(Model.MemberGroup))
{
    <p>@Model.MemberGroup</p>
}
```

```
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = new Guid("796a8d5c-b7bb-46d9-bc57-ab834d0d1248");
    
    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Set the value of the property with alias 'memberGroup'. The value is the specific ID of the member group
    content.SetValue("memberGroup", 1067);
            
    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Set the value of the property with alias 'memberGroup'. 
    content.SetValue("memberGroup", "1067","1068");
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'memberGroup'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.MemberGroup).Alias, 1067);
}
```

---


## Member Picker | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2f42aa8db1c657b38f59faa07307ed9897380267%252FMember-Picker.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4612353c&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5f01d0e0facd2921a06cdde161ce1de6e815ef16%252FMember-Picker-Content-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=131e7650&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.MemberPicker`


`UI Alias: Umb.PropertyEditorUi.MemberPicker`


`Returns: IPublishedContent`


The member picker opens a panel to pick a specific member from the member section. The value saved is of type IPublishedContent.

Data Type Definition Example

Content Example

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@{
    if (Model.HasValue("author"))
    {
        var member = Model.Value<IPublishedContent>("author");
        @member.Name
    }
}
```

```
@{
    if (Model.Author != null)
    {
        var member = Model.Author;
        @member.Name
    }
}
```

```
@using Umbraco.Cms.Core.Services
@using Umbraco.Cms.Core;
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Create a variable for the GUID of the member ID
    var authorId = Guid.Parse("ed944097281e4492bcdf783355219450");

    // Create a udi
    var memberUdi = Udi.Create(Constants.UdiEntityType.Member, authorId);

    // Set the value of the property with alias 'author'. 
    content.SetValue("author", memberUdi);

    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'author'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.Author).Alias, udi);
}
```

---


## Multi Url Picker | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b3b5bfbbc1e52f25da993e2455da0d2235053ff7%252FMulti-Url-Picker-DataType.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=290d6786&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a58955d0ffe3dd8a3d962741b507686b033b2d1f%252FMulti-Url-Picker-Content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=af5c660e&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Getting Absolute URLs

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.MultiUrlPicker`


`UI Alias: Umb.PropertyEditorUi.MultiUrlPicker`


`Returns: IEnumerable<Link> or Link`


Multi URL Picker allows editors to select and sort multiple URLs. The property returns either a single item or a collection, depending on the **Maximum number of items** setting in the Data Type configuration.

When the maximum is set to 1, it returns a single item.

When the maximum is greater than 1, it returns a collection.


The URLs can point to **internal**, **external**, or **media** items.

Data Type Definition Example

Content Example

MVC View Example

Without Models Builder

This example handles the case of `Maximum number of items`

set to `1`:


With Models Builder

And here is the case of `Maximum number of items`

set to `1`:


Getting Absolute URLs

By default, `link.Url`

returns a relative URL for internal content links (for example, /products/, /blog/, and so on). If you need absolute URLs, for example in emails, sitemaps, or cross-domain scenarios, you can use `IPublishedUrlProvider`

with `UrlMode.Absolute`.


Inject `IPublishedUrlProvider`

at the top of your view and resolve internal links using `UrlMode.Absolute`

. External and media links are already stored as absolute strings and pass through unchanged.

When setting values programmatically, you can pass `UrlMode.Absolute`

when building `Link`

objects in code:

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@using Umbraco.Cms.Core.Models
@{
    var links = Model.Value<IEnumerable<Link>>("footerLinks");
    if (links.Any())
    {
        <ul>
            @foreach (var link in links)
            {
                <li><a href="@link.Url" target="@link.Target">@link.Name</a></li>
            }
        </ul>
    }
}
```

```
@using Umbraco.Cms.Core.Models
@{
    var link = Model.Value<Link>("link");
    if (link != null)
    {
        <a href="@link.Url" target="@link.Target">@link.Name</a>
    }
}
```

```
@{
    var links = Model.FooterLinks;
    if (links.Any())
    {
        <ul>
            @foreach (var link in links)
            {
                <li><a href="@link.Url" target="@link.Target">@link.Name</a></li>
            }
        </ul>
    }
}
```

```
@{
    var link = Model.Link;
    if (link != null)
    {
        <a href="@link.Url" target="@link.Target">@link.Name</a>
    }
}
```

```
@using Umbraco.Cms.Core.Models
@using Umbraco.Cms.Core.Models.PublishedContent
@inject Umbraco.Cms.Core.Routing.IPublishedUrlProvider UrlProvider

@{
    var links = Model.Value<IEnumerable<Link>>("footerLinks");
    if (links.Any())
    {
        <ul>
            @foreach (var link in links)
            {
                var url = link.Type == LinkType.Content
                    ? UrlProvider.GetUrl(Umbraco.Content(link.Udi), UrlMode.Absolute)
                    : link.Url;

                <li><a href="@url" target="@link.Target">@link.Name</a></li>
            }
        </ul>
    }
}
```

```
new Link
{
    Target = "_self",
    Name = contentPage.Name,
    Url = contentPage.Url(mode: UrlMode.Absolute),
    Type = LinkType.Content,
    Udi = contentPageUdi
}
```

```
@using Umbraco.Cms.Core
@using Umbraco.Cms.Core.Serialization
@using Umbraco.Cms.Core.Services
@using Umbraco.Cms.Core.Models
@inject IContentService ContentService
@inject IJsonSerializer Serializer
@{
    // Create a variable for the GUID of the page you want to update
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Get the media you want to assign to the footer links property 
    var media = Umbraco.Media("bca8d5fa-de0a-4f2b-9520-02118d8329a8");

    // Create an Udi of the media
    var mediaUdi = Udi.Create(Constants.UdiEntityType.Media, media.Key);

    // Get the content you want to assign to the footer links property 
    var contentPage = Umbraco.Content("665d7368-e43e-4a83-b1d4-43853860dc45");

    // Create an Udi of the Content
    var contentPageUdi = Udi.Create(Constants.UdiEntityType.Document, contentPage.Key);

    // Create a list with different link types
    var externalLinks = new List<Link>
    {
        // External Link
        new Link
        {
            Target = "_blank",
            Name = "Our Umbraco",
            Url = "https://our.umbraco.com/",
            Type = LinkType.External
        },
        // Media 
        new Link
        {
            Target = "_self",
            Name = media.Name,
            Url = media.MediaUrl(),
            Type = LinkType.Media,
            Udi = mediaUdi
        }, 
        // Content 
        new Link
        {
            Target = "_self",
            Name = contentPage.Name,
            Url = contentPage.Url(),
            Type = LinkType.Content,
            Udi = contentPageUdi
        }
    };

    // Serialize the list with links to JSON
    var links = Serializer.Serialize(externalLinks);


    // Set the value of the property with alias 'footerLinks'. 
    content.SetValue("footerLinks", links);

    // Save the change
    ContentService.Save(content);
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'footerLinks'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.FooterLinks).Alias, links);
}
```

---


## Repeatable Textstrings | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-eda135248f982c2befdb373bb5053be1d16ee7f8%252FRepeatable-Textstrings-DataType.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b3fd7a3f&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7c3e61eae190480081f8c691fb5cc15c117afe80%252FMultiple-Textbox-Repeatable-Textstrings-Content%2520%281%29%2520%281%29.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d2157c2b&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.MultipleTextstring`


`UI Alias: Umb.PropertyEditorUi.MultipleTextString`


`Returns: array of strings`


The Repeatable textstrings property editor enables a content editor to make a list of text items. For best use with an unordered-list.

Data Type Definition Example

Content Example

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

To add multiple values to the repeatable text strings property editor you have to put each value on a new line. This can be achieved using either `\r\n\`

or `Environment.NewLine`.


Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@{
    if (Model.Value<string[]>("keyFeatureList").Length > 0)
    {
        <ul>
            @foreach (var item in Model.Value<string[]>("keyFeatureList"))
            {
                <li>@item</li>
            }
        </ul>
    }
}
```

```
@{
    if (Model.KeyFeatureList.Any())
    {
        <ul>
            @foreach (var item in Model.KeyFeatureList)
            {
                <li>@item</li>
            }
        </ul>
    }
}
```

```
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = new Guid("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Set the value of the property with alias 'keyFeatureList'
    content.SetValue("keyFeatureList", "Awesome" + Environment.NewLine + "Super");

    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'keyFeatureList'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.KeyFeatureList).Alias, "Awesome" + Environment.NewLine + "Super");
}
```

---


## Numeric | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-359e2787a82f3c26fffbc8fecd507e12cc6cff17%252Fnumeric-datatype.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8766bf3c&sv=2)

Minimum

Step Size

Maximum

Settings

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-165126a8334537e8771d489757488502bab5955e%252Fnumeric-content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1adeab7e&sv=2)

MVC View Examples

Rendering the output casting to an int (without Models Builder)

Rendering the output casting to a string (Without Models Builder)

With Models Builder

Add values programmatically

Last updated

Was this helpful?

---


## Radiobutton List | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ec80c6b02c108b0e4abc4e83d2e3a780f6ff2a3f%252FRadioButton-List-DataType.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=41046ec8&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-dffc9993677a7fc1f83c60584cb42130c6ec64cf%252FRadioButton-List-Content-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=adf28b93&sv=2)

MVC View Example

Typed

Without Models Builder

With Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.RadioButtonList`


`UI Alias: Umb.PropertyEditorUi.RadioButtonList`


`Returns: string`


Pretty much like the name indicates this Data type enables editors to choose from list of radio buttons and returns the value of the selected item as string.

Data Type Definition Example

You can use dictionary items to translate the values of a Radiobutton List property editor in a multilingual setup. For more details, see the [Creating a Multilingual Site](/umbraco-cms/tutorials/multilanguage-setup#translating-multi-value-property-editors) article.

Content Example

MVC View Example

Typed

Without Models Builder

With Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@if (Model.HasValue("colorTheme"))
{
    var value = Model.Value("colorTheme");
    <p>@value</p>
}
```

```
@if (Model.ColorTheme != null)
{
    var value = Model.ColorTheme;
    <p>@value</p>
}
```

```
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = new Guid("796a8d5c-b7bb-46d9-bc57-ab834d0d1248");
    
    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page
    
    // Set the value of the property with alias 'colorTheme'
    content.SetValue("colorTheme", "water");
            
    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'colorTheme'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.ColorTheme).Alias, "water");
}
```

---


## Rich Text Editor

### Contents

- [Blocks | CMS](#blocks-cms)
- [Configuration | CMS](#configuration-cms)
- [Custom CSS properties | CMS](#custom-css-properties-cms)
- [Extensions | CMS](#extensions-cms)
- [Style Menu | CMS](#style-menu-cms)

---

### Blocks | CMS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-3339e299477ffd34c940dc4927fe123e63db0418%252Frte-blocks-toolbar-insert-button.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=66d97b3f&sv=2)

Configure Blocks

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6aa7845022f9daaa5bc692d75f845c3a4b65a9fa%252Frte-blocks-datatype-configuration.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4024cedc&sv=2)

Editor Appearance

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9e5ebcc88e51f61cb238d19b03b71aedc6c84a43%252Frte-blocks-editor-appearance-settings.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4285d2ab&sv=2)

Data Models

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f85d58fa82b34d489553f45d8f5fd1c6b015ad6a%252Frte-blocks-data-models-settings.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=20eb1805&sv=2)

Catalogue Appearance

Working with Blocks

Adding Blocks to Content

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-47ff9a7eb13ec1a7631216c31a99fee2ae2693a4%252Frte-blocks-adding-to-content-1.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e59dd667&sv=2)

Adding Blocks to Content - Step 1 ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9294e8bed0c76e5fd2c73ab0982d7a5fd741e6ad%252Frte-blocks-adding-to-content-2.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=695b04d8&sv=2)

Adding Blocks to Content - Step 2 ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a204f47163dddacc3f1ef4462549dd4a12da0aa6%252Frte-blocks-adding-to-content-3.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f8439e48&sv=2)

Adding Blocks to Content - Step 3

Rendering Blocks

File Structure

Example Partial View

Example with Settings Model

Type-Safe Rendering with Models Builder

Build a Custom Backoffice View

Best Practices

Content Design

Performance

Accessibility

Related Articles

Last updated

Was this helpful?

---

### Configuration | CMS

Toolbar

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b82806c78ea39ef75feff4c2e43d3f2997ddff2b%252Frte-tiptap-all-toolbar-items.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=62c544e3&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1ddea2150a18a84cbae769125ae7b7c7bbe65127%252Frte-tiptap-capabilities-and-toolbar.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=508f30b&sv=2)

Statusbar

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f05ec89ee054bafb8d9e483007c9e3a3202d9aec%252Frte-tiptap-statusbar.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c2c61ee3&sv=2)

Stylesheets

Dimensions

Maximum size for inserted images

Overlay Size

Available Blocks

Accepted Media Types

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b32feddee4ac855849c7eb8eb6b93ad04f0188e4%252Frte-tiptap-accepted-media-types.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d0e64596&sv=2)

Image Upload Folder

Ignore User Start Nodes

Last updated

Was this helpful?

In this article you can learn about the different options you have for configuring the Rich Text Editor (RTE).

Toolbar

You have full control over which options should be available on the RTE.

In the example above, all the options have been enabled. These options include font styles like bold and italics, bullet lists, and options to embed videos and insert images.

You can customize the look of the toolbar:

Enhance the capabilities of the toolbar by enabling or disabling extensions.

Use the Toolbar designer to group together items and add additional rows if needed.


Statusbar

As well as the toolbar, you can configure extensions for the statusbar.

Stylesheets

To apply custom styles to the Rich Text Editor, you can select from any existing stylesheets.

Stylesheets can be created in the **Settings** section. To learn more about this feature, see the [Stylesheets in the Backoffice](/umbraco-cms/fundamentals/design/stylesheets-javascript) article.

Dimensions

Define `height`

and `width`

of the editor displayed in the content section.

Maximum size for inserted images

Define the maximum size for images added through the Rich Text Editor.

If inserted images are larger than the dimensions defined here, the images will be resized automatically.

Overlay Size

Select the width of the link picker overlay. The overlay size comes in three sizes: Small, Medium, Large, and Full.

Available Blocks

Blocks can be added as elements in the Rich Text Editor. Configuration and rendering of Blocks are described in the [Blocks in Rich Text Editor](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/rich-text-editor/blocks) article.

Accepted Media Types

By default, only Image and Vector Graphics media types are accepted in the Rich Text Editor. You can change this by selecting specific types in the **Accepted media types** setting.

Only matching media types can be picked from the library or uploaded via the toolbar and drag-and-drop.

If an uploaded file matches multiple accepted media types, a picker dialog lets the editor choose the correct type.

Image Upload Folder

Images added through the RTE are by default added to the root of the Media library.

Sometimes you might want to add the images to a specific folder. This folder can be configured using the "Image Upload Folder" setting.

Ignore User Start Nodes

Some of the backoffice users might be restricted to a specific part of the content tree. When the "Ignore User Start Nodes" is checked, the users can pick any piece of content from the content tree, when adding internal links through the RTE.

Last updated

Was this helpful?

Was this helpful?

---

### Custom CSS properties | CMS

```
:root {
    --umb-rte-min-height: 300px;
}
```

Custom CSS properties reference

| CSS Property | Description | Default Value |
|---|---|---|
| `--umb-rte-width` | The width of the rich-text-editor | `unset` |
| `--umb-rte-min-width` | The minimum width of the rich-text-editor | `unset` |
| `--umb-rte-max-width` | The maximum width of the rich-text-editor | `100%` |
| `--umb-rte-height` | The height of the rich-text-editor | `100%` |
| `--umb-rte-min-height` | The minimum height of the rich-text-editor | `100%` |
| `--umb-rte-max-height` | The maximum height of the rich-text-editor | `100%` |

Last updated

Was this helpful?

---

### Extensions | CMS

Information on how to work with Tiptap extensions in the rich text editor.

The Rich Text Editor (RTE) in Umbraco is based on the open-source editor .

Out of the box, Tiptap has limited capabilities, and everything is an extension by design. Basic text formatting features, such as bold, italic, and underline, are their own extensions. This offers great flexibility, making the rich text editor highly configurable. The implementation in Umbraco offers a wide range of built-in extensions to enhance the Tiptap editor capabilities.

Using the same extension points, this article will show you how to add a custom extension to the rich text editor.

Tiptap has a library of supported native extensions. You can find a list of these extensions on the . While many of these are open source, there are also available for commercial subscriptions.

There are three types of extensions: `tiptapExtension`

, `tiptapToolbarExtension`

, and `tiptapStatusbarExtension`.


The `tiptapExtension`

extension is used to register a native . These will enhance the capabilities of the rich text editor itself. For example, to enable text formatting, drag-and-drop functionality and spell-checking.

The `tiptapToolbarExtension`

extension adds a toolbar action that interacts with the Tiptap editor (and native Tiptap extensions).

The `tiptapStatusbarExtension`

extension adds a component to the statusbar, located at the bottom of the Tiptap editor.

This example assumes that you will be creating an Umbraco package using the Vite/Lit/TypeScript setup.
You can learn how to do this [Vite Package Setup](/umbraco-cms/customizing/development-flow/vite-package-setup) article.

In this example, you will take the native Tiptap open-source extension . Then register it with the rich text editor and add a toolbar button to invoke the Task List action.

Install the Highlight extension from the npm registry.


```
npm install @tiptap/extension-highlight
```

Create the code to register the native Tiptap extensions in the rich text editor.


Create the toolbar action to invoke the Highlight extension.


Once you have the above code in place, it can be referenced using a [bundle extension type](/umbraco-cms/customizing/extending-overview/extension-types/bundle).

Upon restarting Umbraco, the new extension and toolbar action will be available in the Tiptap Data Type configuration settings.

Last updated

Was this helpful?

---

### Style Menu | CMS

A Style Select Menu is a configurable extension that adds a cascading menu to the toolbar for applying text styles and formatting. Use a Style Select menu when you want editors to apply predefined, consistent styles instead of manually formatting text.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-792805a78e802700fac0c96508f61a2b74bd1c52%252Frte-tiptap-stylemenu.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=2584efa2&sv=2)

Any custom stylesheets associated with the Rich Text Editor will not auto-generate a style select menu in the toolbar. See the [Creating a Style Select Menu](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/rich-text-editor/style-menu#creating-a-custom-style-select-menu) section below.

To add Style Select to the Rich Text Editor:

Go to

**Settings**.Navigate to

**Data Types**.Select the relevant Data Type.

Drag

**Style Select**from**Available Actions**into the**Toolbar**section.Click

**Save**.

Alternatively, while configuring an editor on a Document Type, you can drag **Style Select** from **Available Actions** into the **Toolbar** section.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-546ec7c47bae80995b1a0affc550fbc37c075cbb%252Fadding-style-select-to-toolbar.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=315e4d2b&sv=2)

Adding Style Select enables the menu, but creating a package manifest is only required if you want custom styles or structure.

Below, you can find an example of how to set up a custom Style Select menu using an [Umbraco Package Manifest](/umbraco-cms/customizing/umbraco-package) file.

Create an

`umbraco-package.json`

file in`App_Plugins/{YourPackageName}`.


The `items`

property defines the structure of the style select menu. Each menu item has the following options:

`label`

:*(required)*The label of the menu item. This supports localization keys.`appearance`

: This defines the appearance of the menu item. The value has 2 optional properties:`icon`

: To prefix an icon to the menu item.`style`

: To apply CSS rules to the menu item.

`data`

: To configure the function of the style select menu item. The value has 3 optional properties:`tag`

: A[supported HTML tag](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/rich-text-editor/style-menu#supported-html-tags)name. This will be applied to the selected text.`class`

: Applies a class attribute with the defined class name to the containing tag of the selected text.`id`

: Applies an ID attribute with the defined ID value to the containing tag of the selected text.

`separatorAfter`

: When`true`

, it will add a line separator after the menu item.`items`

: To enable a cascading menu, an array of nested menu items may be added.

Once configured, the custom style select menu will appear in the Rich Text Editor's

**Toolbar**section. You can look for it in the**Available actions**block.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-72677a589bbec7e925513e47d32a2c336d96037f%252Fcustom-style-select-menu.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4a475222&sv=2)

Due to Tiptap’s strict rich-text schema, only supported HTML tags are allowed in the style select menu *(arbitrary markup will be excluded)*. The following HTML tag names are supported:

`h1`

`h2`

`h3`

`h4`

`h5`

`h6`

`p`

`a`

(link)`blockquote`

`code`

`codeBlock`

`div`

`em`

(italic)`ol`

`strong`

(bold)`s`

(strike-through)`span`

`u`

(underline)`ul`


Last updated

Was this helpful?

---

---


## Slider | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9620542ac7fe47b6fc1dc1d8abdf9c23769cf943%252FSlider-Data-Type-Definition.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f8cc9918&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-94a6744a65d8b0fe02f7c10500d19561ac43af9d%252FSlider-Content-Example-With-Range.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=afccd7d5&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

With a range off

With a range on

Last updated

Was this helpful?

`Schema Alias: Umbraco.Slider`


`UI Alias: Umb.PropertyEditorUi.Slider`


`Returns: decimal`

or `Umbraco.Core.Models.Range<decimal>`


Pretty much like the name indicates this Data type enables editors to choose a value with a range using a slider.

There are two flavors of the slider. One with a single value picker. One with a minimum and maximum value.

Data Type Definition Example

Content Example

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

With a range off

With a range on

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@if (Model.HasValue("singleValueSlider"))
{
    var value = Model.Value<decimal>("singleValueSlider");
    <p>@value</p>
}

@if (Model.HasValue("multiValueSlider"))
{
    var value = Model.Value<Umbraco.Cms.Core.Models.Range<decimal>>("multiValueSlider");
    <p>@(value.Minimum) and @(value.Maximum)</p>
}
```

```
// with a range off
@if (Model.SingleValueSlider != null)
{
    var value = Model.SingleValueSlider;
    <p>@value</p>
}

// with a range on
@if (Model.MultiValueSlider != null)
{
    var minValue = Model.MultiValueSlider.Minimum;
    var maxValue = Model.MultiValueSlider.Maximum;
    <p>@minValue and @maxValue</p>
}
```

```
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Set the value of the property with alias 'singleValueSlider'. 
    content.SetValue("singleValueSlider", 10);

    // Save the change
    ContentService.Save(content);
}
```

```
@using Umbraco.Cms.Core.Models
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Create a variable for the desired value of the 'multiValueSlider' property
    var range = new Range<decimal> {Minimum = 10, Maximum = 12};

    // Set the value of the property with alias 'multiValueSlider'. 
    content.SetValue("multiValueSlider", range);

    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'singleValueSlider'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.SingleValueSlider).Alias, 10);

    // Set the value of the property with alias 'multiValueSlider'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.MultiValueSlider).Alias, new Range<decimal> {Minimum = 10, Maximum = 12});
}
```

---


## Tags | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-007770a99a36a113312d07f127f738d7ef452aeb%252Ftags-DataType.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b4e87b11&sv=2)

Tag group

Storage type

Content Examples

CSV tags

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ad132be4a7ff2b45367988c3bd50fdd3ac1e628f%252FCsv-example-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=874c3181&sv=2)

JSON tags

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-509f6bc80d876cd4d49dca91c119034e08dfd487%252FJson-example-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=32256f10&sv=2)

Tags typeahead

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-36c7d8ab5602d4cc13ae2e6ab87750020195f316%252FTypeahead-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a0b431be&sv=2)

MVC View Example - displays a list of tags

Multiple items - with Models Builder

Multiple items - without Models Builder

Setting Tags Programmatically

More on working with Tags

Last updated

Was this helpful?

---


## Textarea | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0373a9f3dec9bb178a1823e5f5344a123d37743d%252FTextarea-Setup.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=de53b204&sv=2)

Settings

Content Example

Without a character and rows limit

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a705fe2e373e207c19f39dc902741207ffa389f5%252FTextarea-Content-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d786e1a6&sv=2)

With a character limit and rows limit

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-11b0429ae07c22dd6c017b6e61ffaf26394801c6%252FTextarea-Content-Limit-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f7121f87&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Add value programmatically

Last updated

Was this helpful?

---


## Textbox | CMS

How to use the TextBox property editors in Umbraco CMS.

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7580494508826ed5e9bfcd14cbcd9843b46c3912%252FTextbox-Setup.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=633a737d&sv=2)

Content Example

Without a character limit

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0d11476b79d45c8ecd45c65e191ec9f616ec9ba5%252FTextbox-Content-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=24009d9b&sv=2)

With a character limit

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-3fac1920ccf3d7b31eaa79cf2b35dda6803b29e8%252FTextbox-Content-Limit-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e6fb8941&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

Last updated

Was this helpful?

---


## Toggle | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-70eab847d6424b3c9a8f8952b14d10d5a546f56c%252FCheckbox-Data-Type.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5997a507&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-816cd8946248f62dabcc02d62b1112a55e087971%252FCheckbox-Content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=10e6c5b1&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.TrueFalse`


`UI Alias: Umb.PropertyEditorUi.Toggle`


`Returns: Boolean`


Toggle is a standard checkbox which saves either 0 or 1, depending on the checkbox being checked or not.

Data Type Definition Example

The Toggle property has a setting which allows you to set the default value of the checkbox, either checked (true) or unchecked (false).

It is also possible to define a label, that will be displayed next to the checkbox on the content.

Content Example

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@{
    if (!Model.Value<bool>("myCheckBox"))
    {
        <p>The Checkbox is not checked!</p>
    }
}
```

```
@{
    if (!Model.MyCheckbox)
    {
        <p>The Checkbox is not checked!</p>
    }
}
```

```
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = new Guid("796a8d5c-b7bb-46d9-bc57-ab834d0d1248");
    
    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Set the value of the property with alias 'myCheckBox'
    content.SetValue("myCheckBox", true);
            
    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'myCheckBox'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.MyCheckBox).Alias, true);
}
```

---


## User Picker | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4edc07b73e6eeb475c7c246637ed486b0af74f50%252FUser-Picker-DataType.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=61552eb7&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b10862a78f22425116243b67815872cb1a9ba1a1%252FUser-Picker-Content-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6f2d627d&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.UserPicker`


`UI Alias: Umb.PropertyEditorUi.UserPicker`


`Returns: IPublishedContent`


The user picker opens a panel to pick a specific user from the Users section. The value saved is of type IPublishedContent.

Data Type Definition Example

Content Example

MVC View Example

Getting the Value of the property will return the user ID - properties of the User can be accessed by referencing UserService.

Without Models Builder

With Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@using Umbraco.Cms.Core.Services;
@inject IUserService UserService;
@{
    
    if (Model.Value("userPicker") != null)
    {
        var us = UserService;
        var username = us.GetUserById(Model.Value<int>("userPicker")).Name;

        <p>This is the chosen person: @username</p>
        <p>This returns the id value of chosen person: @Model.Value("userPicker")</p>
    }
}
```

```
@using Umbraco.Cms.Core.Services;
@inject IUserService UserService;
@{
    if (Model.UserPicker != null)
    {

        var us = UserService;
        var user = us.GetUserById((int)Model.UserPicker);

        <p>This is the chosen person: @user.Name</p>
        <p>This returns the id value of chosen person: @user.Id)</p>
    }
}
```

```
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = new Guid("796a8d5c-b7bb-46d9-bc57-ab834d0d1248");
    
    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Set the value of the property with alias 'userPicker'. The value is the specific ID of the user
    content.SetValue("userPicker", -1);
            
    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'userPicker'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.UserPicker).Alias, -1);
}
```

---
