# Implement Custom Error Pages | CMS

A set of tutorials for creating and implementating custom error pages in an Umbraco CMS project.

Umbraco is built on Microsoft's .NET Framework and uses ASP.NET. This provides different options when setting up custom error pages on your website.

Implementing custom error handling can make your site look more on-brand and minimize the impact that errors have on user experience. For example, a custom 404 page with helpful links or a search function can add extra value to your site.

In Umbraco, in-code error page handling refers to managing and displaying custom error pages directly through code. This method provides greater flexibility and control over how errors are handled and presented to users, especially within the context of an Umbraco site.

This article contains guides on how to create custom error pages for the most common scenarios:

**Are you looking for a guide to create a custom maintenance page?**

This has been moved to a separate article: [Create a custom maintenance page](/umbraco-cms/tutorials/create-a-custom-maintenance-page).

To follow this guide successfully, ensure you're using Umbraco version 16.1 or later, as it fixes a regression from version 16.0. For more details, see the section in the Release Notes.

A 404 error occurs when a requested page cannot be found, usually due to deleted content, a changed URL, or an invalid path. In Umbraco, you can create and configure custom 404 pages using content from the backoffice.

Go to the

**Settings**section in the backoffice.Create a new

**Document Type with Template**.Name the Document Type

*Page Not Found*.[Optional] Add custom properties (for example, title, message), though most 404 pages are static.

Click

**Save**.Go to the

**Templates**folder and edit the generated template.Add your custom markup and design for the error page in the template.

Click

**Save**.

You can create a *Page Not Found* page directly in your content tree, or organize it within a container for error pages. Using a container allows for better content organization, especially if you plan to handle multiple status codes (for example, 404, 500, maintenance, and so on). Both options work as long as the page ID is referenced correctly in the `appsettings.json`

file.

Create a new

**Document Type**.Name it

*Error Pages Container*.Go to the

**Structure**Workspace view.Enable

**Allow at root**.Add the

*Page Not Found*Document Type as an**Allowed child node types**.Click

**Choose**.

Click

**Save**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4143e5a7981a97b75d1c4e6d8447f5903e540f53%252Fcontainer.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8273d180&sv=2)

Go to the

**Content**section.Create a new content node based on the

*Error Pages Container*Document Type. For example*Error Page*.Click

**Save**or**Save and Publish**.Create a child node, using the

*Page Not Found*Document Type.Name it

*Page Not Found*or similar.This will be the content shown when a 404 error occurs.


Click

**Save**or**Save and Publish**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4fdd494b842d3843c40c350f5a0c340e2e1094ae%252Fpage-not-found.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=add9aeba&sv=2)

`appsettings.json`

fileAfter publishing the *Page Not Found* page, connect it in the configuration:

Go to the

**Info**tab of the*Page Not Found*content item in the Backoffice.Copy the

**Id**of the page (for example: 06cf09c8-c83a-4dd7-84e5-6d98d51e4d12).Go to your project's

`appsettings.json`

file.Add the

`Error404Collection`

setting to`Umbraco:CMS:Content`

, like shown below:

Replace the value for `ContentKey`

with the ID of your own *Page Not Found* page.

You can define different error pages for each language or culture (such as `en-us`

, `da-dk`

, and so on):

Each entry maps a culture to its specific 404 page using the content’s GUID.

It is also possible to set up a 404 error page programmatically using `IContentLastChanceFinder`

. To learn more about `IContentLastChanceFinder`

, read the [Custom Routing](/umbraco-cms/implementation/custom-routing) article. Use this approach only if you need dynamic logic, multi-tenant routing, or other custom behavior.

