# Health Check | CMS

Health Checks are used to determine the state of your Umbraco project. Learn more about each of them in this section.

Looking for the .NET health probe endpoints used by orchestrators and load balancers? See [Health Probes](/umbraco-cms/fundamentals/setup/server-setup/health-probes).

The Settings section of the Umbraco backoffice holds a dashboard named "Health Check". It is a handy list of checks to see if your Umbraco installation is configured according to best practices. It's possible to add your custom-built health checks.

For inspiration when building your checks you can look at the checks we've , as well as our [guides](/umbraco-cms/extending/health-check/guides). Some examples will follow in this document.

Umbraco comes with the following checks by default:

Category

**Configuration****Notification Email Settings (id:****3E2F7B14-4B41-452B-9A30-E67FBC8E1206****)**- checks that the "from" email address used for email notifications has been changed from its default value

Category

**Data Integrity****Database data integrity check (id:****73DD0C1C-E0CA-4C31-9564-1DCA509788AF****)**- checks for various data integrity issues in the Umbraco database**Untrusted database constraints (id:****0B1E71E4-8D37-4F9B-A9A4-86C5B9EA5B0B****)**- on SQL Server, checks for foreign key or check constraints that are untrusted (`is_not_trusted = 1`

), which indicates pre-existing data integrity issues that must be resolved manually

Category

**Live Environment****Debug Compilation Mode (id:****61214FF3-FC57-4B31-B5CF-1D095C977D6D****)**- should be set to`debug="false"`

on your live site**Runtime Mode (id:****8E31E5C9-7A1D-4ACB-A3A8-6495F3EDB932****)**- should be set to`Production`

on your live site

Category

**Permissions****Folder & File Permissions (id:****53DBA282-4A79-4B67-B958-B29EC40FCC23****)**- checks that the folders and files set with write permissions that are either required or recommended can be accessed

Category

**Security****Application URL Configuration (id:****6708CA45-E96E-40B8-A40A-0607C1CA7F28****)**- checks if the Umbraco application URL is configured for your site.**Click-Jacking Protection (id:****ED0D7E40-971E-4BE8-AB6D-8CC5D0A6A5B0****)**- checks to see if a header or meta-tag is in place to indicate whether the site can be hosted in an IFRAME. Normally this is best set to deny permission for this to be done, to prevent what is known as attacks**Content/MIME Sniffing Protection (id:****1CF27DB3-EFC0-41D7-A1BB-EA912064E071****)**- checks that your site contains a header used to protect against Multipurpose Internet Mail Extensions (MIME) sniffing vulnerabilities**Cookie hijacking and protocol downgrade attacks Protection (HSTS) (id:****E2048C48-21C5-4BE1-A80B-8062162DF124****)**- checks if your HTTPS site contains the Strict-Transport-Security Header (HSTS). If not - adds with a default of 18 weeks**Cross-site scripting Protection (id:****F4D2B02E-28C5-4999-8463-05759FA15C3A****)**- checks for the presence of the X-XSS-Protection-header**Content Security Policy (CSP) (id:****10BEBF47-C128-4C5E-9680-5059BEAFBBDF****)**- checks that your site has a CSP header to defend against Cross-Site Scripting (XSS) and data injection attacks.**Excessive Headers (id:****92ABBAA2-0586-4089-8AE2-9A843439D577****)**- checks to ensure that various headers that can provide details about the technology used to build and host the website have been removed**HTTPS Configuration (id:****EB66BB3B-1BCD-4314-9531-9DA2C1D6D9A7****)**- to determine if the current site is running on a secure connection**UseHttps check**- when the site is running on HTTPS,`Umbraco.Cms.Core.Configuration.Models.GlobalSettings.UseHttps`

needs to be enabled to secure the backoffice. The setting can be found under`Umbraco:CMS:Global`

in the`appsettings.json`

file**Imaging Hash-based Message Authentication Code (HMAC) Secret Key**- verifies the presence of a configured imaging[HMAC secret key](/umbraco-cms/reference/configuration/imagingsettings). The setting can be found under`Umbraco:CMS:Imaging:HMACSecretKey`

