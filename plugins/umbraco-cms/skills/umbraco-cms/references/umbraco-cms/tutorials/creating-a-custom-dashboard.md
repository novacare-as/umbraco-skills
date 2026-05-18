# Creating A Custom Dashboard

## Contents

- [Adding functionality to the Dashboard | CMS](#adding-functionality-to-the-dashboard-cms)
- [Adding localization to the dashboard | CMS](#adding-localization-to-the-dashboard-cms)
- [Using Umbraco UI library in the Dashboard | CMS](#using-umbraco-ui-library-in-the-dashboard-cms)

---

## Adding functionality to the Dashboard | CMS

Use resources and get data for your dashboard.

This is the third part of our guide to building a custom dashboard. This part continues work on the dashboard we built in part two: [Add localization to the dashboard](/umbraco-cms/tutorials/creating-a-custom-dashboard/adding-localization-to-the-dashboard). But it goes further to show how to add functionality and data to our dashboard.

The steps we will go through in this part are:

Umbraco has a large selection of contexts that you can use in your custom Property Editors and Dashboards. For this example, we will welcome the editor by name. To achieve this we can make use of the Umbraco Contexts.

To get information on the current user that's currently logged in, we first need to get the context and its token. We use the Current User Context to receive the user that is currently logged in.

Import the

`UMB_CURRENT_USER_CONTEXT`

and the`type UmbCurrentUserModel`

for the logged-in user. We also need to update the import from lit decorators to get`state`

in the`welcome-dashboard.element.ts`

file:

```
import { LitElement, css, html, customElement, state } from "@umbraco-cms/backoffice/external/lit";
import { type UmbCurrentUserModel, UMB_CURRENT_USER_CONTEXT } from "@umbraco-cms/backoffice/current-user";
```

Now that we have access to the Current User Context, we can consume it in the constructor to obtain the current user. We do this using the

`consumeContext`

method, which is available on our element because we extended using`UmbElementMixin`

. As the first thing in the`export class MyWelcomeDashboardElement`

add the following to the element implementation :

```...

@state()
private _currentUser?: UmbCurrentUserModel;

constructor() {
    super();
    this.consumeContext(UMB_CURRENT_USER_CONTEXT, (instance) => {
        this._observeCurrentUser(instance);
    });
}

private async _observeCurrentUser(instance: typeof UMB_CURRENT_USER_CONTEXT.TYPE) {
    this.observe(instance.currentUser, (currentUser) => {
        this._currentUser = currentUser;
    });
}...

```

The entire `welcome-dashboard.element.ts`

file is available for reference at the end of the step to confirm your placement for code snippets.

Now that we have the current user, we can access a few different things. Let's get the

`name`

of the current user, so that we can welcome the user:

Your dashboard should now look something like this:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2ffb4829d22c4f632be6cb7bec6fc4c3ad64c5c7%252FCreate_dashboard_functionality.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=af6f444c&sv=2)

### See the entire file: welcome-dashboard.element.ts

Let's dive deeper into some new resources and see what we can do with them.

Before we can get data from the server we need to start up the repository that handles said data.

Let's say we want to get the data of all of the users of our project.

To get the user data, we need to start up the user repository.

We are also going to need a type for our user details.


Import

`UmbUserDetailModel`

and`UmbUserCollectionRepository`:


Start up the repository and then create a new

`async`

method that we call from the constructor. We are also going to create a new`state`

for our array that is going to contain our user details:

Notice that the user repository has a lot of methods that we can use. We are going to use

`requestCollection`

to get all the users.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ebc88d8d4fb756b64ebfbfa49d35a8e999f51d73%252FCreate_dashboard_functionality_gettting_data.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5892303e&sv=2)

The method `requestCollection`

returns a promise, so let's `await`

the data and save the data in our array:

Now that we have the data from the repository, we need to render the data.

We are going to use the

`repeat`

directive to loop through the array of users and render each user. We are also going to create a new method`_renderUser`

that will render the user details. Add the`repeat`

directive to the import:

Add the following to the

`render`

method and create the`_renderUser`

method:

To make it more readable, add some CSS as well:


We recommend using variables for colors and sizing. See why and how you could achieve this in the next part where we will use the [Umbraco UI Library](/umbraco-cms/tutorials/creating-a-custom-dashboard/extending-the-dashboard-using-umbraco-ui-library).

We now should have our welcome dashboard filled showing a list of all users:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2393d1f459033ad963cd9faad8490726a353e1a8%252FCreate_dashboard_functionality_users_list.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ccec8b36&sv=2)

