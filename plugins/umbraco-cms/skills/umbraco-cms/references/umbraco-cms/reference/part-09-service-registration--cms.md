# Reference — Part 9: Service Registration | CMS → Website Output Caching | CMS

## Service Registration | CMS

Learn how to configure Umbraco to run only the services required on each specific server in your setup.

Supported Configurations

| Configuration | AddCore() | AddBackOfficeSignIn() | AddBackOffice() | AddWebsite() | AddDeliveryApi() |
|---|---|---|---|---|---|
| Full (default) | |||||
| Website + Delivery API | |||||
| Website + Basic Auth | |||||
| Website Only | |||||
| Delivery APIOnly |

Configuration use cases

Full Umbraco (default)

Website + Delivery API (no backoffice)

Website with basic authentication (no backoffice)

Website only

Delivery API only

Key differences between configurations

Middleware

Endpoints

Considerations for Composers

Last updated

Was this helpful?

---


## Templating

### Contents

- [Macros | CMS](#macros-cms)
- [Modelsbuilder](#modelsbuilder)
- [Mvc](#mvc)

---

### Macros | CMS

Last updated

Was this helpful?

**Are you looking for documentation about Macros and/or Partial View Macros?

Macros and Partial View Macros have been removed with the release of Umbraco 14.

We recommend using [Partial Views](/umbraco-cms/fundamentals/design/partial-views) or [Blocks in the Rich Text Editor](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/rich-text-editor/blocks) as a replacement.

Learn more about the decision for remove Macros in the official announcement: [Breaking change: Macros will be removed in Umbraco 14 arrow-up-right](https://github.com/umbraco/Announcements/issues/14)

Last updated

Was this helpful?

Was this helpful?

---

### Modelsbuilder

#### Contents

- [Builder Modes | CMS](#builder-modes-cms)
- [Configuration | CMS](#configuration-cms)
- [Tips and Tricks | CMS](#tips-and-tricks-cms)
- [Introduction | CMS](#introduction-cms)
- [Understand and Extend | CMS](#understand-and-extend-cms)
- [Using Interfaces | CMS](#using-interfaces-cms)

---

#### Builder Modes | CMS

Modelsbuilder modes

Models Builder can be used in different modes:

InMemory models

SourceCode models


The mode is indicated by the `Umbraco:CMS:ModelsBuilder:ModelsMode`

key in the configuration (`appsettings.json`

files).

**Example ****appsettings.json**** configuration**

```
{
  "Umbraco": {
    "CMS": {
      "ModelsBuilder": {
        "ModelsMode": "InMemoryAuto"
      }
    }
  }
}
```

Replace `InMemoryAuto`

with one of the valid options: `SourceCodeAuto`

, `SourceCodeManual`

, or `InMemoryAuto`

depending on your preferred mode.

Corresponds to the `InMemoryAuto`

setting value.

With **InMemory** models, models are generated and compiled on the fly, in memory, at runtime. They are available in views exclusively.

This is for a setup that exclusively uses the Umbraco backoffice, and do not use custom code such as controllers. Whenever a content type is modified, models are updated without restarting Umbraco (in the same way .cshtml views are recompiled).

Generation *can* fail for various reasons, in which case Umbraco will run without models (and front-end views fail to render). Umbraco's log file should contain all details about what prevented the generation, but it is probably faster to check the Models Builder dashboard, which should report the last error that was encountered, if any.

Models Builder maintains some files in `~/umbraco/Data/TEMP/InMemoryAuto`:


`models.generated.cs`

contains the generated models code`all.generated.cs`

contains the compiled code (models merged with non-generated files)`models.hash`

contains a hash code of the content types`all.dll.path`

contains the path to the compiled DLL file containing all the models`Compiled/generated.cs{GUID}.dll`

the dll containing all the generated models`models.err`

contains the last generation error information, if any

The `models.hash`

file is used when Umbraco restarts, to figure out whether models have changed and need to be re-generated. Otherwise, the local `models.generated.cs`

file is reused.

Corresponds to the `SourceCodeManual`

and `SourceCodeAuto`

setting values.

With **SourceCode** models, models are generated in the `~/umbraco/models`

directory, and that is all. It is then up to you to decide how to compile the models (e.g. by including them in a Visual Studio solution).

Generation *can* fail for various reasons, in which case no models are generated. Umbraco's log file should contain all details about what prevented the generation, but it is probably faster to check the Models Builder dashboard, which should report the last error that was encountered, if any.

The modelsbuilder works much in the same way whether using `SourceCodeManual`

or `SourceCodeAuto`

. The only real difference between the two are that with `SourceCodeManual`

you must manually trigger the generation of the models from the models builder dashboard, whereas with `SourceCodeAuto`

the models are automatically generated whenever content types change.

These modes are not available in the embedded version of Models Builder. See the full version of .

Last updated

Was this helpful?

---

#### Configuration | CMS

Explanation of how to configure models builder

The following configuration option can be set in the application settings (in the `appsettings.json`

file):

`Umbraco.CMS.ModelsBuilder.ModelsMode`

determines how Models Builder generates models. Valid values are:`Nothing`

: Do not generate models.`InMemoryAuto`

(default): Generate models in a dynamic in-memory assembly.`SourceCodeManual`

: Generate models in`~/umbraco/models`

(but do not compile them) whenever the user clicks the "Generate models" button on the Models Builder dashboard in the Settings section.`SourceCodeAuto`

: Generate models in`~/umbraco/models`

(but do not compile them) anytime a content type changes.

`Umbraco.CMS.ModelsBuilder.ModelsNamespace`

(string, default is`Umbraco.Cms.Web.Common.PublishedModels`

) specifies the generated models' namespace.`Umbraco.CMS.ModelsBuilder.FlagOutOfDateModels`

(bool, default is`true`

) indicates whether out-of-date models (for example after a content type or Data Type has been modified) should be flagged.`Umbraco.CMS.ModelsBuilder.ModelsDirectory`

(string, default is`~/umbraco/models`

) indicates where to generate models and manage all files. Has to be a virtual directory (starting with`~/`

) below the website root (see also:`AcceptUnsafeModelsDirectory`

below).`Umbraco.CMS.ModelsBuilder.AcceptUnsafeModelsDirectory`

(bool, default is`false`

) indicates that the directory indicated in`ModelsDirectory`

is allowed to be outside the website root (e.g.`~/../../some/place`

). Due to this being a potential security risk, it is not allowed by default.`Umbraco.CMS.ModelsBuilder.DebugLevel`

(int, default is zero) indicates the debug level. Set to greater than zero to enable detailed logging. For internal / development use.

The example below shows an example configuration using the SourceCodeManual mode.

```
{
  "$schema": "https://json.schemastore.org/appsettings.json",
  "Umbraco": {
    "CMS": {
      "ModelsBuilder": {
        "ModelsMode": "SourceCodeManual"
      }
    }
  }
}
```

It is recommended to generate models in your development environment only and change the ModelsMode to `Nothing`

for your staging and production environments.

Models Builder ships with a dashboard in the *Settings* section of Umbraco's backoffice. The dashboard does three things:

Details on how Models Builder is configured

Provides a way to generate models (in SourceCodeManual mode only)

Reports the last error (if any) that would have prevented models from being properly generated


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-07969cbfdbac260b5531e3ca2f2c2aa60e98b480%252FModelsBuilderDashboard-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f31300ff&sv=2)

Last updated

Was this helpful?

---

#### Tips and Tricks | CMS

Cool things you can do with models

```
@functions
{
  // Declare how to render a news item
  void RenderContent(NewsItem item)
  {
    <div>News! @item.Title</div>
  }

  // Declare how to render a product
  void RenderContent(Product item)
  {
    <div>Product! @product.Name cheap at @product.Price</div>
  }
}

@{
  RenderContent((dynamic) Model);
}
```

Last updated

Was this helpful?

Cool things you can do with models

It's possible with Razor to define functions for rendering HTML. We can leverage our strongly typed models when doing this, and even provide overloads for different types of models. That will automatically be called for different models using `dynamic`


```
@functions
{
  // Declare how to render a news item
  void RenderContent(NewsItem item)
  {
    <div>News! @item.Title</div>
  }

  // Declare how to render a product
  void RenderContent(Product item)
  {
    <div>Product! @product.Name cheap at @product.Price</div>
  }
}

@{
  RenderContent((dynamic) Model);
}
```

It's not recommended to create a template and doing all the rendering via razor function, but it can be nifty for rendering search results.

A thing that's important to note here is that `RenderContent`

is called from a codeblock, and not as `@RenderContent((dynamic) Model);`

the reason for this is that if you try to use the latter, razor will expect for the function to return something for it to render.

By casting the strongly typed to a dynamic when calling the **RenderContent** method, you tell C# to do late runtime binding. You also tell it to pick the proper **RenderContent** implementation depending on the actual Common Language Runtime (CLR) type of the **content** object. Using dynamic here is OK and will not pollute the rest of the code.

Last updated

Was this helpful?

Was this helpful?

---

#### Introduction | CMS

Modelsbuilder introduction

Models Builder is a tool that can generate a complete set of strongly-typed published content models for Umbraco. By default, a slimmed down version of Models Builder is embedded with the main Umbraco distribution.

Models can be used anywhere that content is retrieved from the content cache, i.e. in MVC views, controllers, etc. In other words, when using the Models Builder, the content cache does not return `IPublishedContent`

objects anymore, but strongly typed models, implementing `IPublishedContent`.


For each content, media and member type in the Umbraco setup, the generator creates a `*.generated.cs`

file, corresponding to the type. For instance, a document type with a textstring property named Title, and a rich text editor named BodyText will look like this:

```
//------------------------------------------------------------------------------
// <auto-generated>
//   This code was generated by a tool.
//
//    Umbraco.ModelsBuilder.Embedded v15.0.0
//
//   Changes to this file will be lost if the code is regenerated.
// </auto-generated>
//------------------------------------------------------------------------------

using System;
using System.Linq.Expressions;
using Umbraco.Cms.Core.Models.PublishedContent;
using Umbraco.Cms.Core.PublishedCache;
using Umbraco.Cms.Infrastructure.ModelsBuilder;
using Umbraco.Cms.Core;
using Umbraco.Extensions;

namespace Umbraco.Cms.Web.Common.PublishedModels
{
/// <summary>NewsItem</summary>
[PublishedModel("newsItem")]
public partial class NewsItem : PublishedContentModel
{
  // helpers
#pragma warning disable 0109 // new is redundant
  [global::System.CodeDom.Compiler.GeneratedCodeAttribute("Umbraco.ModelsBuilder.Embedded", "15.0.0")]
  public new const string ModelTypeAlias = "newsItem";
  [global::System.CodeDom.Compiler.GeneratedCodeAttribute("Umbraco.ModelsBuilder.Embedded", "15.0.0")]
  public new const PublishedItemType ModelItemType = PublishedItemType.Content;
  [global::System.CodeDom.Compiler.GeneratedCodeAttribute("Umbraco.ModelsBuilder.Embedded", "15.0.0")]
  [return: global::System.Diagnostics.CodeAnalysis.MaybeNull]
  public new static IPublishedContentType GetModelContentType(IPublishedContentTypeCache contentTypeCache)
  	=> PublishedModelUtility.GetModelContentType(contentTypeCache, ModelItemType, ModelTypeAlias);
  [global::System.CodeDom.Compiler.GeneratedCodeAttribute("Umbraco.ModelsBuilder.Embedded", "15.0.0")]
  [return: global::System.Diagnostics.CodeAnalysis.MaybeNull]
  public static IPublishedPropertyType GetModelPropertyType<TValue>(IPublishedContentTypeCache contentTypeCache, Expression<Func<Page, TValue>> selector)
    => PublishedModelUtility.GetModelPropertyType(GetModelContentType(contentTypeCache), selector);
#pragma warning restore 0109

  private IPublishedValueFallback _publishedValueFallback;

  // ctor
  public NewsItem(IPublishedContent content, IPublishedValueFallback publishedValueFallback)
    : base(content, publishedValueFallback)
  {
    _publishedValueFallback = publishedValueFallback;
  }

  // properties

  ///<summary>
  /// BodyText
  ///</summary>
  [global::System.CodeDom.Compiler.GeneratedCodeAttribute("Umbraco.ModelsBuilder.Embedded", "15.0.0")]
  [global::System.Diagnostics.CodeAnalysis.MaybeNull]
  [ImplementPropertyType("bodyText")]
  public virtual global::Umbraco.Cms.Core.Strings.IHtmlEncodedString BodyText => this.Value<global::Umbraco.Cms.Core.Strings.IHtmlEncodedString>(_publishedValueFallback, "bodyText");

  ///<summary>
  /// Title
  ///</summary>
  [global::System.CodeDom.Compiler.GeneratedCodeAttribute("Umbraco.ModelsBuilder.Embedded", "15.0.0")]
  [global::System.Diagnostics.CodeAnalysis.MaybeNull]
  [ImplementPropertyType("title")]
  public virtual string Title => this.Value<string>(_publishedValueFallback, "title");
  }
}
```

Now since this is an automatically generated file, it's a bit messy, the important part is that it has all the properties defined and strongly typed:

And:

Umbraco's content cache returns these objects *natively*: No need to map, convert or anything; the following code runs:

If your view inherits from `UmbracoViewPage<NewsItem>`

then the model is the content item itself and the syntax is `@Model.Title`.


Models Builder respects the content types' inheritance tree, i.e. models inherit from each other if required, and mixins (content type compositions) are represented by interfaces.

Models Builder is a "*code-after**_" solution. It only generates code from content types that already exist in Umbraco. It is not a "*code-first*" solution - code-first is a much more complex question.

And once you are using strongly typed models, there are some [cool things](/umbraco-cms/reference/templating/modelsbuilder/coolthingswithmodels) that you can do.

The Models Builder is by default embedded in Umbraco. If you need more complex features than what is provided, you still need to add the full package. However, as of right now the package is not updated to be able to handle NetCore or Umbraco V9.

Check [the official releases on the Models Builder GitHub repository arrow-up-right](https://github.com/zpqrtbnk/Zbu.ModelsBuilder/releases)

At the core of the strongly typed models "experience" is the `IPublishedModelFactory`

interface. This interface is part of the Umbraco core codebase. It is responsible for mapping the internal `IPublishedContent`

implementations returned by the content cache, to strongly typed models. There is a default factory shipped with Umbraco and it is possible to replace this by custom implementations. When using the default factory, models do *not* necessarily need to be generated by Models Builder.

Models Builder is one way to generate models for the default, built-in factory. Models can be generated automatically or straight from the Settings section of the Umbraco backoffice, for more info see [builder modes](/umbraco-cms/reference/templating/modelsbuilder/builder-modes).

Last updated

Was this helpful?

---

#### Understand and Extend | CMS

Understanding and Extending ModelsBuilder in Umbraco

Umbraco’s Models Builder automatically generates strongly typed models for content types, allowing developers to work with Umbraco data in a structured and efficient manner. This article explains how models are generated, how composition and inheritance work, and best practices for extending models without causing issues.

Models Builder generates each content type as a partial class. For example, a content type named `TextPage`

results in a `TextPage.generated.cs`

file with a structure like this:

```
/// <summary>TextPage</summary>
[PublishedModel("textPage")]
public partial class TextPage : PublishedContentModel
{
  //static helpers
  public new const string ModelTypeAlias = "textPage";

  public new const PublishedItemType ModelItemType = PublishedItemType.Content;

  public new static IPublishedContentType GetModelContentType(IPublishedContentTypeCache contentTypeCache)
  	=> PublishedModelUtility.GetModelContentType(contentTypeCache, ModelItemType, ModelTypeAlias);

  public static IPublishedPropertyType GetModelPropertyType<TValue>(IPublishedContentTypeCache contentTypeCache, Expression<Func<Page, TValue>> selector)
    => PublishedModelUtility.GetModelPropertyType(GetModelContentType(contentTypeCache), selector);

  private IPublishedValueFallback _publishedValueFallback;

  //constructor
  public TextPage(IPublishedContent content, IPublishedValueFallback publishedValueFallback)
    : base(content, publishedValueFallback)
  {
    _publishedValueFallback = publishedValueFallback;
  }

  // properties

  ///<summary>
  /// Header
  ///</summary>
  [ImplementPropertyType("header")]
  public virtual string Header => this.Value<string>(_publishedValueFallback, "header");
}
```

In the above code:

The model includes a constructor and static helpers to fetch the content type (

`PublishedContentType`

) and property type (`PublishedPropertyType`

).The most important part is the property definition (

`Header`

), which retrieves values from Umbraco.

You can use helper methods to access content and property types:

Umbraco content types can be composed of multiple other content types. Unlike traditional C# inheritance, Umbraco allows a content type to inherit properties from multiple sources.

In Umbraco v14, the traditional .NET Inheritance feature has been removed. Instead, properties are inherited through Composition, allowing for greater flexibility in managing content types.

For example, a `TextPage`

might be composed of:

**MetaInfo**content type (inherits`Author`

and`Keywords`

properties).**PageInfo**content type (inherits`Title`

and`MainImage`

properties).

Each content type in a composition is generated both as a class and as an interface. The `MetaInfo`

content type would be generated as:

And the `TextPage`

model would be generated as:

In addition to composition, earlier versions of Umbraco allowed content types to have a parent-child relationship. In the Umbraco backoffice, a content type appears underneath its parent.

The option to add child content types in the backoffice was removed in v14. Migrated sites may still have the child content types set up. New content types can be inherited through Composition.

This type of inheritance is treated differently since the content type is always **composed of its parent**. The child content type *inherits directly* (as in C# inheritance) from the parent class.

If `AboutPage`

is a child of TextPage, its generated model would inherit directly from `TextPage`:


Since models are partial classes, developers can extend them by adding additional properties.

For Example:

Models Builder does not recognize custom partial classes during regeneration. If your custom class conflicts with the generated class (e.g., overriding a constructor), it will cause compilation errors.

Overloaded constructors will not be used because models are always instantiated using the default constructor.

For more complex customizations, use the full version of .

From Umbraco 11.4, you can implement the `IModelsGenerator`

interface to customize how models are generated. This allows you to replace Umbraco’s default implementation using dependency injection:

The interface can be accessed via `Infrastructure.ModelsBuilder.Building.ModelsGenerator`.


Extending models should be used to add stateless, local features to models. It should not be used to transform *content* models into view models or manage trees of content.

A customer has "posts" that has two "release date" properties. One is a true date picker property and is used to specify an actual date and to order the posts. The other is a string that is used to specify dates such as "Summer 2015" or "Q1 2016". Alongside the title of the post, the customer wants to display the text date, if present, else the actual date. If none of those are present, the Umbraco update date should be used. Keep in mind that each view can contain code to deal with the situation, but it is much more efficient to extend the `Post`

model:

Simplified view:

Because, by default, the content object is passed to views, one can be tempted to add view-related properties to the model. Some properties that do *not* belong to a *content* model would be:

A

`HomePage`

property that retrieves the "home page" content item.A

`Menu`

property that lists navigation items.

Generally speaking, anything that is tied to the current request, or that depends on more than the modeled content, is a bad idea. There are much cleaner solutions, such as using true *view model* classes that would be populated by a true controller and look like:

One can also extend Umbraco's views to provide a special view helper that gives access to important elements of the website:

The model's scope and lifecycle are *unspecified*. It may exist only for your request or be cached and shared across all requests.

The code has a major issue: the `TextPage`

model caches a `HomePageDocument`

model that will not update when the home page is re-published.

As a rule of thumb, models should never reference and cache other models.

Last updated

Was this helpful?

---

#### Using Interfaces | CMS

Using interfaces with modelsbuilder

When using compositions, Models Builder generates an interface for the composed model, which enables us to not have to switch back to using `Value()`

for the composed properties.

A common use-case for this is if you have a separate composition for the "SEO properties" `Page Title`

and `Page Description`.


You would usually use this composition on both your `Home`

and `Textpage`

document types. Since both `Home`

and `Textpage`

will implement the generated `ISeoProperties`

interface, you will still be able to use the simpler models builder syntax (e.g. `Model.PageTitle`

).

However, you won't be able to use the nice models builder syntax on any master template, since a master template needs to be bound to a generic `IPublishedContent`

. So you'd have to resort to the *ever-so-slightly* clumsier `Model.Value("pageTitle")`

syntax to render these properties. It is possible to solve this issue of master templating, by using partial views, to render the SEO specific properties.

If you create a partial and change the first line to use the *interface name* for the model binding, you can use the nice Models Builder syntax when rendering the properties, like this:

```
@inherits Umbraco.Cms.Web.Common.Views.UmbracoViewPage<ISeoProperties>
<title>@Model.PageTitle</title>
<meta name="description" content="@Model.PageDescription">
```

You can then render the partial from your Master Template with something like this (assuming the partial is named `Metatags.cshtml`

):

```
<head>
    @Html.Partial("Metatags")
</head>
@RenderBody()
```

It's important to note though, that this master template will only work for content types that use the Seo Properties composition.

Last updated

Was this helpful?

---

---

### Mvc

#### Contents

- [View/Razor Examples | CMS](#viewrazor-examples-cms)
- [Creating Forms | CMS](#creating-forms-cms)
- [Using MVC Partial Views in Umbraco | CMS](#using-mvc-partial-views-in-umbraco-cms)
- [Querying & Traversal | CMS](#querying-traversal-cms)
- [Using View Components in Umbraco | CMS](#using-view-components-in-umbraco-cms)
- [Working with MVC Views in Umbraco | CMS](#working-with-mvc-views-in-umbraco-cms)

---

#### View/Razor Examples | CMS

Rendering the raw value of a field from IPublishedContent

```
@Model.Value("bodyContent")
```

Rendering the converted value of a field from IPublishedContent

```
@Model.Value<double>("amount")
@Model.Value<IHtmlString>("bodyContent")
```

Rendering some member data

```
@if(Members.IsLoggedIn()){
    var profile = Members.GetCurrentMemberProfileModel();
    var umbracomember = Members.GetByUsername(profile.UserName);

    <h1>@umbracomember.Name</h1>
    <p>@umbracomember.Value<string>("bio")</p>
}
```

Last updated

Was this helpful?

---

#### Creating Forms | CMS

Last updated

Was this helpful?

Creating an HTML form to submit data with MVC in Umbraco is possible in a few steps.

If you want to create a Form:

Using view models, views, controllers, and a handy HtmlHelper extension method called BeginUmbracoForm, see the

[Creating Forms](/umbraco-cms/fundamentals/code/creating-forms)article.Using Umbraco Forms, see the article.


Last updated

Was this helpful?

Was this helpful?

---

#### Using MVC Partial Views in Umbraco | CMS

This section will show you how to use MVC Partial Views in Umbraco.

Please note, this is documentation relating to the use of native MVC partial views

Partial views allow you to reuse components between your views (templates).

The locations to store Partial Views when rendering in the Umbraco pipeline is:

```
~/Views/Partials
```

The standard MVC partial view locations will also work:

```
~/Views/Shared
~/Views/Render
```

The `~/Views/Render`

location is valid because the controller that performs the rendering in the Umbraco codebase is the: `Umbraco.Cms.Web.Common.Controllers.RenderController`


If however you are [Hijacking an Umbraco route](/umbraco-cms/reference/routing/custom-controllers) and specifying your own controller to do the execution, then your partial view location can also be:

```
~/Views/{YourControllerName}
```

A quick example of a content item that has a template that renders out a partial view template for each of its child documents:

The MVC template markup for the document:

```
@inherits Umbraco.Cms.Web.Common.Views.UmbracoViewPage
@{
    Layout = null;
}

<html>
<body>
@foreach(var page in Model.Children().Where(x => x.IsVisible()))
    {
        <div>
            @Html.Partial("ChildItem", page)
        </div>
    }
</body>
</html>
```

The partial view (located at: `~/Views/Partials/ChildItem.cshtml`

)

Normally you would create a partial view by using the `@model MyModel`

syntax. However, inside of Umbraco you will probably want to have access to the handy properties available on your normal Umbraco views like the Umbraco helper: `@Umbraco`

and the Umbraco context: `@UmbracoContext`

. The good news is that this is possible. Instead of using the `@model MyModel`

syntax, you need to inherit from the correct view class, so do this instead:

By inheriting from this view, you'll have instant access to those handy properties and have your view created with a strongly typed custom model.

Another case you might have is that you want your Partial View to be strongly typed with the same model type (`IPublishedContent`

) as a normal template if you are passing around instances of IPublishedContent. To do this, have your partial view inherit from `Umbraco.Cms.Web.Common.Views.UmbracoViewPage`

(like your normal templates). When you render your partial, a neat trick is that you can pass it an instance of `IPublishedContent`

. For example:

You don't normally need to cache the output of Partial views, like you don't normally need to cache the output of User Controls. However, there are times when this is necessary and so we provide caching output of partial views. This is done by using an HtmlHelper extension method:

The above will cache the output of your partial view for one hour when not running Umbraco in `debug`

mode. Additionally, there are a few optional parameters you can specify to this method. Here is the full method signature:

So you can specify to cache by member and/or by page and also specify additional view data to your partial view. * *However**, if your view data is dynamic (meaning it could change per page request) the cached output will still be returned. This same principle applies if the model you are passing in is dynamic. Please be aware of this: if you have a different model or viewData for any page request, the result will be the cached result of the first execution. If this is not desired you can generate your own cache key to differentiate cache instances using the contextualKeyBuilder parameter

To create multiple versions based on one or more viewData parameters you can do something like this:

Or using a custom helper function:

Or even based on a property on the Model (though if Model is the current page then `cacheByPage`

should be used instead):

Regardless of the complexity here the contextualKeyBuilder function needs to return a single string value.

Caching is only enabled when your application has `debug="false"`

. When `debug="true"`

caching is disabled. Also, the cache of all CachedPartials is emptied on Umbraco publish events.

Last updated

Was this helpful?

---

#### Querying & Traversal | CMS

Querying for content and media by id

```
// to return IPublishedContent
@Umbraco.Content(1234)
```

```
// to return the strongly typed (IEnumerable<Umbraco.Core.Models.IPublishedContent>) collection
@Umbraco.Content(1234, 4321, 1111, 2222)
```

```
// to return the Umbraco.Core.Models.IPublishedContent
@Umbraco.Content(Guid.Parse("ca4249ed-2b23-4337-b522-63cabe5587d1"))
```

```
// to return the Umbraco.Core.Models.IPublishedContent
@Umbraco.Content(Udi.Create("document", Guid.Parse("ca4249ed-2b23-4337-b522-63cabe5587d1")))
```

```
@Umbraco.Media(9999)
@Umbraco.Media(9999,8888,7777)
@Umbraco.Media(9999)
@Umbraco.Media(9999,8888,7777)
@Umbraco.Content(Guid.Parse("ca4249ed-2b23-4337-b522-63cabe5587d1"))
@Umbraco.Content(Udi.Create("media", Guid.Parse("ca4249ed-2b23-4337-b522-63cabe5587d1")))
```

Traversing

Complex querying (Where)

Some examples

Where children are visible

Traverse for sitemap

Content sub menu

Complex query

Last updated

Was this helpful?

---

#### Using View Components in Umbraco | CMS

In the previous versions of MVC, we used Child Actions to build reusable components/widgets consisting of both Razor markup and backend logic. The backend logic was implemented as a controller action and marked with a *[ChildActionOnly]* attribute. Child Actions are no longer supported in ASP.NET Core MVC. Instead, we will use the *View Component* feature.

View components replace the traditional Controller (SurfaceController)/Partial View relationship and instead offers a modular approach of separating your views in to several smaller units. View Components are self-contained objects that consistently render HTML from a Razor view.

View components are:

Generated from a C# class

Derived from the base class ViewComponent and

Associated with a Razor file (*.cshtml) to generate markup.


are similar to partial views but they are much more powerful compared to the partial views. View components do not use model binding, instead they work with the data provided when calling it.

View Components can be implemented in any part of the web application. There are some possibilities to duplicate code like Header, Navigation Pane, Login Panel, Menu, Shopping Cart, Footer, BlockList Items and so on. View Components behave like a web part containing both business logic and UI design. This is because they create a package which can be reused in multiple parts of the web application.

A view component code consists of two parts:

The View Component class derived from the

`ViewComponent`

class:```
[ViewComponent(Name = "Employee")]
public class EmployeeViewComponent : ViewComponent
{}
```

Returns a Task object as

`IViewComponentResult`

:```
public IViewComponentResult Invoke()
{
    return Content("Hi I'm an Employee Component");
}
```


In this example, let's create a ViewComponent for a Product List and render it on the *HomePage* of the website.

Create a folder named **ProductView**. In this folder, create a new class named **ProductViewViewComponent.cs** as below:

In **Views** folder, create new folders at `Views\Shared\Components\ProductView`

. In the **ProductView** folder, create a new file named **Default.cshtml** as below:

Adding the following declaration will give access to the UmbracoHelper object inside the ViewComponent View

You can invoke a ViewComponent from anywhere (even from within a Controller or another ViewComponent). Since this is our Product List, we want it rendered on the Home page - so we’ll invoke it from our HomePage.cshtml file using:

You can read about different ways of invoking your view component in the section of the Microsoft Documentation.view=aspnetcore-5.0)

By default, the framework searches for the Component View path in the following areas:

`/Views/{Controller Name Folder}/Components/{View Component Name Folder}/{View Name}`

`/Views/Shared/Components/{View Component Name Folder}/{View Name}`


Last updated

Was this helpful?

---

#### Working with MVC Views in Umbraco | CMS

*Working with MVC Views and Razor syntax in Umbraco*

All Umbraco views inherit from `Umbraco.Cms.Web.Common.Views.UmbracoViewPage<ContentModels.NameOfYourDocType>`

along with the using statement `@using ContentModels = Umbraco.Cms.Web.Common.PublishedModels;`

. This exposes many properties that are available in razor. The properties on the Document Type can be accessed in a number of ways:

@Model (of type

`Umbraco.Web.Mvc.ContentModel`

) -> the model for the view which contains the standard list of IPublishedContent properties but also gives you access to the typed current page (of type whatever type you have added in the angled brackets).@Umbraco (of type

`UmbracoHelper`

) -> contains many helpful methods, from rendering fields to retrieving content based on an Id and tons of other helpful methods.[See UmbracoHelper Documentation](/umbraco-cms/reference/querying/umbracohelper)@Html (of type

`HtmlHelper`

) -> the same HtmlHelper you know and love from Microsoft but we've added a bunch of handy extension methods like @Html.BeginUmbracoForm@UmbracoContext (of type

`Umbraco.Cms.Web.Common.UmbracoContext`

)

This is probably the most used method which renders the contents of a field using the alias of the content item.

```
@Model.Value("bodyContent")
```

If you're using the method from within a partial view then be aware that you will need to inherit the context so the method knows which type to get the desired value from. You'd do this at the top of partial view and so strongly typed properties can then be accessed in the partial view. For instance you can pass "HomePage" like this:

```
@inherits UmbracoViewPage<HomePage>...
@Model.Value("title")
```

You will also need to pass the "Context" to the @Model.Value() method if you're looping over a selection like this where we pass the "item" variable.

Looping over a selection works in a similar way. If you have a property that contains, for instance, an IEnumberable collection, you can access the individual items using a foreach loop. Below illustrates how you might do that using "item" as a variable.

If you want to convert a type and it's possible, you can do that by typing a variable and assigning the value from your property to it. This could look like the example below.

In this example, we are looping through a list of items with the custom made type TeamMember assigned. This means we are able to access the strongly typed properties on the TeamMember item.

`IMemberManager`

is the gateway to everything related to members when templating your site. [IMemberManager Documentation](/umbraco-cms/reference/querying/imembermanager)

Models Builder allows you to use strongly typed models in your views. Properties created on your document types can be accessed with this syntax:

When Models Builder resolve your properties it will also try to use value converters to convert the values of your data into more convenient models. This allows you to access nested objects as strong types instead of having to rely on dynamics and risking having a lot of potential errors when working with these.

Last updated

Was this helpful?

---

---

---


## Umbraco Flavored Markdown | CMS

**Are you looking for Label Property Configuration?**
With the removal of AngularJS, advanced label rendering is now handled using Umbraco Flavored Markdown.

Umbraco Flavored Markdown (UFM) is the dialect of Markdown, used to support property descriptions and advanced labels within the Umbraco CMS backoffice. These can be used with Block editors (Block Grid, Block List) and Collection View columns (in Grid and Table views).

If you are not familiar with Markdown, you can read more about its philosophy and syntax on the .

Using Markdown for labels provides basic text formatting. It natively supports the use of HTML, enabling web components for complex label templating scenarios.

UFM is built on top of and specifications. The implementation for Umbraco 14 has been developed as an extension to the .

The essence of the UFM syntax is curly brackets with an alias prefix delimited with a colon.

```
{<alias prefix>: <contents>}
```

For clarity...

The opening token is

`{`

Left Curly BracketThe alias prefix can be any valid Unicode character(s), including emojis

Followed by

`:`

Colon, (not part of the alias prefix itself)The contents within the curly brackets can include any Unicode characters, including whitespace

The closing token is

`}`

Right Curly Bracket

An example of this syntax to render a value of a property by its alias is: `{umbValue: headline}`.


The curly brackets indicate that the UFM syntax should be processed. The `umbValue`

alias prefix indicates which UFM component should be rendered, and the `headline`

contents are the parameter that is passed to that UFM component.

With this example, the syntax `{umbValue: headline}`

would be processed and rendered as the following markup:

The internal working of the `ufm-label-value`

component would then be able to access the property's value using the [Context API](/umbraco-cms/customizing/foundation/context-api).

In addition, a filter syntax can be applied to UFM contents. This can be useful for formatting or transforming a value without needing to develop your own custom UFM component.

The syntax for UFM filters uses a pipe character `|`

(Vertical Line). Multiple filters may be applied, and the value from the previous filter is passed onto the next.

To display a rich-text value, stripping out the HTML markup and limiting it to the first 15 words could use the following filters:

Please note, using `umbValue`

directly with a rich-text value will not display the contents. This is due to the complexity of the underlying data structure. The `stripHtml`

filter has been designed to support the rich-text value. Alternatively, you may use the UFM Expression syntax to access the raw rich-text value, like `${ bodyText.markup }`.


The following UFM filters are available to use.

| Name | Alias | Example syntax |
|---|---|---|
| Bytes | `bytes` | `{umbValue: umbracoBytes | bytes}` |
| Fallback | `fallback` | `{umbValue: headline | fallback:N/A}` |
| Lowercase | `lowercase` | `{umbValue: headline | lowercase}` |
| Strip HTML | `stripHtml` | `{umbValue: bodyText | stripHtml}` |
| Title Case | `titleCase` | `{umbValue: headline | titleCase}` |
| Truncate | `truncate` | `{umbValue: intro | truncate:30:...}` |
| Uppercase | `uppercase` | `{umbValue: headline | uppercase}` |
| Word Limit | `wordLimit` | `{umbValue: intro | wordLimit:15}` |

Starting from version 16.4, both the kebab-case (for example, `strip-html`

, `title-case`

,and `word-limit`

) and the camelCase syntax (for example, `stripHtml`

, `titleCase`

, and `wordLimit`

) are supported.

The kebab-case syntax is scheduled for removal in version 18, so it’s recommended to begin using the camelCase syntax going forward.

UFM can also support JavaScript-like expressions to allow for basic logic within label templates and descriptions. This is especially useful for advanced label rendering, fallback values, and dynamic formatting without developing your own custom UFM components or filters.

Expressions are defined using the `${ ... }`

syntax. This is different to the syntax outlined above. You can use standard JavaScript operators, function calls, and property access.

**Examples:**

Expressions can reference property aliases, perform calculations, concatenate strings, and more.

Arithmetic (

`+`

,`-`

,`*`

,`/`

)Logical (

`&&`

,`||`

,`!`

)Conditional (

`? :`

)Function calls (limited to safe native/built-in functions like

`toUpperCase()`

,`toLowerCase()`

, etc.)Property access (

`myProperty.length`

)

All expressions are evaluated in a sandbox. Only safe operations and methods are allowed. Access to global objects, external APIs, or unsafe functions will be blocked. To extend expressions with your own functions, it is recommended to use the piped UFM Filter syntax.

The following UFM components are available to use.

Label Value

Localize

Content Name

Link Title


More UFM components will be available in upcoming Umbraco releases.

The Label Value component will render the current value of a given property alias.

The alias prefix is `umbValue`

. An example of the syntax is `{umbValue: headline}`

, which would render the component as `<ufm-label-value alias="headline"></ufm-label-value>`.


For brevity and backwards-compatibility, the `=`

marker prefix can be used, e.g. `{=headline}`.


The Localize component will render a localization for a given term key.

The alias prefix is `umbLocalize`

. An example of the syntax is `{umbLocalize: general_name}`

, which would render the component as `<ufm-localize alias="general_name"></ufm-localize>`.


Similarly, for brevity and backwards-compatibility, the `#`

marker prefix can be used, e.g. `{#general_name}`.


The Content Name component will render the name of a content item, (either Document, Media or Member), from the value of a given property alias. Multiple values will render the names as a comma-separated list.

The alias prefix is `umbContentName`

. An example of the syntax is `{umbContentName: pickerAlias}`

, which would render the component as `<ufm-content-name alias="pickerAlias"></ufm-content-name>`.


The Content Name component supports content-based pickers, such as the Document Picker, Content Picker (formerly known as Multinode Treepicker), and Member Picker. Support for the advanced Media Picker will be available in an upcoming Umbraco release.

The Link Title component will render the title of a link from the value of a given Link Picker property editor. Multiple links will render the titles as a comma-separated list.

The alias prefix is `umbLink`

. An example of the syntax is `{umbLink: pickerAlias}`

, which would render the component as `<ufm-link alias="pickerAlias"></ufm-link>`.


If you wish to develop your own custom UFM component, you can use the `ufmComponent`

extension type:

The corresponding JavaScript/TypeScript API would contain a method to render the custom label/markup.

Using the `{myCustom: myCustomText}`

syntax would render the following markup: `<ufm-custom-component text="myCustomText"></ufm-custom-component>`

. Inside the `ufm-custom-component`

component code, you can perform any logic to render your required markup.

If you wish to develop custom UFM filter, you can use the `ufmFilter`

extension type:

The corresponding JavaScript/TypeScript API would contain a function to transform the value.

Using the `{umbValue: headline | reverse}`

syntax where `headline`

having a value of `Hello world`

would be transformed to `dlrow olleH`.


When the markdown has been converted to HTML, the markup will be run through post-processing sanitization to ensure security and consistency within the backoffice.

As of Umbraco 14, the is used to sanitize the markup and prevent Cross-site scripting (XSS) attacks.

The sanitized markup will be...

Valid HTML

Anchor links will have their target set to

`_blank`

Only web components that have a prefix of

`ufm-`

,`umb-`

or`uui-`

will be allowed to render

If you would like to render UFM within your own web components in the Umbraco CMS backoffice, you can use the `umb-ufm-render`

component:

Last updated

Was this helpful?

---


## Inversion of Control / Dependency injection | CMS

Inversion of Control/Dependency Injection in Umbraco

```
IUmbracoBuilder.Services
```

Registering dependencies

Choosing a strategy for registering dependencies

Registering dependencies in the

`Program.cs`

fileRegistering dependencies in a composer

Registering dependencies in bundles

Service lifetime

| Name | Lifetime | Description |
|---|---|---|
| Transient | Creates a new instance | A new instance will be created each time it's injected. |
| Scoped | One unique instance per web request (connection) | Scoped services are disposed of at the end of the request. Be careful not to resolve a scoped service from a singleton, as it may lead to an incorrect state in subsequent requests. |
| Singleton | One unique instance for the whole web application | The single instance will be shared across all web requests. |

Injecting dependencies

Injecting dependencies into a class

Injecting dependencies into a View or Template

Other things you can inject

UmbracoHelper

ExamineManager

ILogger

Using DI in Services and Helpers

Last updated

Was this helpful?

---


## Webhooks | CMS

Umbraco webhooks enable seamless integration and real-time updates by notifying external services about content changes and events within the Umbraco CMS

Getting Started

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1bf4ebe58736fb0fc6ad42b3956cd6da2b27f12d%252Fwebhook-section-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=da40091b&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6d902061380d30f7d077a1d3bfa87b07e94cde65%252Fcreate-webhook-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=64d5f4a9&sv=2)

Configuring a Webhook

URL

Events

| Event Name | Description |
|---|---|
| Content Published | Fires when content is published. |
| Content Unpublished | Fires when content is unpublished. |
| Content Deleted | Fires when content is deleted. |
| Media Deleted | Fires when a media item is deleted. |
| Media Saved | Fires when a media item is saved. |

Content Type Filtering

Custom Headers

Default Behavior of Umbraco Webhooks

JSON Payload

Legacy

Minimal

Extended

Configuring Payload Types

Default Headers

| Header Name | Description |
|---|---|
| `user-agent: Umbraco-Cms/{version}` | Identifies the Umbraco version sending the webhook. |
| `umb-webhook-retrycount: {number}` | Indicates the retry count for a webhook request. |
| `umb-webhook-event: {event}` | Specifies the event that triggered the request. Example: `umb-webhook-event: Umbraco.ContentPublished` . |

Extending Webhooks

Adding Custom Events

Replacing Webhook Events

Webhook Settings

| Setting | Description |
|---|---|
| `Enabled` | Enables or disables webhooks. |
| `MaximumRetries` | Sets the maximum number of retry attempts. |
| `Period` | Defines the retry interval. |
| `EnableLoggingCleanup` | Enables automatic cleanup of logs. |
| `KeepLogsForDays` | Determines how long webhook logs are retained. |
`PayloadType` | Sets the webhook
|

Testing Webhooks

Last updated

Was this helpful?

### Expanding Webhook Events | CMS

Explore new webhook event options, detailed setup, specific content triggers, and improved logging and retry mechanisms.

Umbraco developers can create their own webhook events.

This article demonstrates the process of implementing custom webhook events using the `WebhookEventBase<TNotification>`

base class.

The `WebhookEventBase<TNotification>`

class serves as the foundation for creating custom webhook events. Here's a brief overview of its key components:

**Alias**: The property that must be overridden to provide a unique identifier for the webhook event.**EventName**: A property that represents the name of the event. It is automatically set based on the provided alias unless explicitly specified.**EventType**: A property that categorizes the event type. It defaults to "Others" but can be customized using the`WebhookEventAttribute`

.**WebhookSettings**: The property containing the current webhook settings.**ProcessWebhooks**: The method responsible for processing webhooks for a given notification.**ShouldFireWebhookForNotification**: The method determining whether webhooks should be fired for a specific notification.**ConvertNotificationToRequestPayload**: An optional method allowing customization of the notification payload before sending it to webhooks.

To create a custom webhook event, follow these steps:

**Derive from**

:**WebhookEventBase<TNotification>```
public class YourCustomEvent : WebhookEventBase<YourNotificationType>
{
    // Constructor and required overrides go here
}
```

**Override the Alias Property**:Provide a unique identifier for the event using the

`Alias`

property:```
public override string Alias => "YourUniqueAlias";
```

**Apply****WebhookEventAttribute****(Optional)**:Use the

`WebhookEventAttribute`

to specify the event name and type. Apply this attribute to the custom event class:```
[WebhookEvent("Your Event Name", "YourEventType")]
public class YourCustomEvent : WebhookEventBase<YourNotificationType>
{
    // Constructor and required overrides go here
}
```

Umbraco already has some types as constants, which you can find at

`Constants.WebhookEvents.Types`

. If this attribute is not specified, the event name will default to the alias, and the type will default to`Other`

.**Implement Notification Handling**:If needed, customize the handling of the notification in the

`HandleAsync`

method.**Register Your Webhook Event**:Ensure that Umbraco is aware of the custom event by registering it in a composer:

```
using Umbraco.Cms.Core.Composing;

public class CustomWebhookComposer : IComposer
 {
     public void Compose(IUmbracoBuilder builder)
     {
         builder.WebhookEvents().Add<YourCustomEvent>();
     }
 }
```

**Implement Optional Overrides**: Depending on requirements, methods such as`ConvertNotificationToRequestPayload`

and`ShouldFireWebhookForNotification`

can be overridden to customize the behavior of the webhook event.

The code below shows a sample implementation of a custom webhook event. The `YourCustomEvent`

class is derived from the `WebhookEventBase<YourNotificationType>`

class, and it overrides the `Alias`

property to provide a unique identifier for the event. The `WebhookEventAttribute`

is applied to the class to specify the event name and type.

For scenarios where the webhook event is content-specific, Umbraco provides another base class: `WebhookEventContentBase<TNotification, TEntity>`

. This class is an extension of the generic `WebhookEventBase<TNotification>`

and introduces content-related functionalities.

The `WebhookEventContentBase<TNotification, TEntity>`

class is designed for content-specific webhook events, where `TEntity`

is expected to be a type that implements the `IContentBase`

interface.

To leverage the `WebhookEventContentBase<TNotification, TEntity>`

class, follow these steps:

**Derive from**

:**WebhookEventContentBase<TNotification, TEntity>****Override the Required Methods**:**GetEntitiesFromNotification**: Implement this method to extract content entities from the notification.**ConvertEntityToRequestPayload**: Implement this method to customize the content entity payload before sending it to webhooks.

The

`ContentPublishedWebhookEvent`

class demonstrates how these methods are overridden.

**ProcessWebhooks Implementation**:The

`ProcessWebhooks`

method in this class has been enhanced to iterate through content entities obtained from the notification. It checks the content type of each entity against the specified webhook's content type keys, firing webhooks only for matching entities.

Last updated

Was this helpful?

---


## Website Output Caching | CMS

Boost website performance with opt-in server-side output caching for Umbraco pages that are rendered with Razor templates.

Umbraco provides opt-in output caching for server-side rendered pages. When enabled, the server caches the full rendered HTML response and serves it directly for subsequent requests. The Razor pipeline, and whatever logic is triggered from that, is not re-executed until the cache expires or is evicted.

Under the hood, the feature uses the built-in .

**Output caching vs. response caching**

Output caching and [Response Caching](/umbraco-cms/reference/response-caching) serve different purposes:

**Output caching**caches the rendered response**on the server**. Subsequent requests are served from cache without re-executing the rendering pipeline. This is what reduces server load.**Response caching**sets`Cache-Control`

HTTP headers that tell**browsers and proxies**to cache the response. The server still processes every request that reaches it.

The two are complementary — you can use both together.

The Content Delivery API has its own output caching support. For details, see the [Output caching](/umbraco-cms/reference/content-delivery-api/output-caching) article in the Delivery API section.

Every front-end page request on a typical Umbraco site runs the full Razor rendering pipeline. For most sites, content changes infrequently relative to how often it is read. A site might be published a few times a day but serve thousands of requests per hour.

Even a short cache duration is effective. A 10-second cache collapses all concurrent requests within that window into a single Razor execution. During traffic spikes, the server CPU stays flat instead of scaling linearly with requests.

However, output caching does come with trade-offs:

The cache consumes additional server memory.

Editors may experience a short delay between publishing and the updated page appearing. Active eviction on publish, via the built-in defaults and custom use of extension points, keeps this minimal.


*not*to use output caching

Output caching can be a poor fit in some cases:

Pages that vary per user due to server-side personalization (for example, member-specific content rendered in Razor). If personalization is handled client-side via JavaScript, output caching can still be used.

Pages where editors require immediate publishing with guaranteed zero delay.


Output caching is **disabled by default**. Enabling it is an opt-in decision.

Enable output caching by adding the `OutputCache`

section to the `Website`

configuration in `appsettings.json`:


| Property | Type | Default | Description |
|---|---|---|---|
| `Enabled` | `bool` | `false` | Enables or disables website output caching. |
| `ContentDuration` | `TimeSpan` | `00:00:10` (10 seconds) | Default cache duration for rendered pages. Can be overridden per content item using `IWebsiteOutputCacheDurationProvider` . |

All standard Umbraco pages are cached. This covers every page routed through the default Umbraco rendering pipeline. Pages rendered by custom controllers that inherit from `RenderController`

are also cached (see [Custom MVC controllers (Umbraco Route Hijacking)](/umbraco-cms/reference/routing/custom-controllers)).

The following requests are excluded from caching by default:

**Preview mode**requests.**Authenticated member**requests.Responses where the server sets

`Cache-Control: no-store`

. This includes pages that render`@Html.AntiForgeryToken()`

, because the anti-forgery middleware sets this header automatically.Responses that include

`Set-Cookie`

headers.Pages where the routing pipeline sets

`SetNoCacheHeader`

on the published request.Controllers that implement

`IRenderController`

directly without inheriting from`RenderController`.


Cached pages are automatically evicted when content changes. This works through a tagging system: when a page is cached, it is tagged with identifiers that describe the page. When content changes, the relevant tags are targeted for eviction.

Each cached page is automatically tagged with:

Its own

**content key**.The keys of all its

**ancestors**in the content tree.Its

**content type**alias.The keys of any

**related items**referenced through picker properties (content pickers, media pickers, member pickers), tracked through Umbraco's automatic relations.

These tags enable eviction at multiple levels:

**By content item**: When a content item is published, unpublished, moved, or deleted, the cached page for that item is evicted via its content key tag.**By branch**: Branch operations, such as moving a node with children, evict all descendants via the ancestor tags.**By relations**: When content, media, or a member is saved, any pages that reference the changed item are evicted via the relation tags.**By content type**: All pages of a given content type can be evicted via the content type tag.**Global**: A full content cache refresh evicts all cached pages.

Output caching works in load-balanced setups through one of two approaches. Either keep a separate in-memory cache on each server, or share a single cache across all servers via a distributed store. Each comes with trade-offs around memory, latency, and operational complexity.

The default `IOutputCacheStore`

implementation is in-process memory. Each server maintains its own cache, and eviction is distributed across the cluster through `ContentCacheRefresherNotification`

. When content changes on one server, every server in the cluster receives the notification and evicts the relevant entries from its local cache. This keeps cached content consistent without requiring any shared infrastructure.

The trade-offs of this approach:

**Memory duplication**: Each server holds its own copy of the same cached pages. Total memory across the cluster scales with the number of servers, although per-server memory is unaffected.**Per-server warm-up**: A visitor routed to a server that has not yet served a particular page experiences a cache miss, even if other servers have it cached.**Cache lost on restart**: When a server process restarts (deployment, app pool recycle), its cache starts empty until requests rebuild it.

This is a reasonable choice for many load-balanced sites. It requires no additional infrastructure, and the cost of per-server warm-up is small relative to the savings over uncached rendering.

For a single shared cache across all instances, you can swap the default in-memory store for any `IOutputCacheStore`

implementation. The most common option is , via Microsoft's [Microsoft.AspNetCore.OutputCaching.StackExchangeRedis arrow-up-right](https://www.nuget.org/packages/Microsoft.AspNetCore.OutputCaching.StackExchangeRedis)

To use Redis as the backing store, install the package and register it in `Program.cs`

before `AddOutputCache`:


For full configuration details, see the [Microsoft documentation on Redis output cache arrow-up-right](https://learn.microsoft.com/aspnet/core/performance/caching/output#redis-cache)

The trade-offs of this approach:

**Network round-trip per request**: Each cache lookup reads from Redis over the network. Redis is fast, but there is a small added latency on every cached response compared to in-process memory.**External dependency**: A Redis outage stops cached responses from being served on every server. Requests fall back to the uncached rendering pipeline, so the site remains available, but the performance benefits disappear until Redis recovers.**Operational cost**: A managed Redis service is an additional running cost, and a self-hosted Redis cluster requires monitoring and maintenance.**Lower total memory**: Cached content is stored once, regardless of how many servers are in the cluster.**Single shared warm-up**: A new server joining the cluster benefits immediately from the existing cache, and the cache survives individual server restarts and deployments.

Defaulting to the in-memory approach unless you have a specific reason to switch is a reasonable first step. It is simpler, faster on a per-request basis, and works without any extra moving parts.

Consider Redis when one or more of the following apply:

The cluster has many servers (typically four or more), so the duplicated memory cost across instances becomes significant.

Cached pages are large enough that holding a copy on each server is expensive — for example, long content-heavy pages cached for extended durations.

New servers join the cluster frequently (auto-scaling), and starting with an empty cache on each new instance produces noticeable load spikes on origins or downstream systems.

You want cached content to survive deployments and restarts.


The feature provides extension points for customizing caching behavior. Each is registered through dependency injection.

**Interface:** `IWebsiteOutputCacheRequestFilter`

**Registration:** Single — replace the default with `builder.Services.AddUnique<IWebsiteOutputCacheRequestFilter, YourFilter>()`.


Controls whether a request is eligible for output caching. The default implementation (`DefaultWebsiteOutputCacheRequestFilter`

) returns `false`

for preview mode and authenticated member requests. It exposes `virtual`

methods for each check, so you can inherit and override individual concerns.

**Example — allow caching for authenticated members:**

Register the filter in a composer:

**Example — skip caching for a specific content type:**

**Interface:** `IWebsiteOutputCacheDurationProvider`

**Registration:** Single — replace the default with `builder.Services.AddUnique<IWebsiteOutputCacheDurationProvider, YourProvider>()`.


Override the cache duration per content item. Return `null`

to use the configured default, a positive `TimeSpan`

to override, or `TimeSpan.Zero`

to disable caching for that content item.

**Example — different durations per content type:**

**Interfaces:** `IWebsiteOutputCacheTagProvider`

and `IWebsiteOutputCacheEvictionProvider`

**Registration:** Multiple — add with `builder.Services.AddSingleton<>()`

. Multiple providers of each type are additive.

These two interfaces work as a pair to support cross-content eviction scenarios:

`IWebsiteOutputCacheTagProvider`

adds custom tags to cached pages when they are stored.`IWebsiteOutputCacheEvictionProvider`

returns tags to evict when a content change occurs.

Tags can also be targeted directly from custom code using `IWebsiteOutputCacheManager.EvictByTagAsync()`.


**Example — evict a blog category page when one of its blog posts is published:**

In this example, a blog site has two Document Types: `blogCategory`

and `blogPost`

. Each blog post has a content picker property with the alias `blogCategory`

that references its category. When a blog post is published, the selected category page should be evicted so it reflects the change.

The tag provider tags each category page with a tag that includes the category's content key. The eviction provider checks whether the changed content is a blog post. If so, it reads the picker value to return the tag for the selected category.

Register both providers in a composer:

**Interface:** `IWebsiteOutputCacheManager`

**Usage:** Inject via dependency injection. All methods are no-ops when output caching is not enabled.

Evict cache entries from custom code. This is useful when external data changes that affect rendered pages.

Available methods:

`EvictContentAsync(Guid contentKey)`

— evicts the cached page for a specific content item.`EvictAllAsync()`

— evicts all cached pages.`EvictByTagAsync(string tag)`

— evicts all cached pages with a specific tag.

**Interface:** `IWebsiteOutputCacheVaryByProvider`

**Registration:** Multiple — add with `builder.Services.AddSingleton<IWebsiteOutputCacheVaryByProvider, YourProvider>()`

. Multiple providers are additive.

Control which request dimensions produce separate cache entries. Each provider receives the `HttpContext`

and the ASP.NET Core `CacheVaryByRules`

object.

**Example — vary only by specific query parameters, ignoring tracking parameters:**

With this provider registered, `/?utm_source=google`

serves the same cached response as `/`

, while `/?page=2`

produces a separate cache entry.

**Example — vary by a custom culture cookie:**

If your site uses a cookie to store the visitor's preferred culture, you can create separate cache entries per culture value.

Controllers that inherit from `RenderController`

inherit output caching automatically. No additional configuration is needed.

To **opt out** of caching for a specific controller, apply the `[OutputCache(NoStore = true)]`

attribute:

Controllers that implement `IRenderController`

directly (without inheriting from `RenderController`

) are **not** cached by default. To opt in, apply the output cache policy:

For more details on route hijacking, see the [Custom MVC controllers (Umbraco Route Hijacking)](/umbraco-cms/reference/routing/custom-controllers) article.

The output cache policy logs all cache decisions at `Debug`

level. Enable debug logging for the caching namespace:

Log messages include why caching was skipped (preview mode, authenticated member, no-store header, feature disabled). When caching is applied, the logs show the content key, duration, and tag count.

The `Age`

response header on cached responses indicates how long the response has been served from cache.

While output caching is a great way to boost performance, it should never be used as a band-aid to solve poor uncached performance. Umbraco's Razor rendering pipeline is generally performant without caching.

If you experience performance issues with page rendering, your first step should be to diagnose and fix the root cause. This could be any number of things, like:

Expensive or un-performant value converters.

Slow external API calls made during rendering.

Inefficient queries or excessive database access in views or controllers.

Overly complex Razor view logic.

...or something else entirely.


Hiding such problems behind output caching should only ever be considered as a short-term solution. In the long run it will not be a sustainable fix.

Last updated

Was this helpful?

---
