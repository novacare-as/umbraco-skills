# Extension Registry

## Contents

- [Extension Manifest Introduction | CMS](#extension-manifest-introduction-cms)
- [Register an Extension | CMS](#register-an-extension-cms)
- [Replace, Exclude, or Unregister | CMS](#replace-exclude-or-unregister-cms)

---

## Extension Manifest Introduction | CMS

Learn about the different methods for declaring an Extension Manifest.

This page explains what an Extension Manifest for a Umbraco backoffice extension is. It outlines the manifest structure, required fields, and optional features used across types.

Umbraco reads the extension manifest to register the extension in the Extension Registry. Each extension is of a certain type and this determines the required fields of the manifest and its available capabilities. An Extension Manifest declares a single backoffice extension along with its configuration.

Some extensions need extra assets, such as a JavaScript file with a Web Component.

The abilities of the extensions rely on the specific extension type. The type sets the scene for what the extension can do and what it needs to be utilized. Some extension types can be made purely via the manifest, like a section or menu item. Other types require files, like a JavaScript file containing a Web Component, like a custom property editor. An Extension Manifest has a strict format where some properties are required and some depend on the Extension Type. An Extension Manifest can be written as a JavaScript or JSON object. You can learn more about this when [registering an extension](/umbraco-cms/customizing/extending-overview/extension-registry/register-extensions).

A minimal Extension Manifest looks like this:

```
{
    "type": "...",
    "alias": "my.customization",
    "name": "My customization"
}
```

These fields are all required and have the following meaning:

`type`

— The type defines the purpose of the extension. Umbraco has many[extension types](/umbraco-cms/customizing/extending-overview/extension-types)available.`alias`

— Unique identifier for this manifest. Prefix it with something that makes your extension unique. For example:*FictiveCompany.MyProject.Dashboard.Overview*.`name`

— Representational name of this manifest. This name does not need to be unique, but this can be beneficial when debugging extensions. This name also shows up in the Extensions Insights in the backoffice of Umbraco. For example:*My Fictive Company Overview Dashboard*.

Most extension types support the use of the following generic features for their Manifest:

`weight`

- Define a weight to determine the importance or visual order of this extension. A higher weight gives a more prominent position. For instance, for a dashboard it determines its order between other dashboards.`overwrites`

- If you want to omit an existing extension, then define one or more Extension Aliases that this extension should omit when presented. Read more in[Replace, Exclude or Unregister extensions](/umbraco-cms/customizing/extending-overview/extension-registry/replace-exclude-or-unregister).`conditions`

- Define one or more conditions that must pass for the extension to become available. For instance, don't show a section if you don't have the proper rights. Read more in[Extension Conditions](/umbraco-cms/customizing/extending-overview/extension-conditions).`kind`

- Some extension types can reference a predefined`kind`

. By specifying a`kind`

, the manifest inherits the`kind`

's properties. This allows for reuse of predefined settings. See .`meta`

- Many Extension Types require additional information declared as part of a`meta`

field. It depends on the Extension Type what is required. For instance label and icon of a menu item.

For more information, see an overview of all possible [Extension Types](/umbraco-cms/customizing/extending-overview/extension-types) and their requirements.

Last updated

Was this helpful?

---

## Register an Extension | CMS

You can bring new UI or additional features to the Backoffice by registering an Extension via an Extension Manifest.

Umbraco-package.json

```
{
    "name": "My Customizations",
    "extensions": [
        {
            "type": "...",
            "alias": "my.customization.extension1",
            "name": "My customization extension 1"...
        },...
    ]
}
```

```
{
    "$schema": "../../umbraco-package-schema.json",
    "name": "My Customizations",
    "extensions": [...
    ]
}
```

Advanced Registration

The Bundle Approach

The Entry Point Approach

Registration with JavaScript

Last updated

Was this helpful?

---

## Replace, Exclude, or Unregister | CMS

You may want to replace or completely remove an extension. Depending on your interest, 3 different options are available.

Besides adding extensions to Umbraco, sometimes you want to change what is already there. You can replace extensions with your own and exclude or unregister extensions.

You can replace an existing extension by another one. You can do this by defining the `overwrites`

property in your [Extension Manifest](/umbraco-cms/customizing/extending-overview/extension-registry/extension-manifest) with one Extension Alias. For multiple `overwrites`

you can provide the Extension Aliases that need to be replaced as an array.

This example overrides the `save and preview`

button with an external "preview" button (single overwrite):

```
const manifest = {
    type: 'workspaceAction',
    alias: 'my.WorkspaceAction.ExternalPreview',
    name: 'My workspace action for external preview',
    overwrites: 'Umb.WorkspaceAction.Document.SaveAndPreview'...
};
```

This example overrides both the `save and preview`

button as well as the `save`

button with an external "preview" button (multiple overwrite):

```
const manifest = {
    type: 'workspaceAction',
    alias: 'my.WorkspaceAction.ExternalPreview',
    name: 'My workspace action for external preview',
    overwrites: ['Umb.WorkspaceAction.Document.SaveAndPreview', 'Umb.WorkspaceAction.Document.Save']...
};
```

If your extension has conditions, the overwritten extensions will only be hidden when your extension is displayed. This means that the overwrites only have an effect if all the conditions are permitted and the extensions are displayed at the same spot.

When you exclude an extension, the extension will never be displayed. This allows you to permanently hide, for example, a menu or a button. This does not unregister the extension, but rather flags it as excluded. This also means that no one else can register an extension with the same alias as the excluded extension.

Currently, it is not possible to un-exclude extensions once excluded.

The following JavaScript code hides the `Save and Preview`

button from the Document Workspace.

When and where you execute this code depends on your situation. In many cases, it makes sense to execute this on boot, using the [entry point approach](/umbraco-cms/customizing/extending-overview/extension-types/backoffice-entry-point).

You can also choose to unregister an extension. You should only use this on extensions you registered yourself and have control over. Otherwise, you might try to remove an extension before it is registered. A use case for this, is if you temporarily registered an extension and you want to remove it again.

In other cases, you can use the `overwrites`

or `exclude`

option. The difference with the `exclude`

approach is that unregistering removes the extension from the Extension Registry. This allows you to re-register extensions with the same alias.

When and where you execute this code depends on your situation. In many cases, it makes sense to execute this on boot, using the [entry point approach](/umbraco-cms/customizing/extending-overview/extension-types/backoffice-entry-point).

Last updated

Was this helpful?

---
