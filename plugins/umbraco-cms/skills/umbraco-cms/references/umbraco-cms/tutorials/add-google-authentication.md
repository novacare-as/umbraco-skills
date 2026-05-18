# Add Google Authentication (Users) | CMS

A tutorial on setting up Google authentication for the Umbraco CMS backoffice users.

The Umbraco Backoffice supports external login providers (OAuth) for performing authentication of your users. This could be any OpenIDConnect provider such as Entra ID/Azure Active Directory, Identity Server, Google, or Facebook.

In this tutorial, we will take you through the steps of setting up a Google login for the Umbraco CMS backoffice.

When you log in to the Umbraco Backoffice, you need to enter your username and password. Integrating your website with Google authentication adds a button that you can click to log in with your Google account.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-3e352036d3dab906e6b5908bdc25625a2d619719%252FgoogleLoginScreen.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=cc1998e5&sv=2)

We are sure a lot of content editors and implementors of your Umbraco sites would love to have one less password to remember. Click **Sign in with Google** and if you are already logged in with your Google account, it will log you in directly.

For this tutorial, you need:

installed.

A account.

A working .


The first thing to do is set up a Google API. To do this, you need to go to and log in with your Google account.

Click the project dropdown and select

**New Project**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-00833e5cb3cca25149dba3005f3372ac3cb1cd5d%252FProject_dropdown_list_v13.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1fcfcd09&sv=2)

Project dropdown list Enter a

**Project name**,**Organization**, and**Location**.Click

**Create**.

Open the newly created project from the project dropdown.

Click

**Enable APIs and Services**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4ce36c0cf0ec8aa8c09978faca63a265db7ca552%252FEnable_Apis_v13.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=57f4eb75&sv=2)

Enable APIs Type

**Google+ API**in the**Search**field.Select it and then

**Enable**it.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d25f3f8d27a4ece1b7144a043738f06670c3eb46%252FEnable_Google_API_v13.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c6a6bb0a&sv=2)

Enable Google APIs

Before you can create the credentials, you need to configure your consent screen.

Click

**OAuth consent screen**from the left-side navigation menu.Choose the

**User Type**that fits your setup.Click

**Create**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-63b08c1fdcf76ce2781cd13db5e3906a2834c2f8%252FUser_Type_v13.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c1572195&sv=2)

Select User Type Fill in the required information:

App name

User support email

Developer contact information


Click

**Save and Continue**.Select the scopes your project needs.

Click

**Save and Continue**.Verify the details you have provided.

Click

**Back to Dashboard**to complete creating the Consent screen.

Click

**Credentials**from the left-side navigation menu.Click

**Create Credentials**.Select

**OAuth Client ID**from the dropdown.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-01a8daed547e2146caf64156b0bc9c6fafb22f9a%252FOAuth_Client_Id_v13.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=61a75123&sv=2)

Select OAuth Client ID Select

**Web Application**from the**Application type**dropdown.Enter the following details:

Application

**Name****Authorized JavaScript origins****Authorized redirect URIs**

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-68465f1443286dc327c93b48bdbf1764793b7799%252Fcredentials_v13.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1ef14a2c&sv=2)

Credentials Click

**Create**.

A popup appears displaying the **Client Id** and **Client Secret**. You will need these values later while configuring your solution.

The **Client Id** and **Client Secret** can always be accessed from the **Credentials** tab in the **APIs & Services** menu.

Once the Google API is set up it is time to install the Google Auth provider on the Umbraco project.

If you are working with a Cloud project, see the article to complete this step.

You can install and manage packages in a project.

Navigate to your project/solution folder.


If you have cloned down an Umbraco Project, you will need to navigate to the `src`

folder where you can see a `.csproj`

file.

Open a command-line of your choice such as "Command Prompt" at the mentioned location.

Run the following command to install the

`Microsoft.AspNetCore.Authentication.Google`

package.Once the package is installed, open the

**.csproj**file to ensure if the package reference is added:

You can check the before installing it.

For more information on installing and using a package with the .Net CLI, see .

To use an external login provider such as Google on your Umbraco CMS project, you have to implement a couple of new classes:

A custom-named

`BackOfficeExternalLoginProviderOptions`

configuration class.A custom-named

`GoogleOptions`

configuration class.A Composer to tie it all together.

An Umbraco backoffice manifest declaration.


You can create these files in a location of your choice. In this tutorial, the files will be added to an `ExternalUserLogin/GoogleAuthentication`

folder for the C# classes. You will also need an `\App_Plugins\my-auth-providers`

folder location for the frontend registration.

Create a new class:

`GoogleBackOfficeExternalLoginProviderOptions.cs`

.Add the following code to the file:


The code used here, enables [auto-linking](/umbraco-cms/reference/security/external-login-providers#auto-linking) with the external login provider. This enables the option for users to login to the Umbraco backoffice prior to having a backoffice User.

Set the `autoLinkExternalAccount`

to `false`

in order to disable auto-linking in your implementation.

Create a new class:

`GoogleBackOfficeAuthenticationOptions`

.Add the following code to the file:


Replace

**YOURCLIENTID**and**YOURCLIENTSECRET**with the values from the**OAuth Client Ids Credentials**window. Or use the to read the values from app settings (or other sources).Register both

`ConfigureNameOptions`

into a composer and add the provider to Umbraco

Register the provider with the backoffice client by adding the following file to the manifest file in

`/App_Plugins/my-auth-providers/umbraco-package.json`:


Build and run the website.

Log in to the backoffice using the Google Authentication option.


If auto-linking is disabled, the user will need to follow these steps in order to be able to use Google Authentication:

Login to the backoffice using Umbraco credentials.

Select your user profile in the top-right corner.

Click

**Link your Google account**under External login providers.Choose the account you wish to link.


For future backoffice logins, the user will be able to use Google Authentication.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-3e352036d3dab906e6b5908bdc25625a2d619719%252FgoogleLoginScreen.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=cc1998e5&sv=2)

[Previous Creating a Multilingual Site chevron-left](/umbraco-cms/tutorials/multilanguage-setup)

[Next Add Microsoft Entra ID authentication (Members) chevron-right](/umbraco-cms/tutorials/add-microsoft-entra-id-authentication)

Last updated

Was this helpful?