### See the entire file: welcome-dashboard.element.ts

With all of the steps completed, you should have a functional dashboard that welcomes the user and shows a list of all users. Hopefully, this tutorial has given you some ideas on what is possible to do when creating a dashboard.

You can also go further and [extend the dashboard](/umbraco-cms/tutorials/creating-a-custom-dashboard/extending-the-dashboard-using-umbraco-ui-library) with UI elements from the Umbraco UI Library.

[Previous Adding localization to the dashboard chevron-left](/umbraco-cms/tutorials/creating-a-custom-dashboard/adding-localization-to-the-dashboard)

[Next Using Umbraco UI library in the Dashboard chevron-right](/umbraco-cms/tutorials/creating-a-custom-dashboard/extending-the-dashboard-using-umbraco-ui-library)

Last updated

Was this helpful?

---

## Adding localization to the dashboard | CMS

Set up localization for your dashboard.

Overview

Setup Localization Files

```
export default {
  welcomeDashboard: {
    label: "Welcome Dashboard",
    heading: "Welcome",
    bodytext: "This is the Backoffice. From here, you can modify the content, media, and settings of your website.",
    copyright: "© Sample Company 20XX",
  }
};
```

Register Localization Files

Using the Localization Files

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d1b3548aea5ff8a59226e80def85e37070b13c86%252Fwelcome-eng.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e60da2e0&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-58bd8bda153422f0eaa32dc3154ec1869722d6fc%252Fwelcome-da.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4e9aa52e&sv=2)

Going Further

Last updated

Was this helpful?

Set up localization for your dashboard.

Overview

This is the second part of our guide to building a Custom Dashboard. This part continues work on the dashboard we built in part one: [Creating a Custom Dashboard](/umbraco-cms/tutorials/creating-a-custom-dashboard). It further shows how to handle localization in a custom dashboard.

The steps we will go through in second part are:

Setup Localization Files

In the

`welcome-dashboard`

folder create a new folder called "`Localization`

"Then create two new files

`en.js`

and`da-dk.js`:


Add the following code to

`en.js`


/App_Plugins/welcome-dashboard/Localization/en.js

```
export default {
  welcomeDashboard: {
    label: "Welcome Dashboard",
    heading: "Welcome",
    bodytext: "This is the Backoffice. From here, you can modify the content, media, and settings of your website.",
    copyright: "© Sample Company 20XX",
  }
};
```

Add the following code to

`da-dk.js`


Register Localization Files

Now let's update the `umbraco-package.json`

file from the `welcome-dashboard`

folder to register our new localization files:

Run `npm run build`

in the `welcome-dashboard`

folder and then run the project.

We can use the `umb-localize`

element to get the localizations out, which takes a key property in.

Using the Localization Files

Let's start using the localizations. In the `umbraco-package.json`

file, we will already be using the `#welcomeDashboard_label`

key for the dashboard label. Go ahead and replace `"label": "Welcome Dashboard"`

with `"label": "#welcomeDashboard_label"`.


The `#`

is used to indicate that the value is a key and not a string.

We will now use the `umb-localize`

element to get the translations for the dashboard. Update the `welcome-dashboard.element.ts`:


Run `npm run build`

in the `welcome-dashboard`

folder and then run the project.

The dashboard's text will appear depending on the user's language.

If the user's language is Danish, the dashboard will use the text from our

`da-dk`

file.If the user's language is English, the dashboard will use the text from our

`en`

file.If the key is not found in the current language, the fallback language (

`en`

) will be used.

The text between the open and close tags of `umb-localize`

is the fallback value. This is used in case the key can't be found at all.

This is how our dashboard should now look like:

Tip: If you do not have many translations, you can also choose to include the localizations directly in the meta-object. Read more about translations in the [Localization](/umbraco-cms/extending/language-files) article.

Going Further

With the part completed, you should have a dashboard welcoming your users' language.

In the next part, we will look into how to add more functionality to the dashboard using some of the Contexts that Umbraco offers.

Last updated

Was this helpful?

Was this helpful?

/App_Plugins/welcome-dashboard/Localization/da-dk.js

```
export default {
  welcomeDashboard: {
    label: "Velkomst Dashboard",
    heading: "Velkommen",
    bodytext: "Dette er Backoffice. Herfra kan du ændre indholdet, medierne og indstillingerne på din hjemmeside.",
    copyright: "© Sample Selskab 20XX",
  }
};
```

