# Creating A Property Editor

## Contents

- [Adding configuration to a Property Editor | CMS](#adding-configuration-to-a-property-editor-cms)
- [Adding server-side validation | CMS](#adding-server-side-validation-cms)
- [Custom value conversion for rendering | CMS](#custom-value-conversion-for-rendering-cms)
- [Integrating context with a Property Editor | CMS](#integrating-context-with-a-property-editor-cms)

---

## Adding configuration to a Property Editor | CMS

Adding configuration options to the editor.

This is step two in the guide to building a Property Editor. This step builds on part one and covers adding configuration options to the editor.

This article covers the following:

An important part of building good Property Editors is making them flexible so they can be reused in many contexts. The Rich Text Editor, for example, lets you choose which buttons and stylesheets to use per instance.

The same editor can be reused with different configurations.

To add a Data Type configuration field to the Suggestion Property Editor:

Open the

`umbraco-package.json`

file.Add the

`settings`

object inside the`meta`

object.Add some

`properties`:


```...
    "meta": {...
        "settings": {
            "properties": [
                {
                    "alias": "disabled",
                    "label": "Disabled",
                    "description": "Disables the suggestion button",
                    "propertyEditorUiAlias": "Umb.PropertyEditorUi.Toggle"
                },
                {
                    "alias": "placeholder",
                    "label": "Placeholder text",
                    "description": "A nice placeholder description to help out our editor!",
                    "propertyEditorUiAlias": "Umb.PropertyEditorUi.TextBox"
                },
                {
                    "alias": "maxChars",
                    "label": "Max characters allowed",
                    "description": "The maximum number of allowed characters in a suggestion",
                    "propertyEditorUiAlias": "Umb.PropertyEditorUi.Integer"
                }
            ]
        }...
    }
```

The code above adds three configuration fields. Each entry in the `properties`

collection represents a Configuration field.

`Disabled`

uses the Toggle Property Editor UI. This enables to switch the suggestion button on or off and provides the user with a toggle button.`Placeholder text`

uses the TextBox Property Editor UI, allowing the user to write a text.`Max characters allowed`

uses the Integer Property Editor UI, enabling the user to enter a numeric value.

The Property Editor UI needs to be declared as it declares what User Interface should be used for this field.

You can use any Property Editor UI to define Configuration fields. The alias of a given Property Editor UI can be found in Data Type configurations using that Property Editor.

Add default values for the new configuration fields:


### See the entire file: umbraco-package.json

`defaultData`

only applies to newly created Data Types. If you already saved the Data Type in [Part 1](/umbraco-cms/tutorials/creating-a-property-editor) of the tutorial, adding `defaultData`

here won't automatically populate the existing configuration. Umbraco only reads default values when a Data Type is first created. If your Data Type already exists, you have two options:

Manually set the values by going to

**Settings**→**Data Types**. Open your Data Type and enter the values there.Delete and recreate the Data Type to have

`defaultData`

take effect automatically.

Save the files and reload the backoffice. You can now see the Configurations in the Data Type:


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e450d30e0fdc33ff7636666539bbb50f3b835012%252Fsuggestion-editor-config_3.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=41a613ed&sv=2)

The next step is to gain access to our new configuration options. For this, open the `suggestions-property-editor-ui.element.ts`

file.

Create some state variables that can store our configurations:


Let's create a config property. Add a new import and add the following property:


Look up the alias of the config and then grab the value by said alias:


Let's use the `placeholder`

and `maxChars`

for the input field and the `disabled`

option for the suggestion button.

Add a new import

`ifDefined`:


Update the render method:


### See the entire file: suggestions-property-editor-ui.element.ts

Run the command

`npm run build`

in the`suggestions`

folder.Run the project.

Go to the

**Content**section of the Backoffice to see the new changes in the property editor:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-91aa34f5216bcdf39cd20b610a7f2d9fe5a07ba8%252Fsuggestion-editor-backoffice_2.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=112e58d8&sv=2)

The Data Type now has configuration options wired up to the Property Editor. The next part covers integrating context with the Property Editor.

[Previous Creating a Property Editor chevron-left](/umbraco-cms/tutorials/creating-a-property-editor)

[Next Integrating context with a Property Editor chevron-right](/umbraco-cms/tutorials/creating-a-property-editor/integrating-context-with-a-property-editor)

Last updated

Was this helpful?

---

## Adding server-side validation | CMS

Adding server-side validation for a Property Editor.

Overview

When should I use a Data Editor?

Implementing server-side validation

```
using Umbraco.Cms.Core.Models;
using Umbraco.Cms.Core.PropertyEditors;

namespace Umbraco.Docs.PropertyEditors;

[DataEditor("My.DataEditor.Suggestions", ValueEditorIsReusable = true)]
public class MySuggestionsDataEditor : DataEditor
{
    public MySuggestionsDataEditor(IDataValueEditorFactory dataValueEditorFactory)
        : base(dataValueEditorFactory)
    {
    }

    protected override IDataValueEditor CreateValueEditor()
        => DataValueEditorFactory.Create<MySuggestionsDataValueEditor>(Attribute!);
}
```

Coupling the Property Editor and the Data Editor

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8efb55eb5a35c5a82d34033dbe36900dcc7cc39b%252Fsuggestion-editor-config_4.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b6888c43&sv=2)

Advanced Data Editor use-cases

Custom content indexing for search

Server-side data conversion to and from the client

Last updated

Was this helpful?

### Default Property Editor Schema aliases | CMS

An overview of the default Property Editor Schema aliases

| Property Editor Schema alias | .NET runtime type |
|---|---|
| Umbraco.Plain.DateTime | `System.DateTime` |
| Umbraco.Plain.Decimal | `System.Decimal` |
| Umbraco.Plain.Integer | `System.Int32` |
| Umbraco.Plain.Json | `System.Text.Json.JsonDocument` |
| Umbraco.Plain.String | `System.String` |
| Umbraco.Plain.Time | `System.TimeSpan` |

Last updated

Was this helpful?

---

## Custom value conversion for rendering | CMS

Add a Property Value Converter for custom Property Editor value conversion.

Overview

When should I use a Property Value Converter?

Implementing a Property Value Converter

Last updated

Was this helpful?

Add a Property Value Converter for custom Property Editor value conversion.

Overview

In the previous steps, we created a custom Property Editor for the Umbraco backoffice client. In this step, we will discuss how to convert the Property Editor values for use when rendering the website.

To this end, we will create a Property Value Converter that converts the stored suggestion text into a custom rendering model.

When should I use a Property Value Converter?

A Property Value Converter is usually not necessary. Based on the chosen `propertyEditorSchemaAlias`

, Umbraco will automatically provide appropriately typed models for rendering the Property Editor. For more information, see the [Default Property Editor Schema Alias options](/umbraco-cms/tutorials/creating-a-property-editor/adding-server-side-validation/default-property-editor-schema-aliases) article.

The most common use-cases for building a Property Value Converter are:

Property Editors that store values which require server-side conversion, in order to render an appropriate output.

Property Editors with specific caching requirements.

Tailoring the Property Editor output value specifically for the .


Implementing a Property Value Converter

A Property Value Converter must meet a few required responsibilities:

Identifying itself as being able to convert values for a given Property Editor.

Declaring the concrete runtime type it will be outputting.

Performing the value conversion from the stored


The following code snippet outlines how these could be solved for our `suggestion`

Property Editor.

We have used the property type editor UI alias from `umbraco-package.json`

in the implementation of `IsConverter()`.


For more advanced Property Value Converter techniques (for example, controlling caching), see the [Property Value Converters](/umbraco-cms/customizing/property-editors/property-value-converters) article.

Last updated

Was this helpful?

Was this helpful?

MySuggestionsPropertyValueConverter.cs

```
using Umbraco.Cms.Core.Models.PublishedContent;
using Umbraco.Cms.Core.PropertyEditors;

namespace Umbraco.Docs.PropertyEditors;

// the Property Value Converter that handles the suggestions Property Editor
public class MySuggestionsPropertyValueConverter : PropertyValueConverterBase
{
    // 1. converts properties with the property type editor UI alias "My.PropertyEditorUi.Suggestions"
    public override bool IsConverter(IPublishedPropertyType propertyType)
        => propertyType.EditorUiAlias == "My.PropertyEditorUi.Suggestions";

    // 2. yields outputs of type MySuggestionsModel
    public override Type GetPropertyValueType(IPublishedPropertyType propertyType)
        => typeof(MySuggestionsModel);

    // 3. converts the suggestion (string) to the output type (MySuggestionsModel)
    public override object? ConvertIntermediateToObject(
        IPublishedElement owner,
        IPublishedPropertyType propertyType,
        PropertyCacheLevel referenceCacheLevel,
        object? inter,
        bool preview)
        => inter is string suggestion
            ? new MySuggestionsModel
            {
                Suggestion = $"Here's a suggestion for you: {suggestion}"
            }
            : null;
}

// the custom rendering model for the suggestions Property Editor
public class MySuggestionsModel
{
    public required string Suggestion { get; init; }
}
```

---

## Integrating context with a Property Editor | CMS

Integrate one of the built-in Umbraco Contexts.

Overview

Setting up the contexts

```
import { UMB_NOTIFICATION_CONTEXT, UmbNotificationContext, UmbNotificationDefaultData} from '@umbraco-cms/backoffice/notification';
import { UmbElementMixin } from '@umbraco-cms/backoffice/element-api';
```

```
export default class MySuggestionsPropertyEditorUIElement extends UmbElementMixin((LitElement)) implements UmbPropertyEditorUiElement {
```

```
#notificationContext?: UmbNotificationContext;

constructor() {
    super();

    this.consumeContext(UMB_NOTIFICATION_CONTEXT, (instance) => {
        this.#notificationContext = instance;
    });
}
```

Using the notification context

![A danger notification reading 'Nothing to trim!' displayed in the Umbraco backoffice.](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-728e7e9d1a06fe3d53981659f70d54b8d4a013cf%252Fnothing-to-trim.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7f0aa87c&sv=2)

Adding more logic to the context

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5a964fd5215e8f29021d4cfe2c006280a237aead%252Fcreating-a-property-editor-trim.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=df42585b&sv=2)

Enforcing the Character Limit

Making the editor a Form Control

1

Import

`UmbLitElement`

and `UmbFormControlMixin`

2

Update the Lit import

3

Update the class declaration

4

Replace

`value`

with a getter/setter5

Add a validation rule

6

Register the input as a form control

Adding a character counter

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b19c11615bf309a0fd202a2a08120174647b4dce%252Fblock-publishing.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f85aa5d4&sv=2)

Wrap up

Last updated

Was this helpful?

---
