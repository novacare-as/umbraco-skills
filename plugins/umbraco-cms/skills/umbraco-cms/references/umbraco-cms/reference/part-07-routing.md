# Reference — Part 7: Routing → Searching | CMS

## Routing

### Contents

- [Custom MVC controllers (Umbraco Route Hijacking) | CMS](#custom-mvc-controllers-umbraco-route-hijacking-cms)
- [Custom Middleware | CMS](#custom-middleware-cms)
- [Custom MVC Routes | CMS](#custom-mvc-routes-cms)
- [URL Rewrites in Umbraco | CMS](#url-rewrites-in-umbraco-cms)
- [Request Pipeline](#request-pipeline)
- [Special Property Type aliases for routing | CMS](#special-property-type-aliases-for-routing-cms)
- [Surface controllers | CMS](#surface-controllers-cms)
- [Umbraco API Controllers | CMS](#umbraco-api-controllers-cms)
- [URL Redirect Management | CMS](#url-redirect-management-cms)

---

### Custom MVC controllers (Umbraco Route Hijacking) | CMS

Use a custom MVC controller to handle and control incoming requests for content pages based on a specific Document Type, also called Route Hijacking.

*Use a custom controller to handle and control incoming requests for content pages based on a specific Document Type*

By default, all front-end requests to an Umbraco site are auto-routed via the 'Index' action of a core Controller: `Umbraco.Cms.Web.Common.Controllers.RenderController`

. This core controller handles the incoming request, builds the associated PublishedContent model, and passes this to the appropriate Umbraco Template/MVC View.

It is however possible to implement a custom Controller to replace this default implementation to give complete control over this execution.

For example:

To enrich the view model passed to the template with additional properties (from other published content items or outside Umbraco)

To implement serverside paging

To implement any custom/granular security

To return alternative templates depending on some custom business logic


This replacement of the default controller can be made 'globally' for all requests (see last example). It can also be by *'hijacking'* requests for types of pages based on their specific Document Type following this controller naming convention: `[DocumentTypeAlias]Controller`.


In the following example, imagine an Umbraco site with a set of 'product' pages created from a Document Type called 'Product Page' with an alias 'productPage'.

Create a custom locally declared controller in the Umbraco web application project named 'ProductPageController'.

Ensure that this controller inherits from the base controller `Umbraco.Cms.Web.Common.Controllers.RenderController`.


eg:

All requests to any **product** pages in the site will be **hijacked** and routed through the custom ProductPageController.

If you prefer to use an async controller your need to override both the sync and the async Index()-methods. This is done to disable the default behavior from the base controller.

This example shows the default behavior that Umbraco's core RenderController provides. The 'Index' action of the controller is executed, and the CurrentTemplate helper sends the model containing the details of the published content item related to the request to the relevant template/view.

A further convention is that if an action on the controller has a name that matches the template name, this action will be executed instead of the default 'Index' action.

In this example, the Product Page Document Type has two templates 'ProductPage' and 'ProductAmpPage'. We can hijack and handle the requests to the two templates differently.

Create the Controller as before:

The page in Umbraco will have a single 'template' selected as it's default template, but it's possible to call this same page on a different template by adding `?altTemplate=othertemplatename`

to the Url QueryString eg:

`/products/superfancyproduct/?altTemplate=ProductAmpPage`


Document Type name = controller name

Template name = action name (if no action matches or is not specified - then the 'Index' action will be executed).

Controller Inherits from

`Umbraco.Cms.Web.Common.Controllers.RenderController`


The steps to achieve this will differ, depending if your template views are using IPublishedContent or Modelsbuilder generated Models.

By default, your Umbraco Template will be based on the `ContentModel`

that the default `RenderController`

passes through to it.

The default inherits statement:

or if you are using **modelsbuilder**:

`<>`

contains a model generated for each Document Type to give strongly typed access to the Document Type properties in the template view.

To use a specific custom view model, the `@inherits`

directive will need to be updated to reference your custom model using the `Umbraco.Cms.Web.Common.Views.UmbracoViewPage<T>`

format where 'T' is the type of your custom model.

So for example, if your custom model is of type 'MyProductViewModel' then your `@inherits`

directive will look like:

Views will likely specify a master view to use as the common layout for the site HTML. When using a custom view model it's necessary to make sure this doesn't conflict with any implementation in the master layout view. Eg. if your master layout view is inheriting from a specific model `UmbracoViewPage<SpecificModel>`

and using a property from SpecificModel that isn't available in your custom model an exception will be thrown. To avoid this you could:

Keep your Master layout view 'generically typed', eg. only have

`@inherits UmbracoViewPage`

, and use Model.Value syntax to access properties. orBreak the dependency on

`Umbraco.Cms.Core.Models`

in your master layout by having it instead inherit from`Umbraco.Cms.Web.Common.Views.UmbracoViewPage<ISomeInterface>`

. This would be where ISomeInterface is implemented by all your models and contains the properties that the master layout view uses. orEnsure your custom models inherit from whichever class is used to strongly type the master layout view.


In most cases you will need your custom model to build upon the underlying existing PublishedContent model for the page. This can be achieved by making your custom model inherit from a special base class called `PublishedContentWrapped`:


`PublishedContentWrapped`

will take care of populating all the usual underlying Umbraco properties and means the `@Model.`

syntax will continue to work in the layouts used by your template.

Using Modelsbuilder you will find that all the generated models have a constructor that takes an IPublishedContent item in a similar way:

The models generated by Modelsbuilder are created as partial classes so it's possible to extend them by adding your own partial classes with matching signature.

We can now populate our custom view model in our controller and use the values from the custom model in our template view:

and in our template

You can also pass values directly into the controller action using the query string.

The values in the `querystring`

will be bound to the matching parameters defined in the controller's action:

Injecting services into your controller constructors is possible with Umbraco's underlying dependency injection implementation. See [Services and Helpers](/umbraco-cms/implementation/services#custom-services-and-helpers) for more info on this.

For example:

To wire up a concrete instance of IMadeUpProductService, use a composer:

See [Composing](/umbraco-cms/implementation/composing) for further information.

`RenderController`

You can replace Umbraco's default implementation of RenderController with your own custom controller for all MVC requests. This is possible by assigning your own default controller type in the Umbraco setup during initialization.

You can achieve this by updating the options for `UmbracoRenderingDefaultsOptions`

in `Program.cs`.


First of all, you have to create your own controller. Your custom implementation of RenderController should either inherit from the core `RenderController`

as in the examples above or implement the `IRenderController`

interface.

Implement the `IRenderController`:


Or inherit from `RenderController`


When [Website Output Caching](/umbraco-cms/reference/website-output-caching) is enabled, controllers that inherit from `RenderController`

inherit caching automatically. You can opt out for a specific controller by applying `[OutputCache(NoStore = true)]`

to the `Index()`

action.

The last step is to configure Umbraco to use your implementation. You can do that in the `Program.cs`

class.

Last updated

Was this helpful?

---

### Custom Middleware | CMS

Customizing the ASP.NET middleware pipeline in Umbraco

Middleware is responsible for processing/customizing an incoming request before generating an outgoing response. Shortly defined the middleware is a step to check the requests before giving a response back.

Umbraco automatically configures all required middleware in the `WithMiddleware()`

method in a specific order based on the .

You can use Umbraco pipeline filters in case you want to add your own middleware before, in-between or after the default Umbraco middleware. Filters are added by configuring the `UmbracoPipelineOptions`

and require an instance of `IUmbracoPipelineFilter`

that contains the following callbacks:

`PrePipeline`

- executed before any Umbraco-specific middleware is added, an example can be[URL rewrites](/umbraco-cms/reference/routing/iisrewriterules).`PreRouting`

- executed after the static files middleware and before the is added (using`UseRouting()`

). It can also be used to change the incoming URL.`PostRouting`

- executed after the routing middleware is added and can be used to

.[configure Cross-origin resource sharing (CORS) arrow-up-right](https://learn.microsoft.com/en-us/aspnet/core/security/cors?view=aspnetcore-7.0)`PostPipeline`

- executed after all Umbraco-specific middleware is added.`Endpoints`

- executed right before the Umbraco-specific endpoints are added using`WithEndpoints()`.


The addition of the `PostRouting`

callback is to allow correctly configuring the Cross-Origin Resource Sharing (CORS) middleware without having to use the `WithCustomMiddleware()`

method.

`IUmbracoPipelineFilter`

is an interface in Umbraco that allows the creation of custom filters which then modifies the behavior of the request pipeline. It can be used to change different aspects of how Umbraco handles incoming requests, such as changing content or adding security checks.`WithCustomMiddleware()`

is a method that can be used in Umbraco for adding custom middleware. This includes some specific customizable instructions that run in the request processing pipeline.

Using `WithCustomMiddleware()`

instead of `WithMiddleware()`

should only be used as a last resort. This is because Umbraco can break if you forget to add middleware or add them in the wrong order.

Create a composer with the following:

```

using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Web.Common.ApplicationBuilder;

public class CorsComposer : IComposer
{
    public const string AllowAnyOriginPolicyName = nameof(AllowAnyOriginPolicyName);

    public void Compose(IUmbracoBuilder builder)
        => builder.Services
        .AddCors(options => options.AddPolicy(AllowAnyOriginPolicyName, policy => policy.AllowAnyOrigin()))
        .Configure<UmbracoPipelineOptions>(options => options.AddFilter(new UmbracoPipelineFilter("Cors", postRouting: app => app.UseCors())))
        // For testing only
        .Configure<UmbracoPipelineOptions>(options => options.AddFilter(new UmbracoPipelineFilter("CorsTest", endpoints: app => app.UseEndpoints(endpoints =>
        {
            endpoints.MapGet("/echo", context => context.Response.WriteAsync("echo")).RequireCors(AllowAnyOriginPolicyName);
            endpoints.MapGet("/echo2", context => context.Response.WriteAsync("echo2"));
        }))));
}
```

You should be able to request `/echo`

from any origin, but get an error when trying to fetch `/echo2`

from a foreign origin. This can be tested by pasting the following JavaScript code in browser console when not on the local origin/Umbraco website (such as umbraco.com):

This should return the following:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-00a3e277451b075118cd20fcc836494c1d2406db%252Fcustom-middleware-cors-browser-example.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3779898d&sv=2)

An additional bonus is that this doesn't require any changes in your `Program.cs`

file. It also allows packages to enable Cross-Origin Resource Sharing (CORS) and configure their own policies.

Users that currently use `WithCustomMiddleware()`

will need to add calls to `RunPreRouting()`

and `RunPostRouting()`

. This is similar to Umbraco adding additional middleware in future versions.

Last updated

Was this helpful?

---

### Custom MVC Routes | CMS

Setting up your own controllers and routes that exist alongside the Umbraco pipeline.

*Documentation about how to setup your own custom controllers and routes that need to exist alongside the Umbraco pipeline*

There's two places you can specify your routing, depending on whether it's in the context of a package, or your own site. If it's your own site you can do it in the `Program.cs`

file, within the `WithEndpoints`

method call like so:

```
app.UseUmbraco()
    .WithMiddleware(u =>
    {
        u.UseBackOffice();
        u.UseWebsite();
    })
    .WithEndpoints(u =>
    {
        // This is where to put the custom routing

        u.UseBackOfficeEndpoints();
        u.UseWebsiteEndpoints();
    });
```

If you're creating a package you won't have access to the `Program.cs`

file. Instead you must use a composer, for an example of this, see the example below.

Umbraco doesn't interfere with any user defined routes that you wish to have. Your custom routes to your own custom controllers will work perfectly and seamlessly alongside Umbraco's routes.

For a request to be considered executing in an Umbraco context, and therefore the Umbraco pipeline, it needs to have an HTTP request feature with the type `UmbracoRouteValues`

, all the information required for Umbraco to handle the request is stored there. The question is now, how do we add this request feature? There's three possibilities:

Do it manually - This requires that you have a custom route, controller, even middleware, and manually assign the

`UmbracoRouteValues`

as an HTTP request feature, however you see fit. To create an`UmbracoRouteValues`

object generally requires:`IUmbracoContextAccessor`

(to access the`CleanedUmbracoUrl`

),`IPublishedRouter`

(to create the`IPublishedRequestBuilder`

),`IPublishedRequestBuilder`

(to set the published content and to build the`IPublishedRequest`

),`IPublishedRequest`

to assign to the`UmbracoRouteValues`

. As you can see this is a lot of work, but luckily there's some much easier ways.Route a custom controller that implements the

`IVirtualPageController`

interface, assigning the`UmbracoRouteValues`

to the HTTP requests will then be taken care of for you.Route a custom controller with conventional routing, using the typical call to

`endpoints.MapControllerRoute`

, and then call`.ForUmbracoPage()`

with an action for finding content on what`MapControllerRoute`

returns, now`UmbracoRouteValues`

will automatically be applied to any request to that controller.

Don't fret if this all seems a bit overwhelming, we'll be going through an example of the last two options.

As mentioned, with this approach we need to implement the `IVirtualPageController`

interface, this interface only has one method `FindContent`

which accepts an `ActionExecutingContext`:


It can also be helpful to inherit from the `UmbracoPageController`

since this includes some useful helper methods such as `CurrentPage`

, do however note that it is *not* possible to inherit from `RenderController`

when doing custom routes like this.

Let's create a shop controller, with an Index action showing all our products. We will also add a Product action showing custom data about the product that could exists outside Umbraco. A common approach in a scenario like this is to have a "real" Umbraco node as a starting point. In this example we will use an empty "Products" Document Type with a Collection, and "Product" Document Type containing a Stock-Keeping Unit (SKU). We also need some content based on those document types, a "Products" content node, which contains two product nodes, each with their own SKU.

After that bit of setup we can go ahead and create our shop controller which inherits from `UmbracoPageController`

and implements `IVirtualPageController`

, it'll look like this:

Now you'll see that `FindContent`

is complaining because we're not returning anything yet, but let's start by creating our to action methods that `FindContent`

will find content for.

First off we have the Index method:

With this method we return the view with the content found by the `FindContent`

method. This can then be used to list all the children in the view with `Model.Children()`.


Next we have our Product method:

Here, we get some extra data from a different source. In this case, a `DbContext`

, but this can be anything you want, using the ID we get from the route values. We use this extra data to create a custom model, which includes the available stores, which we then render the view with.

It's important to note that this custom model must implement `IPublishedContent`

, to do this we inherit from the `ContentModel`

class, in this case our model looks like this:

What's great about this is that we can use this model as a type argument when inheriting from `UmbracoViewPage`

in our model like so:

Which makes the model typed, so we can access the available stores like so:

But let's get back to our controller, the last thing we need now is to implement `FindContent`

method so we can find content for our actions and serve it to them. First we need to be able to get our content, and properties, so we need to inject `IUmbracoContextAccessor`

and `IPublishedValueFallback`

and save them to some fields like so:

Now that we have our dependencies, and our action methods, we're finally ready to implement the `FindContent`

method:

Start by retrieving the product root using the `UmbracoContext`

to obtain it based on its ID. Next, let's figure out what action is being requested. To do this, cast the `actionExecutingContext.ActionDescriptor`

to a `ControllerActionDescriptor`

and use its `ActionName`

property. If the action name is index, it returns the product root. If it's a product, we get the SKU from the route value `id`

and find the matching child node.

There's only one last thing to do. We need to register our shop controller. If you're creating a controller for your own site you can do it in the `Program.cs`

like so:

There's nothing Umbraco-specific about the controller routing; it's using the default `MapController`

route of the `EndpointRouteBuilder`

. Give the mapping a name, a pattern for the controller, and some default values, so if no action is specified, it will default to `Index`.


If you're creating a package you won't have access to the `Program.cs`

, so instead you can use a composer with an `UmbracoPipelineFilter`

like so:

With that we have our controller with a custom route within an Umbraco context.

If the endpoint of your custom route is considered a client-side request e.g. **/sitemap.xml**, you will need to make a few changes to get this to work.

Define your route as before, specifying the correct client type route:

You will need to configure your route request options within your **Program.cs** class. For single routes:

Or it can handle multiple routes:

In your **FindContent** method you should still be able to access and use **IUmbracoContextAccessor** through standard DI:

There is currently a bug in all versions below 9.5, where this fix won't work for mapping a client-side request to an Umbraco Controller. See [https://github.com/umbraco/Umbraco-CMS/issues/12083 arrow-up-right](https://github.com/umbraco/Umbraco-CMS/issues/12083)

One of the benefits of the `IVirtualPageController`

is that it allows you to use attribute routing. If you wish to use attribute routing you must use an `IVirtualPageController`

and decorate your controller and/or actions with the `Route`

attribute. If we want to convert our above example into using attribute routing we must first add the attributes to our actions:

Now all we need to do is change our routing to use `EndpointRouteBuilder.MapControllers();`

instead of adding a specific route.

This will give us routing that's similar to what we have in the other example. It's worth noting that there's no defaults when using attribute routing, so to allow our index action to be accessed through both `/shop`

and `/shop/index`

, we add two attributes, specifying both routes individually.

Making a custom route within the Umbraco context using `ForUmbracoPage`

is similar to using `IVirtualPageController`

. The main difference is that with `ForUmbracoPage`

we no longer find the content from within the controller. Instead we assign the `FindContent`

method when routing the controller. One important thing about `ForUmbracoPage`

is that attribute routing is *not* available. To make our example from above work with `ForUmbracoPage`

, we want to remove any attribute routing, and no longer implement `IVirtualPageController`

. We'll also remove the `FindContent`

method, our controller will then end up looking like this:

As you can see we still inherit from `UmbracoPageController`

to get access to the helper method `CurrentPage`

, but the rest is a normal controller.

The Umbraco magic will now instead happen where we route the controller, here we will pass a `Func<ActionExecutingContext, IPublishedContent>`

delegate to the `ForUmbracoPage`

method, this delegate is then responsible for finding the content, for instance using a composer with the same logic as in the `IVirtualPageController`

it will look like this:

The `Compose`

method of our composer is much the same as any other normal routing. The one difference is that we call `ForUmbracoPage`

on the `MapControllerRoute`

where we pass in our `FindContent`

method. The `FindContent`

method is almost the same as it was in the controller in the `IVirtualPageController`

example, with one important difference. Since we can no longer inject our required service into the constructor, we instead request them using `actionExecutingContext.HttpContext.RequestServices.GetRequiredService`

. You should *not* save the `HttpContext`

or the `IServiceProvider`

you get from the `actionExecutingContext`

to a field or property on the class. The reason for this is that they will be specific to each request.

With this we have a custom routed controller within the Umbraco pipeline. If you navigate to `/shop`

or `/shop/product/<SKU>`

you will see the controllers actions being called with the content found in `FindContent`.


Last updated

Was this helpful?

---

### URL Rewrites in Umbraco | CMS

When to use the URL Rewriting Middleware

Using the URL Rewriting Middleware

Example

```
<?xml version="1.0" encoding="utf-8" ?>
<rewrite>
  <rules>
    <rule name="Redirect umbraco.io to preferred domain" stopProcessing="true">
      <match url=".*" />
      <conditions>
        <add input="{HTTP_HOST}" pattern="\.umbraco\.io$" />
        <add input="{REQUEST_URI}" pattern="^/App_Plugins/" negate="true" />
        <add input="{REQUEST_URI}" pattern="^/umbraco" negate="true" />
      </conditions>
      <action type="Redirect" url="https://example.com/{R:0}" />
    </rule>
  </rules>
</rewrite>
```

Rewrite rule shortcuts

Examples of rewrite rules

External Resources

Example: Remove a Trailing Slash

Example: Enforce HTTPS

Example: Redirect Non-www to www

Example: Remove the .aspx Extension

Example: Custom Rewrite Rules for Umbraco Cloud

Example: Serving Files from the

`.well-known`

Path![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5e1e50d0030b595f9ff43dc43f361890dd1e7f5f%252Fupload-verification-file.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=196e4237&sv=2)

Last updated

Was this helpful?

---

### Request Pipeline

#### Contents

- [FindPublishedContentAndTemplate() | CMS](#findpublishedcontentandtemplate-cms)
- [IContentFinder | CMS](#icontentfinder-cms)
- [Inbound request pipeline | CMS](#inbound-request-pipeline-cms)
- [Outbound request pipeline | CMS](#outbound-request-pipeline-cms)
- [Published Content Request Preparation | CMS](#published-content-request-preparation-cms)

---

#### FindPublishedContentAndTemplate() | CMS

The followed method is called on the "PublishedContentRequest.PrepareRequest()" method: `FindPublishedContentAndTemplate()`

. We discuss shortly what this method is doing:

FindPublishedContent ()

Handles redirects

HandlePublishedContent()

FindTemplate()

FollowExternalRedirect()

HandleWildcardDomains()


No content?

Run the LastChanceFinder

Is an IContentFinder, resolved by ContentLastChanceFinderResolver

By default, is null (= ugly 404)

Follow internal redirects

Take care of infinite loops

Ensure user has access to published content

Else redirect to login or access denied published content

Loop while there is no content

Take care of infinite loops


Use altTemplate if

Initial content

Internal redirect content, and InternalRedirectPreservesTemplate is true

No alternate template?

Use the current template if one has already been selected

Else use the template specified for the content, if any

Alternate template?

Use the alternate template, if any

Else use what’s already there: a template, else none


Alternate template is used only if displaying the intended content

Except for internal redirects

If you enable InternalRedirectPreservesTemplate

Which is false by default


Alternate template replaces whatever template the finder might have set

ContentFinderByNiceUrlAndTemplate

/path/to/page/template1?altTemplate=template2 template2


Alternate template does not falls back to the specified template for the content

/path/to/page?altTemplate=missing no template

Even if the page has a template


But preserves whatever template the finder might have set

/path/to/page/template1?altTemplate=missing template1



Content.GetPropertyValue("umbracoRedirect")

If it’s there, sets the published content request to redirect to the content

Will trigger an external (browser) redirect


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d104f053c7a7fde0a824c7d1f3cd510d5cffedc2%252Fculture-and-hostnames-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f389b202&sv=2)

Finds the deepest wildcard domain between

Domain root (or top)

Request’s published content

If found, updates the request’s culture accordingly


This implements separation between hostnames and cultures

Last updated

Was this helpful?

---

#### IContentFinder | CMS

Information about creating your own content finders

```
public interface IContentFinder
{
  Task<bool> TryFindContent(IPublishedRequestBuilder contentRequest);
}
```

Example

```
public class MyContentFinder : IContentFinder
{
    private readonly IUmbracoContextAccessor _umbracoContextAccessor;

    public MyContentFinder(IUmbracoContextAccessor umbracoContextAccessor)
    {
        _umbracoContextAccessor = umbracoContextAccessor;
    }

    public Task<bool> TryFindContent(IPublishedRequestBuilder contentRequest)
    {
        var path = contentRequest.Uri.GetAbsolutePathDecoded();
        if (path.StartsWith("/woot") is false)
        {
            return Task.FromResult(false); // Not found
        }

        if (!_umbracoContextAccessor.TryGetUmbracoContext(out var umbracoContext))
        {
            return Task.FromResult(false);
        }

        // Have we got a node with ID 1234
        var content = umbracoContext.Content.GetById(1234);
        if (content is null)
        {
            // If not found, let another IContentFinder in the collection try.
            return Task.FromResult(false);
        }

        // If content is found, then render that node
        contentRequest.SetPublishedContent(content);
        return Task.FromResult(true);
    }
}
```

Adding and removing IContentFinders

Umbraco builder extension

Composer

NotFoundHandlers

Last updated

Was this helpful?

Information about creating your own content finders

The `IContentFinder`

is not available when using the **Content Delivery API**. Create your own implementation of the`IApiContentPathResolver`

interface to provide similar functionality.

To create a custom content finder, with custom logic to find an Umbraco document based on a request, implement the IContentFinder interface:

```
public interface IContentFinder
{
  Task<bool> TryFindContent(IPublishedRequestBuilder contentRequest);
}
```

and use either an Umbraco builder extension, or a composer to add it to it to the `ContentFindersCollection`.


Umbraco runs all content finders in the collection 'in order', until one of the IContentFinders returns true. Once this occurs, the request is then handled by that finder, and no further IContentFinders are executed. Therefore the order in which ContentFinders are added to the ContentFinderCollection is important.

The ContentFinder can set the PublishedContent item for the request, or template or even execute a redirect.

Example

This IContentFinders will find a document with id 1234, when the Url begins with /woot.

```
public class MyContentFinder : IContentFinder
{
    private readonly IUmbracoContextAccessor _umbracoContextAccessor;

    public MyContentFinder(IUmbracoContextAccessor umbracoContextAccessor)
    {
        _umbracoContextAccessor = umbracoContextAccessor;
    }

    public Task<bool> TryFindContent(IPublishedRequestBuilder contentRequest)
    {
        var path = contentRequest.Uri.GetAbsolutePathDecoded();
        if (path.StartsWith("/woot") is false)
        {
            return Task.FromResult(false); // Not found
        }

        if (!_umbracoContextAccessor.TryGetUmbracoContext(out var umbracoContext))
        {
            return Task.FromResult(false);
        }

        // Have we got a node with ID 1234
        var content = umbracoContext.Content.GetById(1234);
        if (content is null)
        {
            // If not found, let another IContentFinder in the collection try.
            return Task.FromResult(false);
        }

        // If content is found, then render that node
        contentRequest.SetPublishedContent(content);
        return Task.FromResult(true);
    }
}
```

Adding and removing IContentFinders

You can use either an extension on the Umbraco builder or a composer to access the `ContentFinderCollection`

and add or remove specific `ContentFinders`.


Learn more about registering dependencies and when to use which method in the [Dependency Injection](/umbraco-cms/reference/using-ioc) article.

Umbraco builder extension

First create the extension method:

Then invoke in the `Program.cs`

file:

Composer

NotFoundHandlers

To set your own 404 finder create an IContentLastChanceFinder and set it as the ContentLastChanceFinder. (perhaps you have a multilingual site and need to find the appropriate 404 page in the correct language).

A `IContentLastChanceFinder`

will always return a 404 status code. This example creates a new implementation of the `IContentLastChanceFinder`

and gets the 404 page for the current language of the request.

You can configure Umbraco to use your own implementation in the `Program.cs`

file:

When adding a custom `IContentLastChanceFinder`

to the pipeline any `Error404Collection`

-settings in `appSettings.json`

will be ignored.

Last updated

Was this helpful?

Was this helpful?

```
using RoutingDocs.ContentFinders;
using Umbraco.Cms.Core.DependencyInjection;
using Umbraco.Cms.Core.Routing;

namespace RoutingDocs.Extensions;

public static class UmbracoBuilderExtensions
{
    public static IUmbracoBuilder AddMyCustomContentFinders(this IUmbracoBuilder builder)
    {
        // Add our custom content finder just before the core ContentFinderByUrl
        builder.ContentFinders().InsertBefore<ContentFinderByUrlNew, MyContentFinder>();
        // You can also remove content finders, this is not required here though, since our finder runs before the url one
        builder.ContentFinders().Remove<ContentFinderByUrlNew>();
        // You use Append to add to the end of the collection
        builder.ContentFinders().Append<AnotherContentFinderExample>();
        // or Insert for a specific position in the collection
        builder.ContentFinders().Insert<AndAnotherContentFinder>(3);
        return builder;
    }
}
```

```
builder.CreateUmbracoBuilder()
    .AddBackOffice()
    .AddWebsite()
    .AddDeliveryApi()
    .AddComposers()
    .AddMyCustomContentFinders()
    .Build();
```

```
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.DependencyInjection;
using Umbraco.Cms.Core.Routing;

namespace RoutingDocs.ContentFinders;

public class UpdateContentFindersComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        // Add our custom content finder just before the core ContentFinderByUrl
        builder.ContentFinders().InsertBefore<ContentFinderByUrlNew, MyContentFinder>();
        // You can also remove content finders, this is not required here though, since our finder runs before the url one
        builder.ContentFinders().Remove<ContentFinderByUrlNew>();
        // You use Append to add to the end of the collection
        builder.ContentFinders().Append<AnotherContentFinderExample>();
        // or Insert for a specific position in the collection
        builder.ContentFinders().Insert<AndAnotherContentFinder>(3);
    }
}
```

```
using Umbraco.Cms.Core.PublishedCache;
using Umbraco.Cms.Core.Routing;
using Umbraco.Cms.Core.Services;

namespace RoutingDocs.ContentFinders;

public class My404ContentFinder : IContentLastChanceFinder
{
    private readonly IDomainService _domainService;
    private readonly IPublishedContentCache _publishedContentCache;

    public My404ContentFinder(
        IDomainService domainService,
        IPublishedContentCache publishedContentCache)
    {
        _domainService = domainService;
        _publishedContentCache = publishedContentCache;
    }

    public async Task<bool> TryFindContent(IPublishedRequestBuilder contentRequest)
    {
        // Find the root node with a matching domain to the incoming request
        var allDomains = (await _domainService.GetAllAsync(true)).ToList();
        var domain = allDomains
            .FirstOrDefault(f => f.DomainName == contentRequest.Uri.Authority
                                    || f.DomainName == $"https://{contentRequest.Uri.Authority}"
                                    || f.DomainName == $"http://{contentRequest.Uri.Authority}");

        var siteId = domain != null ? domain.RootContentId : allDomains.Any() ? allDomains.FirstOrDefault()?.RootContentId : null;


        var siteRoot = _publishedContentCache.GetById(false, siteId ?? -1);

        if (siteRoot is null)
        {
            return false;
        }

        // Assuming the 404 page is in the root of the language site with alias fourOhFourPageAlias
        var notFoundNode = siteRoot.Children()?.FirstOrDefault(f => f.ContentType.Alias == "fourOhFourPageAlias");

        if (notFoundNode is not null)
        {
            contentRequest.SetPublishedContent(notFoundNode);
        }

        // Return true or false depending on whether our custom 404 page was found
        return contentRequest.PublishedContent is not null;
    }
}
```

```
builder.CreateUmbracoBuilder()
    .AddBackOffice()
    .AddWebsite()
    .AddDeliveryApi()
    .AddComposers()
     // If you need to add something Umbraco specific, do it in the "AddUmbraco" builder chain, using the IUmbracoBuilder extension methods.
    .SetContentLastChanceFinder<RoutingDocs.ContentFinders.My404ContentFinder>()
    .Build();
```

---

#### Inbound request pipeline | CMS

How the Umbraco inbound request pipeline works

```
public class PublishedContentRequest
{
  public Uri Uri { get; }…
}
```

```
public bool HasDomain { get; }
public DomainAndUri Domain { get; }
public CultureInfo Culture { get; }
```

```
public bool HasPublishedContent { get; }
public IPublishedContent PublishedContent { get; set; }
public bool IsInternalRedirect { get; }
public bool IsRedirect {get; }
```

```
public bool HasTemplate { get; }
public string GetTemplateAlias { get; }
public ITemplate Template {get; }
```

Last updated

Was this helpful?

How the Umbraco inbound request pipeline works

The inbound process is triggered by `UmbracoRouteValueTransformer`

and then handled with the Published router. The [published content request preparation](/umbraco-cms/reference/routing/request-pipeline/published-content-request-preparation) process kicks in and creates a `PublishedRequestBuilder`

which will be used to create a `PublishedContentRequest`.


The `PublishedContentRequest`

object represents the request which Umbraco must handle. It contains everything that will be needed to render it. All this occurs when the Umbraco modules knows that an incoming request maps to a document that can be rendered.

```
public class PublishedContentRequest
{
  public Uri Uri { get; }…
}
```

There are 3 important properties, which contains all the information to find a node:

```
public bool HasDomain { get; }
public DomainAndUri Domain { get; }
public CultureInfo Culture { get; }
```

Domain is a DomainAndUri object that is a standard Domain plus the fully qualified uri. For example, the Domain may contain "example.com" whereas the Uri will be fully qualified for example "https://example.com/".

It contains the content to render:

```
public bool HasPublishedContent { get; }
public IPublishedContent PublishedContent { get; set; }
public bool IsInternalRedirect { get; }
public bool IsRedirect {get; }
```

Contains template information:

```
public bool HasTemplate { get; }
public string GetTemplateAlias { get; }
public ITemplate Template {get; }
```

The published request is created using the `PublishedRequestBuilder`

, which implements `IPublishedRequestBuilder`

. It's only in this builder that it's possible to set values, such as domain, culture, published content, redirects, and so on.

You can subscribe to the 'routing request' notification, which is published right after the `PublishedRequestBuilder`

has been prepared, but before the request is built, and processed. Here you can modify anything in the request before it is built and processed! For example content, template, etc:

Last updated

Was this helpful?

Was this helpful?

```
using Umbraco.Cms.Core.Events;
using Umbraco.Cms.Core.Notifications;

namespace Umbraco9.NotificationHandlers;

public class PublishedRequestHandler : INotificationHandler<RoutingRequestNotification>
{
    public void Handle(RoutingRequestNotification notification)
    {
        var requestBuilder = notification.RequestBuilder;
        // Do something with the IPublishedRequestBuilder here 
    }
}
```

---

#### Outbound request pipeline | CMS

Learn how the Umbraco outbound request pipeline works.

The **outbound pipeline** consists out of the following steps:

To explain these steps, the following content tree is used as an example:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b43408895928c6e7ec346716a717961e1847d24b%252Fsimple-content-tree-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=2a12bc9f&sv=2)

When a URL is constructed, Umbraco converts every node in the tree into a segment. Each published content item has a corresponding URL segment.

In the example above, "Our Products" becomes "our-products" and "Swibble" becomes "swibble".

Segments are created by the URL Segment Provider.

The Dependency Injection (DI) container of an Umbraco implementation contains a collection of `UrlSegmentProviders`

. This collection is populated during Umbraco startup. Umbraco ships with a 'DefaultUrlSegmentProvider', but custom implementations can be added to the collection.

When the `GetUrlSegment`

extension method is called for a content item and culture combination, each registered `IUrlSegmentProvider`

in the collection is executed in collection order. This continues until `UrlSegmentProvider`

returns a segment value for the content. No further `UrlSegmentProviders`

in the collection are executed after that point. If no segment is returned by any provider in the collection, the `DefaultUrlSegmentProvider`

is used as a fallback. This ensures that a segment is always created.

To create a new URL Segment Provider, implement the `IUrlSegmentProvider`

interface:

Each culture variation can have a different URL segment.

The returned string becomes the URL segment for the node. The value cannot contain the URL segment separator character `/`

. A value such as `5678/swibble`

would create additional segments, which is not allowed.

When content is published, Umbraco checks whether the URL segment has changed before traversing descendant nodes to create redirects. The redirect tracker uses `HasUrlSegmentChanged`

to compare the draft segment (what the segment will be after publishing) against the currently published segment. If the segment is unchanged, descendant traversal is skipped because no descendant URLs can have changed either.

The default implementations of `HasUrlSegmentChanged`

and `MayAffectDescendantSegments`

handle the common case automatically. Custom providers only need to override these methods in specific scenarios:


: Override if your provider derives segments from external state (for example, a database or API) rather than from content properties. The default implementation compares the draft segment to the published segment using**HasUrlSegmentChanged**`GetUrlSegment`.


: Override to return**MayAffectDescendantSegments**`true`

if your provider computes descendant URL segments based on ancestor data that does not affect the ancestor's own segment. When ancestor data changes the ancestor's segment, Umbraco already traverses descendants. This method covers the rare case where ancestor data changes without changing the ancestor's segment, but still affects descendant segments.

The following example adds the unique SKU or product reference of a product page to the existing URL segment.

The returned string becomes the native URL segment. There is no need for URL rewriting.

For the "swibble" product in the example content tree, `ProductPageUrlSegmentProvider`

returns the segment `swibble--123xyz`

, where `123xyz`

is the unique product SKU for the swibble product.

Register the custom `UrlSegmentProvider`

with Umbraco using a composer:

The Default URL Segment Provider builds segments by checking for one of the following values, in this order:

A property with alias

`umbracoUrlName`

on the node. This is a convention-based way to give editors control of the segment name. With variants, this can vary by culture.The name of the content item, for example

`content.Name`.


The Umbraco string extension `ToUrlSegment()`

is used to produce a clean, URL-safe segment.

To create a path, the pipeline uses the segments of each node.

In the example, the "swibble" node receives the path `/our-products/swibble`

. Using the `ProductPageUrlSegmentProvider`

from above, the path becomes `/our-products/swibble-123xyz`.


In a multi-site scenario, an internal path such as `/our-products/swibble-123xyz`

could belong to any of the sites, or match multiple nodes across multiple sites. In this case, additional sites have their internal path prefixed by the node ID of their root node. Any content node with a hostname defines a new root for paths.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-46efababb12bd7d250be16023876235698b1ae2b%252Fpath-example-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d20c88b9&sv=2)

| Node | Segment | Internal Path |
|---|---|---|
| Our Values | our-values | /our-values |
| Our Products | our-products | /our-products |
| Swibble | swibble-123xyz | /our-products/swibble-123xyz |
| Dibble | dibble-456abc | /our-products/dibble-456abc |
| Another Site | another-site | 9676/ |
| Their Values | their-values | 9676/their-values |

Paths can be cached. Scheme, domain, and current request cannot be cached.

Domain without path:

`www.site.com`

produces`1234/path/to/page`

.Domain with path:

`www.site.com/dk`

produces`1234/dk/path/to/page`

.No domain specified:

`/path/to/page`

.`HideTopLevelNodeFromPath`

set to`true`

: the path becomes`/to/page`.


The URL of a node consists of a complete : the Schema, Domain name, port, and path.

In the example, the "swibble" node has the URL: `http://example.com/our-products/swibble`.


URL generation is handled by the URL Provider. The URL Provider is called whenever a URL is requested in code, for example:

The DI container of an Umbraco implementation contains a collection of `UrlProviders`

. This collection is populated during Umbraco startup. Umbraco ships with a `DefaultUrlProvider`

, but custom implementations can be added to the collection. When `.Url`

is called, each `IUrlProvider`

in the collection is executed in collection order until a particular `IUrlProvider`

returns a value.

Umbraco ships with a `DefaultUrlProvider`

, which maps the structure of the content tree to URLs out of the box. In Umbraco 15 and later, this is implemented as `NewDefaultUrlProvider`.


If the current domain matches the root domain of the target content, return a relative URL. Otherwise, return an absolute URL.

If the target content has one root domain, use that domain to build the absolute URL.

If the target content has more than one root domain, determine which one to use to build the absolute URL.

Complete the absolute URL with the scheme (HTTP or HTTPS). Use the scheme from the domain if one is specified; otherwise use the current request scheme.

If

`addTrailingSlash`

is`true`

, add a trailing slash.Add the virtual directory.


If the URL provider encounters collisions when generating content URLs, it selects the first available node and assigns the URL to that node. The remaining nodes are marked as colliding and do not receive a generated URL. Fetching the URL of a node with a collision URL results in an error string that includes the node ID, for example `#err-1094`

. This can happen when an `umbracoUrlName`

property overrides the generated URL of a node, or when multiple root nodes exist without hostnames assigned.

Publishing an unpublished node with a conflicting URL may change the active node rendered at that URL. This occurs when the newly published node takes priority based on sort order in the tree.

Create a custom URL Provider by implementing the `IUrlProvider`

interface:

The `UrlInfo`

object returned by `GetUrl`

can contain a custom URL.

When implementing a custom URL Provider, consider the following:

Cache results where possible.

Handle schemes (HTTP vs HTTPS) and hostnames.

Inbound routing may require a matching

`IContentFinder`.


For small changes to URL generation logic, inherit from `NewDefaultUrlProvider`

and override the `GetUrl()`

virtual method rather than implementing `IUrlProvider`

from scratch.

This example replaces the default URL provider with a custom implementation, based on `NewDefaultUrlProvider`

. The custom URL provider implements a new routing scheme for product pages.

The code below alters the outbound URL for product pages but does not provide matching inbound URL routing. This **will** break inbound routing, making the product pages unroutable.

To restore inbound routing, implement a custom content finder. See [IContentFinder](/umbraco-cms/reference/routing/request-pipeline/icontentfinder) for more information.

Use a composer to replace the default URL provider with the custom implementation:

To use multiple URL providers, add them with multiple `Insert`

calls. Umbraco cycles through all registered providers until one returns a non-`null`

value. If all custom providers return `null`

, Umbraco falls back to the default URL provider. The last provider added with `Insert`

is the first to execute.

The `GetOtherUrls`

method is used only in the Umbraco Backoffice. It provides editors with a list of other URLs that also map to the node.

For example, the convention-based `umbracoUrlAlias`

property allows editors to specify a comma-delimited list of alternative URLs for a node. A corresponding `AliasUrlProvider`

is registered in the `UrlProviderCollection`

to display this list in the backoffice **Info** panel.

Implement this method when the URL provider supports a custom preview URL scheme.

A common use case is providing external preview environments for headless sites. See [Additional preview environments support](/umbraco-cms/reference/content-delivery-api/additional-preview-environments-support) for a complete example.

Most custom URL providers do not support this. A default implementation returning `null`

is sufficient in those cases:

The URL Provider Mode specifies whether the URL provider produces absolute or relative URLs. `Auto`

is the default.

The available modes are:

Change the default setting in the `Umbraco:CMS:WebRouting`

section of `appsettings.json`:


See [WebRouting config reference documentation](/umbraco-cms/reference/configuration/webroutingsettings) for more information on routing settings.

The `ISiteDomainMapper`

implementation is used in the `IUrlProvider`

. It filters a list of `DomainAndUri`

objects to return the one that best matches the current request.

Create a custom `SiteDomainMapper`

by implementing `ISiteDomainMapper`:


The `MapDomain`

methods receive the current request URI. Custom logic determines which domain to use for a site in the context of that request. The `SiteDomainMapper`

receives the current URI and all eligible domains, and returns the single domain used by the URL Provider to construct the URL.

Only a single `ISiteDomainMapper`

can be registered with Umbraco.

Register the custom `ISiteDomainMapper`

using the `SetSiteDomainHelper`

extension method:

Umbraco ships with a default `SiteDomainMapper`

that supports grouping sets of domains together. In a multi-environment setup such as Umbraco Cloud, multiple domains may be configured for a single site. For example, live, staging, testing, and a backoffice domain. Each domain is set up as a **Culture and Hostname** entry inside Umbraco.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-86545ee310c7fdf68c4ab175304d03d9cc33c951%252Fculture-and-hostnames-v17.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=55d5e3ff&sv=2)

Without a `SiteDomainMapper`

, editors see the full list of possible URLs for each content item across all configured domains:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2362f44f052115cd29156a0e8fe1a823313a1337%252Fno-sitedomainhelp-v17.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d2a431e1&sv=2)

This can lead to confusion. Clicking a staging URL may display content from a different environment or database.

To avoid this, use the default `SiteDomainMapper`

's `AddSite`

method to group related URLs together. Because the `SiteDomainMapper`

is registered in the DI container, create a component to add the sites in the `Initialize`

method:

Register the component with a composer:

When an editor visits the backoffice, the **Links** panel filters the displayed URLs to only those in the same site group as the current domain. An editor visiting via `myproject-staging.euwest01.umbraco.io`

sees only the staging URL:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-dbfeaa88d2f1832e62d7b9867b9fe08f2c3f3cd7%252Fstaging-only-staging-v17.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=12951164&sv=2)

An editor visiting via `myproject-dev.euwest01.umbraco.io`

sees only the `dev`

and `live`

URLs:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8ca1f8805bff3882e515fd877d2af63329352dd8%252Fbackoffice-see-prod-v17.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=393aef78&sv=2)

This is a grouping, not a one-to-one mapping. Multiple URLs can be added to a group. In the example above, an editor visiting via `myproject.euwest01.umbraco.io`

(the live domain) would also see `myproject-dev.euwest01.umbraco.io`

listed, as both belong to the `dev`

group.

The `SiteDomainMapper`

includes a `BindSites`

method to bind different site groupings together:

Visiting the backoffice via `myproject-dev.euwest01.umbraco.io`

now lists all domains from both the `dev`

and the `staging`

group.

Last updated

Was this helpful?

---

#### Published Content Request Preparation | CMS

How Umbraco prepares content requests

Is started in `UmbracoRouteValueTransformer`

where it gets the `HttpContext`

and `RouteValueDictionary`

from the netcore framework:

```
 async ValueTask<RouteValueDictionary> TransformAsync(…)
```

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

.This is what actually routes your request to the correct controller and action, and allows you to hijack routes.


Set the route values to the http context.

Handles posted form data.

Returns the route values to netcore so it routes your request correctly.


When the `RouteRequestAsync`

method is invoked on the `PublishedRouter`

it will:

FindDomain().

Handle redirects.

Set culture.

Find the published content.

Only if it doesn't exist, allowing you to handle it in a custom way with a custom router handler.


Find the template.

Set the culture (again, in case it was changed).

Publish

`RoutingRequestNotification`

.Handle redirects and missing content.

Initialize a few internal stuff.


We will discuss a few of these steps below.

The FindDomain method looks for a domain matching the request Uri

Using a greedy match:

`domain.com/foo`

takes over`domain.com`

.Sets published content request’s domain.

If a domain was found.

Sets published content request’s culture accordingly.

Computes domain Uri based upon the current request (

`domain.com`

for`http://domain.com`

or`https://domain.com`

).

Else.

Sets published content request’s culture by default (first language, else system).



When finding published content the `PublishedRouter`

will first check if the `PublishedRequestBuilder`

already has content, if it doesn't the content finders will kick in. There a many different types of content finders, such as find by url, by id path, and more. If none of the content finders manages to find any content, the request will be set as 404, and the `ContentLastChanceFinder`

will run, this will try to find a page to handle a 404, if it can't find one, the ugly 404 will be used.

You can also implement your own content finders and last chance finder, for more information, see [IContentFinder](/umbraco-cms/reference/routing/request-pipeline/icontentfinder)

The `PublishedRouter`

will also follow any internal redirects, but it is limited to avoid spiraling out of control due to an infinite redirect loop.

Once the content has been found, the `PublishedRouter`

moves on to finding the template.

First off it checks if any content was found, if it wasn't it sets the template to null, since there can't be a template without content.

Next it checks to see if there is an alternative template which should be used. An alternative template will be used if the router can find a value with the key "altTemplate", in either the querystring, form, or cookie, and there is content found by the contentfinders, so not the 404 page, or it's an internal redirect and the web routing setting has `InternalRedirectPreservesTemplate`.


If no alternative template is found the router will get the template with the file service, using the ID specified on the published content, and then assign the template to the request.

If an alternative template is specified, the router will check if it's an allowed template for the content, if the template is not allowed on that specific piece of content it will revert to using the default template. If the template is allowed it will then use the file service to get the specified alternative template and assign the template to the request.

The router will pick up the redirect and redirect. There is no need to write your own redirects:

In case the router can't find a template, it will try and verify if there's route hijacking in place, if there is, it will run the hijacked route. If route hijacking is not in place, the router will set the content to null, and run through the routing of the request again, in order for the last chance finder to find a 404.

Last updated

Was this helpful?

---

---

### Special Property Type aliases for routing | CMS

Describes special property type aliases which can be used to customise routing

umbracoRedirect

umbracoInternalRedirectId

umbracoUrlName

umbracoUrlAlias

Filtering

Last updated

Was this helpful?

Describes special property type aliases which can be used to customise routing

*There are a few special/reserved Umbraco Property Type aliases that can be used which can manipulate how the standard Umbraco routing pipeline works. You can add these Property Types to any Document Type and if values are assigned to these properties, Umbraco will adjust its routing accordingly. See below for full details.*

umbracoRedirect

Creating a property alias with this name and using a Content Picker property editor lets you create a 302 temporary redirect. This in effect means that when a user navigates to this node, they will be redirected away from it.

umbracoInternalRedirectId

Add this property alias to your Document Type with a Content Picker property editor and Umbraco will load the selected page’s content transparently without performing any URL redirection. This essentially performs a rewrite.

umbracoUrlName

This property when created as a text string lets you provide a different URL name to what is created by default by the name of the node. If you enter a value for this property and save/publish the content node you will see that its main URL is updated with a new path suffix.

umbracoUrlAlias

Using this alias on a Text String lets you provide a comma-separated list of alternate full URL paths for the node. For example, if your URL was `/some-category/some-page/content-node`

, by adding an umbracoUrlAlias of "flowers", a user can navigate to the node by going to `/flowers`

. The URL alias remains in the browser address bar as a 'mask' over the real URL. You can also specify paths like `flowers/roses/red`.


Filtering

Last updated

Was this helpful?

Was this helpful?

---

### Surface controllers | CMS

Information about Surface Controllers in Umbraco

*A surface controller is an MVC controller that interacts with the front-end rendering of an Umbraco page. They can be used for rendering view components and for handling form data submissions. Surface controllers are auto-routed, meaning that you don't have to add/create your own routes for these controllers to work.*

It is a regular ASP.NET Core MVC controller that:

Is auto-routed, meaning you don't have to setup any custom routes to make it work

Is used for interacting with the front-end of Umbraco (not the backoffice)


Since any surface controller inherits from the `Umbraco.Cms.Web.Website.Controllers.SurfaceController`

class, the controller instantly supports many of the helper methods and properties that are available on the base `SurfaceController`

class including `UmbracoContext`

. Therefore, all surface controllers have native Umbraco support for:

Interacting with Umbraco routes during HTTP POSTs (i.e.

`return CurrentUmbracoPage();`

)Rendering forms in Umbraco (i.e.

`@using (Html.BeginUmbracoForm<MyController>(...)){}`

)Rendering of ASP.NET Core MVC view components


Surface controllers are plugins, meaning they are found when the Umbraco application boots. There are 2 types of surface controllers: **locally declared** & **plugin based**. The main difference between the two is that a plugin based controller gets routed via an MVC area, which is defined in the controller (see below). Because a plugin based controller is routed via an MVC area, it means that the views can be stored in a custom folder specific to the package it is being shipped in. This can be done without interfering with the local developer's MVC view files.

A locally declared surface controller is one that is not shipped within an Umbraco package. It is created by the developer of the website they are creating. If you are planning on shipping a surface controller in an Umbraco package, then you will need to create a plugin based surface controller (see the next heading).

To create a locally declared surface controller:

Create a controller that inherits from

`Umbraco.Cms.Web.Website.Controllers.SurfaceController`

The controller must be a public class.

The controller must call the base constructor of

`SurfaceController`

The controller's name must be suffixed with the term

`Controller`

The controller must be inside a namespace


For example:

All locally declared controllers gets routed to:

They do not get routed via an MVC area, so any views must exist in the following folders:

`/Views/{controllername}/`

`/Views/Shared/`

`/Views/`


If you get a 404 error when trying to access your surface controller, you may have forgotten to add a namespace to it!

If you are shipping a surface controller in a package, then you should definitely be creating a plugin based surface controller. The only difference between creating a plugin based controller and locally declared controller, is that you need to add an attribute to your class, which defines the MVC area you'd like your controller to be routed through. Here's an example:

In the above, the surface controller will belong to the MVC area called 'SurfaceControllerPackage'. Perhaps it is obvious, but if you are creating a package that contains many surface controllers, then you should most definitely ensure that all of your controllers are routed through the same MVC area.

All plugin based controllers get routed to:

Since they get routed via an MVC area, your views should be placed in the following folder:

`~/App_Plugins/{areaname}/Views/{controllername}/`

`~/App_Plugins/{areaname}/Views/Shared/`


Since you can only place static files in your package's `App_Plugin`

folder, it is highly recommended to use a name that matches your package. This helps ensure your views can be found.

The controller itself should not be placed in the App_Plugins folder, the App_Plugins folder is for static files only, compiled files like the controller will be included in the dlls used by the nuget package.

If you only want a surface controller action to be available when it's used within an Umbraco form and not from the auto-routed URL, you can add the `[ValidateUmbracoFormRouteString]`

attribute to the action method. This can be especially useful for plugin based controllers, as this makes sure the actions can only be activated from a form whenever it's used within the website.

Whenever you render an Umbraco form within your view using `Html.BeginUmbracoForm<MyController>(...)`

, the forms action will be the URL of the current page (not the auto-routed URL of the surface controller). Umbraco will therefore add a hidden `ufprt`

field to the form with an encrypted value containing the controller, action and optional area (known as the 'Umbraco form route string'). On form submission, this value is decrypted and Umbraco will activate the specified action of the surface controller.

In Umbraco 9 the `__RequestVerificationToken`

token is automatically added to forms for you, so you no longer need to add `@Html.AntiForgeryToken()`

to your forms.

Cross-Site Request Forgery (CSRF) is an attack that forces an end user to execute unwanted actions on a web application in which they are currently authenticated.

By default, `Html.BeginUmbracoForm`

and `Html.BeginForm`

adds an antiforgery token.

If the token is not added automatically, for instance, if you don't use `Html.BeginUmbracoForm`

or use an overload to `Html.BeginForm`

where you've set the `antiForgery`

parameter to false, you can add it manually like so:

If you are using a SurfaceController the antiforgery token will automatically be validated. However, if you are using a standard (non-umbraco) controller, you can manually specify it with the `ValidateAntiForgeryToken`

attribute:

The `BeginUmbracoForm`

and `BeginForm`

will only add the antiforgery token to the form as a hidden input. This means that you have to manually handle this if you're sending the request via JavaScript, for example, ajax.

The routing expects the antiforgery token to be in a header called `RequestVerificationToken`

. You can use the `beforeSend`

hook to read the antiforgery token and set it as a header if you're using ajax:

For more information, see the article.

Surface controller actions can be asynchronous. A common naming convention for asynchronous methods is using an `Async`

suffix for the action name. However, this will not work by default due to the inner workings of ASP.NET Core MVC.

Consider the following asynchronous surface controller action:

To use this action in a view you can add this:

But once you click the button, you will encounter an error message along the lines of: `InvalidOperationException: Could not find a Surface controller route in the RouteTable for controller name MySurface`.


To counter this you need to instruct ASP.NET Core MVC to explicitly accept the `Async`

suffix for controller names in the `program.cs`:


Alternatively you can rename your surface controller action so it does not contain the `Async`

suffix.

You can read more about the surface controller [action result helpers](/umbraco-cms/reference/routing/surface-controllers/surface-controllers-actions).

Last updated

Was this helpful?

#### Surface controller actions | CMS

Information about Surface Controller Actions Result Helpers in Umbraco

CurrentUmbracoPage

```
namespace RoutingDocs.Controllers;

public class MyController : SurfaceController
{
    public MyController(
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
    public IActionResult PostMethod()
    {
        if (!ModelState.IsValid)
        {
            return CurrentUmbracoPage();
        }

        return RedirectToCurrentUmbracoPage();
    }
}
```

RedirectToCurrentUmbracoPage

Querystring parameter using a string value

RedirectToCurrentUmbracoUrl

RedirectToUmbracoPage

Last updated

Was this helpful?

---

### Umbraco API Controllers | CMS

A guide to implementing APIs in Umbraco projects

What is an API?

Public APIs in Umbraco

```
using Microsoft.AspNetCore.Mvc;

namespace UmbracoDocs.Samples;

[ApiController]
[Route("/api/shop/products")]
public class ProductsController : Controller
{
    [HttpGet]
    public IActionResult GetAll() => Ok(new[] { "Table", "Chair", "Desk", "Computer" });
}
```

Adding member protection to public APIs

Examples

Backoffice API Controllers

Last updated

Was this helpful?

A guide to implementing APIs in Umbraco projects

This article describes how to work with API Controllers in Umbraco to create REST services.

`UmbracoApiController`

has been removed from Umbraco CMS as of version 15.

Read the article [Porting old Umbraco APIs](/umbraco-cms/reference/routing/umbraco-api-controllers/porting-old-umbraco-apis) for more details.

What is an API?

The Microsoft ASP.NET Core API documentation is a great place to familiarize yourself with API concepts. It can be found on the .

Public APIs in Umbraco

A public API in Umbraco is created as any other ASP.NET Core API:

ProductsController.cs

```
using Microsoft.AspNetCore.Mvc;

namespace UmbracoDocs.Samples;

[ApiController]
[Route("/api/shop/products")]
public class ProductsController : Controller
{
    [HttpGet]
    public IActionResult GetAll() => Ok(new[] { "Table", "Chair", "Desk", "Computer" });
}
```

Adding member protection to public APIs

To protect your APIs based on front-end membership, you can annotate your API controllers with the `[UmbracoMemberAuthorize]`

attribute.

There are 3 parameters that can be supplied to control how the authorization works:

To allow all members, use the attribute without supplying any parameters.

You can apply these attributes either at controller level or at action level.

Read more about members and member login in the [Member Registration and Login](/umbraco-cms/tutorials/members-registration-and-login) article.

Examples

This will allow any logged in member to access all actions in the `ProductsController`

controller:

This will only allow logged in members of type "Retailers" to access the `GetAll`

action:

This will only allow members belonging to the "VIP" group to access any actions on the controller:

This will only allow the members with ids 1, 10 and 20 to access the `GetAll`

action:

Backoffice API Controllers

Read the [Creating a Backoffice API article](/umbraco-cms/tutorials/creating-a-backoffice-api) for a comprehensive guide to writing APIs for the Management API.

The Umbraco Backoffice API is also known as the Management API. Thus, a Backoffice API Controller is often referred to as a Management API Controller.

Last updated

Was this helpful?

Was this helpful?

```
// Comma delimited list of allowed member types
string AllowType

// Comma delimited list of allowed member groups
string AllowGroup

// Comma delimited list of allowed member Ids
string AllowMembers
```

ProductsController.cs

```
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Web.Common.Filters;

namespace UmbracoDocs.Samples;

[ApiController]
[Route("/api/shop/products")]
[UmbracoMemberAuthorize]
public class ProductsController : Controller
{
    [HttpGet]
    public IActionResult GetAll() => Ok(new[] { "Table", "Chair", "Desk", "Computer" });
}
```

ProductsController.cs

```
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Web.Common.Filters;

namespace UmbracoDocs.Samples;

[ApiController]
[Route("/api/shop/products")]
public class ProductsController : Controller
{
    [HttpGet]
    [UmbracoMemberAuthorize("Retailers", "", "")]
    public IActionResult GetAll() => Ok(new[] { "Table", "Chair", "Desk", "Computer" });
}
```

ProductsController.cs

```
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Web.Common.Filters;

namespace UmbracoDocs.Samples;

[ApiController]
[Route("/api/shop/products")]
[UmbracoMemberAuthorize("", "VIP", "")]
public class ProductsController : Controller
{
    [HttpGet]
    public IActionResult GetAll() => Ok(new[] { "Table", "Chair", "Desk", "Computer" });
}
```

ProductsController.cs

```
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Web.Common.Filters;

namespace UmbracoDocs.Samples;

[ApiController]
[Route("/api/shop/products")]
public class ProductsController : Controller
{
    [HttpGet]
    [UmbracoMemberAuthorize("", "", "1,10,20")]
    public IActionResult GetAll() => Ok(new[] { "Table", "Chair", "Desk", "Computer" });
}
```

#### Porting old Umbraco API Controllers | CMS

Tips to porting over API controllers from Umbraco 13 and below

Porting over

`UmbracoApiController`

implementations```
using Microsoft.AspNetCore.Mvc;

namespace UmbracoDocs.Samples;

[ApiController]
[Route("/umbraco/api/products")]
public class ProductsController : Controller
{
    [HttpGet("getall")]
    public IActionResult GetAll() => Ok(new[] { "Table", "Chair", "Desk", "Computer" });
}
```

```
using Microsoft.AspNetCore.Mvc;
using Umbraco.Cms.Web.Common.Controllers;

namespace UmbracoDocs.Samples;

public class ProductsController : UmbracoApiController
{
    public IActionResult GetAll() => Ok(new[] { "Table", "Chair", "Desk", "Computer" });
}
```

Porting over "plugin based" implementations

Backoffice API Controllers

Last updated

Was this helpful?

---

### URL Redirect Management | CMS

URL redirect management in Umbraco

Whenever a document is published, and this causes changes to its URL (and any of its descendants' URLs), Umbraco makes a note of the old URLs. Whenever an incoming request is served and the default content finders cannot find a matching published document, Umbraco checks whether the URL matches one of these saved URLs. If a match is found, Umbraco returns a "301 Redirect" response pointing to the new URL of the document.

The URL Redirect Management functionality does not support rewriting "rules" (e.g. regular expressions), nor complex scenarios (e.g. changing the culture and hostnames configuration). There are already powerful solutions to deal with these types of situations, such as Microsoft's own module for IIS. Since netcore is decoupled from the webserver hosting it, your approach for URL rewriting, outside what Umbraco provide out of the box, will depend on what you use to host your solutions, but for more info on the IIS Url Rewrite module have a look at the .

It is possible to list the redirect URLs via the *Redirect Url Management* dashboard in the *Content* section. This dashboard lists the original URL, new URL, and culture. It also allows you to delete a URL redirect.

In addition, the dashboard can be used to disable or enable the 301 Redirect Management (via the `appsettings.json`

configuration option described below - note that this requires an application restart to take effect).

Anytime a document is published and its corresponding *url segment* changes, Umbraco checks its URL (and all its descendants' URLs) for changes. For every URL that has changed, it creates (or updates) a row in the `umbracoRedirectUrl`

table. Rows in this table contain: the old url, the create date, and the target content identifier, culture, and a url hash.

Umbraco registers a new content finder, `ContentFinderByRedirectUrl`

, which runs as a normal content finder after the other content finders. It looks for the incoming URL in the database table and, if found, computes the URL of the target document and returns a "301 Redirect". These redirects are considered "permanent". It's good to note that we explicitly set `no-cache`

headers on these redirects so that when they change, browsers update the URL immediately. They are a "true" 301, however, and search engines will accept them as such.

The 301 Redirect Management feature is enabled by default.

It is possible to disable the feature entirely (both generating URLs in the database table, and running the content finder) by editing the `appsettings.json`

file:

```
"Umbraco": {
  "CMS": {
    "WebRouting": {
      "DisableRedirectUrlTracking": false
    }
  }
}
```

See [the web routing config reference](/umbraco-cms/reference/configuration/webroutingsettings) for more configuration options

Last updated

Was this helpful?

---

---


## Scheduling | CMS

Run a background job on a recurring basis

It is possible to run recurring code using a recurring background job. Background job classes should implement the `IRecurringBackgroundJob`

interface, which controls when and where the job gets run.

Once you have created your background job class, register it using a Composer. It will be detected at startup and a new `HostedService`

will be created to run your job.

Be aware you may or may not want this background job to run on all servers. If you are using Load Balancing with multiple servers, see [load balancing documentation](/umbraco-cms/fundamentals/setup/server-setup/load-balancing) for more information

`IRecurringBackgroundJob`

Properties and MethodsDefines how often the job runs. This property is a `TimeSpan`.


```
// Run this job every 5 minutes
TimeSpan Period = TimeSpan.FromMinutes(5);
```

Defines how long to wait after application startup before running the task for the first time. Default is 3 minutes. This property is a `TimeSpan`.


```
// Wait 3 minutes after application startup before starting to run this job.
TimeSpan Delay = TimeSpan.FromMinutes(3);
```

Specifies a list of roles that should run this job. In a multi-server setup, you may want your job to run on *all* servers or only on *one* of your servers.

For example, a temporary file cleanup task might need to run on all servers. A database import job might be better to be run once per day on a single server.

By default: `{ Single, SchedulingPublisher }`

, meaning it runs on one server only.

For more information about server roles, see the [Load Balancing](/umbraco-cms/fundamentals/setup/server-setup/load-balancing#scheduling-and-server-role-election) documentation.

An event used to notify the background job service if the job’s period changes dynamically.

For example, if the period for your job is controlled by a configuration file setting, you can trigger the `PeriodChanged`

event when the configuration changes.

See the [Example](/umbraco-cms/reference/scheduling#example) below on how to implement the `PeriodChanged`

event.

The main method where your job logic is implemented.

This example shows the minimum code necessary to implement the `IRecurringBackgroundJob`

interface. The job runs every 60 minutes on all servers.

This example shows how to inject other Umbraco services into your background job. This example cleans the recycle bin every 60 minutes. To do so, it injects an `IContentService`

to access the Recycle bin and an `IScopeProvider`

to provide an ambient scope for the `EmptyRecycleBin`

method.

The complex example builds on the previous one by injecting additional services. It includes a logger to log error messages, a profiler to capture timings, and an `IServerRoleAccessor`

to log the current server role. Additionally, it injects an `IOptionsMonitor`

to allow the period to be updated while the server is running. It also demonstrates how to trigger the `PeriodChanged`

event to signal the job's host.

All we need to do here is to create the composer where we register the background job with `AddRecurringBackgroundJob`.


Learn more about how to register dependencies in the [Dependency Injection](/umbraco-cms/reference/using-ioc) article.

`RecurringHostedServiceBase`

is a low-level base class. It implements the dotnetcore interface `IHostedService`

to run itself in the background, and creates and manages the timer that runs the job on a recurring basis.

`RecurringBackgroundJobHostedService`

is an Umbraco specific Hosted Service that extends `RecurringHostedServiceBase`

. It uses some system-level Umbraco services to ensure that your jobs only execute once Umbraco is up and running. It checks:

Server Roles - see above for more discussion about Server roles

MainDom - The

`MainDom`

lock ensures that only one instance of Umbraco is running at a time on a given machine. This ensures the integrity of certain files used by Umbraco. See[Host Synchronization](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/azure-web-apps#host-synchronization)for more details.Runtime State - On a fresh install or when waiting for a database upgrade, Umbraco may be fully up and running yet.


The `RecurringBackgroundJobHostedService`

publishes a number of notifications that can be hooked to report on the status of background jobs. All notifications extend from the base `Umbraco.CMS.Infrastructure.Notifications.RecurringBackgroundJobNotification`

class.

The following notifications are available:

Starting

Started

Stopping

Stopped

Executing

Executed

Failed

Ignored


The Starting/Started and Stopping/Stopped notification pairs are published when the `RecurringBackgroundJobHostedService`

is started or stopped. The start event normally occurs soon after application start as part of the .Net WebHost startup process. Similarly the stop event would happen as part of application shutdown.

These notifications are there to support low-level debugging of background jobs to ensure they are starting/stopping correctly. Due to the timing of the notification, all handlers associated with these notifications should not depend on any Umbraco services, including database access.

The Ignored notification is published when a background job's schedule is triggered, but the Umbraco runtime checks prevent it from running.

This notification is there to support low-level debugging of background jobs to ascertain why they are/aren't running. As the runtime checks include runtime state readiness, this event may be triggered during the install phase. Any notification handlers associated with this notification should **also** conduct their own checks before relying on Umbraco services, including database access.

These notifications will be triggered in pairs depending on the success/failure of the job itself.

The executing notification is triggered before the job is run.

The executed notification is triggered after the job is completed.

The failed notification is triggered from the catch block if an exception is thrown.


For **successful** job runs, the following notifications will be published:

Executing

Executed


For **failed** job runs, the following notifications will be published:

Executing

Failed


When load balancing the backoffice, all servers will have the `SchedulingPublisher`

role. This means the approach described above for restricting jobs to specific server roles will not work as intended. All servers will match the `SchedulingPublisher`

role.

Instead, for jobs that should only run on a single server, you should implement an `IDistributedBackgroundJob`.


`IDistributedBackgroundJob`

is separate from `IRecurringBackgroundJob`

, and is tracked in the database to ensure that only a single server runs the job at any given time. This also means that you are not guaranteed what server will run the job, but you are guaranteed that only one server will run it.

By default, distributed background jobs are checked every 5 seconds, with an initial delay of 1 minute after application startup. These settings can be changed in appsettings, see [Distributed jobs settings](/umbraco-cms/reference/configuration/distributedjobssettings) for more information.

To implement a custom distributed background job, create a class that implements the `IDistributedBackgroundJob`

interface. As with `IRecurringBackgroundJob`

, dependency injection (DI) is available in the constructor.

It's required to give your job a unique name via the `Name`

property. This is used to track the job in the database.

The period is specified via the `Period`

property, which controls how often the job should run. In this example, it runs every 20 seconds.

It's not required to manually register the job in the database, however, you must register it to DI so Umbraco can find it. This can be done with a composer or in `Program.cs`


Last updated

Was this helpful?

---


## Searching | CMS

*Search in Umbraco is powered by Examine out of the box, which is a Lucene-based search and index engine for Umbraco. Umbraco provides everything required to have powerful and fast search up and running on your website. You can also extend or replace the available configuration to exactly match your requirements. This documentation focuses on the Examine implementation.*

Examine and Lucene are external parts used in Umbraco. When working with either of the two, we strongly recommend using their official documentation.

Understand how Examine works and walk through the many available options and settings in Umbraco.

Umbraco HQ offers a training course covering the inner workings of Examine and Lucene, query debugging, and knowledge of the search tool. The course targets backend ASP.NET MVC developers who need to build real-world search applications with Umbraco.

[Explore the Searching and Indexing with Examine Training Course arrow-up-right](https://umbraco.com/training/course-details/searching-and-indexing/)

Last updated

Was this helpful?

### Examine

### Contents

- [Corrupt Indexes | CMS](#corrupt-indexes-cms)
- [Examine Management | CMS](#examine-management-cms)
- [Examine Manager | CMS](#examine-manager-cms)
- [Custom indexing | CMS](#custom-indexing-cms)
- [PDF indexes and multisearchers | CMS](#pdf-indexes-and-multisearchers-cms)
- [Quick-start | CMS](#quick-start-cms)

---

### Corrupt Indexes | CMS

How to deal with Corrupt Examine indexes

Last updated

Was this helpful?

How to deal with Corrupt Examine indexes

The data integrity of Examine index files can be compromised if for example files are removed. When this happens, Umbraco considers the index to be corrupt.

As some systems are already hooked into the Examine index lifecycle, resolving this issue outside the application is safest.

Resolution in a self-hosted environment

The following steps cover clearing out corrupt indexes in a self-hosted environment.

Stop the website/app pool.

Remove the directory containing the corrupted index files.

Restart the website.


Resolution on Umbraco Cloud

The following steps cover clearing out corrupt indexes in a setup hosted on Umbraco Cloud.

Open the project in the Cloud Portal.

Select the correct environment.

Access KUDU.

Open the debug console.

Choose CMD.

Navigate to

`C:\home\site\wwwroot\umbraco\Data\Temp`

. 7- Click the delete button next to the index file.Restart the environment.


Last updated

Was this helpful?

Was this helpful?

---

### Examine Management | CMS

*Provides an overview of the available Examine functionality available directly within the Umbraco backoffice*

The Umbraco backoffice allows you to view details about your Examine indexes and searchers - all in one place. You can see which fields are being indexed, rebuild the indexes if there's a problem, and test keywords to see what results would be returned.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8fcfc7620ef4b4c664aa2819b89c38113bc611ca%252Foverview-examine-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6d547124&sv=2)

The Examine Management dashboard, accessible from within the Settings section, is split into two sections: Indexers and Searchers.

From the Indexers section, you can view details about each Examine index currently configured within your Umbraco installation. Clicking any of these indexes will show you additional options, each discussed below.

This section displays properties of the selected index, including the number of stored documents and fields.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-415f0115197a25467549e7bb39555e0c47ee922f%252FExternal-indexes-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=2eeef9a3&sv=2)

Within the Indexers it displays the details for the index provider as well.

This can be useful to confirm the configuration that Umbraco is using and to ensure it is working as expected. This section also displays the full file path of the index itself.

This section also provides the ability to rebuild the index, should this be required. Depending on how much content your website has, rebuilding the search indexes could take a while and affect the site performance temporarily. It is not recommended to do this while the website is under high load.

From here, you can see the default system fields that are stored for each document within the search index. That includes the number of fields document, and the score which is calculated by Examine depending on how closely the individual results matched the search term.

From the Searchers section, you can view details about each Examine searcher currently configured within your Umbraco installation. Clicking any of these searchers will take you to a search page, where you can test out your search terms.

You can see an example here how to configure an Examine searcher in the [Examine Multisearcher documentation](/umbraco-cms/reference/searching/examine/pdfindex-multisearcher#multi-index-searchers).

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b8bbb00d317542c672be6e3533ecb29140fb8c83%252Fexamine-management-search-field.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c375f92e&sv=2)

The search field allows you to enter a search term and receive results back from the searcher in question. You can confirm if your query is working as expected. Matching results are returned in their raw format, with the score, document ID and Name being returned. The score is calculated by Examine depending on how closely the individual results matched the search term.

Last updated

Was this helpful?

---

### Examine Manager | CMS

Last updated

Was this helpful?

Accessing the singleton can be done by using dependency injection.

In a class you can inject the IExamineManager interface:

```
using Examine;

namespace MyCustomUmbracoSolution;

public class MyClass
{
    private readonly IExamineManager _examineManager;
    public MyClass(IExamineManager examineManager)
    {
        _examineManager = examineManager;
    }
}
```

In a view the IExamineManager can be injected as well:

```
@inject IExamineManager ExamineManager;
```

This returns an active instance of the ExamineManager which exposes operations such as:

Default index & search providers

Full collection of index & search providers

All indexing and searching methods


Searching

Important to note that the `Search`

methods on the ExamineManager will call the Search methods of the **default** search provider specified in config. If you want to search using a specific provider, there are generally two approaches for this.

If you want to use the searcher of a specific index, you should get the the searcher via the index:

If you have configured a custom searcher that you wish to use instead, you can access the searcher directly via the `IExamineManager`

instance:

An example using a custom searcher is below:

Indexing

When you wanna populate an index, you will need to use the `IExamineManager`

and get the specific index. The build-in index names are all available as constants from the `Umbraco.Cms.Core.Constants.UmbracoIndexes`

namespace

The indexing methods available on a single index are:

Last updated

Was this helpful?

Was this helpful?

```
@inherits UmbracoViewPage
@using Examine
@using Umbraco.Cms.Core
@inject IExamineManager ExamineManager
@{

    // Get the search text from the query string
    string query = Context.Request.Query["query"];

    // Try to get the "ExternalIndex" from the Examine manager
    if (ExamineManager.TryGetIndex(Constants.UmbracoIndexes.ExternalIndexName, out IIndex index))
    {

        // Search via the searcher of the index
        ISearchResults searchResults = index.Searcher.Search(query);

        // Check whether the search revealed any results
        if (searchResults.Any())
        {
            <ul>
                @foreach (ISearchResult result in searchResults)
                {

                    // Skip the result if the ID is null
                    if (result.Id is null) continue;

                    // Skip the result if not found in the content cache
                    if (Umbraco.Content(result.Id) is not {} node) continue;

                    <li>
                        <a href="@node.Url()">@node.Name</a>
                    </li>

                }
            </ul>
        }

    }

}
```

```
bool canGetSearcher = ExamineManager.TryGetSearcher("MyCustomSearcher", out ISearcher searcher);
```

```
@inherits UmbracoViewPage
@using Examine
@inject IExamineManager ExamineManager
@{

    // Get the search text from the query string
    string query = Context.Request.Query["query"];

    // Try to get the "MyCustomSearcher" searcher
    if (ExamineManager.TryGetSearcher("MyCustomSearcher", out ISearcher searcher))
    {

        // Search via the searcher
        ISearchResults searchResults = searcher.Search(query);

        // Check whether the search revealed any results
        if (searchResults.Any())
        {
            <ul>
                @foreach (ISearchResult result in searchResults)
                {

                    // Skip the result if the ID is null
                    if (result.Id is null) continue;

                    // Skip the result if not found in the content cache
                    if (Umbraco.Content(result.Id) is not {} node) continue;

                    <li>
                        <a href="@node.Url()">@node.Name</a>
                    </li>

                }
            </ul>
        }

    }

}
```

```
if (_examineManager.TryGetIndex(Umbraco.Cms.Core.Constants.UmbracoIndexes.ExternalIndexName, out IIndex index))
{
   // Use index here
}
```

```
void DeleteFromIndex(IEnumerable<string> itemIds);
void DeleteFromIndex(this IIndex index, string itemId);
void IndexExists();
void IndexItems(IEnumerable<ValueSet> values);
```

---

### Custom indexing | CMS

Learn how to build and customize the indexes that comes with your Umbraco website.

You can modify the built-in indexes in the following ways:

- giving you control over exactly what data goes into them and how the fields are configured

Changing the field value types to change how values are stored in the index

Changing the

`IValueSetValidator`

to change what goes into the indexTake control of the entire index creation pipeline to change the implementation


We can do all this by using the `ConfigureNamedOptions`

pattern.

We will start by creating a ConfigureExamineOptions class, that derives from `IConfigureNamedOptions<LuceneDirectoryIndexOptions>`:


```
using Examine.Lucene;
using Microsoft.Extensions.Options;

namespace Umbraco.Docs.Samples.Web.CustomIndexing;

public class ConfigureExternalIndexOptions : IConfigureNamedOptions<LuceneDirectoryIndexOptions>
{
    public void Configure(string name, LuceneDirectoryIndexOptions options)
    {
        throw new System.NotImplementedException();
    }

    public void Configure(LuceneDirectoryIndexOptions options)
    {
        throw new System.NotImplementedException();
    }
}
```

In this sample we are altering the external index and thus we name the class `ConfigureExternalIndexOptions`

. If you are altering multiple indexes, it is recommended to have separate classes for each index - i.e. `ConfigureExternalIndexOptions`

for the external index, `ConfigureInternalIndexOptions`

for the internal index and so on.

When using the `ConfigureNamedOptions`

pattern, we have to register this in a composer for it to configure our indexes, this can be done like this:

The `ComposeAfter`

attribute usage guarantees that the composer will run after the core composer responsible for setting up the default index details.

By default, Examine will store values into the Lucene index as "Full Text" fields, meaning the values will be indexed and analyzed for a textual search. However, if a field value is numerical, date/time, or another non-textual value type, you might want to change how the value is stored in the index. This will let you take advantage of some value type-specific search features such as numerical or date range.

There is some documentation about this in the .

The easiest way to modify how a field is configured is using the `ConfigureNamedOptions`

pattern like so:

This will ensure that the `price`

field in the index is treated as a `double`

type (if the `price`

field does not exist in the index, it is added).

An `IValueSetValidator`

is responsible for validating a `ValueSet`

to see if it should be included in the index. For example, by default the validation process for the ExternalIndex checks if a `ValueSet`

has a category type of either "media" or "content" (not member). If a `ValueSet`

was passed to the ExternalIndex and it did not pass this requirement it would be ignored.

The `IValueSetValidator`

is also responsible for filtering the data in the `ValueSet`

. For example, by default the validator for the MemberIndex will validate on all the default member properties, so an extra property "PhoneNumber", would not pass validation, and therefore not be included.

The `IValueSetValidator`

implementation for the built-in indexes, can be changed like this:

Remember to register `ConfigureMemberIndexOptions`

in your composer.

The following example will show how to create an index that will only include nodes based on the **Product**.

It is recommended to use the existing built-in `ExternalIndex`

. You should then query based on the `NodeTypeAlias`

instead of creating a new separate index based on that particular node type. However, should the need arise, the example below will show you how to do it.

Take a look at the [Examine Quick Start](/umbraco-cms/reference/searching/examine/quick-start) guide to see some examples of how to search the ExternalIndex.

To create this index we need five things:

An

`UmbracoExamineIndex`

implementation that defines the index.An

`IConfigureNamedOptions`

implementation that configures the index fields and options.An

`IValueSetBuilder`

implementation that builds index value sets a piece of content.An

`IndexPopulator`

implementation that populates the index with the value sets for all applicable content.An

`INotificationHandler`

implementation that updates the index when content changes.A composer that adds all these services to the runtime.


This is only an example of how you could do indexing. In this example, we're indexing all content, both published and unpublished.

In certain scenarios only published content should be added to the index. To achieve that, you will need to implement your own logic to filter out unpublished content. This can be somewhat tricky as the published state can vary throughout an entire structure of content nodes in the content tree. For inspiration on how to go about such filtering, you can look at the .

The index will only update its content when you manually trigger an index rebuild in the Examine dashboard. This is not always the desired behavior for a custom index.

To update your index when content changes, you can use notification handlers.

The following handler class does not automatically update the descendant items of the modified content nodes, such as removing descendants of deleted content. If changes to the parent content item can affect its children or descendant items in your setup, refer to the [UmbracoContentIndex.PerformDeleteFromIndex() in Umbraco arrow-up-right](https://github.com/umbraco/Umbraco-CMS/blob/main/src/Umbraco.Examine.Lucene/UmbracoContentIndex.cs#L124-L153)*product*.

You can find further inspiration for implementing notification handlers (*for example, for media updates*) in the .

The order of these registrations matters. It is important to register your index with `AddExamineLuceneIndex`

before calling `ConfigureOptions`.


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ee91e43bba0bdf9ed841956569a15cfe26993282%252Fexamine-management-product-index.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1bde652b&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-100222968ed167e3d089388f41ba51bf490a92b7%252Fexamine-management-product-document.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1142b507&sv=2)

If you have a need, you can also use an Examine index for other data, that you aren't managing as Umbraco content.

As an illustrative example, consider a collection of books. This example uses a hardcoded collection. In a real-world scenario, the data would more likely come from a database.

As with the previous example, define an index. At this time, Umbraco data isn't being indexed; the implementation inherits directly from `LuceneIndex`:


The index is customized and fields are defined as before via `IConfigureNamedOptions`:


And once again, a composer is required to register the necessary components:

With this in place, the details of the index will be available under the **Settings** > **Examine Management** > **Indexes** screen.

To verify indexing and querying, a controller can be used:

Last updated

Was this helpful?

---

### PDF indexes and multisearchers | CMS

If you want to index PDF files and search for them you will need to use the .

Install with NuGet:`dotnet add package Umbraco.ExaminePDF`


This will create a new Examine index called "PDFIndex", which will appear in "Examine Management" dashboard under the "Settings" section. Using this index you can start searching the contents of any PDF files uploaded to the media section.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F7405322%2F189886089-d23b45c7-814b-4101-b143-31c5cd9fa655.png&width=768&dpr=3&quality=100&sign=49b7745b&sv=2)

A multi-index searcher is a searcher that can search multiple indexes. This can be helpful when you for example want to search both the external and internal indexes. You can register a multi-index searcher with the ExamineManager on startup like:

With this approach, the multi-index searcher will show up in the "Examine Management" dashboard.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F7405322%2F189887744-af2d8e69-4807-4407-868d-b43e9fa9518d.png&width=768&dpr=3&quality=100&sign=870c4e3c&sv=2)

The multi-index searcher can be resolved in code from the ExamineManager like this:

The implementation of IPdfTextExtractor is PdfSharpTextExtractor in this library, which uses PDFSharp to extract the bytes to convert to text. That implementation doesn't deal well with Unicode text which means when some PDF files are read, the result will be 'junk' strings.

It is certainly possible to replace the IPdfTextExtractor using your own composer like

`composition.RegisterUnique<IPdfTextExtractor, MyCustomSharpTextExtractor>();`


The iTextSharp library deals with Unicode in a better way but is a paid for license. If you wish to use iTextSharp or another PDF library you can swap out the IPdfTextExtractor with your own implementation.

Last updated

Was this helpful?

---

### Quick-start | CMS

*This guide will help you get set up quickly using Examine with minimal configuration options. Umbraco ships Examine with 3 indexes: internal, external, and members. The internal index should not be used for searching when returning results on a public website because it includes content that has not been published yet. Instead, you can use the external index to get up and running.*

In the coming examples, the has been used, as it provides some example content that can be searched. Therefore, some of the examples below may require 'the setting up of templates, etc' if you follow the guide on your existing site.

The starter kit comes with some Templates, Document Types, and content nodes created already. We will use some of these to set up a basic search system. This is a 'Quick Start' guide, as many more complex searches are possible with Examine.

We will make it possible to 'search' on the *People* page, by adding a search bar to the template page: `people.cshtml`

- add the following form at the top of the template, but underneath the `<nav>`

element:

```...
</nav>
-->
<div>
    <form action="@Model.Url()" method="get">
        <input type="text" placeholder="Search" name="query"/>
        <button>Search</button>
    </form>
</div>
<div class="employee-grid">...
```

This will create a basic input field at the top of the page and make it post to the same people page when submitted along with the search term.

The best practice for POST requests is to encapsulate the request handling in a controller. To do this we will leverage the concept of [route hijacking](/umbraco-cms/reference/routing/custom-controllers).

Let's start by creating a `PeopleController`

that derives from `RenderController`

and add an `Index`

method.

It is important to name our controller by the convention

. In our case the view is named People, so the controller is named *NameOfViewController*`PeopleController`.


To search anything from our controller, we first need to create a service that handles the actual search logic. We'll start by creating an interface for our service.

Now create a default implementation of the service interface.

And finally register the service in `Startup`.


To perform the search we will first need to get a reference to the particular Examine index that we want to search. Then we will use this index to access its corresponding `Searcher`

. We use the `Searcher`

to construct the query logic to execute and search the index.

Umbraco ships with three indexes:

ExternalIndex - available to use for indexing published unprotected content.

InternalIndex - which Umbraco's backoffice search uses.

MembersIndex - which Umbraco's Membership implementation uses.


[You can create your own indexes too](/umbraco-cms/reference/searching/examine/indexing) if you need to analyse text in a different language for example.

The service `IExamineManager`

is used to retrieve an Examine index by its 'alias', so we need to inject that service into our `SearchService`.


With the `IExamineManager`

injected in our `SearchService`

, we can implement the `SearchContentNames`

method. We do this using the `Searcher`

for the Examine index 'ExternalIndex'.

We reference the External index by its alias "ExternalIndex". Umbraco has a set of 'Constants' that refer to the indexes that can be more convenient to use `Constants.UmbracoIndexes`

. So, in the example here we could have used `Constants.UmbracoIndexes.ExternalIndexName`

instead of "ExternalIndex".

The `Searcher`

has a CreateQuery method, where you can choose to search content, media or members eg:

From here you can see how we can chain together the logic to perform the search. In the example, we are searching all `content`

using the `person`

Document Type, where the `nodeName`

is equal to the search term that was typed in the input bar.

Calling `.Execute()`

at the end of the query logic triggers the search and returns a set of matching search results, which we can loop through to get the IDs of the resulting content items.

We want to retrieve the actual content from the IDs. For that, we need the `UmbracoHelper`

, which must be injected into our service as well. The final implementation of `SearchService`

then looks like this.

After getting the ids from our search, we then loop through the list and return the content.

We will now need a custom view model so that we can pass our search results to the view. Our view model needs to inherit from `PublishedContentWrapped`

because our People view is expecting a model that is content. We then wrap the content and add the search data, all in a convenient view model.

Now that we've created our service to handle the actual search logic, and our view model to pass the search results to the view, let's look at using them in the controller. We will want to update the `Index()`

method to get out the query string from the request, then create a view model and populate the `SearchResults`

property by using our service.

The final thing we need to do is update the view to use our new view model. We do that by changing the `@inherits`

line in the view.

Let's now use the view model to display the search results. We'll place them directly under the form we created earlier.

Examine has a lot of different ways to query data. Building upon the example from before, here are a few other searches that can be done to get different data:

Let's say you want to search through **all content nodes** by their **file names**. You could amend the query from before like this:

To do the search like above, but only use Lucene to query, amend the query from before like this:

To search through **all child nodes of a specific node** by their **bodyText property**, amend the query from before like this:

Last updated

Was this helpful?

---

---
