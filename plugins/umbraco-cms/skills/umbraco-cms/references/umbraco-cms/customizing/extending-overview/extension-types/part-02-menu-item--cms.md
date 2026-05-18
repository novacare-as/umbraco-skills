# Extension Types — Part 2: Menu Item | CMS → Workspaces

## Menu Item | CMS

Create menu items that appear throughout the backoffice, in sidebars, button flyouts, and more.

Menu Item extensions are used together with [Menu](/umbraco-cms/customizing/extending-overview/extension-types/menu) extensions. Menu items can be added to custom menus, sidebars, and even the built-in Umbraco menus. Developers can either use the default Menu Item component or create custom Menu Item elements and register them as extensions.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f1f63f6aa159b46b6713fa84fc5e2d4572f51b5e%252Fmenu-item.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c3d98864&sv=2)

Menu Item extensions can be defined either with JSON in `umbraco-package.json`

or with JavaScript/TypeScript.

To add custom menu items, define a single `menuItem`

manifest and link an element to it. Inside that element, you can fetch data and render as many menu items as needed based on that data.

Extension authors define the menu manifest, then register it dynamically/during runtime using a [Backoffice Entry Point](/umbraco-cms/customizing/extending-overview/extension-types/backoffice-entry-point) extension.

The `menuItem`

extension type accepts an optional `entityType`

property. When set, this property automatically links the menu item to the matching workspace and shows any registered Entity Actions for that entity type.

The Umbraco backoffice streamlines displaying menu items by providing three kinds that extension authors can reuse. These menu item kinds cover common tasks, including registering `links`

, `actions`

, and `trees`.


Use a link menu item to navigate to another location, typically external URLs.

Developers can use an action menu item when they want to execute custom logic that runs when the item is clicked. This kind is similar to the default menu item but does not support `entityType`

, and therefore does not automatically link to workspaces or Entity Actions.

Use a tree menu item to show a submenu based on a tree structure. Any existing, registered Tree Repositories can be referenced by its extension alias (`treeAlias`

property) in the Menu Item manifest. This will render a fully functional tree-based menu.

To display tree items at the root level without a parent folder node, add `hideTreeRoot: true`

to the menu item's meta:

The `hideTreeRoot`

property must be set on the menuItem manifest, not the tree manifest.

**Note:** You do not need a custom menu item subclass to display menu item extensions. Creating a custom class is optional.

To render custom menu items, developers can use the . This component supports nested menu structures with minimal markup.

`<uui-menu-item>`

elements accept a `has-children`

boolean attribute, which shows a caret icon to indicate nested items. When using Lit, you can bind this with the `?`

directive, for example: `?has-children=${boolVariable}`.


Custom elements can fetch data and render menu items using markup like the example above. Storing fetched results in a `@state()`

property ensures the component re-renders whenever the value changes.

**Note:** Extension authors can use the `kind`

property to define the type of menu item. Supported values include `tree`

and `list`.


Developers can add their own menu items to the built-in Umbraco menus.

Examples of built-in menus include:

Content -

`Umb.Menu.Content`

Media -

`Umb.Menu.Media`

Settings -

`Umb.Menu.StructureSettings`

Templating -

`Umb.Menu.Templating`

And so on.


You can find all available Umbraco menus (nine in total) using the Extension Insights browser by selecting **Menu** from the dropdown.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-15450daf90164075918b418ad2a1f87657c8a150%252Fextension-types-backoffice-browser.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=998cfbe&sv=2)

To add a menu item to an existing menu, use the `meta.menus`

property.

Last updated

Was this helpful?

---


## Menu | CMS

Create menus that appear throughout the backoffice, including in sidebars and button flyouts.

Last updated

Was this helpful?

Create menus that appear throughout the backoffice, including in sidebars and button flyouts.

Menu extensions contain one or more [menu item extensions](/umbraco-cms/customizing/extending-overview/extension-types/menu-item) and can appear throughout the backoffice, such as in sidebars and flyouts.

Creating a custom menu

Menu extensions can be created using either JSON or TypeScript. Both approaches are shown below.

Extension authors define the menu manifest, then register it dynamically/during runtime using a [Backoffice Entry Point](/umbraco-cms/customizing/extending-overview/extension-types/backoffice-entry-point) extension.

See Also

[Section Sidebar](/umbraco-cms/customizing/extending-overview/extension-types/sections/section-sidebar)for information on creating menus for navigation within section extensions.[Menu Item](/umbraco-cms/customizing/extending-overview/extension-types/menu-item)for information on creating menu items.

Last updated

Was this helpful?

Was this helpful?

umbraco-package.json

```
{
    "$schema": "../../umbraco-package-schema.json",
    "name": "My Package",
    "version": "0.1.0",
    "extensions": [
        {
            "type": "menu",
            "alias": "My.Menu",
            "name": "My Menu"
        }
    ]
}
```

my-menu/manifests.ts

```
import type { ManifestMenu } from '@umbraco-cms/backoffice/menu';

export const menuManifest: ManifestMenu = {
    type: 'menu',
    alias: 'My.Menu',
    name: 'My Menu'
};
```

entrypoints/entrypoints.ts

