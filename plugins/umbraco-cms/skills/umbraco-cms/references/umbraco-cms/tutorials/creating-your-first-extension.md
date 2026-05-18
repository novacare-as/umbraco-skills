# Creating your First Extension | CMS

Learn how to create your first extension for Umbraco.

This guide will help you set up your first extension with a Web Component using two ways:

Before following this tutorial, make sure to read the [Setup Your Development Environment](/umbraco-cms/customizing/development-flow) article.

This article is also part of the prerequisites for [Creating a Property Editor](/umbraco-cms/tutorials/creating-a-property-editor) and [Creating a Custom Dashboard](/umbraco-cms/tutorials/creating-a-custom-dashboard) tutorials.

Extensions will go into a folder called `App_Plugins`

. If you don't have this folder, you can create it at the root of your Umbraco project.

We consider it best practice to use at least TypeScript and some kind of build tool to write your extensions. However, since Umbraco's extension system is written entirely in JavaScript, it's possible to create extensions with vanilla JavaScript. We will briefly go through what that looks like:

Go to the

`App_Plugins`

folder and create a new folder called`my-vanilla-extension`

In the newly created folder, create a file called

`umbraco-package.json`

. Then add the following code :

```
{
  "$schema": "../../umbraco-package-schema.json",
  "name": "My.Vanilla.Extension",
  "version": "0.1.0",
  "extensions": [
    {
      "type": "dashboard",
      "alias": "my.vanilla.extension",
      "name": "My Vanilla Extension",
      "js": "/App_Plugins/my-vanilla-extension/vanilla-extension.js",
      "weight": -1,
      "meta": {
        "label": "My Vanilla Extension",
        "pathname": "my-vanilla-extension"
      },
      "conditions": [
        {
          "alias": "Umb.Condition.SectionAlias",
          "match": "Umb.Section.Content"
        }
      ]
    }
  ]
}
```

This code sets up a basic package with a dashboard extension.

Adding `$schema`

to `umbraco-package.json`

will give you IntelliSense for this file to help you see different options for your package.

Next, create a new JavaScript file called

`vanilla-extension.js`

and insert the following code:

Now we have a JavaScript file with a Web Component which gets linked to a Dashboard Extension as part of the Package Manifest JSON.

Press the F5 button in your favorite IDE or run

`dotnet run`

in a command line to run the project. You will see the new dashboard in the**Content**section.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d132d1b4d23596441a4678bf6e360bba63b7a8a7%252FCreate_first_extension_Vanilla.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8782b0cf&sv=2)

Clicking the button will open a notification with the message "Hello".

You now have a working extension with a dashboard Web Component written in plain JavaScript and no build tool. However, Umbraco recommends building extensions with a setup using TypeScript and a build tool such as . Umbraco uses the library for building web components which we will be using throughout this guide.

If you want to learn more about Vite, you can read the [Vite Package Setup](/umbraco-cms/customizing/development-flow/vite-package-setup) article. It will go into more detail about the setup and how to use Vite with Umbraco. For this tutorial, we will assume you have read the article and have Vite installed.

Vite comes with a set of really good presets to get you quickly up and running with libraries and languages. Examples: Lit, Svelte, and vanilla Web Components with both JavaScript and TypeScript. We will use their preset of Lit and TypeScript.

Find a place where you want to keep your source files. If you followed the article, you will have a folder in the root of your project called `Client`

. This is where all your source files live. Vite will copy all compiled files and assets to the `App_Plugins`

folder.

Be aware that any files in the `App_Plugins`

folder are publicly available. If you want to keep your source files private, you should create a new folder outside of the `App_Plugins`

folder.

Navigate to the new

`Client`

project folder.If you have not done so already, you should install our Backoffice package from NPM. You can install the package using the following command:


This will add a package to your devDependencies containing the TypeScript definitions for the Umbraco Backoffice.

If you see any errors during this process, make sure that you have the right tools installed (Node, .NET, and so on). Also, make sure you have followed the steps on how to [Setup Your Development Environment](/umbraco-cms/customizing/development-flow).

Navigate to

`src/my-element.ts`

, open the file and replace it with the following code:

If you create multiple dashboards it's necessary to change the alias of `@customElement`

to a unique alias in the `my-element.ts`

file. If it's not changed then it will conflict with the other dashboards that use the same alias and therefore only one will show.

The code above defines a Web Component that contains a button that when clicked will open a notification with a message to the user.

Build the

`ts`

file at the root of the`Client`

folder so that we can use it in our package:

After running the build, you will see a new file in the `App_Plugins/Client`

folder with the name `client.js`

. This is the file we will use in our package.

Enter the following in the

`umbraco-package.json`

file:

Now we have a JavaScript file with a Web Component which gets linked to a Dashboard Extension as part of the Package Manifest JSON.

Press the F5 button in your favorite IDE or run

`dotnet run`

in a command line to run the project. Then you will see the new dashboard show up in the Content section.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-298fc34e257a6ff9f25c9830866b340f2b77ad54%252FCreate_first_extension_Typescript.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3dd55697&sv=2)

Clicking the button will open a notification with the message "#h5yr".

Now that you have created your first extension (which is a dashboard), you can continue to the next tutorial: [Creating a Custom Dashboard](/umbraco-cms/tutorials/creating-a-custom-dashboard).

You can also read more about the [Umbraco Package Manifest](/umbraco-cms/customizing/umbraco-package) to learn more about the different options you have when creating an extension.

Last updated

Was this helpful?