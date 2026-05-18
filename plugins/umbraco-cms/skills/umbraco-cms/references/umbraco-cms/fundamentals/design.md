# Design

## Contents

- [Partial Views | CMS](#partial-views-cms)
- [Rendering Content | CMS](#rendering-content-cms)
- [Rendering Media | CMS](#rendering-media-cms)
- [Stylesheets And JavaScript | CMS](#stylesheets-and-javascript-cms)
- [Templates](#templates)

---

## Partial Views | CMS

Information on working with partial views in Umbraco

A Partial View (`.cshtml`

file) is a regular view that can be used multiple times throughout your site. A Partial View is used to break up large markup files into smaller components such as header, footer, navigation menu, and so on. It helps to reduce the duplication of code. A partial view renders a view within the parent view.

You can create and edit partial views from the **Partial Views** folder in the **Settings** section of the Backoffice.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-293bfd5f7a6236a33247ec78ae0984a46bddde01%252Fcreate-partial.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1babfb7c&sv=2)

In the **Create** menu, there are three options available:

Empty partial view

Partial view from snippet

Folder... (for keeping the partial views organized)


To create a partial view:

Go to the

**Settings**section in the Umbraco backoffice.Click

**...**next to the**Partial Views**folder.Choose

**Create**.Select

**Empty partial view**.Enter a partial view name.

Click the

**Save**button. You will now see the partial view markup in the backoffice editor.

![Created partial view](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-59a225d601a266af68e1d5e6f7911a14e1a60b38%252FCreated-partial-view.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c9c3511a&sv=2)

By default, the partial views are saved in the `Views/Partials`

folder in the solution.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6064691f5ad93e9ad5fadd6b638b045228ffe019%252Fpartial-views-in-directory.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=307a0ecd&sv=2)

To create a partial view from the snippet:

Go to the

**Settings**section in the Umbraco backoffice.Click

**...**next to the**Partial Views**folder.Choose

**Create**.Select

**Empty partial view from snippet**.Select the snippet you want to create a partial view for and enter a partial view name. The code snippet you selected is displayed in the backoffice editor.

Click the

**Save**button.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4ee069f7343f7293038b546c412f79f1a62f0f94%252FCreated-partial-view-from-snippet.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5af383a8&sv=2)

Umbraco provides the following partial view snippets:

Empty - Creates an empty partial view file.

Breadcrumb - Creates a breadcrumb of parents using the

`Ancestors()`

method to generate links in an unordered HTML list. It displays the name of the current page without a link.Edit Profile - Creates a Member profile model that can be edited.

List Ancestors From Current Page - Displays a list of links to the parents of the current page using the

`Ancestors()`

method to generate links in an unordered HTML list. It displays the name of the current page without a link.List Child Pages From Current Page - Displays a list of links to the children of the current page using the

`Children()`

method to generate links in an unordered HTML list.List Child Pages Ordered By Date - Displays a list of links to the children of the current page using the

`Children()`

method to generate links in an unordered HTML list. The pages are sorted by the creation date in a descending order using the`OrderByDescending()`

method.List Child Pages Ordered By Name - Displays a list of links to the children of the current page using the

`Children()`

method to generate links in an unordered HTML list. The pages are sorted by the page name using the`OrderBy()`

method.List Child Pages With DocType - Displays only the children of a certain Document Type.

List Descendants From Current Page - Displays a list of links for every page below the current page in an unordered HTML list.

Login - Displays a login form.

Login Status - Displays the user name if the user is logged in.

Multinode Tree-picker - Lists the items from a Multinode tree picker using the picker's default settings.

Navigation - Displays a list of links of the pages under the top-most page in the Content tree. It also highlights the currently active page/section in the navigation menu.

Register Member - Displays a Member registration form. It will only display the properties marked as

**Member can edit**on the**Info**tab of the Member Type.Site Map - Displays a list of links of all the visible pages of the site using the

`Traverse()`

method to select and display the markup and links as nested unordered HTML lists.

To create a folder:

Go to the

**Settings**section in the Umbraco backoffice.Click

**...**next to the**Partial Views**folder.Choose

**Create**.Select

**Folder**.Enter a folder name.

Click the

**Create**button.

![Created folder](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9c11c2c080f15826c770b8db32c4290d3c23b95a%252FCreated-folder.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b8c460f6&sv=2)

To render a partial view into any template, use any of these helper methods:

`PartialAsync`

(async Razor helper)`<partial>`

Razor tag helperLast updated

Was this helpful?

---

## Rendering Content | CMS

*The primary task of any template is to render the values of the current page or the result of a query against the content cache.*

Each property in your [Document Type](/umbraco-cms/fundamentals/data/defining-content#what-is-a-document-type) has an alias, this is used to specify where in the template view to display the value.

```
<h1>@Model.Value("pageTitle")</h1>
<div>@Model.Value("bodyContent")</div>
<time>@Model.Value("articleDate")</time>
```

You can specify the type of data being returned to help you format the value for display.

In our example, we have a string, a date and some rich text:

```
<h1>@(Model.Value<string>("pageTitle"))</h1>
<div>@(Model.Value<IHtmlEncodedString>("bodyContent"))</div>
<p>Article date: <time>@(Model.Value<DateTime>("articleDate").ToString("dd/MM/yyyy"))</time></p>
```

To use `IHtmlEncodedString`

as the typed value, add the `@using Umbraco.Cms.Core.Strings;`

directive.

```
<h1>@Model.PageTitle</h1>
<div>@Model.BodyContent</div>
<time>@Model.ArticleDate.ToString("dd/MM/yyyy")</time>
```

The `.Value()`

method has a number of optional parameters that support scenarios where we want to "fall-back" to some other content.

To use the `fallback`

type, add the `@using Umbraco.Cms.Core.Models.PublishedContent;`

directive.

To display a static, default value when a property value is not populated on the current content item:

A second supported method is to traverse up the tree ancestors to try to find a value. If the current content item isn't populated for a property, we can retrieve the value from the parent, grand-parent, or a higher ancestor in the tree. The first ancestor encountered that has a value will be the one returned.

If developing a multi-lingual site and fall-back languages* have been configured, the third method available is to retrieve a value for a different language, if the language we are requesting does not have content populated. In this way, we could render a field containing French content for a property if it's populated in that language, and if not, default to English.

We can also combine these options to create some more sophisticated scenarios. For example, we might want to fall-back via language first, and if that doesn't find any populated content, then try to find a value by traversing through the ancestors of the tree. We can do that using the following syntax, with the order of the fall-back options provided determining the order that content will be attempted to be retrieved:

In this example, we are looking for content firstly on the current node for the default language, and if not found we'll search through the ancestors. If failing to find any populated value from them, we'll use the provided default:

We can use similar overloads when working with ModelsBuilder, for example:

Fall-back languages can be configured via the

**Languages**tree within the**Settings**section.Each language can optionally be provided with a fall-back language, that will be used when content is not populated for the language requested and the appropriate overload parameters are provided.

It is possible to chain these language fall-backs, so requesting content for Portuguese, could fall-back to Spanish and then on to English.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-bb48e1690366f3476a7695e7437acd5248edf35d%252Flanguage-fallback.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b8e0925a&sv=2)

Configuring fall-back languages


In many cases, you want to do more than display values from the current page, like creating a list of pages in the navigation. You can access content relative to the current page using methods such as `Children()`

, `Descendants()`

& `Ancestors()`

. Explore the [full list of methods](/umbraco-cms/reference/templating/mvc/querying#traversing).

You can do this by querying content relative to your current page in template views:

You can use the Query Builder in the template editor to build more advanced queries. ![Query button](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2d4e00f98b809da3ef94dbde24b11347c60e7c82%252Fbutton-v8.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=a6e63fcc&sv=2)


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-53dd76262ebc185941ea43c5b1139db7bfd737eb%252Fquery-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=bc2a86fa&sv=2)

Last updated

Was this helpful?

---

## Rendering Media | CMS

Info on rendering media items and imaging cropping

*Templates (Views) can access items in the* [Media library](/umbraco-cms/fundamentals/data/creating-media) *to assist in displaying rich content like galleries*.

In the following examples, we will be looking at rendering an `Image`.


Image is only one of the 'types' of Media in Umbraco. The same principles apply to all Media Types. The properties available to render will be different from Media Type to Media Type. For example, a `File`

will not have a Width property.

A media item is not only a reference to a static file. Like content, it is a collection of fields, such as width, height, and file path. This means that accessing and rendering media in a Template is similar to rendering content.

An uploaded image in the Media library is based on the Media Type `Image`

which has a number of standard properties:

Name

Width & Height

Size

Type (based on file extension)

UmbracoFile (the path to the file or JSON data containing crop information)


These standard properties are pre-populated and set during the upload process. For example, this means that the width and height are calculated for you.

If you want to add further properties to use with your Media Item, edit the Image Media Type under **Settings**. In this example, we are going to retrieve an image from the Media section. Then we will render out an `img`

tag using the URL of the media item and use the Name as the value for the `alt`

attribute.

The Media item in the following sample will use a sample Guid (`55240594-b265-4fc2-b1c1-feffc5cf9571`

). This example is **not using Models Builder**.

```
@{
    // The Umbraco Helper has a Media method that will retrieve a Media Item by Guid in the form of IPublishedContent. In this example, the Media Item has a Guid of 55240594-b265-4fc2-b1c1-feffc5cf9571

    var mediaItem = Umbraco.Media(Guid.Parse("55240594-b265-4fc2-b1c1-feffc5cf9571"));

    if (mediaItem != null)
    {
        // To get the URL for your media item, you use the Url method:
        var url = mediaItem.Url();
        // to read a property by alias
        var imageHeight = mediaItem.Value<int>("umbracoHeight");
        var imageWidth = mediaItem.Value<int>("umbracoWidth");
        var orientationCssClass = imageWidth > imageHeight ? "img-landscape" : "img-portrait";

        <img src="@url" alt="@mediaItem.Name" class="@orientationCssClass"/>
    }
}
```

But wait a second, Umbraco comes with [Models Builder](/umbraco-cms/reference/templating/modelsbuilder). This means that you can use strongly typed models for your media items if Models Builder is enabled (which it is by default).

As with example one, we are accessing a MediaType `image`

using the same Guid assumption.

It is always worth having null-checks around your code when retrieving media in case the conversion fails or Media() returns null. This makes your code more robust.

If you upload a video file (such as `.mp4`

) to the Media library, Umbraco will store it as a Video Media Type by default. Unlike images, video files won’t include properties like `umbracoWidth`

or `umbracoHeight`

, but you can still retrieve the media item and render it using the `<video>`

HTML tag.

The example above assumes that:

You've uploaded an

`.mp4`

file to the**Media**section.You want to include basic playback controls in the browser.

You know the media item’s ID.


You can also add custom properties to your Video Media Type (for example: `thumbnail`

, `autoplay`

, `caption`

) under **Settings** > **Media Types**.

`File`

Accessing other media items can be performed in the same way. The techniques are not limited to the `Image`

type, but it is one of the most common use cases.

The Image Cropper can be used with `Image`

Media Types and is the default option for the `umbracoFile`

property on an `Image`

Media Type.

When working with the Image Cropper for an image the `GetCropUrl`

extension method is used to retrieve cropped versions of the image. Details of the Image Cropper property editor and other examples of using it can be found in the [Image Cropper article](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/image-cropper). The following is an example to help you get started with the Image Cropper.

This example assumes that you have set up a crop called **square** on your Image Cropper Data Type.

If you want the original, uncropped image, you can ignore the GetCropUrl extension method and use one of the previously discussed approaches as shown below.

Last updated

Was this helpful?

---

## Stylesheets And JavaScript | CMS

Information on working with stylesheets and JavaScript in Umbraco.

Stylesheets in the Backoffice

Creating a stylesheet

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7dc66b621a4a8b422735beeb5f138fa8dcad1e7a%252Fcreating-stylesheet.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6757fa2f&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5ef36e3457aa710aff1b8894cce1fcb15247293f%252Fstylesheet-editor.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=45082987&sv=2)

Using stylesheets

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f2fbedbfe171e1938503f6c04943b608b0c1540b%252Flinking-stylesheet.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=771f5af3&sv=2)

