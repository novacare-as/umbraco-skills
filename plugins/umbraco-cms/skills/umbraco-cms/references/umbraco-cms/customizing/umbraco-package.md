# Umbraco Package | CMS

An extension begins with a Umbraco Package

A Package is declared via an Umbraco Package JSON file. This describes the Package and declares one or more UI Extensions. The Package declaration is a JSON file that is stored in the `App_Plugins/{YourPackageName}`

folder. The file is named `umbraco-package.json`.


Here is a sample package. It should be stored in a folder in `App_Plugins/{YourPackageName}`

, with the name `umbraco-package.json`

. In this example, the package name is `SirTrevor`

and is a text box property Data Type.

Before Umbraco 14, a package was declared in a `package.manifest`

file instead of `umbraco-package.json`

. The old format is no longer supported, but you can migrate the contents to the new format.

```
{
    "id": "My.Nuget.Package",
    "name": "Sir Trevor",
    "version": "1.0.0-beta",
    "extensions": [
        {
            "type": "propertyEditorUi",
            "alias": "Sir.Trevor",
            "name": "Sir Trevor Property Editor UI",
            "element": "/App_Plugins/SirTrevor/SirTrevor.js",
            "meta": {
                "label": "Sir Trevor",
                "propertyEditorSchemaAlias": "Umbraco.TextBox",
                "icon": "icon-code",
                "group": "Pickers"
            }
        }
    ]
}
```

The `umbraco-package`

accepts these fields:

The unique identifier for your package. This is used to identify your package and should be unique to your package. If you are creating a package that is distributed via NuGet, you should use the NuGet package ID as the ID for your package.

Allows you to specify a friendly name for your package that will be used for telemetry. If no name is specified the name of the folder will be used instead.

The version of your package, if this is not specified there will be no version-specific information for your package. This is used for telemetry and to help users understand what version of your package they are using. It is also used for package migrations. The version should follow the format.

With this field, you can control the telemetry of this package, this will provide Umbraco with the knowledge of how many installations use this package.

The default is `true`.


Also known as: `allowPackageTelemetry`


This field is used to allow public access to the package. If set to `true`

, the package will be available for anonymous usage, for example on the login screen. If set to `false`

, the package will only be available to logged-in users.

The default is `false`.


The `importmap`

field is an object that contains two properties: `imports`

and `scopes`

. This is used to define the import map for the package. The `imports`

property is an object that contains the import map for the package. The `scopes`

property is an object that contains the scopes for the package.

**Example**

This example shows how to define an import map for a module exported by a package:

The `imports`

object contains the import map for the package. The key is the specifier for the module that is being imported, and the value is the URL of the module.

This allows developers to consume modules that are exported by a package without having to know the exact path to the module:

Umbraco supports the current specification of the property as outlined on MDN Web Documentation: .

The `extensions`

field is an array of Extension Manifest objects. Each object describes a single client extension.

Read more about Extension Types in the Backoffice to get a better understanding of the different types of extensions:

[Full List of Extension Types chevron-right](/umbraco-cms/customizing/extending-overview/extension-types#full-list-of-extension-types)

`conditions`

propertyEach extension in the `extensions`

array can include an optional `conditions`

property. This is an array of condition objects that must all be satisfied before the extension is loaded and activated. It gives you fine-grained control over where and when an extension appears in the backoffice.

**Structure**

Each condition object requires at minimum an `alias`

identifying which condition to evaluate. Many conditions also accept a `match`

value specifying what to match against.

Common aliases include:

`Umb.Condition.WorkspaceAlias`

`Umb.Condition.SectionAlias`

`Umb.Condition.WorkspaceEntityType`

`Umb.Condition.UserPermission.Document`.


For a full list and details, see the [Extension Conditions](/umbraco-cms/customizing/extending-overview/extension-types/condition) article.

Make your IDE be aware about the opportunities of the `umbraco-package.json`

by adding a JSON schema. This gives your code editor abilities to autocomplete and knowledge about the format. This helps to avoid mistakes or errors when editing the `umbraco-package.json`

file.

Editors like Visual Studio can use the `$schema`

notation in your file.

Hover over any of the properties to see the description of the property. You can also use the `Ctrl + Space`

(Windows/Linux) or `CMD + Space`

(macOS) shortcut to see the available properties.

Umbraco scans the `App_Plugins`

folder for `umbraco-package.json`

files **two levels deep**. When found, the packages are loaded into the system.

You may need to restart the application, if you add a new file or modify an existing manifest:

If the runtime mode is `Production`

, the manifests are cached for 30 days or until the application is restarted to improve performance. In other runtime modes, the cache is cleared every 10 seconds.

You can implement the interface to provide your own package manifest reader. This can be useful if you want to load package manifests from a different location or source.

Umbraco also supports projects that contain static web assets. The `umbraco-package.json`

file can be placed in the `wwwroot`

folder of the RCL project. The package will be loaded when the RCL is referenced by the main project. You must map the web path to `App_Plugins`

in your `.csproj`

file:

Read more about getting set up for Backoffice development in the [Customize Backoffice](/umbraco-cms/customizing/overview) section.

Last updated

Was this helpful?