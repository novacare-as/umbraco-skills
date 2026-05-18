# Create a custom maintenance page | CMS

Learn how to make your site visitors aware of any ongoing maintenance on the project.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8387dbb4ea8b5dd906239de9eb5585796e03045b%252FmaintenancePage.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b76ad040&sv=2)

Customize the maintenance page

Disable the maintenance page

Last updated

Was this helpful?

Learn how to make your site visitors aware of any ongoing maintenance on the project.

A maintenance page will be shown when an Umbraco project is running an upgrade. This prevents visitors from landing on an upgrade page or seeing content meant for project maintainers.

Customize the maintenance page

The following guide will take you through the steps to customize and brand the default maintenance page.

Go to the root of your Umbraco project files.

Create a new folder called

`UmbracoWebsite`

, and open it.Add a new file called

`maintenance.cshtml`

.Add your custom markup to the file.


Keeping the Umbraco project in Upgrade mode for a longer time is not recommended. Most migrations can be executed while the website continues to work.

Disable the maintenance page

As most upgrades can be done without the website having to restart or go down, the maintenance page can be disabled.

Open the project

`appSettings.json`

file.Add the following configuration:


Last updated

Was this helpful?

Was this helpful?

appSettings.json

```
{
    "Umbraco": {
        "CMS": {
            "Global": {
                "ShowMaintenancePageWhenInUpgradeState": false
            }
        }
    }
}
```