umbraco-package.json

```
{...
  "extensions": [
    {...},
    {
      "type": "localization",
      "alias": "MyPackage.Localize.En",
      "name": "English",
      "meta": {
        "culture": "en"
      },
      "js": "/App_Plugins/welcome-dashboard/Localization/en.js"
    },
    {
      "type": "localization",
      "alias": "MyPackage.Localize.DaDK",
      "name": "Danish",
      "meta": {
        "culture": "da-dk"
      },
      "js": "/App_Plugins/welcome-dashboard/Localization/da-dk.js"
    }
  ]
}
```

umbraco-package.json

```
{
  "$schema": "../../umbraco-package-schema.json",
  "name": "My.WelcomePackage",
  "version": "0.1.0",
  "extensions": [
    {
      "type": "dashboard",
      "alias": "my.welcome.dashboard",
      "name": "My Welcome Dashboard",
      "element": "/App_Plugins/welcome-dashboard/dist/welcome-dashboard.js",
      "elementName": "my-welcome-dashboard",
      "weight": -1,
      "meta": {
        "label": "#welcomeDashboard_label",
        "pathname": "welcome-dashboard"
      },
      "conditions": [
        {
          "alias": "Umb.Condition.SectionAlias",
          "match": "Umb.Section.Content"
        }
      ]
    },
    {
      "type": "localization",
      "alias": "MyPackage.Localize.En",
      "name": "English",
      "meta": {
        "culture": "en"
      },
      "js": "/App_Plugins/welcome-dashboard/Localization/en.js"
    },
    {
      "type": "localization",
      "alias": "MyPackage.Localize.DaDK",
      "name": "Danish",
      "meta": {
        "culture": "da-dk"
      },
      "js": "/App_Plugins/welcome-dashboard/Localization/da-dk.js"
    }
  ]
}
```

welcome-dashboard.element.ts

```
render() {
    return html`
      <h1>
        <umb-localize key="welcomeDashboard_heading">Welcome</umb-localize>
        Dashboard
      </h1>
      <div>
        <p>
          <umb-localize key="welcomeDashboard_bodytext">
            This is the Backoffice. From here, you can modify the content,
            media, and settings of your website.
          </umb-localize>
        </p>
        <p>
          <umb-localize key="welcomeDashboard_copyright">
            © Sample Company 20XX
          </umb-localize>
        </p>
      </div>
    `;
  }
```

welcome-dashboard.element.ts

```
import { LitElement, css, html, customElement} from "@umbraco-cms/backoffice/external/lit";
import { UmbElementMixin } from "@umbraco-cms/backoffice/element-api";

@customElement('my-welcome-dashboard')
export class MyWelcomeDashboardElement extends UmbElementMixin(LitElement) {

  render() {
    return html`
      <h1>
        <umb-localize key="welcomeDashboard_heading">Welcome</umb-localize>
        Dashboard
      </h1>
      <div>
        <p>
          <umb-localize key="welcomeDashboard_bodytext">
            This is the Backoffice. From here, you can modify the content,
            media, and settings of your website.
          </umb-localize>
        </p>
        <p>
          <umb-localize key="welcomeDashboard_copyright">
            © Sample Company 20XX
          </umb-localize>
        </p>
      </div>
    `;
  }

  static styles = [
    css`
      :host {
        display: block;
        padding: 24px;
      }
    `,
  ];
}

export default MyWelcomeDashboardElement;

declare global {
  interface HTMLElementTagNameMap {
    'my-welcome-dashboard': MyWelcomeDashboardElement;
  }
}
```

---

## Using Umbraco UI library in the Dashboard | CMS

Now that we have data for our dashboard we might want to make it look prettier. To do this we can use the Umbraco UI library.

Overview

Umbraco UI Library

UI Box

```
render() {
    return html`
        <uui-box>

            // rest of the render code

        </uui-box>
    `;
}
```

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-41774b290b1d09fc087f583adbaeab4172575309%252FCreate_dashboard_functionality_users_list_ui_styled.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=de562358&sv=2)

UI Table

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-71dc772189f166d99e7b32cdeb68f3f775ae5a71%252FCreate_dashboard_functionality_users_list_ui_styled_table.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8aab698b&sv=2)

**Challenge (optional)**

Wrap up

Last updated

Was this helpful?

---