in the`appsettings.json`

file

Category

**Services****SMTP Settings (id:****1B5D221B-CE99-4193-97CB-5F3261EC73DF****)**- checks that an Simple Mail Transfer Protocol (SMTP) server is configured and is accepting requests for sending emails


Each check returns a message indicating whether or not the issue in question has been found on the website installation. This could be an error that should be fixed, or a warning you should be aware of.

Some of them can also be rectified via the dashboard, by clicking the **Fix** button and in some cases providing some required information. These changes usually involve writing to configuration files that will often trigger a restart of the website.

As well as viewing the results of health checks via the Settings section dashboard, you can set up the checks to be run on a schedule and be notified of the results by email. It's also possible to disable certain checks if they aren't applicable in your environment.

For more information, see the [Reference > Configuration > Health checks](/umbraco-cms/reference/configuration/healthchecks) article.

You can build your own health checks. There are two types of health checks you can build: **configuration checks** and **general checks**.

Each health check is a class that needs to have a `HealthCheck`

attribute. This attribute has a few things you need to fill in:

GUID - a unique ID that you've generated for this specific check

Name - give it a short name so people know what the check is for

Description - describes what the check does in detail

Group - this is the category for the check if you use an existing group name (like "Configuration") the check will be added in that category, otherwise a new category will appear in the dashboard


These are small checks that take an key and confirm that the value that's expected is there. If the value is not correct, there will be a link to a guide on how to set this value correct.

A configuration check needs to inherit from

`Umbraco.Cms.Core.HealthChecks.Checks.AbstractSettingsCheck`

A configuration check needs the

`HealthCheck`

attribute as noted at the start of this document`ReadMoreLink`

is a link to an external guide that will help you to troubleshoot any problems`ValueComparisonType`

can either be`ValueComparisonType.ShouldEqual`

or`ValueComparisonType.ShouldNotEqual`

`ItemPath`

is the IConfiguration key path leading to the configuration value that you want to verify`Values`

is a list of values that are available for this configuration item - in this example it can be`RemoteOnly`

or`On`

, they're both acceptable for a live site.For checks using the

`ShouldEqual`

comparison method, make sure to set one of these values to`IsRecommended = true`

.Where

`ShouldNotEqual`

is used the fix will require the user to provide the correct setting

`CurrentValue`

is the current value from the configuration setting`CheckSuccessMessage`

and`CheckErrorMessage`

are the messages returned to the userIt is highly recommended to use the

`LocalizedTextService`

so these can be localized. You can add the text in`~/Config/Lang/en-US.user.xml`

(or whatever language you like)


This can be anything you can think of, the results and the rectify action are completely under your control.

A general check needs to inherit from

`Umbraco.Cms.Core.HealthChecks.HealthCheck`

A general check needs the

`HealthCheck`

attribute as noted at the start of this documentAll checks run when the dashboard is loaded, this means that the

`GetStatus()`

method gets executedYou can return multiple status checks from

`GetStatus()`


A status check returns a

`HealthCheckStatus`

If a

`HealthCheckStatus`

has a`HealthCheckAction`

defined then the "Fix" button will perform that action once clickedSometimes, the button to fix something should not be called "Fix", change the

`Name`

property of a`HealthCheckAction`

to provide a better name`HealthCheckAction`

has a`Description`

property so that you can provide information on what clicking the "Rectify" button will do (or provide links to documentation, for example)`HealthCheckStatus`

has a few result levels:`StatusResultType.Success`

`StatusResultType.Error`

`StatusResultType.Warning`

`StatusResultType.Info`


A

`HealthCheckAction`

needs to provide an alias for an action that can be picked up in the`ExecuteAction`

method

It is highly recommended to use the

`LocalizedTextService`

so text can be localized. You can add the text in`~/Config/Lang/en-US.user.xml`

(or whatever language you like)

An example check:

Health check notifications can be scheduled to run periodically and notify you of the results. Included with Umbraco is a notification method to deliver the results via email. In a similar manner to how it's possible to create your health checks, you can also create custom notification methods to send the message summarising the status of the health checks via other means. Again, for further details on implementing this, refer to the [existing notification methods within the core code base arrow-up-right](https://github.com/umbraco/Umbraco-CMS/tree/v10/dev/src/Umbraco.Core/HealthChecks/NotificationMethods)