JavaScript files in the Backoffice

Creating a JavaScript file

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-01e9e9ccbfeb8e00101b55cd2fa0d2613b13a66c%252Fcreating-scripts.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c53a2408&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-05e545fe84e7f302ec22b333222c4b6f3f346d3e%252Fsample-Javacsript.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9ee9150d&sv=2)

Using JavaScript files

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-45f213d66c0fc51615496adb72b94b47e6ace72d%252Fscript-reference.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c39a8ea3&sv=2)

Rich Text Editor styling

Last updated

Was this helpful?

---

## Templates

### Contents

- [Basic Razor Syntax | CMS](#basic-razor-syntax-cms)
- [Razor Cheatsheet | CMS](#razor-cheatsheet-cms)

---

### Basic Razor Syntax | CMS

How to perform common logical tasks in Razor like if/else, foreach loops, switch statements and using the @ character to separate code and markup

The @ symbol

```
@* Writing a value inside a html element *@

<p>@Model.Name</p>

@* Inside an attribute *@
<a href="@Model.Url()">@Model.Name</a>

@* Using it to start logical structures *@
@if (selection?.Length > 0)
{
    <ul>
        @foreach (var item in selection)
        {
            <li>
                <a href="@item.Url(PublishedUrlProvider)">@item.Name</a>
            </li>
        }
    </ul>
}
```

Embedding comments in razor

If/else

Foreach loops

Switch block

More information

Last updated

Was this helpful?

---

### Razor Cheatsheet | CMS

All the code snippets you need to get a jump start on building templates with Razor in Umbraco CMS.

Last updated

Was this helpful?

All the code snippets you need to get a jump start on building templates with Razor in Umbraco CMS.

The Razor Cheatsheet is a collection of common methods used for building templates and views in Umbraco CMS.

Get the Umbraco 11 Cheatsheet:

You can also find the where you can give feedback, contribute, or download the template used to *generate* the sheet.

Use the cheatsheet if you:

Use Models Builder on your project and

Use Umbraco 11.


Most of the methods in the Umbraco 11 version of the cheatsheet will also work in Umbraco 10 and 9.

Last updated

Was this helpful?

Was this helpful?

---

---
