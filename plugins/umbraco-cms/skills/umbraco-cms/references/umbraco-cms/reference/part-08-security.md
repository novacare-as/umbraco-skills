# Security

## Security

### Contents

- [API rate limiting | CMS](#api-rate-limiting-cms)
- [BackOfficeUserManager and Events | CMS](#backofficeusermanager-and-events-cms)
- [Basic Authentication | CMS](#basic-authentication-cms)
- [Cookies | CMS](#cookies-cms)
- [Replacing the basic username/password check | CMS](#replacing-the-basic-usernamepassword-check-cms)
- [External login providers | CMS](#external-login-providers-cms)
- [Lightweight external members | CMS](#lightweight-external-members-cms)
- [Locking of Users and password reset | CMS](#locking-of-users-and-password-reset-cms)
- [Reset admin password | CMS](#reset-admin-password-cms)
- [Umbraco Security Hardening | CMS](#umbraco-security-hardening-cms)
- [Umbraco Security Settings | CMS](#umbraco-security-settings-cms)
- [Sensitive data | CMS](#sensitive-data-cms)
- [Server-side file validation | CMS](#server-side-file-validation-cms)
- [Sanitizing the Rich Text Editor | CMS](#sanitizing-the-rich-text-editor-cms)
- [Setup Umbraco for a FIPS Compliant Server | CMS](#setup-umbraco-for-a-fips-compliant-server-cms)
- [HTTPS | CMS](#https-cms)
- [Two-factor Authentication | CMS](#two-factor-authentication-cms)

---

### API rate limiting | CMS

How to take advantage of the built-in rate limiting middleware of ASP.NET Core in Umbraco.

Since ASP.NET Core 7, you can use the to rate limit your APIs. You can apply the `EnableRateLimiting`

and `DisableRateLimiting`

attributes to add rate limiting on a controller or endpoint level. In this article, we will go through how you can configure and utilize different rate limiting strategies for Umbraco APIs.

Rate limiting helps control the number of requests to an API, typically within a specified time frame or based on other parameters. This ensures the stability, availability, and security of your APIs. The key benefits are:

Preventing server or application overload

Improving security and protecting against DDoS attacks

Reducing unnecessary resource usage, thereby cutting down on costs


You can configure rate limiting in Umbraco by composition. To use the middleware, you need to register the rate limiting services first:

```
public class ApiRateLimiterComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.Services.AddRateLimiter(rateLimiterOptions =>
        {
            // Default is 503 (Service Unavailable)
            rateLimiterOptions.RejectionStatusCode = StatusCodes.Status429TooManyRequests;

            // Write your code to configure the middleware here (rate limiting policies)
        });
    }
}
```

After that, you have to apply the `RateLimitingMiddleware`

by creating an Umbraco pipeline filter. `UseRateLimiter()`

must be called after `UseRouting()`

, therefore we use the `PostRouting`

to make sure this happens in the correct order:

With the set-up in place, let's take a look at some limiter options.

Inside `AddRateLimiter()`

we can use the `GlobalLimiter`

option to set a global rate limiter for all requests:

In the above example, we have added a `FixedWindowLimiter`

and configured it to automatically replenish permitted requests and permit 2 requests per 10 seconds. There are different algorithms and techniques for implementing rate limiting, which can vary depending on your use case. For more information, check the currently supported .

If you want to be more granular, you can configure different rate limits for different endpoints in `AddRateLimiter()`

as well:

In the code snippet above, we have configured 2 fixed window limiters with different settings, and different policy names (`"fixed1"`

and `"fixed2"`

). We can apply these policies to specific endpoints within Umbraco using the same `UmbracoPipelineFilter`:


This part of the code shows how to apply the `fixed1`

policy to the `AuthenticationController.PostRequestPasswordReset`

endpoint, responsible for handling password reset requests. We can do that by dynamically modifying the endpoint's metadata - attaching the `EnableRateLimitingAttribute`

with the name of the policy which needs to be applied. This enables us to enforce the defined rate limits on a particular endpoint.

For your reference, here is the complete `ApiRateLimiterComposer.cs`

implementation.

When Umbraco runs behind a WAF or reverse proxy, rate-limiting may fail if the client IP address is not forwarded correctly. Configure your proxy or WAF to send the original client IP using headers like X-Forwarded-For. This will prevent all requests appearing to come from one IP address which would cause incorrect rate-limit enforcement.

Last updated

Was this helpful?

---

### BackOfficeUserManager and Events | CMS

The BackOfficeUserManager is the ASP.NET Core Identity UserManager implementation in Umbraco. It exposes APIs for working with Umbraco User's via the ASP.NET Core Identity, including password handling

Extending

Example

```
builder.CreateUmbracoBuilder()
    .AddBackOffice()
    .AddWebsite()
    .AddDeliveryApi()
    .AddComposers()
    .SetBackOfficeUserManager<CustomBackOfficeUserManager>()
    .Build();
```

```
 public class CustomBackOfficeUserManager : BackOfficeUserManager
{
    public CustomBackOfficeUserManager(
        IIpResolver ipResolver,
        IUserStore<BackOfficeIdentityUser> store,
        IOptions<BackOfficeIdentityOptions> optionsAccessor,
        IPasswordHasher<BackOfficeIdentityUser> passwordHasher,
        IEnumerable<IUserValidator<BackOfficeIdentityUser>> userValidators,
        IEnumerable<IPasswordValidator<BackOfficeIdentityUser>> passwordValidators,
        BackOfficeErrorDescriber errors,
        IServiceProvider services,
        IHttpContextAccessor httpContextAccessor,
        ILogger<CustomBackOfficeUserManager> logger,
        IOptions<UserPasswordConfigurationSettings> passwordConfiguration,
        IEventAggregator eventAggregator,
        IBackOfficeUserPasswordChecker backOfficeUserPasswordChecker)
        : base(
            ipResolver,
            store,
            optionsAccessor,
            passwordHasher,
            userValidators,
            passwordValidators,
            errors,
            services,
            httpContextAccessor,
            logger,
            passwordConfiguration,
            eventAggregator,
            backOfficeUserPasswordChecker)
    {
    }

    //Override whatever you need, e.g. SupportsUserTwoFactor.
    public override bool SupportsUserTwoFactor => false;
}
```

Notifications

Example: Signing out of Auth0 after backoffice logout

Last updated

Was this helpful?

---

### Basic Authentication | CMS

Protect the front-end of your Umbraco website with basic authentication using backoffice user credentials.

Basic authentication protects the front-end of your Umbraco website using backoffice user credentials. When enabled, visitors must authenticate before accessing any page.

The feature supports username and password login, two-factor authentication, and external login providers (Google, Microsoft, and others). Authentication uses a standalone server-rendered login page that works independently of the backoffice.

Enable basic authentication in `appsettings.json`:


```
"Umbraco": {
  "CMS": {
    "BasicAuth": {
      "Enabled": true,
      "RedirectToLoginPage": true
    }
  }
}
```

With `RedirectToLoginPage`

set to `true`

, visitors are redirected to a login page at `/umbraco/basic-auth/login`

. With it set to `false`

, the browser shows its native authentication pop-up.

Set `RedirectToLoginPage`

to `true`

when using external login providers or two-factor authentication. The browser's native pop-up cannot complete these flows.

For the full list of configuration options, see the [Basic Authentication Settings](/umbraco-cms/reference/configuration/basicauthsettings) article.

When `RedirectToLoginPage`

is set to `true`

, the login flow works as follows:

A visitor requests a protected page.

The middleware redirects to

`/umbraco/basic-auth/login?returnPath=...`

.The visitor enters their backoffice credentials.

If two-factor authentication is required, the visitor is redirected to

`/umbraco/basic-auth/2fa`

.On successful authentication, the visitor is redirected back to the original page.


External login providers appear as buttons on the login page when configured. See the [External login providers](/umbraco-cms/reference/security/external-login-providers) article for setup instructions.

When two-factor authentication is required for a user, the login flow redirects to the 2FA page automatically. This happens even when `RedirectToLoginPage`

is set to `false`

, because the browser's native pop-up cannot complete a 2FA flow.

Basic authentication works in frontend-only deployments where the backoffice is not available. To enable this, register `AddBackOfficeSignIn()`

in your `Program.cs`:


`AddBackOfficeSignIn()`

registers backoffice identity and cookie authentication without the full backoffice. This enables the standalone login page with support for two-factor authentication and external login providers.

For details on the available configurations, see the [Service Registration](/umbraco-cms/reference/service-registration) article.

When using the full backoffice setup with `AddBackOffice()`

, backoffice sign-in is included automatically. You do not need to add `AddBackOfficeSignIn()`

separately.

The built-in login and 2FA pages use minimal styling and work without customization. To match your site's design, you can provide custom Razor views.

Set the view paths in `appsettings.json`:


The login view receives a `BasicAuthLoginModel`

with the following properties:

`ReturnPath`

— the URL to redirect to after login.`ErrorMessage`

— an error message to display (null when no error).`ExternalLoginProviders`

— a list of configured external login providers to render as buttons.

The 2FA view receives a `BasicAuthTwoFactorModel`

with the following properties:

`ReturnPath`

— the URL to redirect to after verification.`ErrorMessage`

— an error message to display (null when no error).`TwoFactorProviders`

— a list of available 2FA providers.

Use the built-in views at `/umbraco/BasicAuthLogin/Login.cshtml`

and `/umbraco/BasicAuthLogin/TwoFactor.cshtml`

as a reference when creating custom views.

Last updated

Was this helpful?

---

### Cookies | CMS

Learn about the cookies required for accessing the Umbraco Backoffice and their purposes.

Necessary Cookies

| Name | Purpose | Expiration |
|---|---|---|
| UMB_PREVIEW | Allows a previewed page to act as a published page only on the browser which has initialized previewing. | Session |
| UMB-WEBSITE-PREVIEW-ACCEPT | Client-side cookie that determines whether the user has accepted to be in Preview Mode when visiting the website. | Session |
| umb_installId | Used to store the Umbraco software installer id. | Session |
| UMB_UPDCHK | Enables your system to check for the Umbraco software updates. | Session |
| UMB-XSRF-V | Used to store the backoffice antiforgery token validation value. | Session |
| TwoFactorRememberBrowser | Default authentication type used for storing that 2FA is not needed on next login | Session |
| UMB_SESSION | Preserves the visitor's session state across page requests. | Session |

```
builder.Services.AddSession(options =>
    {
        options.Cookie.Name = "UMB_SESSION";
        options.Cookie.HttpOnly = true;
        options.Cookie.SecurePolicy = CookieSecurePolicy.Always;
    });
```

[Previous BackOfficeUserManager and Events chevron-left](/umbraco-cms/reference/security/backofficeusermanager-and-notifications)

[Next Replacing the basic username/password check chevron-right](/umbraco-cms/reference/security/custom-password-check)

Last updated

Was this helpful?

---

### Replacing the basic username/password check | CMS

You can specify your own logic to validate a username and password against a custom data store. Learn more about it in this section.

```
using System.Threading.Tasks;
using Umbraco.Core.Models.Identity;
using Umbraco.Core.Security;

namespace MyNamespace;

public class MyPasswordChecker : IBackOfficeUserPasswordChecker
{
    public Task<BackOfficeUserPasswordCheckerResult> CheckPasswordAsync(BackOfficeIdentityUser user, string password)
    {
        var result = (password == "test")
            ? Task.FromResult(BackOfficeUserPasswordCheckerResult.ValidCredentials)
            : Task.FromResult(BackOfficeUserPasswordCheckerResult.InvalidCredentials);

        return result;
    }
}
```

```
builder.CreateUmbracoBuilder()
.AddBackOffice()
.AddWebsite()
.AddDeliveryApi()
.AddComposers()
.Build();

builder.Services.AddUnique<IBackOfficeUserPasswordChecker, MyPasswordChecker>();
```


Last updated

Was this helpful?

---

### External login providers | CMS

Umbraco supports external login providers (OAuth) for performing authentication of your users and members.

Both the Umbraco backoffice users and website members support external login providers (OAuth) for performing authentication. This could be any OpenIDConnect provider such as Entra ID/Azure Active Directory, Identity Server, Google, or Facebook.

Unlike previous major releases of Umbraco the use of the Identity Extensions package is no longer required.

Install an appropriate Nuget package for the provider you wish to use. Some popular ones found in Nuget include:

In some cases, when using Azure AD for login, you may encounter the following error: `OpenIdConnectProtocol requires the jwt token to have an 'iss' claim`

. Install a newer version of `Microsoft.IdentityModel.Protocols.OpenIdConnect`

to solve this problem.

External login providers will invoke a callback to the website on a known path. For example, Open ID Connect will use the path `/signin-oidc`

, whilst Google uses `/signin-google`

. You should add this path to the [configured reserved paths](/umbraco-cms/reference/configuration/globalsettings#reserved-paths).

For example, with Open ID Connect, you should configure:

```
  "Umbraco": {
    "CMS": {
      "Global": {
        "ReservedPaths": "~/app_plugins/,~/install/,~/mini-profiler-resources/,~/umbraco/,~/signin-oidc/,",
```

This avoids Umbraco treating this call back as a potential request for content, improving performance of the authentication operation.

When you are configuring an external login for **backoffice users** with basic authentication, you need to enable `RedirectToLoginPage`

in the [Basic Authentication Settings](/umbraco-cms/reference/configuration/basicauthsettings#redirecttologinpage).

This redirects users to a standalone server-rendered login page where external provider buttons are displayed. Without this setting, the browser shows a native authentication popup that does not support external login providers.

External login providers also work in frontend-only deployments where the backoffice is not available. Register `AddBackOfficeSignIn()`

in your `Program.cs`

to enable this. See the [Basic Authentication](/umbraco-cms/reference/security/basic-authentication) article for details.

[Add Microsoft Entra ID authentication (Members) chevron-right](/umbraco-cms/tutorials/add-microsoft-entra-id-authentication)

[Add Google Authentication (Users) chevron-right](/umbraco-cms/tutorials/add-google-authentication)

#### Umbraco OpenIdConnect Example [Community-made]

This community-created package with a complete Umbraco solution incl. an SQLite database demonstrates how OpenID Connect can be used: .

It is great for testing and for trying out the implementation before building it into your project.

**This project is not managed or maintained by Umbraco HQ.**

#### Umbraco Entra ID (Azure AD) Example [Community-made]

This community-created package will allow you to automatically create Umbraco user accounts for users in your directory. This will then associate the Umbraco users with groups based on their AD group: .

**This project is not managed or maintained by Umbraco HQ.**

When you are implementing your own custom authentication on Users and/or Members on your Umbraco CMS website, you are effectively extending existing features.

The process requires adding a couple of new classes (`.cs`

files) to your Umbraco project:

**Custom-named configuration**to add additional configuration for handling different options related to the authentication.[See a generic example of the configuration class to learn more.](/umbraco-cms/reference/security/external-login-providers#custom-named-configuration)A

**composer and named**to extend on the default authentication implementation in Umbraco CMS for either Users or Members.[See a generic example to learn more.](/umbraco-cms/reference/security/external-login-providers#generic-backoffice-login-provider-composer)

You can setup similar behavior using a [static extension class](/umbraco-cms/reference/security/external-login-providers#static-extension-class) and add them straight into the `Program.cs`

file. But you will lose access to dependency injection this way, thus our helper class.

It is also possible to register the configuration class directly into the extension class. See examples of how this is done in the [generic examples for the static extension class](/umbraco-cms/reference/security/external-login-providers#static-extension-class).

Traditionally, a backoffice User or frontend Member will need to exist in Umbraco first. Once they exist there, they can link their user account to an external login provider.

In many cases, however, the external login provider you install will be the source of truth for all of your users and members.

In this case, you will want to provide a Single Sign On (SSO) approach to logging in. This would enable the creation of user accounts on the external login provider and then automatically give them access to Umbraco. This is called **auto-linking**.

When auto-linking is configured, then any auto-linked user or member will have an empty password assigned. This means that they will not be able to log in locally (via username and password). In order to log in locally, they will have to assign a password to their account in the backoffice or the edit profile page.

For users specifically, if the `DenyLocalLogin`

option is enabled, all password-changing functionality in the backoffice is disabled, and local login is not possible.

In some cases, you may want to flow a Claim returned in your external login provider to the Umbraco backoffice identity's Claims. This could be the authentication cookie. Flowing Claims between the two can be done during the `OnAutoLinking`

and `OnExternalLogin`.


The reason for wanted to flow a Claim could be to store the external login provider user ID into the backoffice identity cookie. It can then be retrieved on each request to look up data in another system needing the current user ID from the external login provider.

Do not flow large amounts of data into the backoffice identity. This information is stored in the backoffice authentication cookie and cookie limits will apply. Data like Json Web Tokens (JWT) needs to be [persisted](/umbraco-cms/reference/security/external-login-providers#storing-external-login-provider-data) somewhere to be looked up and not stored within the backoffice identity itself.

This is a simplistic example of brevity including no null checks, etc.

In some cases, you may need to persist data from your external login provider like Access Tokens, etc.

You can persist this data to the affiliated user's external login data via the `IExternalLoginWithKeyService`

. The `void Save(Guid userOrMemberKey,IEnumerable<IExternalLoginToken> tokens)`

overload takes a new model of type `IEnumerable<IExternalLogin>`.


`IExternalLogin`

contains a property called `UserData`

. This is a blob text column which can store any arbitrary data for the external login provider.

Be aware that the local Umbraco user must already exist and be linked to the external login provider before data can be stored here. In cases where auto-linking occurs and the user isn't yet created, you need to store the data in memory first during auto-linking. Then you can persist the data to the service once the user is linked and created.

For some providers, it does not make sense to use auto-linking. This is especially true for public providers such as Google or Facebook.

In those cases, it would mean that anyone who has a Google or Facebook account can log into your site.

If auto-linking for public providers such as these was needed you would need to limit the access. This can be done by domain or other information provided in the claims using the options/callbacks specified in those provider's authentication options.

When auto-linking for the backoffice you will want to define what user groups the user will be part of. This is done via the `defaultUserGroups`

parameter provided to the constructor of `ExternalSignInAutoLinkOptions`

(see example below). You will need to explicitly assign these. If the value is not set the user will be part of no groups.

Umbraco Cloud uses Umbraco ID for all authentication, including access to the Umbraco Backoffice.

Umbraco ID automatically removes the native Umbraco login from the backoffice. When only one login provider is registered, Umbraco redirects to the Umbraco ID login screen.

Adding your own login provider to a Cloud project stops the automatic redirect. Available login providers are shown instead.

Umbraco Cloud also offers an external login provider feature, where you only have to bring your own configuration. For more information, see .

Auto-linking on Member authentication only makes sense if you have a public member registration already or the provider does not have public account creation.

The following section presents a series of generic examples.

"*Provider*" is a placeholder used to replace the names of actual external login providers. When you implement your own custom authentication, you will need to use the correct method names for the chosen provider. Otherwise, the examples will not work as intended.

The configuration file is used to configure a handful of different options for the authentication setup. A generic example of such file is shown below.

Next, you need to register the button in the BackOffice. This is done by adding a manifest file to the `App_Plugins/ExternalLoginProviders`

folder.

You have a few options to configure the button:

`element`

- Define your own custom element for the button. This is useful if you want to display something other than a button, For example: a link or an image. For more information, see the[Customizing the BackOffice Login Button](/umbraco-cms/reference/security/external-login-providers#customizing-the-backoffice-login-button)section.`forProviderName`

- The name of the provider you are configuring. This should match the`SchemeName`

in the`GenericBackOfficeExternalLoginProviderOptions`

class with "Umbraco." prepended.`meta.label`

- The label to display on the button. The user will see this text. For example: "Sign in with Generic".`meta.defaultView.icon`

- The icon to display on the button. You can use any of the icons from the Umbraco Icon Picker. If you want to use a custom icon, you need to first register it to the.`icons`

extension point`meta.defaultView.color`

- (Default: "default") The color style of the button. You can use any color style from the .Default (blue)

Positive (green)

Warning (yellow)

Danger (red)


`meta.defaultView.look`

- (Default: "secondary") The look of the button. You can use any of the looks from the .Primary (solid background color, white text)

Secondary (grey background, colored text)

Outline (white background with sold grey border, colored text)

Placeholder (white with dotted grey border, colored text)


`meta.behavior.autoRedirect`

- Automatically redirects the user to the external login provider, skipping the Umbraco login page, unless the user has specifically logged out or timed out.`meta.behavior.popupTarget`

- (Default: "umbracoAuthPopup") The target for the popup window. This is the name of the window that will be opened when the user clicks the button. If you want to open the login page in a new tab, you can set this to "_blank".`meta.behavior.popupFeatures`

- (Default: "width=600,height=600,menubar=no,location=no,resizable=yes,scrollbars=yes,status=no,toolbar=no") The features of the popup window. This is a string of comma-separated key-value pairs. For example: "width=600,height=600". You can read more on the .`meta.linking.allowManualLinking`

- Allows the user to link or unlink their account from the BackOffice. You need to allow manual linking on the`ExternalSignInAutoLinkOptions`

as well.

The button will now be displayed on the login page in the Umbraco Backoffice.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6d030c6f9963ea98bf8303ba1f887f32867274a5%252Flogin-external.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ebec936&sv=2)

A composer and `genericAuthenticationOptions`

configuration class to setup the authentication options for the generic authentication provider using dependency injection. Replace `genericAuthenticationOptions`

with the Options method from the provider you are using.

The extension class is required to extend on the default authentication implementation in Umbraco CMS. A generic example of such extension class can be seen below.

For a more in-depth article on how to set up OAuth providers in .NET refer to the .

If you want to customize the login button, you can do so by adding a custom element to the manifest file. This is useful if you want to display something other than a button. For example, a link or an image.

The path to the custom view is a virtual path, like this example: `"~/App_Plugins/MyPlugin/BackOffice/my-external-login.js"`.


When a custom view is specified, it is 100% up to this module to perform all the required logic.

The module should define a Custom Element and export it as default. Optionally, the Custom Element can declare a number of properties to be passed to it. These properties are:

`manifest`

: The manifest object for the provider that you registered in the`umbraco-package.json`

file.`onSubmit`

: A function that is called when the form is submitted. This function will handle the form submission and redirect the user to the external login provider.`userLoginState`

: The current view state of the user. This can be one of the following values:`loggingIn`

: The user is on the login screen.`loggedOut`

: The user clicked the logout button and is on the logged-out screen.`timedOut`

: The user's session has timed out and they are on the timed-out screen.


**TypeScript**

If you use TypeScript, you can use this interface to define the properties:

The Custom Element can be implemented in a number of ways with many different libraries or frameworks. The following examples show how to make a button appear and redirect to the external login provider. You will learn how to use the `externalLoginUrl`

property to redirect to the external login provider. The login form should look like this when you open Umbraco:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-696bcbe5e631226f6f12a81107e77145429318db%252Fexternal-login-provider-javascript.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=147557f2&sv=2)

When you click the button, the form will submit a POST request to the `externalLoginUrl`

property. The external login provider will then redirect back to the Umbraco site with the user logged in.

You have access to the [Umbraco UI Library](/umbraco-cms/customizing/ui-library) in the custom element. You can use the UI components directly in your template.

It is possible to use a library such as to render the custom element needed for the Login screen.

The following example shows how to use Lit to render the custom element.

The custom element will render a form with a button. The button will submit the form to the `externalLoginUrl`

property.

No logic needs to be performed in the `constructor`

method because Lit will automatically update any event listeners. Styling is also handled by Lit in the `static styles`

property.

In this example, Lit version 3 is used and imported from a node module. You must set up npm and install the Lit package first. You should use a bundler such as to bundle the Lit library with your custom element.

To learn more about how to set up a project with Vite, see the [Creating your first extension](/umbraco-cms/tutorials/creating-your-first-extension) tutorial.

It is also possible to use vanilla JavaScript with Lit.

The following example imports Lit from a CDN and uses it to render the custom element needed for the Login screen:

It is necessary to define a template first and then the custom element itself. The template is a small HTML form with a button.

The custom element will then render the template and attach an event listener for clicks on the button in the `constructor`

method.

Some external login providers, such as Microsoft Entra ID, may send large query strings when the response mode is set to `query`

. By default, IIS restricts the maximum allowed query string length, which can cause the external login callback to fail with a 404 error.

This typically occurs during the authentication callback to Umbraco.

This limitation is imposed by IIS and is not specific to Umbraco. For more details on configuring request limits, see the official Microsoft documentation on the .

To resolve this, increase the allowed query string and URL length by setting `maxQueryString`

and `maxUrl`

in your `web.config`

file.

For example:

Last updated

Was this helpful?

---

### Lightweight external members | CMS

Lightweight external members let you authenticate members through an external identity provider without storing them as full content entities in Umbraco.

Background

Trade-offs

| Area | Content-based member | Lightweight external member |
|---|---|---|
| Backoffice editing | Full edit surface | Read-only view with an External badge. |
| Member Type properties | Stored as content properties | Not used — profile data is stored as JSON. |
| Password and local login | Supported | Not supported — external authentication only. |
| Two-factor authentication | Supported | Not supported — external provider feature. |
| Relation tracking | Available | Not available — no `umbracoNode` entry. |
| Public access rules | Type-based and group-based | Group-based only. |
| Management API | Full read and write | Read-only; creation via auto-link or `IExternalMemberService` . |
| Write cost per save | Multiple tables, versioning, full re-index | Single row update and deferred index entry. |

Enabling external-only members

Handling profile data

Reading profile data

In C#

In Razor templates

Handling member groups

Converting to a content member

Related articles

Last updated

Was this helpful?

---

### Locking of Users and password reset | CMS

Learn about the security features put in place to protect Umbraco users from unauthorized access and password breaches.

Password reset on login screen

Password reset of a non-existing user

Password reset of a locked user

Reset admin user password

Last updated

Was this helpful?

---

### Reset admin password | CMS

Step one: Clear the connection string status in configuration

```
{
  "ConnectionStrings": {
    "umbracoDbDSN": ""
  }
}
```

Step Two: Run the installer

Last updated

Was this helpful?

There is one default admin user in any Umbraco installation. This is the first user of the system.

Step one: Clear the connection string status in configuration

The first step is to clear the connection string to the database in the configuration. This is done to trigger the installation wizard.

That means that in your appsettings configuration files it should look like this:

```
{
  "ConnectionStrings": {
    "umbracoDbDSN": ""
  }
}
```

**Note that configuration can be read from many sources**

Remember to check this connection string is not provided through environment variables or other configuration sources.

Step Two: Run the installer

If you now open your browser and surf to the website, you will see that the installer launches. Enter your new details, and use the original connection string. You are good to go.

Make sure you protect a production websites from being highjacked as anyone will be able to reset the password during the last step. This does also work if your site is in an upgrading state.

Last updated

Was this helpful?

Was this helpful?

---

### Umbraco Security Hardening | CMS

Learn how to strengthen the security of your Umbraco installation, and reduce the risk of unauthorized access.

Lock down access to your Umbraco folder (IIS)

```
<rule name="Ignore" stopProcessing="true">
    <match url="^(?:umbraco/api|umbraco/surface)/" />
    <action type="None" />
</rule>
```

```
<rule name="Ignore" stopProcessing="true">
    <match url="^(?:umbraco/api|umbraco/surface|umbraco/webservices)/" />
    <action type="None" />
</rule>
```

```
<rule name="Allowed IPs" stopProcessing="true">
    <match url="^(?:umbraco)(?:/|$)" />
    <conditions>
        <add input="{REMOTE_ADDR}" negate="true" pattern="213.3.10.8|88.4.43.108" />
    </conditions>
    <action type="AbortRequest" />
</rule>
```

Last updated

Was this helpful?

---

### Umbraco Security Settings | CMS

Last updated

Was this helpful?

Password settings

The settings for Umbraco passwords are configurable in appsettings. There are two different configuration objects - One for Umbraco Members and one for Users.

For more information see the [Security Settings documentation](/umbraco-cms/reference/configuration/securitysettings#user-password-settings).

Password reset settings

Umbraco backend users can [reset their own password](/umbraco-cms/reference/security/password-reset), or if they try too much, have a locked out account.

To deactivate the User password reset look at the [Umbraco Settings Security](/umbraco-cms/reference/configuration/securitysettings#allow-password-reset) section.

To configure password reset verify the [Backoffice Login Password Reset](/umbraco-cms/fundamentals/backoffice/login#password-reset) section.

Other security settings

[disableAlternativeTemplates](/umbraco-cms/reference/configuration/webroutingsettings#disable-alternative-templates)If set to false this can be used to try to render pages in a way that they are not supposed to[disableFindContentByIdPath](/umbraco-cms/reference/configuration/webroutingsettings#disable-find-content-by-id-path)If set to false this can be used to do an enumeration of the nodes in your website and find hidden pages.Umbraco Forms: and DisableFormCaching


Last updated

Was this helpful?

Was this helpful?

---

### Sensitive data | CMS

Marking fields and properties on member data as sensitive will hide the data in those fields for backoffice users that are not privy to the data.

Grant or deny access to sensitive data

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b0264767ced408b5c8e7b38ca889a877d40d0382%252Fsensitive-data-hidden-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=dca87fd8&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-392cf74e23aad8fd6a2f78fab364aaa9f80bb05e%252Fsensitive-data-user-group-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4309ce9b&sv=2)

Marking data as sensitive

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8ffd02dbaf59f2445b5a23d6dfda8d534c1aa8a4%252Fupdate-member-type-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=dbb71e08&sv=2)

Last updated

Was this helpful?

---

### Server-side file validation | CMS

This section describes how you can implement File Validation

Implementing a FileStreamSecurityValidator

Example FileStreamSecurityAnalyzer

```
public class SvgXssSecurityAnalyzer : IFileStreamSecurityAnalyzer
    {
        public bool ShouldHandle(Stream fileStream)
        {
            // reduce memory footprint by partially reading the file
            var startBuffer = new byte[256];
            var endBuffer = new byte[256];
            fileStream.Read(startBuffer);
            if (endBuffer.Length > fileStream.Length)
                fileStream.Seek(0, SeekOrigin.Begin);
            else
                fileStream.Seek(fileStream.Length - endBuffer.Length, SeekOrigin.Begin);
            fileStream.Read(endBuffer);
            var startString = System.Text.Encoding.UTF8.GetString(startBuffer);
            var endString = System.Text.Encoding.UTF8.GetString(endBuffer);
            return startString.Contains("<svg")
                   && startString.Contains("xmlns=\"http://www.w3.org/2000/svg\"")
                   && endString.Contains("/svg>");
        }

        public bool IsConsideredSafe(Stream fileStream)
        {
            var streamReader = new StreamReader(fileStream); // do not use a using as this will dispose of the underlying stream
            var fileContent = streamReader.ReadToEnd();
            return !(fileContent.Contains("<script") && fileContent.Contains("/script>"));
        }
    }
```

Last updated

Was this helpful?

This section describes how you can implement File Validation

Sometimes it might be necessary to validate the contents of a file before it gets saved to disk when uploading through the backoffice.

To help with this, Umbraco supplies a `FileStreamSecurityValidator`

that runs all registered `IFileStreamSecurityAnalyzer`

implementations on the file streams it receives from it's different file upload endpoints. When any of the analyzers deem the file to be unsafe, the endpoint disregards the file and shows a relevant validation message where appropriate. This all happens in memory before the stream is written to a temporary file location.

Implementing a FileStreamSecurityValidator

The `IFileStreamSecurityAnalyzer`

needs a single method to be implemented:

`IsConsideredSafe`

: This method should return false if the analyzer finds a reason not to trust the file

Example FileStreamSecurityAnalyzer

The following class shows how one could potentially guard against Cross-site scripting(XSS) vulnerabilities in an svg file.

```
public class SvgXssSecurityAnalyzer : IFileStreamSecurityAnalyzer
    {
        public bool ShouldHandle(Stream fileStream)
        {
            // reduce memory footprint by partially reading the file
            var startBuffer = new byte[256];
            var endBuffer = new byte[256];
            fileStream.Read(startBuffer);
            if (endBuffer.Length > fileStream.Length)
                fileStream.Seek(0, SeekOrigin.Begin);
            else
                fileStream.Seek(fileStream.Length - endBuffer.Length, SeekOrigin.Begin);
            fileStream.Read(endBuffer);
            var startString = System.Text.Encoding.UTF8.GetString(startBuffer);
            var endString = System.Text.Encoding.UTF8.GetString(endBuffer);
            return startString.Contains("<svg")
                   && startString.Contains("xmlns=\"http://www.w3.org/2000/svg\"")
                   && endString.Contains("/svg>");
        }

        public bool IsConsideredSafe(Stream fileStream)
        {
            var streamReader = new StreamReader(fileStream); // do not use a using as this will dispose of the underlying stream
            var fileContent = streamReader.ReadToEnd();
            return !(fileContent.Contains("<script") && fileContent.Contains("/script>"));
        }
    }
```

You can [register it during startup or with a composer arrow-up-right](/umbraco-cms/reference/using-ioc#registering-dependencies)

This is an example of registering the class with a composer:

Then you can upload a file with the following content to the backoffice and see that it is not persisted.

Last updated

Was this helpful?

Was this helpful?

```
public class ServerSideValidationComposer : IComposer
    {
        public void Compose(IUmbracoBuilder builder)
        {
            builder.Services.AddSingleton<IFileStreamSecurityAnalyzer, SvgXssSecurityAnalyzer>();
        }
    }
```

```
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg">
   <polygon id="triangle" points="0,0 0,50 50,0" fill="#009900" stroke="#004400"/>
   <script type="text/javascript">
      alert('xss');
   </script>
</svg>
```

---

### Sanitizing the Rich Text Editor | CMS

This section describes how to sanitize the Rich Text Editor serverside

Last updated

Was this helpful?

This section describes how to sanitize the Rich Text Editor serverside

The Rich Text Editor is sanitized on the frontend by default, however, you may want to do this serverside as well. The libraries that are out there tend to have strict dependencies. That is why we will leave it up to you how you want to sanitize the HTML.

Implementing your own IHtmlSanitizer

We have added an abstraction called `IHtmlSanitizer`

, which by default does nothing. You can override it with your own implementation to handle sanitization as you see fit. This interface has a single method: `string Sanitize(string html)`

. The output of this method is what will be stored in the database when you save a Rich Text Editor.

To add your own sanitizer you must first create a class the implements the interface:

```
using Umbraco.Cms.Core.Security;

namespace MySite.HtmlSanitization;

public class MyHtmlSanitizer : IHtmlSanitizer
{
    public string Sanitize(string html)
    {
        // Sanitize the html parameter here
        return "<h1>Sanitized HTML</h1>";
    }
}
```

The `Sanitize`

method in this implementation is where you can use a library. You could also use your own sanitizer implementation, to sanitize the Rich Text Editor input.

Now that you've added your own custom `IHtmlSanitizer`

you must register it in the container to replace the existing NoOp sanitizer.

You can register it directly in the `Program.cs`

or use a composer.

Learn more about registering dependencies and when to use which method in the [Dependency Injection](/umbraco-cms/reference/using-ioc) article.

The extension method could look like the following:

The extension can then be invoked in the `CreateUmbracoBuilder()`

builder chain in the `Program.cs`

file:

Another option is to create a composer for handling the extension method:

With your custom sanitizer in place the Rich Text Editor will always contain the "Sanitized HTML" heading. This shows that everything is working as expected, and that whatever your sanitizer returns is what will be saved.

Last updated

Was this helpful?

Was this helpful?

```
using Umbraco.Cms.Core.DependencyInjection;
using Umbraco.Cms.Core.Security;
using Umbraco.Extensions;

namespace MySite.HtmlSanitization;

public static class BuilderExtensions
{
    public static IUmbracoBuilder AddHtmlSanitizer(this IUmbracoBuilder builder)
    {
        builder.Services.AddUnique<IHtmlSanitizer, MyHtmlSanitizer>();
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
    .AddHtmlSanitizer() // Call you extension method here.
    .Build();
```

```
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.DependencyInjection;
using Umbraco.Cms.Core.Security;
using Umbraco.Extensions;

namespace MySite.HtmlSanitization;

public class SanitizerComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.Services.AddUnique<IHtmlSanitizer, MyHtmlSanitizer>();
    }
}
```

---

### Setup Umbraco for a FIPS Compliant Server | CMS

What is FIPS?

How can I test my site with FIPS enabled?

What version of Umbraco is FIPS compliant?

Umbraco 9.0.0 and key dependencies are FIPS compliant

FAQ

Last updated

Was this helpful?

*This tutorial walks through configuring Umbraco and Lucene to be FIPS compliant and serve up websites on a server with FIPS enabled.*

FIPS should only be added for compliance. It is **not** a recommended approach for added security. For more information read [Why Microsoft is not recommending "FIPS Mode" anymore. arrow-up-right](https://techcommunity.microsoft.com/t5/microsoft-security-baselines/why-we-8217-re-not-recommending-8220-fips-mode-8221-anymore/ba-p/701037)

What is FIPS?

The Federal Information Processing Standard (FIPS) Publication 140-2, (), is a U.S. government computer security standard used to define approved cryptographic modules. The FIPS 140 standard also sets forth requirements for key generation and for key management.

Microsoft Windows has a "FIPS mode" of operation where it detects the cryptographic algorithms used by software running on it and will throw exceptions if it detects the use of non-FIPS compliant algorithms. Using MD5 hashing is generally the biggest culprit of issues running on FIPS enabled servers.

How can I test my site with FIPS enabled?

FIPS can be enabled through your Local Group Policy, Registry Setting, or Network Adapter setting. For more information about how to enable FIPS mode on Windows see this tutorial:

What version of Umbraco is FIPS compliant?

Umbraco 7.6.4+ has implemented checks for when FIPS mode is enabled on the server that it is installed on. When FIPS mode is detected, the cryptographic algorithms for hashing are changed to a FIPS compliant algorithm. When FIPS mode is disabled, then Umbraco uses backward compatible algorithms (MD5) so as not to affect existing installs. As of Umbraco version 7.6.4, the FIPS compliant cryptographic algorithm used is SHA1.

Umbraco 9.0.0 and key dependencies are FIPS compliant

Since Umbraco 9, the dependency to Lucene.NET is updated to version 4+. Thereby are both Umbraco and all key dependencies FIPS compliant.

FAQ

**Can I install Umbraco directly on a version of Windows with FIPS mode enabled?**

Installing to the FIPS server may not work. It's best to deploy an existing known working version to the FIPS server.

Last updated

Was this helpful?

Was this helpful?

---

### HTTPS | CMS

This article covers the recommended way of working with HTTPS and Umbraco CMS.

We highly encourage the use of HTTPS on Umbraco websites especially in production environments. By using HTTPS you greatly improve the security of your website.

There are multiple benefits of HTTPS:

Trust - when your site is delivered over HTTPS your users will see that your site is secured, they are able to view the certificate assigned to your site and know that your site is legitimate

Removing an attack vector called (or network Sniffing)

Guards against , an attacker will have a hard time obtaining an authentic Secure Sockets Layer (SSL) certificate

Google likes HTTPS, it may help your site's rankings


Another benefits of HTTPS is that you are able to use the protocol if your web server and browser support it.

Umbraco allows you to force HTTPS for all backoffice communications by using the following configuration:

In Umbraco 9, set the UseHttps key in `appSettings`

to true.

```
{
    "Umbraco": {
        "CMS": {
            "Global": {
                "UseHttps": true
            }
        }
    }
}
```

This options does multiple things when it is turned on:

Ensures that the backoffice authentication cookie is set to (so it can only be transmitted over https)

All non-https requests to any backoffice controller are redirected to https

All self delivered Umbraco requests are performed over https

All Umbraco notification emails with links generated have https links

All authorization attempts for backoffice handlers and services will be denied if the request is not over https


The .NET5+ way to handle this, is by adding this `HttpsRedirectionMiddleware`

to your pipeline in `Program.cs`

. This can be done by adding `app.UseHttpsRedirection();`

before the call to `app.UseUmbraco()`

in the `Configure`

method:

Once you enable HTTPS for your site you should redirect all requests to your site to HTTPS. This can be done with an IIS rewrite rule. The IIS rewrite module needs to be installed for this to work, most hosting providers will have that enabled by default.

In your `web.config`

find or add the `<system.webServer><rewrite><rules>`

section and put the following rule in there. This rule will redirect all requests for the site `http://mysite.com`

URL to the secure `https://mysite.com`

URL and respond with a permanent redirect status.

The rule includes an ignore for `localhost`

. If you run your local environment on a different URL than `localhost`

you can add additional ignore rules. Additionally, if you have a staging environment that doesn't run on HTTPS, you can add that to the ignore rules too.

*In HTTPS, the communication protocol is encrypted using Transport Layer Security (TLS), or, formerly, its predecessor, Secure Sockets Layer (SSL)* -

While the deprecated SSL (2.0 and 3.0) are not supported anymore by modern browsers, some of the Umbraco configuration still uses SSL. But rest assured, that is **only** the name.

Last updated

Was this helpful?

---

### Two-factor Authentication | CMS

Umbraco users and members support a two-factor authentication (2FA) abstraction for implementing a 2FA provider of your choice.

This article includes guides for implementing two-factor authentication options for both backoffice users and website members:

Two-factor authentication (2FA) for Umbraco Users and Members is activated by implementing an `ITwoFactorProvider`

interface and registering the implementation. The implementation can use third-party packages to support authentication apps like the Microsoft- or Google Authentication Apps.

If you are using , you can enable multi-factor authentication in Umbraco ID. For more information, see the article.

The following guide will take you through implementing an option for your website members to enable two-factor authentication.

A setup for members needs to be implemented on your website in order for you to follow this guide. This setup should include:

Login and logout options.

Public access restriction configured on at least 1 content item.


As an example, the guide will use the . This package works for both Google and Microsoft authenticator apps. It can be used to generate the QR code needed to activate the app for the website.

Install the

`GoogleAuthenticator`

Nuget Package on your project.Create a new file in your project:

`UmbracoAppAuthenticator.cs`

.Update the file with the following code snippet.


```
using Google.Authenticator;
using System.Runtime.Serialization;
using Umbraco.Cms.Core.Security;
using Umbraco.Cms.Core.Services;

namespace My.Website;

/// <summary>
/// Model with the required data to setup the authentication app.
/// </summary>

[DataContract]
public class QrCodeSetupData : ISetupTwoFactorModel
{
    /// <summary>
    /// The secret unique code for the user and this ITwoFactorProvider.
    /// </summary>
    public string? Secret { get; init; }

    /// <summary>
    /// The SetupCode from the GoogleAuthenticator code.
    /// </summary>
    public SetupCode? SetupCode { get; init; }
}

/// <summary>
/// App Authenticator implementation of the ITwoFactorProvider
/// </summary>
public class UmbracoAppAuthenticator : ITwoFactorProvider
{
    /// <summary>
    /// The unique name of the ITwoFactorProvider. This is saved in a constant for reusability.
    /// </summary>
    public const string Name = "UmbracoAppAuthenticator";

    private readonly IMemberService _memberService;

    /// <summary>
    /// Initializes a new instance of the <see cref="UmbracoAppAuthenticator"/> class.
    /// </summary>
    public UmbracoAppAuthenticator(IMemberService memberService)
    {
        _memberService = memberService;
    }

    /// <summary>
    /// The unique provider name of ITwoFactorProvider implementation.
    /// </summary>
    /// <remarks>
    /// This value will be saved in the database to connect the member with this  ITwoFactorProvider.
    /// </remarks>
    public string ProviderName => Name;

    /// <summary>
    /// Returns the required data to setup this specific ITwoFactorProvider implementation. In this case it will contain the url to the QR-Code and the secret.
    /// </summary>
    /// <param name="userOrMemberKey">The key of the user or member</param>
    /// <param name="secret">The secret that ensures only this user can connect to the authenticator app</param>
    /// <returns>The required data to setup the authenticator app</returns>
    public Task<ISetupTwoFactorModel> GetSetupDataAsync(Guid userOrMemberKey, string secret)
    {
        var member = _memberService.GetById(userOrMemberKey);

        var applicationName = "testingOn15";
        var twoFactorAuthenticator = new TwoFactorAuthenticator();
        SetupCode setupInfo = twoFactorAuthenticator.GenerateSetupCode(applicationName, member.Username, secret, false);
        return Task.FromResult<ISetupTwoFactorModel>(new QrCodeSetupData()
        {
            SetupCode = setupInfo,
            Secret = secret
        });
    }

    /// <summary>
    /// Validated the code and the secret of the user.
    /// </summary>
    public bool ValidateTwoFactorPIN(string secret, string code)
    {
        var twoFactorAuthenticator = new TwoFactorAuthenticator();
        return twoFactorAuthenticator.ValidateTwoFactorPIN(secret, code);
    }

    /// <summary>
    /// Validated the two factor setup
    /// </summary>
    /// <remarks>Called to confirm the setup of two factor on the user. In this case we confirm in the same way as we login by validating the PIN.</remarks>
    public bool ValidateTwoFactorSetup(string secret, string token) => ValidateTwoFactorPIN(secret, token);
}
```

Update

`namespace`

on line 7 to match your project.Customize the

`applicationName`

variable on line 64.Create a Composer and register the

`UmbracoAppAuthenticator`

implementation as shown below.

At this point, the 2FA is active, but no members have set up 2FA yet. The setup of 2FA depends on the type. In the case of App Authenticator, the **view** showing the option to edit member profiles needs to be modified.

If you already have a members-only page with the edit profile options, you can skip directly to step 8.

Add or choose a members-only page that should have the two-factor authentication setup.

The page needs to be behind the public access.

The page should

**not**be using strongly types models.

Open the view file for the selected page.

Add the following code:


Update the

`@using`

in line 4 to match the namespace of your project.[Optional] Customize the text fields and buttons to match your websites tone of voice (lines 33-39).


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-bcc5c98c1a97f2bb6a95563e2dffbc932298ec57%252F2fa-members-configuration.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8a17f5df&sv=2)

Login to the website using a test member.

Navigate to the page where the QR code was added.

Scan the QR code and add the verification code.

Logout of the website.

Login and verify that it asks for the two factor authentication.


You can also check that the **Two-factor Authentication** option is checked on the member in the Umbraco backoffice.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-af270105742f24077ec2e44482917ce199d15a3f%252F2fa-member-backoffice.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b5354bc7&sv=2)

When a 2FA login is requested for a member, the `MemberTwoFactorRequestedNotification`

is published. This notification can also be used to send the member a one-time password via e-mail or phone. Even though these 2FA types are as App Authentication, it is still a massive improvement compared to no 2FA.

The following guide will take you through implementing an option for backoffice users to enable two-factor authentication.

This guide will not cover setting up the UI for user login and edits as this is handled elsewhere in the CMS.

Two-factor authentication also works with basic authentication, including in frontend-only deployments where the backoffice is not available. When a user with 2FA enabled logs in via the basic authentication login page, they are redirected to a standalone 2FA page at `/umbraco/basic-auth/2fa`

. For frontend-only setups, register `AddBackOfficeSignIn()`

in your `Program.cs`

. See the [Basic Authentication](/umbraco-cms/reference/security/basic-authentication) article for details.

As an example, the guide will use the . This package works for both Google and Microsoft authenticator apps. It can be used to generate the QR code needed to activate the app for the website.

Install the

`GoogleAuthenticator`

Nuget Package on your project.Create a new file in your project:

`UmbracoUserAppAuthenticator.cs`

.Update the file with the following code snippet.


Update

`namespace`

on line 7 to match your project.Customize the

`applicationName`

variable on line 59.Create a new file in your project:

`UmbracoUserAppAuthenticatorComposer.cs`

.Implement a new composer and register the

`UmbracoUserAppAuthenticator`

implementation as shown below.

Update the

`namespace`

on line 4 to match your project.

With the 2FA in place, the provider needs to be registered in the backoffice client so the user can use it.

Add a new file to your project directory:

`~/App_Plugins/TwoFactorProviders/umbraco-package.json`

.Add the following code to the new file:


At this point, the 2FA is active, but no users have set up 2FA yet.

Each user can now enable the configured 2FA providers on their user.

Access the Umbraco backoffice.

Click the user avatar in the top-right corner.


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-01db58ce5fa63c88a9e55988c02ca1cdbc58d6a4%252Fuser-panel.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d68064cd&sv=2)

Select

`Configure Two-Factor`

button to get a list of all enabled two-factor providers.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d488ece44513af88096087d50b9a3f1c61f1d7c2%252Fconfigure-2fa.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=45c97814&sv=2)

Select

`Enable`

to show the configured view.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8b7a18236b99a521598e2819426d13bc238f64ec%252Fenable-2fa.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a8b49e20&sv=2)

Follow the instructions to configure 2FA.


When the authenticator is enabled correctly, a disable button is shown instead.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5a35c04db384bed1b23ba747793765c4991e8a7b%252Fdisable-2fa.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=15605601&sv=2)

To disable the two-factor authentication on your user, it is required to enter the verification code.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a33c3229877fa3452735e387861a6aa9bb50fbf0%252Fverify-disable.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b50c9044&sv=2)

If the code is correct, the provider is disabled.

When a 2FA login is requested for a user, the `UserTwoFactorRequestedNotification`

is published. This notification can also be used to send the user a one-time password via e-mail or phone. Even though these 2FA types are as App Authentication, it is still a massive improvement compared to no 2FA.

When a user with 2FA enabled logs in, they will be presented with a screen to enter the verification code:

While the 2FA is enabled, the user will be presented with this screen after entering the username and password.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-34bad2a407a96521b50b07ab06386c41fd6fe363%252F2fa-login-default-view.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=66ab22eb&sv=2)

If the code is correct, the user will be logged in. If the code is incorrect, the user will be presented with an error message.

This screen is set up to work well with 2FA providers that require a one-time code to be entered. The code field follows best practices for accessibility in terms of labeling and autocompletion.

A user can have more than one 2FA provider activated simultaneously. In this case, the user will be presented with a dropdown to choose which provider to use before entering a code.

The 2FA experience can be customized in Umbraco. This can be done by creating a custom view for the activation screen and the login screen. This is useful if you have a 2FA provider that requires something else than a one-time code to be entered.

The following examples show how to customize the 2FA activation screen and the 2FA login screen.

The examples are using the library to create custom elements. This is the recommended way of creating custom elements in Umbraco. Lit is a light-weight library that augments the to provide a declarative, performant, and interoperable way to create web components.

The examples are using the `@umbraco-cms/backoffice`

package to get access to the Umbraco backoffice components and services. This package is included in Umbraco and can be used to create custom elements that look and feel like the rest of the Umbraco backoffice.

They are written in vanilla JavaScript and C#, but the same principles can be applied to other languages. For more information about creating custom elements in Umbraco with a bundler and TypeScript, see the [Development Flow](/umbraco-cms/customizing/development-flow) article.

The 2FA activation screen can be customized. This should be done if you have a 2FA provider that does not require a one-time code to be entered.

To customize the 2FA activation screen, you need to create a JavaScript module. The module should export a default custom element to be used in the activation screen. This module should be placed in the `App_Plugins/TwoFactorProviders`

folder.

This module will show a QR code and an input field for the user to enter the code from the authenticator app. When the user submits the form, the code will be sent to the server to validate. If the code is correct, the provider will be enabled.

To replace the default activation screen with the custom view, you need to register the element in the `umbraco-package.json`

file that you created before. The final form of the file should look like this:

The 2FA login screen can also be customized. This should be done if you have a 2FA provider that requires something else than a one-time code to be entered.

You should only customize the 2FA login screen in certain cases, for example:

If you have a provider that requires a non-numeric field or additional info.

If you have a provider that requires the user to scan a QR code, you should additionally show the QR code.

If you need to authenticate the user in a different way than the default option.


You need to create a JavaScript module that exports a default custom element to be used in the login screen. This module should be placed in the `App_Plugins`

folder. The module should be registered using a composer.

You can use the following code as a starting point. This will give you a view looking like this, where the user can enter a code and click a button to verify the code. This is similar to the built-in view in Umbraco. In a real world scenario, you would probably want to authenticate the user in a different way.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-32e6e6ae8076fe2c7863c0b87d6b13fc82d88e7f%252F2fa-login-custom-view.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=96f173cd&sv=2)

The following code is an example of a custom 2FA login screen using . This is the recommended way of creating a custom 2FA login screen. Lit is a light-weight library that augments the to provide a declarative, performant, and interoperable way to create web components.

The element registers two properties: providers and returnPath. These properties are used to render the view. The providers property is an array of strings, where each string is the name of a 2FA provider. The returnPath is the path to redirect to after a successful login. Both supplied by the login screen automatically.

We need to register the custom view using a composer. This can be done on the `IUmbracoBuilder`

in your startup or a composer. In this case, we will add a composer to your project. This composer will overwrite the `IBackOfficeTwoFactorOptions`

to use the custom view.

Last updated

Was this helpful?

---

---
