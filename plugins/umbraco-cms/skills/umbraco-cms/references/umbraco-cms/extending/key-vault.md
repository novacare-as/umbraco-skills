# Configuring Azure Key Vault | CMS

A guide for configuring Azure Key Vault

From a security perspective, storing your application secrets in Azure Key Vault is always a good solution. This could be a connection string or other keys.

This article tells you how to configure your application so it is ready to use a Key Vault.

Depending on your hosting situation there are a few approaches to incorporating Azure Key Vault into your application.

Before you begin, you need to install the `Azure.Extensions.AspNetCore.Configuration.Secrets`

and the `Azure.Identity`

NuGet packages. There are two approaches to installing the packages:

Use your favorite Integrated Development Environment (IDE) and open up the NuGet Package Manager to search and install the packages

Use the command line to install the package


Navigate to your project folder, which is the folder that contains your `.csproj`

file. Now use the following `dotnet add package`

command to install the packages:

```
dotnet add package Azure.Extensions.AspNetCore.Configuration.Secrets
dotnet add package Azure.Identity
```

You can find the database connection string under the `Umbraco:CMS:ConnectionStrings`

section in the `appsettings.json`

file. For more information, see the [Connection strings settings](/umbraco-cms/reference/configuration/connectionstringssettings) article.

The next step is to add the Azure Key Vault endpoint to the `appsettings.json`

file (or create as an Environment Variable). You can add this endpoint in the root or anywhere in the `appsettings.json`

as long as it is resolved in the `ConfigureAppConfiguration`

method.

After adding the endpoint in the appsettings, it's time to add configuration so that the KeyVault is used. One way to achieve this is to write an extension method for the `WebApplicationBuilder`:


After creating the extension method, it's possible to call it from the `Program.cs`

class, like so:

There are different ways to access the Azure Key Vault. It is important that the user you are logging in with has access to the Key Vault. You can assign roles using the Azure Portal.

Navigate to your Key Vault.

Select Access Control.

Select Add -> Add role assignment.

Select the preferred role.

Search for the user.

Click review + assign


Azure Web Apps offers the ability to directly reference Key Vault secrets as App Settings. The benefit of this is you can securely store your secrets in Key Vault without any code changes required in your application.

To begin we first need to create a **Managed Identity** for the Azure Web App. This enables us to grant granular permissions to an identity representing the Web App.

Head over to your Azure Web App and find **Identity** under **Settings**:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196052374-cebcfbc3-848f-4866-8e0f-70a57e776f60.png&width=768&dpr=3&quality=100&sign=cf80fd06&sv=2)

Under **System assigned** change the Status from Off to **On**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196052406-2205c1bc-504a-41be-86bf-81b1cabbc17f.png&width=768&dpr=3&quality=100&sign=6094f08e&sv=2)

A GUID will then be generated called **Object (principal) ID**. Take note of this ID as we will need it further on.

Alternatively, you can use Role-Based Access Control on your Azure Key Vault.

Learn more about the difference between the two approaches and how to migrate between them on the .

It is assumed you already have a Key Vault set up with a few Umbraco secrets inside. In your Key Vault head to **Access Policies**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196052540-e1368016-ad7a-4b69-b05c-2875a4f11998.png&width=768&dpr=3&quality=100&sign=f68a3e53&sv=2)

At the top select **+ Create**. We are now going to add the **System Managed Identity** for the Web App to Key Vault.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196052612-e3b2041c-785f-46f5-b9b5-d8ad33b893ac.png&width=768&dpr=3&quality=100&sign=8b1b16c4&sv=2)

You will now be presented with different permissions to set for your Web App. You only need **Get** and **List** for **Secret Permissions** only. Click **Next** to continue:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196052668-124d1496-4486-4098-9198-eff809876c80.png&width=768&dpr=3&quality=100&sign=95316dfa&sv=2)

Enter the GUID you took note of earlier, into the **Search Box**. You will see your Web App listed.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196052706-15431bf4-80ea-4bb7-b40e-ebda45264fb7.png&width=768&dpr=3&quality=100&sign=56cbaabc&sv=2)

Click your Web App to Select and click Next and then Create:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196052849-970a97c5-e945-415a-9469-a67f485424ea.png&width=768&dpr=3&quality=100&sign=68c99b6&sv=2)

If you visit the **Access Policies** section again you should now see your web app in the list and its permissions:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196052924-0d0559c0-a414-4bbd-ab91-94fc25dc720f.png&width=768&dpr=3&quality=100&sign=1f773ace&sv=2)

In your Azure Web App head to **Configuration** under **Settings**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196053006-3a95fc5f-1038-4228-9ae4-467050ea5759.png&width=768&dpr=3&quality=100&sign=6df0ed8d&sv=2)

Here we can add **App Settings** and **Connection Strings** to the environment.

Let us start off with the

**Umbraco Database Connection String**.

Under Connection Strings, select **Advanced Edit**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196053130-8fb6c2b9-61c7-4c02-a419-8570174c6646.png&width=768&dpr=3&quality=100&sign=ad936dc0&sv=2)

Once you click on "**Advanced Edit"** a new window will open up. There you will need to paste in the following JSON Object inside the square brackets. Ensure you update `{keyvault-name}`

, `{secret-name}`

and `{version-id}`.


You can obtain the Secret Uri by visiting the specific version of your secret and copying the Url:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196054001-cc215c04-d29c-435a-ae7b-6e8efb7f3faa.png&width=768&dpr=3&quality=100&sign=32d8ad1&sv=2)

The ID is optional but recommended as it enables you to control which version of the secret is used at your discretion. Leave it out if you always want the Web App to pull the latest version of the secret.

Wait a moment and refresh the screen. You should see a Green tick. If you do not have a Green tick you need to review your Access Policies in the previous step.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196053419-f53feba2-b8ed-4b98-99f0-ee68f58ac8e4.png&width=768&dpr=3&quality=100&sign=354c6922&sv=2)

We will perform the same approach for our

**App Settings**. We will be updating the following App Settings for Azure Blob Storage.

Due to the secrets being nested we need to use double underscore `__`

to correctly reference the value on our Web App.

On the Web App select **Advanced Edit** for Application Settings:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196053630-dd90f240-0116-4471-bf7e-73bdbcfcc28a.png&width=768&dpr=3&quality=100&sign=bb56e4ae&sv=2)

When clicking on "Advanced Edit", a new window will open up. There you will need to paste in the following JSON Objects inside the square brackets. Ensure you update `{keyvault-name}`

, `{secret-name}`

and `{version-id}`.


The ID is optional but recommended as it enables you to control which version of the secret is used at your discretion. Leave it out if you always want the Web App to pull the latest version of the secret.

Wait a moment and refresh the screen. You should see Green ticks for both values. If you do not have a Green tick you need to review your Access Policies in the previous step.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2Fuser-images.githubusercontent.com%2F11179749%2F196053743-e507f057-8fe7-4a68-9e2f-7229f1a340d7.png&width=768&dpr=3&quality=100&sign=d375b61e&sv=2)

Last updated

Was this helpful?