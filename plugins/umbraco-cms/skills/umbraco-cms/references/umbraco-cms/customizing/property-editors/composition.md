# Composition

## Contents

- [Property Editor Data Source | CMS](#property-editor-data-source-cms)
- [Property Editor Schema | CMS](#property-editor-schema-cms)
- [Property Editor UI | CMS](#property-editor-ui-cms)

---

## Property Editor Data Source | CMS

Enable Data Source Support

```
{
  type: 'propertyEditorUi',
  name: 'My Property Editor UI with Data Source support',
  //... more
  meta: {
    //... more
    supportsDataSource: {
      enabled: true,
      forDataSourceTypes: ['My.DataSourceType.Custom']
    }
  }
}
```

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ee1158546920dc6db17162fa8b64049e30e486d2%252Fumbraco-docs-data-type-property-editor-data-source%2520%281%29.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=11ac4298&sv=2)

Register a Property Editor Data Source

Data Source Settings

Access Data Source Alias in Property Editor UI

Access Data Source Config in Property Editor UI

Built-in Data Source Types

Last updated

Was this helpful?

---

## Property Editor Schema | CMS

The Server side part of a Property Editor

A Property Editor Schema is the data part of a Property Editor in Umbraco. It defines the type of data that can be stored (string, number, date, JSON) and how that data should be validated. It can also perform conversions of data going in or out of the database.

The schema's `settings`

define the configuration options that are available for the Property Editor (such as maximum characters, allowed file types, etc.). When you create a Data Type, you provide values for these settings. Those configured values are then passed to both the server-side validation and the Property Editor UI.

You can define settings on both the Property Editor Schema and the Property Editor UI. It's good practice to define settings that impact the data (like validation rules) on the Property Editor Schema. Settings that only affect the UI should be set on the Property Editor UI.

For details on the settings structure, see the [Property Editor Schema Extension Type](/umbraco-cms/customizing/extending-overview/extension-types/property-editor-schema) documentation.

In essence, the Property Editor Schema defines the data contract for a Property Editor.

When you want to use a Property Editor to edit content in Umbraco, the Property Editor needs to have a schema. If it does not have a schema, you cannot select the Property Editor when creating a [Data Type](/umbraco-cms/fundamentals/data/data-types). In other scenarios, like when using a Property Editor to edit Data Type settings, a schema is not required.

The Property Editor Schema runs server-side (in C# code) and has the final authority on whether data is valid to commit to the database. The Property Editor UI is where users enter their data. You can have client-side validation, but the Property Editor Schema always makes the ultimate decision. When there is a mismatch between client-side and server-side validation, the server rejects data that the client considers valid.

Because the Property Editor Schema defines how to process and validate data, you can have multiple Property Editor UIs using the same schema. As long as they work with the data as defined in the schema, this works. It also makes it possible to swap out the UI while maintaining the same data.

You can see the used schema of a Property Editor in the backoffice of Umbraco when you create a new [Data Type](/umbraco-cms/fundamentals/data/data-types).

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-865f86e049a00e0281c98dd2cf8bf5201475fa90%252Fproperty-editor-schema-alias-in-backoffice.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9afef198&sv=2)

Umbraco ships with a collection of that cover most scenarios that are less demanding. Although each situation is different, if you answer yes to any of the following statements, it makes sense to create a custom schema:

You expect the schema to be used by multiple Property Editor UIs.

You need a custom

[Property Value Converter](/umbraco-cms/customizing/property-editors/property-value-converters)to convert the data going into the cache, or you want the Umbraco ModelsBuilder to have a more specific, strongly-typed model.You need specific server-side validation of your data that is not covered in the default schemas.

You have specific needs for converting data going into or coming out of the database that are not covered in the default schemas.

You want to be flexible and prepared for future development.


If none of the questions above are relevant to you, the default schemas will cover what's needed.

A Property Editor Schema consists of two server-side and one optional client-side component. This chapter explains these components and their relations.

The server-side components are:

`DataEditor`

, which serves as the definition and factory.`DataValueEditor`

, which performs the actual data handling work.

The client-side component is:

`Property Editor Schema extension`

, which is the registration of the schema in the Extension Registry for use by the frontend.

These components are related in the following way:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4fbe5c313f53a50f510704eb4e822679d814a573%252Fproperty-editor-schema-backend.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c612e8b9&sv=2)

For a complete example, there is a tutorial for creating a Property Editor. It shows how to [implement a schema to add server-side validation](/umbraco-cms/tutorials/creating-a-property-editor/adding-server-side-validation). Use this article together with that tutorial.

The `DataEditor`

is the C# class that implements the Property Editor Schema on the server side. It serves as the blueprint that defines how a Property Editor should work. The `DataEditor`

defines the schema's unique alias, the type of data stored in the database, and the default configuration settings. There is only one `DataEditor`

instance per Property Editor Schema.

A class becomes a Data Editor by inheriting the `DataEditor`

class and adding the `DataEditor`

attribute:

Notice the string `My.DataEditor.Suggestions`

. This is the alias of the Property Editor Schema and is the only connection between the frontend and backend.

The `DataEditor`

attribute has additional optional parameters:

`ValueType`

: Defines how the data is stored in the database. The default is`String`

. Other options are:`Integer`

,`Decimal`

,`DateTime`

,`Date`

,`Time`

,`Text`

, and`Json`

.`ValueEditorIsReusable`

: Defines if the`DataValueEditor`

instance is cached and reused as a singleton or created fresh each time. For most custom Property Editors, the default`true`

value is best for performance. Set this to`false`

if your editor:Maintains state between operations.

Has a complex configuration that varies per Data Type.

Is a block-based editor or a similar complex scenario.



See the [full tutorial on how to implement the DataEditor](/umbraco-cms/tutorials/creating-a-property-editor/adding-server-side-validation).

The `DataValueEditor`

is the workhorse that handles all data operations for the Property Editor Schema. When property values need saving or loading, the `DataEditor`

creates a `DataValueEditor`

instance to do the actual work. This instance converts data between what the editor displays and what gets stored in the database. It also runs server-side validation to ensure data integrity and handles any necessary data transformations.

The `DataEditor`

creates `DataValueEditor`

instances through its `CreateValueEditor()`

method. Each instance is configured with specific settings from the [Data Type](/umbraco-cms/fundamentals/data/data-types). For example, a textbox Property Editor might have one Data Type configured for short text and another for long text. Both use the same `DataEditor`

(the blueprint), but each creates `DataValueEditor`

instances with different maximum length settings.

A class becomes a Data Value Editor by inheriting the `DataValueEditor`

class:

Data Value Editors can have one or more validators. These validators test whether the data complies with the settings configured in the Property Editor.

See the [full tutorial](/umbraco-cms/tutorials/creating-a-property-editor/adding-server-side-validation) on how to implement the `DataValueEditor`.


Before the Property Editor UI can utilize the schema, it needs to be registered in the Extension Registry using a manifest.

The example in this article covers only the basics. See the [Property Editor Schema Extension Type](/umbraco-cms/customizing/extending-overview/extension-types/property-editor-schema) documentation for the complete manifest reference, including configuration settings.

If the Property Editor has no settings, it is technically not required to register the schema in the Extension Registry. The Property Editor UI can reference the alias as defined in the `DataEditor`

, and that will work. However, to show intent and make the schema more visible for frontend developers, it is recommended to register the schema anyway. This also provides a fallback for which Property Editor UI to use in case it cannot be determined.

At minimum, the schema manifest must specify the type, alias, name, and which Property Editor UI should be used by default:

The `alias`

in the manifest must exactly match the alias used in the C# `DataEditor`

attribute. This alias string is the only connection between the server-side implementation and the client-side manifest.

If the schema alias is referenced but not properly registered, the backoffice will display a "Missing Property Editor" error state.

The Property Editor Schema is now complete and ready to use.

This chapter covers advanced scenarios in Property Editor Schema development. It is intended for developers who understand the basic `DataEditor`

and `DataValueEditor`

concepts and want to explore more sophisticated patterns.

Usually, when you create a custom Data Editor Schema, you implement both the Data Editor and the Data Value Editor. If you do not need custom validation or data manipulation, you can use one of the instead. In most cases, you do not need to create a Property Editor Schema at all.

However, it is possible to create a custom Data Editor, but let the handling of the data be handled by the `DataValueEditor`

base class itself. On a Data Editor, you can specify the `ValueType`

. This is the type that determines how the data is stored in the database. The `DataValueEditor`

can process the data based on the `ValueType`

. This means you can create a Data Editor without implementing a custom Data Value Editor.

This pattern is valuable when you need a unique schema identifier. You might use this for targeting in Property Value Converters or custom indexing. However, you do not need custom validation or data conversion.

This example creates a custom `DataEditor`

that reuses the standard JSON `DataValueEditor`:


Now you can target this specific schema in your Property Value Converter:

Last updated

Was this helpful?

---

## Property Editor UI | CMS

Presenting the Editing Experience of a Property Editor

The Property Editor UI is the client-side component that renders the editing interface in the Umbraco backoffice. It provides the visual interface for content editors to interact with their data. The Property Editor Schema validates and stores data on the server. The Property Editor UI focuses on providing an intuitive editing experience through the browser.

A Property Editor UI is a purely frontend extension in the shape of a web component. In this example, we will create a Property Editor UI using an Umbraco Lit element step by step. At the end of the article, the full example is provided.

To create a Property Editor UI, the following needs to be done:

Implement the Umbraco Lit component - the actual visible part.

Register the Property Editor UI using a manifest.


What makes a standard Umbraco Lit component a Property Editor UI is the implementation of the `UmbPropertyEditorUiElement`

interface. The `UmbPropertyEditorUiElement`

interface ensures that your element has the necessary properties and methods to be used as a Property Editor UI element. See the for the full interface definition.

```
import { UmbLitElement } from '@umbraco-cms/backoffice/lit-element';
import type { UmbPropertyEditorUiElement } from '@umbraco-cms/backoffice/property-editor';

// Implement the UmbPropertyEditorUiElement
export default class UmbPropertyEditorUITextBoxElement extends UmbLitElement implements UmbPropertyEditorUiElement {...
}
```

This interface gives access to important information about the data and configuration through a collection of properties. None of them are technically required to implement, but in practice, you need `value`

and probably also `config`.


`value`

: Contains the actual value that will be processed and stored when the content is saved and retrieved. The value is automatically populated when the component loads. When saved, the value is sent to processing and saved to the database.`config`

: The configuration as set on the Data Type.`readonly`

: If you support read-only mode, this will indicate whether the component should be read-only.

For the full interface properties of the `UmbPropertyEditorUiElement`

, see the for more information.

A minimal implementation where the value is read and placed in a textbox looks like this:

In the previous example, the value is read and placed in a text box. However, it will not react to changes in the value. When the value needs to be changed, it is required to dispatch an `UmbChangeEvent`.


As discussed before, both the Property Editor UI and the Property Editor Schema can have settings that are set when creating a Data Type. You can access these settings like this:

Setting the `maxlength`

attribute is used only for client-side validation and to help editors adhere to data validation rules. This does not automatically trigger server-side validation on save. If you need server-side validation, the Property Editor Schema needs to implement this explicitly.

When an editor is creating a Document Type in the backoffice and adds properties, properties can be marked as mandatory. There is also an option to add a custom validation message for that property.

When a property is marked as mandatory, it will automatically perform validation when the content node with that property is saved. This validates whether the `value`

property has a value or not. If not, the custom validation message is displayed.

The validation is handled automatically by the CMS. However, if it makes sense in the context of your Property Editor UI, you can access both the mandatory flag and the custom error message.

The validation above is only performed on the value of the property editor as a whole. When you have complex Property Editor UIs with multiple inputs and advanced validation, you need more advanced validation techniques. See the [UI Library Form Validation documentation](/umbraco-cms/customizing/ui-library#form-validation) on how to implement advanced validation.

The `readonly`

property indicates whether the Property Editor should be in read-only mode. This happens automatically based on:

User permissions - The current user does not have update permissions for this content.

Content locks - Another user is currently editing the content.

Workflow states - Content is in a state that prevents editing (for example, awaiting approval).

Variant restrictions - Editing a culture/segment variant without proper permissions.


By default, Umbraco places an overlay on the Property Editor if it needs to be read-only. In most cases, this is sufficient. However, you can also handle read-only mode in the Property Editor more gracefully.

To properly support read-only mode, the manifest should set the `supportsReadOnly`

property to `true`

, and you need to handle read-only yourself. This means you need to ensure the editor cannot change any content in read-only mode.

The following code is a complete example that includes all the previous examples in this article. This example Property Editor UI:

Reads and updates the value.

Handles configuration.

Handles mandatory and the mandatory message.

Handles read-only mode.


To make your Property Editor UI available in Umbraco, you need to register it using a manifest. The manifest defines the alias, element location, and metadata such as the label, icon, and which schema it works with.

For details on the manifest structure and all available options, see the [Property Editor UI Extension Type](/umbraco-cms/customizing/extending-overview/extension-types/property-editor-ui) documentation.

Last updated

Was this helpful?

---