Each notification method needs to implement the core interface `IHealthCheckNotificationMethod`

and, for ease of creation, can inherit from the base class `NotificationMethodBase`

, which itself implements the `IHealthCheckNotificationMethod`

interface. The class must also be decorated with an instance of the `HealthCheckNotificationMethod`

attribute. There's one method to implement - `SendAsync(HealthCheckResults results)`

- which is responsible for taking the results of the health checks and sending them via the mechanism of your choice.

The following example shows how the core method for sending notification via email is implemented:

If a custom configuration is required for a custom notification method, the following extract can be merged in the `appsettings.json`

file, which will enable the email notification method to be configured:

If you want to get the notifications by email, Simple Mail Transfer Protocol (SMTP) settings should also be configured in the same JSON file.

Last updated

Was this helpful?

## Guides

## Contents

- [Click-Jacking Protection | CMS](#click-jacking-protection-cms)
- [Content Content Security Policy (CSP) | CMS](#content-content-security-policy-csp-cms)
- [Content/MIME Sniffing Protection | CMS](#contentmime-sniffing-protection-cms)
- [Cross-site scripting Protection (X-XSS-Protection header) | CMS](#cross-site-scripting-protection-x-xss-protection-header-cms)
- [Debug Compilation Mode | CMS](#debug-compilation-mode-cms)
- [Excessive Headers | CMS](#excessive-headers-cms)
- [Fixed Application Url | CMS](#fixed-application-url-cms)
- [Folder & File Permissions | CMS](#folder-file-permissions-cms)
- [HTTPS Configuration | CMS](#https-configuration-cms)
- [Notification Email Settings | CMS](#notification-email-settings-cms)
- [SMTP | CMS](#smtp-cms)
- [Strict-Transport-Security Header | CMS](#strict-transport-security-header-cms)
- [Untrusted Database Constraints | CMS](#untrusted-database-constraints-cms)

---

## Click-Jacking Protection | CMS

Learn how to protect your Umbraco site from clickjacking attacks using X-Frame-Options and security headers.

How to fix this health check

Adding Click-Jacking Protection using NWebSec

```...
WebApplication app = builder.Build();
app.UseXfo(options => options.SameOrigin());
```

Adding Click-Jacking Protection using manual middleware

```
app.Use(async (context, next) =>
{
    context.Response.Headers.Add("X-Frame-Options", "SAMEORIGIN");
    await next();
});
```

Last updated

Was this helpful?

---

## Content Content Security Policy (CSP) | CMS

Implement a Content Security Policy (CSP) to protect your Umbraco site from XSS and data injection.

How to fix this health check

CSP nonces

Adding a CSP using custom middleware

```
using Umbraco.Cms.Core.Security;

app.Use(async (context, next) =>
{
    ICspNonceService cspNonceService = context.RequestServices
        .GetRequiredService<ICspNonceService>();
    var nonce = cspNonceService.GetNonce();

    context.Response.Headers.Append("Content-Security-Policy",
        $"default-src 'self'; " +
        $"script-src 'self' 'nonce-{nonce}'; " +
        $"style-src 'self' 'unsafe-inline'; " +
        $"img-src 'self' blob: data: https://news-dashboard.umbraco.com; " +
        $"connect-src 'self'; " +
        $"font-src 'self'; " +
        $"frame-src 'self' https://marketplace.umbraco.com");

    await next();
});

app.UseUmbraco()...
```

Adding a CSP using NWebsec

Last updated

Was this helpful?

---

## Content/MIME Sniffing Protection | CMS

Protect your Umbraco site from MIME sniffing vulnerabilities using security headers like X-Content-Type-Options.

How to fix this health check

Adding Content/MIME Sniffing Protection using NWebSec

```...
WebApplication app = builder.Build();

app.UseXContentTypeOptions();...
```

Adding Content/MIME Sniffing Protection using manual middleware

```
namespace MySite.Middleware;

public class NoSniffMiddleware : IMiddleware
{
    public async Task InvokeAsync(HttpContext context, RequestDelegate next)
    {
        context.Response.Headers.Append("X-Content-Type-Options", "nosniff");
        await next(context);
    }
}
```

[Previous Content Content Security Policy (CSP) chevron-left](/umbraco-cms/extending/health-check/guides/contentsecuritypolicy)

[Next Cross-site scripting Protection (X-XSS-Protection header) chevron-right](/umbraco-cms/extending/health-check/guides/crosssitescriptingprotection)

Last updated

Was this helpful?

---

## Cross-site scripting Protection (X-XSS-Protection header) | CMS

Last updated

Was this helpful?

This header is non-standard and should not be used. Instead, it is recommended to use a [Content Security Policy (CSP)](/umbraco-cms/extending/health-check/guides/contentsecuritypolicy) header.

For more information about the X-XSS-Protection header, and why it should not be used, see .

How to fix this health check

This health check can be fixed by ensuring no middleware adds the header.

Last updated

Was this helpful?

Was this helpful?

---

## Debug Compilation Mode | CMS

Disable debug compilation mode in Umbraco to boost performance by updating JSON configuration.

How to fix this health check

Updating the JSON configuration

```
{
  "Umbraco": {
    "CMS": {
      "Hosting": {
        "Debug": <true|false>
      }
    }
  }
}
```

```
{
  "Umbraco": {
    "CMS": {
      "Hosting": {
        "Debug": false
      }
    }
  }
}
```

Last updated

Was this helpful?

---

## Excessive Headers | CMS

How to fix this health check

Removing headers when hosted on IIS

```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <remove name="X-Powered-By" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" />
    </security>
  </system.webServer>
</configuration>
```

Removing headers when hosted on Kestrel

Last updated

Was this helpful?

*Checks to see if your site reveals information in its headers that gives away unnecessary details about the technology used to build and host it.*

How to fix this health check

This health check can be fixed by removing headers before the response is started.

Be aware these headers are often added by the server and not by the application.

Unless you publicly expose the Kestrel server (), you can't handle this directly in middleware.

Removing headers when hosted on IIS

For IIS you will need to manipulate `web.config`

(If you don't have `web.config`

already in your project you will need to add it at the root). Ensure to remove the custom `X-Powered-By`

and `Server`

header as shown in the following example.

The `removeServerHeader`

attribute is added in IIS 10.0 and does not work in versions of Windows prior to Windows Server version 1709 or Windows 10 version 1709.

```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <remove name="X-Powered-By" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" />
    </security>
  </system.webServer>
</configuration>
```

Removing headers when hosted on Kestrel

By default Kestrel will only expose the `Server`

header. To disable this, you have to configure Kestrel in `Program.cs`

. You can use the `UseKestrel`

extension method on `WebApplicationBuilder`

like in the following example.

Last updated

Was this helpful?

Was this helpful?

```
WebApplicationBuilder builder = WebApplication.CreateBuilder(args);

builder.WebHost.UseKestrel(options => options.AddServerHeader = false);...
```

---

## Fixed Application Url | CMS

How to fix this health check

Updating the JSON configuration

```
{
    "Umbraco": {
        "CMS": {
            "WebRouting": {
                "UmbracoApplicationUrl": "string"
            }
        }
    }
}
```

```
{
    "Umbraco": {
        "CMS": {
            "WebRouting": {
                "UmbracoApplicationUrl": "https://www.my-custom-domain.com/"
            }
        }
    }
}
```

Last updated

Was this helpful?

*Check to make sure a fixed application URL is specified. This URL is for example used when sending emails from backoffice.*
&#xNAN;*If this is not specified in configuration, Umbraco gets the application URL from last host used to request the application*

How to fix this health check

This health check can be fixed by providing configuration on the following path: `Umbraco:CMS:WebRouting:UmbracoApplicationUrl`.


This configuration can be setup in a configuration source of your choice. This guide shows how to set it up in one of the JSON file sources.

Updating the JSON configuration

The following JSON needs to be merged into one of your JSON sources. By default the following JSON sources are used: `appSettings.json`

and `appSettings.<environment>.json`

, e.g. `appSettings.Development.json`

or `appSettings.Production.json`.


```
{
    "Umbraco": {
        "CMS": {
            "WebRouting": {
                "UmbracoApplicationUrl": "string"
            }
        }
    }
}
```

One example that can be used in production

```
{
    "Umbraco": {
        "CMS": {
            "WebRouting": {
                "UmbracoApplicationUrl": "https://www.my-custom-domain.com/"
            }
        }
    }
}
```

If the site is hosted on Umbraco Cloud, changing the above configuration will have no effect. The site will always use the URL set in the`umbraco-cloud.json` file, which can not be changed.

Last updated

Was this helpful?

Was this helpful?

---

## Folder & File Permissions | CMS

How to fix this health check

Updating the file permissions on Windows

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6dc15b3c5af3f035fd54a94fe2d142655bb0ae93%252Ffailed_healthcheck_folder_permissions.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=461ab3d4&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-871cf4630600cf41de9d40c81c5bab7d43177c45%252Ffolder_properties.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=923fe897&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-79a3fc7122eed11009f111edb451eef42fd10dbf%252Ffolder_properties_security.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4deb0121&sv=2)

Last updated

Was this helpful?

*Checks that the web server folder and file permissions are set correctly for Umbraco to run.*

How to fix this health check

This health check can be fixed by ensuring that the process running Umbraco also has write access to the listed folders and files.

Updating the file permissions on Windows

Here's an example of how to adjust permissions for a folder. This process works the same way for files.

First we see an example of an error from the health check

To fix this, we find the specified folder, from the report and choose `Properties`

and the `Security`

tab.

From here you can edit the permissions for a specific user or user group.

For security reasons we recommend only giving write access to the required users or groups.

Last updated

Was this helpful?

Was this helpful?

---

## HTTPS Configuration | CMS

Last updated

Was this helpful?

*Checks if your site is configured to work over HTTPS and if the Umbraco related configuration for that is correct.*

How to fix this health check

This health check checks a couple of things.

First of all, it ensures that your website is running on HTTPS using a valid certificate.

Furthermore, it is used to specify the configuration on the following path: `Umbraco:CMS:Global:UseHttps`.


This configuration can be setup in a configuration source of your choice. This guide shows how to set it up in one of the JSON file sources.

Updating the JSON configuration

The following JSON needs to be merged into one of your JSON sources. By default the following JSON sources are used: `appSettings.json`

and `appSettings.<environment>.json`

, e.g. `appSettings.Development.json`

or `appSettings.Production.json`.


```
{
    "Umbraco": {
        "CMS": {
            "Global": {
                "UseHttps": <false,true>
            }
        }
    }
}
```

One example that can be used:

Last updated

Was this helpful?

Was this helpful?

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

---

## Notification Email Settings | CMS

Last updated

Was this helpful?

*If notifications are used, the 'from' email address should be specified and changed from the default value.*

How to fix this health check

This health check can be fixed by providing configuration on the following path: `Umbraco:CMS:Content:Notifications:Email`.


This configuration can be setup in a configuration source of your choice. This guide shows how to set it up in one of the JSON file sources.

Updating the JSON configuration

The following JSON needs to be merged into one of your JSON sources. By default the following JSON sources are used: `appSettings.json`

and `appSettings.<environment>.json`

, e.g. `appSettings.Development.json`

or `appSettings.Production.json`.


```
{
  "Umbraco": {
    "CMS": {
      "Content": {
        "Notifications": {
          "Email": "<email>"
        }
      }
    }
  }
}
```

One example that can be used:

Last updated

Was this helpful?

Was this helpful?

```
{
  "Umbraco": {
    "CMS": {
      "Content": {
        "Notifications": {
          "Email": "[email protected]"
        }
      }
    }
  }
}
```

---

## SMTP | CMS

Last updated

Was this helpful?

*Checks that valid settings for sending emails are in place.*

How to fix this health check

This health check can be fixed by providing configuration on the following path: `Umbraco:CMS:Global:Smtp`


This configuration can be setup in a configuration source of your choice. This guide shows how to set it up in one of the JSON file sources.

Updating the JSON configuration

The following JSON needs to be merged into one of your JSON sources. By default the following JSON sources are used: `appSettings.json`

and `appSettings.<environment>.json`

, e.g. `appSettings.Development.json`

or `appSettings.Production.json`.


```
{
    "Umbraco": {
        "CMS": {
            "Global": {
                "Smtp": {
                    "From": "<your email>",
                    "Host": "<host>",
                    "Port": <port>,
                    "PickupDirectoryLocation": "<optional directory>",
                    "Username": "<optional username>",
                    "Password": "<optional password>",
                    "DeliveryMethod": "<Network(default)|SpecifiedPickupDirectory|PickupDirectoryFromIis>",
                    "SecureSocketOptions": "<None|Auto(default)|SslOnConnect|StartTls|StartTlsWhenAvailable>"
                }
            }
        }
    }
}
```

An example that can be used on localhost, is if you have a local Simple Mail Transfer Protocol (SMTP) server running during development. This could be a tool like .

Last updated

Was this helpful?

Was this helpful?

```
{
    "Umbraco": {
        "CMS": {
            "Global": {
                "Smtp": {
                    "From": "[email protected]",
                    "Host": "localhost",
                    "Port": 25
                }
            }
        }
    }
}
```

---

## Strict-Transport-Security Header | CMS

Learn about the health checks that check for cookie hijacking and protocol downgrade attacks protection.

Last updated

Was this helpful?

Learn about the health checks that check for cookie hijacking and protocol downgrade attacks protection.

Checks if your site, when running with HTTPS, contains the Strict-Transport-Security Header (HSTS).

How to fix this health check

This health check can be fixed by adding the `Strict-Transport-Security`

header to responses. The header tells browsers that future requests should be made over HTTPS only.

Enabling HSTS on a domain will cause browsers to only use HTTPS (not HTTP) to communicate with your site. Only enable HSTS on domains that can, and should, use HTTPS exclusively.

Using the UseHsts extension method

ASP.NET Core implements HSTS with the `UseHsts`

extension method.

You can add `UseHsts`

after the `env.IsDevelopment()`

check-in `Program.cs`.


```
if (builder.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
else
{
    app.UseHsts();
}
    //...
}
```

This example only enables HSTS if the app is not running in development mode. `UseHsts`

isn't recommended in development because the HSTS settings are highly cacheable by browsers.

It is possible to configure a timespan for the HSTS, preferably six months. This can be done by adding a new builder to the `Program.cs`

file. Learn more in the .

Full details of `UseHsts`

, and additional configuration, can be found in the .

Last updated

Was this helpful?

Was this helpful?

---

## Untrusted Database Constraints | CMS

AI-generated content

# Untrusted Database Constraints

Checks that all Umbraco foreign key and check constraints on SQL Server are trusted.

What is an "untrusted" constraint?

How to fix this health check

1. Identify the untrusted constraints

```
SELECT 'Foreign key' AS ConstraintType, s.name AS SchemaName,
       OBJECT_NAME(fk.parent_object_id) AS TableName, fk.name AS ConstraintName
FROM sys.foreign_keys fk
INNER JOIN sys.schemas s ON fk.schema_id = s.schema_id
WHERE fk.is_not_trusted = 1
  AND (OBJECT_NAME(fk.parent_object_id) LIKE 'umbraco%' OR OBJECT_NAME(fk.parent_object_id) LIKE 'cms%')

UNION ALL

SELECT 'Check constraint', s.name,
       OBJECT_NAME(cc.parent_object_id), cc.name
FROM sys.check_constraints cc
INNER JOIN sys.schemas s ON cc.schema_id = s.schema_id
WHERE cc.is_not_trusted = 1
  AND (OBJECT_NAME(cc.parent_object_id) LIKE 'umbraco%' OR OBJECT_NAME(cc.parent_object_id) LIKE 'cms%');
```

2. Try to re-trust the constraint

3. Find the offending rows

4. Remove the offending rows

5. Re-trust the constraint

6. Re-run the health check

Check constraints

Last updated

Was this helpful?

---