Before following this example, follow the [Create a Page Not Found page in the backoffice](/umbraco-cms/tutorials/custom-error-page#create-a-page-not-found-page-in-the-backoffice) part. The example below will use the *Page Not Found* alias of the Document Type to find and display the error page.

Create a new

`.cs`

file called`PageNotFound.cs`

at the root of the project.Add the following code to the newly created class:


This section guides you in setting up a custom page for handling internal server errors (500 errors) in your Umbraco site. This setup works when:

A template throws an error.

A controller throws an unhandled exception.

A request hits the application, but something fails during rendering or processing.


Go to the

**Settings**section in the Umbraco backoffice.Create a new

**Document Type with Template**called*ErrorPage500*.[Optional] Add any relevant properties to the Document Type.

Click

**Save**.Go to the

**Templates**folder.Add your custom markup and design for the error page in the template. In this case,

*ErrorPage500*.Click

**Save**.

Create a new

**Document Type**.Name it

**Error Pages Container**.Go to the

**Structure**Workspace view.Enable

**Allow at root**.Add the

*ErrorPage500*Document Type as an**Allowed child node types**.Click

**Choose**.

Click

**Save**.

Go to the

**Content**section.Create a new content node based on the

*Error Pages Container*Document Type. For example*Home Page*.Click

**Save**or**Save and Publish**.Create a child node, using the

*ErrorPage500*Document Type.Name it

*Page 500*or similar.This will be the content shown when a 500 error occurs.



To ensure that the 500 page is shown during server errors, you’ll need to configure a custom error controller and route handling.

Create a folder called

`Controllers`

in the root of your Umbraco project.Add a new file called

`ErrorController.cs`

in the`Controllers`

folder.Add the following code to the file:


Replace *YourProjectNamespace* with the actual project namespace. In Visual Studio, you can right-click the project and select **Sync Namespaces**.

Add the

`/error/`

route to the list of reserved paths in the`appSettings.json`

file:

Update

`Program.cs`

to ensure the error route is triggered by unhandled exceptions:

To test locally, replace `app.UseDeveloperExceptionPage();`

with `app.UseExceptionHandler("/error");`

. Otherwise, you'll get the default .NET error page during development.

To trigger a 500 error on your site, try introducing a rendering error:

For example, if a Document Type has a property called `test`

, it is normally rendered as:

To trigger a 500 error, modify it to:

This will generate a server-side error, allowing you to verify that your custom 500 page is displayed correctly.

When Umbraco fails to start, you may see a blank screen or receive a `500.30`

or `502.5`

error. These indicate the web application crashed or failed to initialize.

During startup, Umbraco relies on the ASP.NET Core pipeline. If the app crashes before this pipeline is fully initialized, it can't handle requests or serve custom error pages. That's why you can't rely on Umbraco or ASP.NET Core routing to show error content at this point as it has already failed. For more information, see the documentation.

Instead, the web server itself (IIS, NGINX, Apache, and so on) must serve a static fallback 500 page. This page is independent of the application and helps communicate the issue to users when the site is down.

To handle these types of issues:

Configure your web server (IIS, NGINX, Apache) to serve a static HTML 500 page when the app fails to respond.

Use uptime monitoring to catch failed starts.

Check Umbraco logs in

`App_Data/Logs`

for startup errors.

Sometimes you might experience issues with booting up your Umbraco project. This could be a brand new project, or it could be an existing project after an upgrade.

You will be presented with a generic error page when there is an error during boot.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4e9192e816be7dc8ceffce35e8e10fe615aeb2cf%252FBootFailedGeneric.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=18dd69d5&sv=2)

You can replace the default BootFailed page with a custom static `BootFailed.html`

. Follow the steps below to set it up:

Open your project files.

Navigate to

`wwwroot/config/errors`

If this folder does not exist already, create it.


Add a new file called

*BootFailed.html*.Add your custom markup to the file.


The `BootFailed.html`

page will only be shown if debugging is disabled in the `appsettings.json`

file. Debugging is handled using the **Debug** key under `Umbraco:CMS:Hosting`:


The full error can always be found in the log file.

If you set up everything correctly and the error pages are not showing correctly, make sure that you are not using

Custom

[ContentFinders](/umbraco-cms/reference/routing/request-pipeline/icontentfinder)in your solution,Any packages that allow you to customize redirects, or

Rewrite rules that might interfere with custom error handling.


If your code or any packages configure a custom `IContentLastChanceFinder`

, the settings in `appSettings.json`

will not be used.

For common approaches to handling errors in ASP.NET Core web apps, see the article in the Microsoft Documentation.

Last updated

Was this helpful?