```
import type {
    UmbEntryPointOnInit,
} from "@umbraco-cms/backoffice/extension-api";
import { umbExtensionsRegistry } from "@umbraco-cms/backoffice/extension-registry";
import { menuManifest } from "./../my-menu/manifests.ts";

export const onInit: UmbEntryPointOnInit = (_host, _extensionRegistry) => {
    console.log("Hello from my extension 🎉");

    umbExtensionsRegistry.register(menuManifest);
};
```

---


## Modals

### Contents

- [Custom Modals | CMS](#custom-modals-cms)
- [Modal Route Registration | CMS](#modal-route-registration-cms)

---

### Custom Modals | CMS

New modals can be added to the system via the extension registry.

This article goes through adding new modals to the system. There are three steps to creating a custom modal:

Create a modal element

Declare an Extension Manifest

(Optional) Create a Modal Token


After completing these steps, refer to the example on how to open the modal.

A modal element is a web component that is used to render a modal. It should implement the `UmbModalExtensionElement`

interface. The modal context is injected into the element when the modal is opened in the `modalContext`

property. The modal context is used to close the modal, update the value and submit the modal.

Additionally, the modal element can see its data parameters through the `modalContext`

property. In this example, the modal data is of type `MyModalData`

, and the modal value is of type `MyModalValue`

. The modal context is of type `UmbModalContext<MyModalData, MyModalValue>`

. We are using the data to render a headline and the value to update the value and submit the modal.

```
import { customElement, html, property } from '@umbraco-cms/backoffice/external/lit';
import { UmbLitElement } from '@umbraco-cms/backoffice/lit-element';
import { UmbModalExtensionElement } from '@umbraco-cms/backoffice/modal';
import type { UmbModalContext } from '@umbraco-cms/backoffice/modal';
import type { MyModalData, MyModalValue } from './my-modal.token.js';

@customElement('my-dialog')
export class MyDialogElement
    extends UmbLitElement
    implements UmbModalExtensionElement<MyModalData, MyModalValue> {

    @property({ attribute: false })
    modalContext?: UmbModalContext<MyModalData, MyModalValue>;

    @property({ attribute: false })
    data?: MyModalData;

    private _handleCancel() {
        this.modalContext?.submit();
    }

    private _handleSubmit() {
        this.modalContext?.updateValue({ myData: 'hello world' });
        this.modalContext?.submit();
    }

    render() {
        return html`
            <div>
                <h1>${this.modalContext?.data.headline ?? 'Default headline'}</h1>
                <button @click=${this._handleCancel}>Cancel</button>
                <button @click=${this._handleSubmit}>Submit</button>
            </div>
        `;
    }
}

export const element = MyDialogElement;
```

The class must be exported as an `element`

or `default`

for the Extension Registry to be able to pick up the class.

The modal element needs to be registered in the extension registry. This is done by defining the modal in the manifest file. The `element`

property should point to the file that contains the modal element.

For type safety, it's recommended to use Modal Tokens. Using a Modal Token gives knowledge about the data that can be parsed to the Modal and as well as the type of the value coming back when submitted.

A Modal Token works as a constant that identifies the modal. It is used to open the modal and knows the types of the modal data and modal value. As well, it can contain a preset, containing default data and modal options.

The first argument passed to `UmbModalToken`

is the extension alias; the second is the preset configuration.

A modal token is a generic type that takes two arguments(`<MyModalData, MyModalValue>`

):

The first defines the type of data passed to the modal when opened.

The second defines the type of value returned when the modal is submitted.


To open the modal, call the `umbOpenModal`

method with the Modal Token and data of choice:

The Promise of `umbOpenModal`

is caught if it gets rejected. This is because if the Model gets closed without submission, the Promise is rejected. YThis can be used to carry out a certain action if the modal is cancelled. In this case, `undefined`

is returned when the Modal is cancelled (rejected).

Last updated

Was this helpful?

---

### Modal Route Registration | CMS

You can register modals with a route, making it possible to link directly to that specific modal. This also means the user can navigate back and forth in the browser history

Last updated

Was this helpful?

You can register modals with a route, making it possible to link directly to that specific modal. This also means the user can navigate back and forth in the browser history

A modal can be registered via the `UmbModalRouteRegistrationController`

. The registration accepts a modal token (or extension alias).

```
this.myModalRegistration = new UmbModalRouteRegistrationController(
    this,
    UMB_LINK_PICKER_MODAL
)
    .onSubmit((submitData) => {
        console.log("Modal submitted with data".submitData);
    })
    .observeRouteBuilder((routeBuilder) => {
        this._modalRouteBuilder = routeBuilder;
    });
```

The registration holds an instance of its `UmbModalHandler`

when the modal is active. The modal registration accepts 4 different callbacks:

`onSetup`

- called when the modal is opened`onSubmit`

- called when the modal is submitted`onReject`

- called when the modal is rejected`observeRouteBuilder`

- called when the modal route changes. Use the given route builder to build a route to open the modal

**Additional features of the route Registration:**

Adds unique parts to the path.

A modal registered in a dashboard can be setup in few steps

A modal registered in a property editor needs to become specific for the property and the variant of that property.

Builds some data for the setup.

Rejects a modal by returning false in setup.

Uses a parameter as part of the setup to determine the data going to the modal.


Modal registration for UI as part of a Property Editor

When configuring a routed modal from a Property Editor, it's important to be aware of some facts. Those facts are that the Property Editor shares the same URL path as other Property Editors. This means we need to ensure the registration is unique so it doesn't collide with other Property Editors. To do so we will make use of the Property Alias and the Variant ID.

**Generate the URL to a Modal Route Registration**

The Modal registration has an option to retrieve a URL Builder. This is a function that can be used to generate a URL to a modal:

The `modalLink`

from above could look like this: `/umbraco/backoffice/my/location/modal/Our.Modal.SomethingPicker/my-input-alias`


Notice the Property Editor registration will add the property alias and variant ID to the URL, so it becomes:

`/umbraco/backoffice/my/location/modal/Our.Modal.SomethingPicker/my-property-alias/en-us/my-input-alias`


Last updated

Was this helpful?

Was this helpful?

```


	@property()
	public set alias(value: string | undefined) {
		this.myModalRegistration.setUniquePathValue('propertyAlias', value);
	}

	@property()
	public set variantId(value: string | UmbVariantId | undefined) {
		this.myModalRegistration.setUniquePathValue('variantId', value?.toString());
	}

	private _items = [
		{ name: 'Item 1' },
		{ name: 'Item 2' },
		{ name: 'Item 3' },
	]


	constructor() {
		super();

		this.myModalRegistration = new UmbModalRouteRegistrationController(
			this,
			MY_MODAL_TOKEN
		)
		.addAdditionalPath(`:index`)
		.addUniquePaths(['propertyAlias', 'variantId'])
		.onSetup((params) => {
			// Get item index:
			const indexParam = params.index;
			if (!indexParam) return false;
			let index: number | null = parseInt(params.index);
			if (Number.isNaN(index)) return false;

			// Use the index to find data:
			let data = null;
			if (index >= 0 && index < this._items.length) {
				data = this._items[index];
			} else {
				// If not then make a new pick:
				index = null;
			}

			return {
				index: index,
				itemData: {
					name: data?.name
				},
			};
		})
		.onSubmit((submitData) => {
			if (!submitData) return;
			this._items[submitData.index] = submitData.itemData;
		})
		.observeRouteBuilder((routeBuilder) => {
			this._modalRouteBuilder = routeBuilder;
		});
	}

	render() {
		return html`
			${this._items?.map((item, index) =>
				html`<uui-button look="placeholder" label="Edit item ${index}" .href=${this._modalRouteBuilder?.({ index })}>Add</uui-button>`
			)}
		`;
	}
```

```
const modalLink = _myUrlBuilder?.({ alias: "my-input-alias" });
```

---

---


## Property Editor Schema | CMS

Reference documentation for the propertyEditorSchema extension type

Manifest Structure

Basic Example

```
import type { ManifestPropertyEditorSchema } from '@umbraco-cms/backoffice/property-editor';

export const manifest: ManifestPropertyEditorSchema = {
    type: 'propertyEditorSchema',
    name: 'Text Box',
    alias: 'Umbraco.TextBox',
    meta: {
        defaultPropertyEditorUiAlias: 'Umb.PropertyEditorUi.TextBox',
    },
};
```

Example with Configuration

Manifest Properties

Required Properties

| Property | Type | Description |
|---|---|---|
| type | string | Must be `"propertyEditorSchema"` . |
| alias | string | Unique identifier for the schema. Must match the C# `DataEditor` alias. |
| name | string | Friendly name displayed in the backoffice. |
| meta | object | Metadata object containing schema configuration (see Meta Properties below). |

Optional Properties

| Property | Type | Description |
|---|---|---|
| weight | number | Ordering weight. Higher numbers appear first in lists. |
| kind | string | Optional kind identifier for grouping related schemas. |

Meta Properties

Required Meta Properties

| Property | Type | Description |
|---|---|---|
| defaultPropertyEditorUiAlias | string | The alias of the default Property Editor UI to use with this schema. |

Optional Meta Properties

| Property | Type | Description |
|---|---|---|
| settings | object | Configuration settings for the property editor (see Settings below). |

Settings Structure

Settings Properties Array

| Property | Type | Required | Description |
|---|---|---|---|
| alias | string | Yes | Unique identifier. Must match the C# `ConfigurationEditor` property name. |
| label | string | Yes | Display label for the configuration field. |
| description | string | No | Help text shown below the label. |
| propertyEditorUiAlias | string | Yes | The Property Editor UI to use for editing this configuration value. |
| config | object | No | Optional configuration to pass to the Property Editor UI. |
| weight | number | No | Optional ordering weight for the configuration field. |

Settings Default Data Array

| Property | Type | Required | Description |
|---|---|---|---|
| alias | string | Yes | The alias of the configuration property. |
| value | unknown | Yes | The default value for this configuration. |

Complete Example

Important Notes

Related Documentation

Last updated

Was this helpful?

---


## Property Editor UI | CMS

Reference documentation for the propertyEditorUi extension type

Manifest Structure

Basic Example

```
import type { ManifestPropertyEditorUi } from '@umbraco-cms/backoffice/property-editor';

export const manifest: ManifestPropertyEditorUi = {
    type: 'propertyEditorUi',
    alias: 'My.PropertyEditorUi.TextBox',
    name: 'My Text Box Property Editor UI',
    element: () => import('./my-text-box.element.js'),
    meta: {
        label: 'My Text Box',
        propertyEditorSchemaAlias: 'Umbraco.TextBox',
        icon: 'icon-autofill',
        group: 'common',
    },
};
```

Example with Settings

Manifest Properties

Required Properties

| Property | Type | Description |
|---|---|---|
| type | string | Must be `"propertyEditorUi"` . |
| alias | string | Unique identifier for the UI. |
| name | string | Friendly name displayed in the backoffice. |
| element | function | string | Path to or import function for the web component element. |
| meta | object | Metadata object containing UI configuration (see Meta Properties). |

Optional Properties

| Property | Type | Description |
|---|---|---|
| weight | number | Ordering weight. Higher numbers appear first in lists. |

Meta Properties

Required Meta Properties

| Property | Type | Description |
|---|---|---|
| label | string | Display label shown in the UI picker. |
| propertyEditorSchemaAlias | string | The alias of the Property Editor Schema this UI works with. |
| icon | string | Icon identifier (e.g., `"icon-autofill"` ). |
| group | string | Group name for categorizing property editors. |

Optional Meta Properties

| Property | Type | Description |
|---|---|---|
| settings | object | Configuration settings for the UI (see Settings below). |
| supportsReadOnly | boolean | Indicates whether the UI supports read-only mode. |

Settings Structure

Settings Properties Array

| Property | Type | Required | Description |
|---|---|---|---|
| alias | string | Yes | Unique identifier for this configuration property. |
| label | string | Yes | Display label for the configuration field. |
| description | string | No | Help text shown below the label. |
| propertyEditorUiAlias | string | Yes | The Property Editor UI to use for editing this configuration value. |
| config | object | No | Optional configuration to pass to the Property Editor UI. |
| weight | number | No | Ordering weight for the configuration field. Higher numbers appear first. |
| validation | object | No | Validation rules. Object with `mandatory` (boolean) and optional `mandatoryMessage` (string) properties. |
| propertyEditorDataSourceAlias | string | No | Alias of a data source to use with this configuration property. |

Settings Default Data Array

| Property | Type | Required | Description |
|---|---|---|---|
| alias | string | Yes | The alias of the configuration property. |
| value | unknown | Yes | The default value for this configuration. |

Element Loading

Import Function (Recommended)

String Path

Class Constructor

Complete Example

Icon Names

Group Names

Read-Only Support

Important Notes

Related Documentation

Last updated

Was this helpful?

---


## Property Value Preset | CMS

Provide a preset value for a Property.

The Property Value Preset is an Extension Type that uses an API to provide a Preset Value. The preset value is used when a user scaffolds a new set of Content.

Before creating a Property Value Preset, it is recommended to read about the [Extension Registry in Umbraco](/umbraco-cms/customizing/extending-overview/extension-registry/register-extensions) to understand how extensions work.

The following Manifest declares a preset for the `TextBox`

Property Editors:

```
export const manifest = {
    type: 'propertyValuePreset',
    alias: 'my.propertyValuePreset.TextBox',
    name: 'My Property Value Preset for TextBox',
	weight: 10,
    api: () => import('./my-property-value-preset.js'),
    forPropertyEditorUiAlias: 'Umb.PropertyEditorUi.TextBox'
}
```

`weight`

- Execution order (higher runs first).`forPropertyEditorUiAlias`

- Targets specific Property Editor UI.

A Property Preset Value API could look like this:

This API will set the value to "Hello there" for all properties using the `Umb.PropertyEditorUi.TextBox`

Property Editor UI and all properties based on Schema `Umbraco.TextArea`.


You can also choose to target your Preset for a [Property Editor Schema](/umbraco-cms/tutorials/creating-a-property-editor/adding-server-side-validation/default-property-editor-schema-aliases) .

Define `forPropertyEditorSchemaAlias`

to show the Preset Value for all Properties based on that Schema.

If both `forPropertyEditorSchemaAlias`

and `forPropertyEditorUiAlias`

are defined, it will not limit the target. The matching is independently for each of them.

Notice that `forPropertyEditorSchemaAlias`

only targets the Properties used on the Content Type based data. This could affect Documents, Media, Members, and Blocks, and not properties of a Data Type Configuration.

The `processValue`

method takes four arguments:

`value`

- The current value.`UmbPropertyEditorConfig`

- The Data Type configuration.`UmbPropertyTypePresetModelTypeModel`

- The type arguments, which contains details such as whether the property is mandatory, and how it varies by culture and segment.`UmbPropertyValuePresetApiCallArgs`

- The call arguments, which contains details about the property and document.

The following example is the built-in Property Value Preset for the Umbraco Toggle. The Toggle Data Type has a 'preset state' configuration that is used as the value of the Toggle.

The `processValue`

method is async. You can request the server or use the Context-API to retrieve the necessary information to construct your value.

It is recommended to use the `getContext`

method for retrieving contexts. The method includes a timeout feature that prevents the preset from getting stuck if the context is unavailable during reset.

Because the `processValue`

method takes a value as its first argument, you can append the value constructed by other Presets. In this way, multiple Presets can shape the preset value for a property.

In the case of multiple Property Value Presets targeting the same Property. The `weight`

of the Manifest determines the order they are executed.

This opens up for you to overwrite or alter the Preset Value for Properties that use a Built-in Property Value Preset.

Last updated

Was this helpful?

---


## Sections

### Contents

- [Section Sidebar | CMS](#section-sidebar-cms)
- [Section View | CMS](#section-view-cms)
- [Section | CMS](#section-cms)

---

### Section Sidebar | CMS

Use Section Sidebar extensions to add navigation, coordinate Section Views, and provide additional functionality inside Section extensions.

Manifest Properties

| Property | Type | Required | Description |
|---|---|---|---|
| `type` | string | Yes | Must be `sectionSidebarApp` . |
| `alias` | string | Yes | A unique identifier for this extension. |
| `name` | string | Yes | A human-readable name shown in Extension Insights. |
| `weight` | number | No | Controls the display order when multiple sidebar apps are registered in the same section. Higher values display higher in the sidebar. |
`kind` | string | No | Inherit a preset configuration, for example, `menu` . See
|
`element` | string | No | Path to a custom web component file. |
`elementName` | string | No | The custom element tag name (if not a default export). |
`meta` | object | No | Additional configuration depending on the `kind` used. |
`conditions` | array | No | Conditions that must pass for the app to appear. See
|

`overwrites`

Section Sidebar Apps

Custom Sidebar App Example

Menu Sidebar App Examples

Coordinating subviews with menu items

Adding items to an existing menu

Last updated

Was this helpful?

---

### Section View | CMS

Add auxiliary views to your own Umbraco packages, or to other areas of the Umbraco backoffice.

Creating a custom Section View

Registering Section View extensions

Registering by manifest

Lit Element

Adding Section Views to your own package

Adding Section Views to somewhere else in the backoffice

| Section Aliases |
|---|
| Umb.Section.Content |
| Umb.Section.Media |
| Umb.Section.Settings |
| Umb.Section.Packages |
| Umb.Section.Users |
| Umb.Section.Members |
| Umb.Section.Translation |

Last updated

Was this helpful?

---

### Section | CMS

Introducing Section extensions, a home for custom content and functionality.

**Creating a section**

**Manifests**

**Group permissions**

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-bad7898e2ac835b2bb12b19c1b109ceda80ba9cd%252Fsections-assigning.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f4bde078&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-62299525623c4735504b91352d048ec2148b5ce9%252Fsection-empty.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7e7b8893&sv=2)

**Extend with Sidebar, Dashboards, and more**

**Manifest with empty element**

Last updated

Was this helpful?

Introducing Section extensions, a home for custom content and functionality.

Umbraco extension authors can place their extension in the top-level navigation of the backoffice using Sections. The extension will be placed among the default options such as Content, Media, Settings, etc.

Within the section, authors can add menus, section views, workspace views, or any other content or interface they desire.

Sections can be created by adding a definition in the extension's manifest file.

To enable custom sections for backoffice users, site administrators must first assign permissions to those users. This involves configuring the permission for a user group and assigning users to that group.

To grant access to the custom section, open the Umbraco backoffice, navigate to the **Users** section, and select the **User groups** menu item. Site administrators can create a new user group or modify an existing one.

Once the user group is open, click the **Choose** button under the Sections section. Select the custom section from the slide-out modal to enable access.

After assigning permission, users may need to reload the backoffice for the changes to take effect.

Sections serve as blank canvases within the Umbraco backoffice. Extension authors can integrate other Umbraco extensions into sections, including [custom dashboards](/umbraco-cms/tutorials/creating-a-custom-dashboard), [sidebars](/umbraco-cms/customizing/extending-overview/extension-types/sections/section-sidebar), and [section views](/umbraco-cms/customizing/extending-overview/extension-types/sections/section-view).

Section authors can also skip Umbraco backoffice components and build a fully custom view by creating an empty element.

Using a manifest with only an element is not recommended if you are shipping this as a package. This approach limits the Section to a single element. Instead, use a Dashboard or Section View for your main view, which allows additional Dashboards or Section Views to be added to the Section.

The element file must contain an `element`

, a `default`

export, or specify the element name in the `elementName`

field.

Last updated

Was this helpful?

Was this helpful?

umbraco-package.json

```
{
 "type": "section",
 "alias": "My.Section",
 "name": "My Section",
 "meta": {
  "label": "My.Section",
  "pathname": "my-section"
 }
}
```

manifests.ts

```
const section : UmbExtensionManifest = {
    type: "section",
    alias: "Empty.Section",
    name : 'Empty Section',
    element : () => import('./empty-section.element.js'),
    meta : {
        label : 'Empty Section',
        pathname : 'empty-section'
    }
}
```

---

---


## Tree

### Contents

- [Tree Models | CMS](#tree-models-cms)
- [Tree Repository | CMS](#tree-repository-cms)
- [Trees & Workspaces | CMS](#trees-workspaces-cms)

---

### Tree Models | CMS

Understanding Tree Item and Root models in Umbraco

UmbTreeItemModel

```
interface UmbTreeItemModel {
  unique: string;        // Identifier for selection, navigation, and API calls
  entityType: string;    // Must match Workspace meta.entityType for navigation
  name: string;          // Display name shown in the tree
  hasChildren: boolean;  // Shows expand arrow when true
  isFolder: boolean;     // Visual styling hint
  icon?: string;         // Icon name (e.g., 'icon-document', 'icon-folder')
  parent?: {             // Parent reference for hierarchy and breadcrumbs
    unique: string;      // Parent's identifier
    entityType: string;  // Parent's entity type
  };
}
```

Extending the Model

```
import type { UmbTreeItemModel } from '@umbraco-cms/backoffice/tree';

export interface MyTreeItemModel extends UmbTreeItemModel {
  // Add custom properties
  status: 'draft' | 'published';
  lastModified: string;
}
```

UmbTreeRootModel

Defining a Root Model

Entity Types

Related

Last updated

Was this helpful?

Understanding Tree Item and Root models in Umbraco

Trees use two model types to represent data: **Tree Item Model** for individual nodes and **Tree Root Model** for the root node. Your [Repository](/umbraco-cms/customizing/extending-overview/extension-types/tree/tree-repository) returns these models from its methods.

UmbTreeItemModel

The base interface for Tree Items. All Tree Items must include these properties:

```
interface UmbTreeItemModel {
  unique: string;        // Identifier for selection, navigation, and API calls
  entityType: string;    // Must match Workspace meta.entityType for navigation
  name: string;          // Display name shown in the tree
  hasChildren: boolean;  // Shows expand arrow when true
  isFolder: boolean;     // Visual styling hint
  icon?: string;         // Icon name (e.g., 'icon-document', 'icon-folder')
  parent?: {             // Parent reference for hierarchy and breadcrumbs
    unique: string;      // Parent's identifier
    entityType: string;  // Parent's entity type
  };
}
```

Extending the Model

Add custom properties by extending the base interface:

```
import type { UmbTreeItemModel } from '@umbraco-cms/backoffice/tree';

export interface MyTreeItemModel extends UmbTreeItemModel {
  // Add custom properties
  status: 'draft' | 'published';
  lastModified: string;
}
```

Your repository methods transform API responses into these models when returning data.

UmbTreeRootModel

The root model represents the top-level node of your Tree. It extends `UmbTreeItemModel`

but typically has `unique: null`:


Defining a Root Model

The root model is returned by `requestTreeRoot()`

in your [Tree Repository](/umbraco-cms/customizing/extending-overview/extension-types/tree/tree-repository).

Entity Types

You typically define two entity types - one for the root and one for items:

The `entityType`

values must match the values in your Workspace and Tree Item Manifests. See [Trees & Workspaces](/umbraco-cms/customizing/extending-overview/extension-types/tree/trees-and-workspaces) for how these connect.

Related

[Tree Repository](/umbraco-cms/customizing/extending-overview/extension-types/tree/tree-repository)- Returns Tree models from its methods.[Trees & Workspaces](/umbraco-cms/customizing/extending-overview/extension-types/tree/trees-and-workspaces)- How`entityType`

connects to Workspaces.

Last updated

Was this helpful?

Was this helpful?

```
interface UmbTreeRootModel extends UmbTreeItemModel {
  unique: null;  // Root has no parent, so unique is null
}
```

```
import type { UmbTreeRootModel } from '@umbraco-cms/backoffice/tree';

export interface MyTreeRootModel extends UmbTreeRootModel {
  // Root-specific properties if needed
}

// Example root data returned by repository
const rootData: MyTreeRootModel = {
  unique: null,
  entityType: 'my-tree-root',
  name: 'My Tree',
  hasChildren: true,
  isFolder: true,
  icon: 'icon-folder',
};
```

```
// types.ts
export const MY_TREE_ROOT_ENTITY_TYPE = 'my-tree-root';
export const MY_TREE_ITEM_ENTITY_TYPE = 'my-tree-item';

export interface MyTreeRootModel extends UmbTreeRootModel {
  entityType: typeof MY_TREE_ROOT_ENTITY_TYPE;
}

export interface MyTreeItemModel extends UmbTreeItemModel {
  entityType: typeof MY_TREE_ITEM_ENTITY_TYPE;
}
```

---

### Tree Repository | CMS

Interface

```
interface UmbTreeRepository {
  requestTreeRoot();
  requestTreeRootItems();
  requestTreeItemsOf();
  requestTreeItemAncestors();
}
```

Registering the Repository

```
{
  type: 'repository',
  alias: 'My.Tree.Repository',
  name: 'My Tree Repository',
  api: () => import('./my-tree.repository.js'),
}
```

Implementing a Tree Repository

Static Data Example

Related

Last updated

Was this helpful?

A Tree Repository provides data to populate your Tree. It implements methods to return the root, root items, children of items, and ancestors.

The repository is referenced by your Tree Manifest via `meta.repositoryAlias`.


Interface

The `UmbTreeRepository`

interface defines the methods your repository must implement:

```
interface UmbTreeRepository {
  requestTreeRoot();
  requestTreeRootItems();
  requestTreeItemsOf();
  requestTreeItemAncestors();
}
```

See the full interface in the .

Registering the Repository

Register the Repository in your Manifest:

```
{
  type: 'repository',
  alias: 'My.Tree.Repository',
  name: 'My Tree Repository',
  api: () => import('./my-tree.repository.js'),
}
```

Implementing a Tree Repository

Extend `UmbControllerBase`

and implement the `UmbTreeRepository`

interface.

Static Data Example

Related

[Tree Models](/umbraco-cms/customizing/extending-overview/extension-types/tree/tree-models)-`UmbTreeItemModel`

and`UmbTreeRootModel`

interfaces.[Trees & Workspaces](/umbraco-cms/customizing/extending-overview/extension-types/tree/trees-and-workspaces)- How Tree clicks navigate to Workspaces.[Trees](/umbraco-cms/customizing/extending-overview/extension-types/tree)- Main Tree extension documentation.

Last updated

Was this helpful?

Was this helpful?

static-tree.repository.ts

```
import { UmbControllerBase } from "@umbraco-cms/backoffice/class-api";
import type { UmbApi } from "@umbraco-cms/backoffice/extension-api";
import type { UmbTreeRepository } from "@umbraco-cms/backoffice/tree";

const staticItems = [
  {
    unique: "1",
    entityType: "my-item",
    parent: { unique: null, entityType: "my-root" },
    name: "First Item",
    hasChildren: false,
    isFolder: false,
    icon: "icon-document",
  },
  {
    unique: "2",
    entityType: "my-item",
    parent: { unique: null, entityType: "my-root" },
    name: "Second Item",
    hasChildren: false,
    isFolder: false,
    icon: "icon-document",
  },
];

export class MyStaticTreeRepository
  extends UmbControllerBase
  implements UmbTreeRepository, UmbApi
{
  async requestTreeRoot() {
    return {
      data: {
        unique: null,
        entityType: "my-root",
        name: "My Static Tree",
        hasChildren: true,
        isFolder: true,
        icon: "icon-folder",
      },
    };
  }

  async requestTreeRootItems() {
    const items = staticItems.filter((item) => item.parent.unique === null);
    return { data: { items, total: items.length } };
  }

  async requestTreeItemsOf(args) {
    const items = staticItems.filter(
      (item) => item.parent.unique === args.parent.unique
    );
    return { data: { items, total: items.length } };
  }

  async requestTreeItemAncestors() {
    // Implement as needed
    return { data: [] };
  }
}

export { MyStaticTreeRepository as api };
```

---

### Trees & Workspaces | CMS

How Tree Items navigate to Workspaces when clicked in Umbraco

How Tree Items Connect to Workspaces

Workspace Kind: Routable vs Default

```
// Tree Item Manifest
{
    type: 'treeItem',
    kind: 'default',
    alias: 'My.TreeItem',
    forEntityTypes: ['my-custom-item'],
}

// Workspace Manifest - MUST be routable for Tree navigation
{
    type: 'workspace',
    kind: 'routable',
    alias: 'My.Workspace',
    name: 'My Custom Item Workspace',
    api: () => import('./my-custom-item-workspace.api.js'),
    meta: {
        entityType: 'my-custom-item',  // Must match Tree Item entityType
    },
}
```

Common Issues

Related

Last updated

Was this helpful?

How Tree Items navigate to Workspaces when clicked in Umbraco

Trees and Workspaces are tightly coupled. When users click a Tree Item, Umbraco navigates to a Workspace to edit that item. This connection is established through the `entityType`

, a string identifier that links Tree Items to their corresponding Workspace.

How Tree Items Connect to Workspaces

When you click a Tree Item:

Umbraco reads the

`entityType`

from the Tree Item data.It navigates to the edit Workspace URL, passing the items

`unique`

identifier.

Workspace Kind: Routable vs Default

To support different routes for new and existing items, your Workspace must be routable to have different routes for each case. Use `kind: 'routable'`

and set up matching routes in your Workspace API:

```
// Tree Item Manifest
{
    type: 'treeItem',
    kind: 'default',
    alias: 'My.TreeItem',
    forEntityTypes: ['my-custom-item'],
}

// Workspace Manifest - MUST be routable for Tree navigation
{
    type: 'workspace',
    kind: 'routable',
    alias: 'My.Workspace',
    name: 'My Custom Item Workspace',
    api: () => import('./my-custom-item-workspace.api.js'),
    meta: {
        entityType: 'my-custom-item',  // Must match Tree Item entityType
    },
}
```

Common Issues

**Endless loading when clicking Tree Items?** This usually means:

No Workspace is registered for that

`entityType`

.The

`entityType`

in your Tree data doesn't match the Workspace's`meta.entityType`

. -

Related

[Trees](/umbraco-cms/customizing/extending-overview/extension-types/tree)- Main Tree extension documentation.- Creating Workspace extensions.


Last updated

Was this helpful?

Was this helpful?

---

---


## Workspaces

### Contents

- [Workspace Action Menu Items | CMS](#workspace-action-menu-items-cms)
- [Workspace Context | CMS](#workspace-context-cms)
- [Workspace Actions | CMS](#workspace-actions-cms)
- [Workspace Footer Apps | CMS](#workspace-footer-apps-cms)
- [Workspace Views | CMS](#workspace-views-cms)

---

### Workspace Action Menu Items | CMS

Learn how to create workspace action menu items that extend workspace actions with additional functionality.

Manifest

```
{
	type: 'workspaceActionMenuItem',
	kind: 'default',
	alias: 'example.workspaceActionMenuItem.resetCounter',
	name: 'Reset Counter Menu Item',
	api: () => import('./reset-counter-menu-item.action.js'),
	forWorkspaceActions: 'example.workspaceAction.incrementor',
	weight: 100,
	meta: {
		label: 'Reset Counter',
		icon: 'icon-refresh',
	},
}
```

Key Properties

Kinds

default

previewOption

Implementation

Action Relationship

Primary Action

Menu Item Extensions

Last updated

Was this helpful?

---

### Workspace Context | CMS

Workspace Contexts manages shared state and enables communication between extensions in a workspace.

Purpose

Manifest

```
{
	type: 'workspaceContext',
	name: 'Example Counter Workspace Context',
	alias: 'example.workspaceContext.counter',
	api: () => import('./counter-workspace-context.js'),
	conditions: [
		{
			alias: UMB_WORKSPACE_CONDITION_ALIAS,
			match: 'Umb.Workspace.Document',
		},
	],
}
```

API Implementation

Context Token

Extension Communication

Workspace Action

Workspace View

Last updated

Was this helpful?

---

### Workspace Actions | CMS

Learn how to create workspace actions that provide primary user interactions within workspace environments.

Purpose

Manifest

```
{
	type: 'workspaceAction',
	kind: 'default',
	name: 'Example Count Incrementor Workspace Action',
	alias: 'example.workspaceAction.incrementor',
	weight: 1000,
	api: () => import('./incrementor-workspace-action.js'),
	meta: {
		label: 'Increment',
		look: 'primary',
		color: 'danger',
	},
	conditions: [
		{
			alias: UMB_WORKSPACE_CONDITION_ALIAS,
			match: 'Umb.Workspace.Document',
		},
	],
}
```

Key Properties

Implementation

Workspace Integration

Context Access

Execution Lifecycle

Conditional Execution

Action Menu Integration

Action Events

Event Characteristics

Listening for Action Events

When to Use Events

Common Patterns

Entity Operations

State-Dependent Actions

Multi-Step Operations

Best Practices

Action Availability

Visual Hierarchy

Context Dependencies

Last updated

Was this helpful?

---

### Workspace Footer Apps | CMS

Learn how to create workspace footer apps that provide persistent status information and contextual data in workspace environments.

Purpose

Manifest

```
{
	type: 'workspaceFooterApp',
	alias: 'example.workspaceFooterApp.counterStatus',
	name: 'Counter Status Footer App',
	element: () => import('./counter-status-footer-app.element.js'),
	weight: 900,
	conditions: [
		{
			alias: UMB_WORKSPACE_CONDITION_ALIAS,
			match: 'Umb.Workspace.Document',
		},
	],
}
```

Key Properties

Implementation

Footer App Lifecycle

Initialization

Updates

Common Patterns

Status Indicators

Live Counters

Validation Summary

Best Practices

Performance

Information Density

Context Dependencies

Responsive Design

Visual Consistency

Last updated

Was this helpful?

---

### Workspace Views | CMS

Learn how to create workspace views that provide tab-based content areas for organizing different aspects of entity editing.

Purpose

Manifest

Key Properties

Implementation

Conditions

Built-in Workspace-relevant Conditions

| Alias | Description | Example `match` value |
`Umb.Condition.WorkspaceEntityType` | Requires the workspace to be working on a specific entity type. | `document` , `media` , `member` , `block` , `user` |
`Umb.Condition.WorkspaceAlias` | Restricts the view to a specific workspace. Use the `UMB_WORKSPACE_CONDITION_ALIAS` constant from `@umbraco-cms/backoffice/workspace` for type safety. | `Umb.Workspace.Document` |
`Umb.Condition.WorkspaceContentTypeAlias` | Requires the workspace to be based on a Content Type whose alias matches the value. Use this to target a specific Document Type (for example, only show on Blog Post nodes). | `myCustomDocTypeAlias` |
`Umb.Condition.WorkspaceContentTypeUnique` | Requires the workspace to be based on a Content Type matched by its unique key (GUID). Use this when you need to target a specific Content Type without relying on its alias. | A content type GUID |
`Umb.Condition.SectionAlias` | Restricts the view to a specific section (sidebar area). | `Umb.Section.Content` |
`Umb.Condition.EntityIsTrashed` | Only shows the view if the current entity is in the recycle bin. | No match needed |
`Umb.Condition.EntityIsNotTrashed` | Only shows the view if the current entity is not in the recycle bin. | No match needed |

Targeting a specific Document Type

Custom Conditions

View Lifecycle

Initialization

Tab Navigation

Context Integration

Common Patterns

Entity Information View

Interactive Configuration View

Analytics Dashboard View

Best Practices

View Organization

Context Usage

Performance

Last updated

Was this helpful?

---

---
