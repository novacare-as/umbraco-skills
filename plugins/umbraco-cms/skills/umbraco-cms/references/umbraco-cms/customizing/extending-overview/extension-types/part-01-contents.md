# Extension Types — Part 1: Contents → Localization | CMS

## Contents

- [App Entry Point | CMS](#app-entry-point-cms)
- [Backoffice Entry Point | CMS](#backoffice-entry-point-cms)
- [Block Custom View | CMS](#block-custom-view-cms)
- [Bundle | CMS](#bundle-cms)
- [Collections | CMS](#collections-cms)
- [Extension Conditions | CMS](#extension-conditions-cms)
- [Dashboards | CMS](#dashboards-cms)
- [Entity Actions | CMS](#entity-actions-cms)
- [Entity Bulk Actions | CMS](#entity-bulk-actions-cms)
- [Entity Create Option Action | CMS](#entity-create-option-action-cms)
- [Global Context | CMS](#global-context-cms)
- [Header Apps | CMS](#header-apps-cms)
- [Icons | CMS](#icons-cms)
- [Kinds | CMS](#kinds-cms)
- [Localization | CMS](#localization-cms)
- [Menu Item | CMS](#menu-item-cms)
- [Menu | CMS](#menu-cms)
- [Modals](#modals)
- [Property Editor Schema | CMS](#property-editor-schema-cms)
- [Property Editor UI | CMS](#property-editor-ui-cms)
- [Property Value Preset | CMS](#property-value-preset-cms)
- [Sections](#sections)
- [Tree](#tree)
- [Workspaces](#workspaces)

---


## App Entry Point | CMS

The App Entry Point extension type is used to run some JavaScript code before the user is logged in.

Last updated

Was this helpful?

The App Entry Point extension type is used to run some JavaScript code before the user is logged in.

This manifest declares a single JavaScript file that will be loaded and run when the Backoffice starts. Additionally, the code will also run on the login screen.

See [Backoffice Entry Point](/umbraco-cms/customizing/extending-overview/extension-types/backoffice-entry-point) if you are looking for an Extension that runs when the user is logged in.

It performs the same function as the `backofficeEntryPoint`

extension type, but the difference is that this runs before the user is logged in. Use this to initiate things before the user is logged in or to provide things for the Login screen.

Read more about `backofficeEntryPoint`

to learn how to use it:

Last updated

Was this helpful?

Was this helpful?

---


## Backoffice Entry Point | CMS

The Backoffice Entry Point extension type is used to run some JavaScript code at startup.

```
{
    "name": "Name of your package",
    "alias": "My.Package",
    "extensions": [
        {
         "type": "backofficeEntryPoint",
         "alias": "My.EntryPoint",
         "js": "/App_Plugins/YourFolder/index.js"
        }
    ]
}
```

```
import type { UmbEntryPointOnInit } from '@umbraco-cms/backoffice/extension-api';

/**
 * Perform any initialization logic when the Backoffice starts
 */
export const onInit: UmbEntryPointOnInit = (host, extensionRegistry) => {
    // Your initialization logic here
}

/**
 * Perform any cleanup logic when the Backoffice and/or the package is unloaded
 */
export const onUnload: UmbEntryPointOnUnload = (host, extensionRegistry) => {
    // Your cleanup logic here
}
```

Examples

Register additional UI extensions in the entry point file

Register global CSS

Type IntelliSense

What's next?

Last updated

Was this helpful?

---


## Block Custom View | CMS

Create a custom Web Component to visually represent blocks in Umbraco's Block editors.

Last updated

Was this helpful?

Create a custom Web Component to visually represent blocks in Umbraco's Block editors.

The Block Custom View extension type allows you to define a custom Web Component to visually represent blocks (for example: Block List, Block Grid).

Build a Custom View

Before creating a Block Custom View, make sure you are familiar with the [Extension Registry in Umbraco](/umbraco-cms/customizing/extending-overview/extension-registry/register-extensions). You can also refer to the tutorial [Custom Views for Block List](/umbraco-cms/tutorials/creating-custom-views-for-blocklist) for a step-by-step guide.

Create a Document Type with a property that uses a Block Editor.

Configure at least one Block Type on the Block Editor.

Make sure the Element Type used as the block's Content Model has properties you want to display. For example, a property with alias

`headline`

.Note the

**Element Type**Alias. You will need it shortly.(Optional) Create a

**Settings Model**for the above Element Type if you want to include settings data. For example, add a property with alias`theme`

.Register the custom view in

`umbraco-package.json`

file:

umbraco-package.json

```
{
  "$schema": "../../umbraco-package-schema.json",
  "name": "My.CustomViewPackage",
  "version": "0.1.0",
  "extensions": [
	{
	  "type": "blockEditorCustomView",
	  "alias": "my.blockEditorCustomView.Example",
	  "name": "My Example Custom View",
	  "element": "/App_Plugins/block-custom-view/dist/example-block-custom-view.js",
	  "forContentTypeAlias": "myElementTypeAlias", // your Element Type Alias from Step 4 (e.g. "myHeroBlock")
	  "forBlockEditor": "block-list" // insert block editor type here: "block-list" or "block-grid"
	}
  ]
}
```

The Web Component

The code of your Web Component could look like this:

The TypeScript component (`ExampleBlockCustomView`

) implements `UmbBlockEditorCustomViewElement`

and receives the following reactive properties:

`content`

— the block's content data (for example,`this.content?.headline`

)`settings`

— the block's settings data, if a Settings Model is configured (for example,`this.settings?.theme`

)

These map directly to the properties defined on the Element Type and its Settings Model (if configured).

Last updated

Was this helpful?

Was this helpful?

example-custom-view.ts

```
import { html, customElement, LitElement, property, css } from '@umbraco-cms/backoffice/external/lit';
import { UmbElementMixin } from '@umbraco-cms/backoffice/element-api';
import type { UmbBlockDataType } from '@umbraco-cms/backoffice/block';
import type { UmbBlockEditorCustomViewElement } from '@umbraco-cms/backoffice/block-custom-view';

@customElement('example-block-custom-view')
export class ExampleBlockCustomView extends UmbElementMixin(LitElement) implements UmbBlockEditorCustomViewElement {
	
	@property({ attribute: false })
	content?: UmbBlockDataType;

	@property({ attribute: false })
	settings?: UmbBlockDataType;

	render() {
		return html`
			<h5>My Custom View</h5>
			<p>Headline: ${this.content?.headline}</p>
			<p>Theme: ${this.settings?.theme}</p>
		`;
	}

	static styles = [
		css`
			:host {
				display: block;
				height: 100%;
				box-sizing: border-box;
				background-color: darkgreen;
				color: white;
				border-radius: 9px;
				padding: 12px;
			}
		`,
	];
	
}
export default ExampleBlockCustomView;

declare global {
	interface HTMLElementTagNameMap {
		'example-block-custom-view': ExampleBlockCustomView;
	}
}
```

---


## Bundle | CMS

Gather Extension Manifests in one file

Last updated

Was this helpful?

Gather Extension Manifests in one file

The `bundle`

extension type points to a single JavaScript file that exports or re-exports Extension Manifests written in JavaScript.

It can be used as the entry point for a package, or as a grouping for a set of manifests. A Bundle can reference other Bundles.

Use Bundle as an entry point for a package

If you want to declare your manifests in JavaScript/TypeScript, then Bundle is a great choice.

The following example shows an `umbraco-package.json`

that refers to one bundle, which can then declare manifests.

/App_Plugins/my-package/umbraco-package.json

```
    {
		"name": "My Package Name",
		"version": "1.0.0",
		"extensions": [
			{
				"type": "bundle",
				"alias": "My.Package.Bundle",
				"name": "My Package Bundle",
				"js": "/App_Plugins/my-package/manifests.js"
			}
		]
	}
```

/src/manifests.ts

```
export const manifests: Array<UmbExtensionManifest> = [
	{
		type: 'dashboard',
		name: 'Example Dashboard',
		alias: 'example.dashboard.demo',
		element: () => import('./demo-dashboard.js'),
		weight: 900,
		meta: {
			label: 'Demo example',
			pathname: 'demo-example',
		},
	},
	// ... insert as many manifests as you like
]
```

Ensure you have set up your `tsconfig.json`

to include the `extension-types`

as global types. Like this:

Last updated

Was this helpful?

Was this helpful?

```
{
    "compilerOptions": {...
        "types": [
            "@umbraco-cms/backoffice/extension-types"
        ]
    }
}
```

---


## Collections | CMS

Umbraco Documentation

file-lines Docs Overview

folder-grid CMS

An overview of the available extension types related to collections.

Collection View chevron-right

Previous Workspace Views chevron-left

Next Collection View chevron-right

Last updated 6 months ago

Was this helpful?

### Collection View

### Contents

- [Card View | CMS](#card-view-cms)
- [Custom View | CMS](#custom-view-cms)
- [Reference View | CMS](#reference-view-cms)

---

### Card View | CMS

```
export interface UmbCollectionItemModel {
  unique: string;
  entityType: string;
  name?: string;
  icon?: string;
}
```

Manifest

```
{
  "type": "collectionView",
  "kind": "card",
  "alias": "My.CollectionView.Card",
  "name": "My Card Collection View",
  "conditions": [
    {
      "alias": "Umb.Condition.CollectionAlias",
      "match": "My.Collection" // Collection alias to display this collection view for
    }
  ]
}
```

Custom Card Collection Item

Manifest

Implementation

Last updated

Was this helpful?

When you want to display entities as cards within a collection, use the Card Collection View Kind. This will render a card-style grid layout. Each card renders a default layout with the entity's name and icon. You can further customize the card layout by registering a custom card collection item as needed.

The default Collection Item Model used in a Card Collection View is based on the following interface:

```
export interface UmbCollectionItemModel {
  unique: string;
  entityType: string;
  name?: string;
  icon?: string;
}
```

Register the Card Collection View in the extension registry with the kind set to "card":

Manifest

umbraco-package.json

```
{
  "type": "collectionView",
  "kind": "card",
  "alias": "My.CollectionView.Card",
  "name": "My Card Collection View",
  "conditions": [
    {
      "alias": "Umb.Condition.CollectionAlias",
      "match": "My.Collection" // Collection alias to display this collection view for
    }
  ]
}
```

Custom Card Collection Item

If you want to customize how each item is rendered, you can create and register a custom Card Collection Item.

Manifest

Implementation

Implement your custom Card Collection Item as a Lit element that extends `UmbLitElement`

. This defines how an individual card is rendered in the collection.

Get more information about Card elements and base element starting points at the

Last updated

Was this helpful?

Was this helpful?

umbraco-package.json

```
{
  "type": "entityCollectionItemCard",
  "alias": "My.EntityCollectionItemCard.EntityType",
  "name": "My Entity Type Collection Item Card",
  "element": "/App_Plugins/my-collection/card/my-entity-type-collection-item-card.element.js",
  "forEntityTypes": ["my-entity-type"]
}
```

```
export interface MyCollectionItemModel extends UmbCollectionItemModel {
  // Add custom properties here
}
```

my-entity-type-collection-item-card.element.ts

```
import type { MyCollectionItemModel } from './types.ts';
import type { UmbEntityCollectionItemElement } from '@umbraco-cms/backoffice/collection'
import { UmbDeselectedEvent, UmbSelectedEvent } from '@umbraco-cms/backoffice/event';
import { customElement, html, property } from '@umbraco-cms/backoffice/external/lit';
import { UmbLitElement } from '@umbraco-cms/backoffice/lit-element';

@customElement('my-entity-type-collection-item-card')
export class MyEntityTypeCollectionItemCardElement extends UmbLitElement implements UmbEntityCollectionItemElement {
	@property({ type: Object })
	item?: MyCollectionItemModel;

	@property({ type: Boolean })
	selectable = false;

	@property({ type: Boolean })
	selected = false;

	@property({ type: Boolean })
	selectOnly = false;

	@property({ type: Boolean })
	disabled = false;

	@property({ type: String })
	href?: string;

	#onSelected(event: CustomEvent) {
		if (!this.item) return;
		event.stopPropagation();
		this.dispatchEvent(new UmbSelectedEvent(this.item.unique));
	}

	#onDeselected(event: CustomEvent) {
		if (!this.item) return;
		event.stopPropagation();
		this.dispatchEvent(new UmbDeselectedEvent(this.item.unique));
	}

	override render() {
		if (!this.item) return nothing;

		return html`<div>My Custom Card for ${this.item.entityType}:${this.item.unique}</div>`;
	}
}

declare global {
	interface HTMLElementTagNameMap {
		'my-entity-type-collection-item-card': MyEntityTypeCollectionItemCardElement;
	}
}
```

---

### Custom View | CMS

Manifest

```
{
  "type": "collectionView",
  "alias": "My.CollectionView.Alias",
  "name": "My Collection View",
  "element": "/App_Plugins/my-collection-view/my-collection-view.js",
  "meta": {
    "label": "Table",
    "icon": "icon-list",
    "pathName": "table"
  },
  "conditions": [
    {
      "alias": "Umb.Condition.CollectionAlias",
      "match": "Umb.Collection.Document" // Collection alias to display this collection view for
    }
  ]
}
```

Implementation

Common Collection Match Values

Match Value | Description |
`Umb.Collection.Document` | Targets the Document collection (content items). |
`Umb.Collection.Media` | Targets the Media collection (images, videos, files). |
`Umb.Collection.Member` | Targets the Member collection. |
`Umb.Collection.MemberGroup` | Targets the Member Group collection. |
`Umb.Collection.User` | Targets the User collection. |
`Umb.Collection.UserGroup` | Targets the User Group collection. |
`Umb.Collection.Dictionary` | Targets the Dictionary collection. |

Last updated

Was this helpful?

---

### Reference View | CMS

```
export interface UmbCollectionItemModel {
  unique: string;
  entityType: string;
  name?: string;
  icon?: string;
}
```

Manifest

```
{
  "type": "collectionView",
  "kind": "ref",
  "alias": "My.CollectionView.Ref",
  "name": "My Ref Collection View",
  "conditions": [
    {
      "alias": "Umb.Condition.CollectionAlias",
      "match": "My.Collection" // Collection alias to display this collection view for
    }
  ]
}
```

Custom Reference Collection Item

Manifest

Implementation

Last updated

Was this helpful?

When you want to display entities as a list of references within a collection, use the Reference Collection View Kind. This will render a basic list layout. Each item renders a default layout with the entity's name and icon. You can further customize the item layout by registering a custom Ref Collection Item when needed.

The default Collection Item Model used in a Reference Collection View is based on the following interface:

```
export interface UmbCollectionItemModel {
  unique: string;
  entityType: string;
  name?: string;
  icon?: string;
}
```

Register the Reference Collection View in the extension registry with the kind set to "ref":

Manifest

umbraco-package.json

```
{
  "type": "collectionView",
  "kind": "ref",
  "alias": "My.CollectionView.Ref",
  "name": "My Ref Collection View",
  "conditions": [
    {
      "alias": "Umb.Condition.CollectionAlias",
      "match": "My.Collection" // Collection alias to display this collection view for
    }
  ]
}
```

Custom Reference Collection Item

If you want to customize how each item is rendered, you can create and register a custom Ref Collection Item.

Manifest

Implementation

Implement your custom Ref Collection Item as a Lit element that extends `UmbLitElement`

. This defines how an individual item is rendered in the collection.

Get more information on Reference elements and base element starting points at the

Last updated

Was this helpful?

Was this helpful?

umbraco-package.json

```
{
  "type": "entityCollectionItemRef",
  "alias": "My.EntityCollectionItemRef.EntityType",
  "name": "My Entity Type Collection Item Ref",
  "element": "/App_Plugins/my-collection/ref/my-entity-type-collection-item-ref.element.js",
  "forEntityTypes": ["my-entity-type"]
}
```

```
export interface MyCollectionItemModel extends UmbCollectionItemModel {
  // Add custom properties here
}
```

my-entity-type-collection-item-ref.element.ts

```
import type { MyCollectionItemModel } from './types.ts';
import type { UmbEntityCollectionItemElement } from '@umbraco-cms/backoffice/collection'
import { UmbDeselectedEvent, UmbSelectedEvent } from '@umbraco-cms/backoffice/event';
import { customElement, html, property } from '@umbraco-cms/backoffice/external/lit';
import { UmbLitElement } from '@umbraco-cms/backoffice/lit-element';

@customElement('my-entity-type-collection-item-ref')
export class MyEntityTypeCollectionItemRefElement extends UmbLitElement implements UmbEntityCollectionItemElement {
	@property({ type: Object })
	item?: MyCollectionItemModel;

	@property({ type: Boolean })
	selectable = false;

	@property({ type: Boolean })
	selected = false;

	@property({ type: Boolean })
	selectOnly = false;

	@property({ type: Boolean })
	disabled = false;

	@property({ type: String })
	href?: string;

	#onSelected(event: CustomEvent) {
		if (!this.item) return;
		event.stopPropagation();
		this.dispatchEvent(new UmbSelectedEvent(this.item.unique));
	}

	#onDeselected(event: CustomEvent) {
		if (!this.item) return;
		event.stopPropagation();
		this.dispatchEvent(new UmbDeselectedEvent(this.item.unique));
	}

	override render() {
		if (!this.item) return nothing;
		return html`<div>My Custom Ref for ${this.item.entityType}:${this.item.unique}</div>`;
	}
}

declare global {
	interface HTMLElementTagNameMap {
		'my-entity-type-collection-item-ref': MyEntityTypeCollectionItemRefElement;
	}
}
```

---

---


## Extension Conditions | CMS

Learn how to declare requirements for your extensions using the Extension Conditions.

Extension Conditions let you define specific requirements that must be met for an extension to be available. While not all Extension Types support Conditions, many do.

For information on how to utilize conditions in your Manifest, see the [Utilizing Conditions in your Manifest](/umbraco-cms/customizing/extending-overview/extension-conditions#utilizing-conditions-in-your-manifest) section.

The following conditions are available out of the box, for all extension types that support Conditions.

These conditions don't depend on a specific area of the backoffice.

`Umb.Condition.Switch`

- Toggles on and off based on the`frequency`

set in seconds.`Umb.Condition.MultipleAppLanguages`

- Requires the app to have more than one language, such as a multi-language site.`Umb.Condition.InModal`

- Requires the extension to be rendered inside a modal.`Umb.Condition.Server.IsProductionMode`

- Requires the server to be running in production mode.`Umb.Condition.Delay`

- Delays availability of the extension by the number of milliseconds set in`offset`

.`Umb.Condition.IsRoutableContext`

- Requires (or excludes) the extension being rendered within a routable context. Accepts`match`

(boolean, defaults to`true`

).

Conditions that depend on the currently active section of the backoffice.

`Umb.Condition.SectionAlias`

- Requires the current Section Alias to match the one specified.`Umb.Condition.SectionUserPermission`

- Requires the current user to have permissions to the given Section Alias.

Conditions that depend on the currently active menu.

`Umb.Condition.MenuAlias`

- Requires the current Menu Alias to match the one specified.

Conditions that depend on the currently active workspace.

`Umb.Condition.WorkspaceAlias`

- Requires the current Workspace Alias to match the one specified.`Umb.Condition.WorkspaceEntityType`

- Requires the current workspace to work on the given Entity Type. Examples: 'document', 'block', or 'user'.`Umb.Condition.WorkspaceEntityIsNew`

- Requires the current Workspace data to be new, not yet persisted on the server.`Umb.Condition.WorkspaceContentTypeAlias`

- Requires the current workspace to be based on a Content Type whose Alias matches the one specified.`Umb.Condition.WorkspaceContentTypeUnique`

- Requires the current workspace to be based on a Content Type that uniquely matches the one specified.`Umb.Condition.Workspace.ContentHasProperties`

- Requires the Content Type of the current Workspace to have properties.`Umb.Condition.WorkspaceHasContentCollection`

- Requires the current Workspace to have a Content Collection.`Umb.Condition.Workspace.DocumentIsTrashed`

- Requires the document in the current Workspace to be in the recycle bin.`Umb.Condition.Workspace.DocumentIsNotTrashed`

- Requires the document in the current Workspace not to be in the recycle bin.`Umb.Condition.Workspace.ContentIsLoaded`

- Requires the entity in the current Workspace to have finished loading.

Conditions that depend on the current entity.

`Umb.Condition.Entity.Type`

- Requires the current entity to be of the given type. Accepts`match`

(string) or`oneOf`

(array of strings).`Umb.Condition.Entity.Unique`

- Requires the current entity's unique identifier to match the one specified.`Umb.Condition.EntityHasChildren`

- Requires the current entity to have one or more children.`Umb.Condition.EntityContentType.Unique`

- Requires the current entity's Content Type unique identifier to match the one specified.`Umb.Condition.EntityIsTrashed`

- Requires the current entity to be trashed.`Umb.Condition.EntityIsNotTrashed`

- Requires the current entity not to be trashed.

Conditions that depend on the currently active collection.

`Umb.Condition.CollectionAlias`

- Requires the current Collection Alias to match the one specified.`Umb.Condition.CollectionHasItems`

- Requires the current Collection to contain one or more items.

Conditions that depend on the currently active property.

`Umb.Condition.Property.HasValue`

- Requires the current property to have a value.`Umb.Condition.Property.Writable`

- Requires the current property to be writable (not read-only).

Conditions based on the user who is currently signed in.

`Umb.Condition.CurrentUser.IsAdmin`

- Requires the current user to be an admin as defined by the backend, for example, that they belong to the Administrator group.`Umb.Condition.CurrentUser.GroupId`

- Requires the current user to belong to a specific group by GUID. Accepts`match`

(GUID),`oneOf`

(array),`allOf`

(array), and`noneOf`

(array). Example: '8d2b3c4d-4f1f-4b1f-8e3d-4a6b7b8c4f1e'.`Umb.Condition.CurrentUser.AllowChangePassword`

- Requires the current user to be allowed to change their password.`Umb.Condition.CurrentUser.AllowMfaAction`

- Requires the current user to be allowed to manage Multi-Factor Authentication.`Umb.Condition.CurrentUser.AllowDocumentRecycleBin`

- Requires the current user to be allowed to access the Document recycle bin.`Umb.Condition.CurrentUser.AllowMediaRecycleBin`

- Requires the current user to be allowed to access the Media recycle bin.

Conditions used by entity actions in the Users workspace. They apply to the user that the action is being performed on.

`Umb.Condition.User.AllowChangePassword`

- Requires the selected user to allow a password-change action.`Umb.Condition.User.AllowDeleteAction`

- Requires the selected user to be deletable.`Umb.Condition.User.AllowDisableAction`

- Requires the selected user to be allowed to be disabled.`Umb.Condition.User.AllowEnableAction`

- Requires the selected user to be allowed to be enabled.`Umb.Condition.User.AllowUnlockAction`

- Requires the selected user to be allowed to be unlocked.`Umb.Condition.User.AllowExternalLoginAction`

- Requires external-login actions to be available for the selected user.`Umb.Condition.User.AllowMfaAction`

- Requires Multi-Factor Authentication actions to be available for the selected user.`Umb.Condition.User.IsDefaultKind`

- Requires the selected user to be of the default user kind.`Umb.Condition.User.AllowResendInviteAction`

- Requires the selected user to be allowed to have an invite resent.

Conditions that check whether the current user has a specific permission.

`Umb.Condition.UserPermission.Document`

- Requires the current user to have specific Document permissions. Example: 'Umb.Document.Save'.`Umb.Condition.UserPermission.Document.PropertyValue`

- Requires the current user to have the required permission for the Document's property values.`Umb.Condition.UserPermission.Language`

- Requires the current user to have the required permission for the given Language.`Umb.Condition.UserPermission.Fallback`

- Requires the current user to have specific fallback permissions. Accepts`allOf`

(array of permission verbs) and`oneOf`

(array of permission verbs).

Conditions related to template and Data Type management.

`Umb.Condition.Template.AllowDeleteAction`

- Requires the selected Template to be allowed to be deleted.`Umb.Condition.DataType.AllowDeleteAction`

- Requires the selected Data Type to be allowed to be deleted.

Conditions specific to property editor extensions.

`Umb.Condition.EntityDataPicker.SupportsTextFilter`

- Requires the current Entity Data Picker to support text filtering.

Conditions specific to the Block workspace (used by Block List, Block Grid and similar block-based editors).

`Umb.Condition.BlockWorkspaceHasSettings`

- Requires the block in the current Workspace to have a settings model.`Umb.Condition.BlockEntryShowContentEdit`

- Requires the block entry to be configured to show the content-edit UI.`Umb.Condition.BlockWorkspaceIsExposed`

- Requires the block in the current Workspace to be exposed for the current variant.`Umb.Condition.BlockWorkspaceIsReadOnly`

- Requires the block in the current Workspace to be read-only.

You can make your own Conditions by creating a class that implements the `UmbExtensionCondition`

interface.

The global declaration on the last five lines makes your Condition appear valid for manifests using the type `UmbExtensionManifest`

. Also, the Condition Config Type alias should match the alias given when registering the condition below.

The Condition then needs to be registered in the Extension Registry:

Finally, you can make use of your condition in any manifests:

As shown in the code above, the configuration property `match`

isn't used for our condition. We can do this by replacing the timeout with some other check:

With all that in place, the configuration can look like shown below:

Last updated

Was this helpful?

---


## Dashboards | CMS

A guide to creating custom dashboards in Umbraco

![The Getting Started dashboard in Umbraco](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-3af5f1808e3fe4d9beb35a2149ff8314185fe454%252Fgetting-started-dashboard.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f8915e74&sv=2)

Default Dashboards in Umbraco

| Alias | Name |
|---|---|
| Umb.Section.Content | Content |
| Umb.Section.Media | Media |
| Umb.Section.Settings | Settings |
| Umb.Section.Members | Members |
| Umb.Section.Users | Users |
| Umb.Section.Translation | Dictionary |

| Alias | Section | Weight | Description |
|---|---|---|---|
| Umb.Dashboard.UmbracoNews | Umb.Section.Content | 20 | The Getting Started dashboard users see when they first enter Umbraco. Contains the latest news of Umbraco including outbound links to resources |
| Umb.Dashboard.RedirectManagement | Umb.Section.Content | 10 | Contains a list of active URL redirects |
| Umb.Dashboard.SettingsWelcome | Umb.Section.Settings | 500 | Contains a set of boxes with links to appropriate resources |

Hiding or adding conditional rules to existing dashboards

Restricting to specific user groups

[Extension Conditions chevron-right](/umbraco-cms/customizing/extending-overview/extension-types/condition)

Registering your Dashboard

Example Extension Manifest

Conditions

Properties

| Property | Type | Description |
|---|---|---|
| type | string | The type of extension, should be `dashboard` |
| alias | string | A unique alias for the dashboard extension |
| name | string | The name of the dashboard extension |
| element | string | The path to the JavaScript file that exports the dashboard |
| elementName | string | (Optional) The name of the Web Component that contains the dashboard (only if not a default export) |
| weight | number | (Optional) The weight of the dashboard, higher numbers are displayed first |
| meta | object | Additional metadata for the dashboard |
| Property | Type | Description |
| Label | string | The label shown to the user |
| pathname | string | The routable URL pathname |
| conditions | array | (Optional)
|

Full Example

![The Welcome Dashboard shown in the Content section](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-60c3108958673a6a3d399000c4c36d754cff20b5%252Fwelcome-dashboard.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=51a2d2ea&sv=2)

Last updated

Was this helpful?

---


## Entity Actions | CMS

Entity Actions give developers the ability to add custom actions to a fly-out menu.

Display Modes

Sidebar Context Menu

Workspace Entity Menu

Collection Menu

Picker Menu

Registering an Entity Action

Declare the Entity Action

The Entity Action Class

The

`getHref()`

MethodThe

`execute()`

MethodOverriding the

`UmbEntityActionBase`

ConstructorUser Permission Codes

Standard Umbraco Permission Letters

| Legacy backoffice letter | Verb |
|---|---|
| C | Umb.Document.Create |
| F | Umb.Document.Read |
| A | Umb.Document.Update |
| D | Umb.Document.Delete |
| I | Umb.Document.CreateBlueprint |
| N | Umb.Document.Notifications |
| U | Umb.Document.Publish |
| R | Umb.Document.Permissions |
| Z | Umb.Document.Unpublish |
| O | Umb.Document.Duplicate |
| M | Umb.Document.Move |
| S | Umb.Document.Sort |
| I | Umb.Document.CultureAndHostnames |
| P | Umb.Document.PublicAccess |
| K | Umb.Document.Rollback |

Custom Permission Letters

| Custom Backoffice letter | Verb |
|---|---|
| ⌘ | Placeholder |

Entity Action Permissions

Entity User Permissions

Management Interface

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-245a3d3a5b21ce6f465677806b50507198abdb63%252Fentity-user-permissions-ui.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3871da7b&sv=2)

**Entity User Permissions UI**

Granular User Permission

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2b1a223e7448b977d5d0bd42285da2fd207c35b1%252Fgranular-user-permissions-ui.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=71462269&sv=2)

**Default Granular User Permission UI**

Management Interface

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-cbf863e98a0cea4d0ee0023bcb0e94ad522522c3%252Fgranular-user-permissions-ui-custom.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7a0c6512&sv=2)

**Custom Granular User Permission UI**

Enforcing Permissions

Last updated

Was this helpful?

---


## Entity Bulk Actions | CMS

Bulk Entity Actions perform an action on a selection of items.

Last updated

Was this helpful?

Bulk Entity Actions perform an action on a selection of items.

Extension authors can register an entity bulk action to appear in the collection selection toolbar.

Registering an Entity Bulk Action

Entity Bulk Action extensions can be included by importing a subclass of `UmbEntityBulkActionBase`

to the `api`

property. Placement within the backoffice can be controlled using the conditions property.

The Entity Bulk Action Class

Entity Bulk Action extensions inherit from `UmbEntityBulkActionBase`

, which expects the extension author to provide an implementation of `execute()`

. The `UmbEntityBulkActionBase`

class provides `this.selection`

as a property, which contains a list of uniques from the content nodes that were selected by the user.

When the action is completed, an event on the host element will be dispatched to notify any surrounding elements.

This code sample demonstrates overriding the constructor, which could be helpful in certain circumstances, such as consuming contexts. Extension authors can safely omit the constructor if no such need exists.

Last updated

Was this helpful?

Was this helpful?

```
import { umbExtensionsRegistry } from '@umbraco-cms/backoffice/extension-registry';
import { MyEntityBulkAction } from './entity-bulk-action';

const manifest = {
 type: 'entityBulkAction',
 alias: 'My.EntityBulkAction',
 name: 'My Entity Bulk Action',
 weight: 10,
 api: MyEntityBulkAction,
 meta: {
  icon: 'icon-add',
  label: 'My Entity Bulk Action',
 },
 conditions: [
  {
   alias: 'Umb.Condition.CollectionAlias',
   match: 'my-collection-alias',
  },
 ],
};

umbExtensionsRegistry.register(manifest);
```

```
import {
    UmbEntityBulkActionBase,
    UmbEntityBulkActionArgs,
} from "@umbraco-cms/backoffice/entity-bulk-action";
import { UmbControllerHostElement } from "@umbraco-cms/backoffice/controller-api";

export class MyBulkEntityAction extends UmbEntityBulkActionBase<never> {
    constructor(
        host: UmbControllerHostElement,
        args: UmbEntityBulkActionArgs<never>,
    ) {
        // this constructor is optional, override only if necessary
        super(host, args);
    }

    async execute() {
        // perform a network request
        // await Promise.all(
        //     this.selection.map(async (x) => {
        //         const res = await fetch(`my-server-api-endpoint/${x}`);
        //         return res.json() as never;
        //     })
        // );

        // or fetch repository
        // const repository = ...
        // await repository.processItems(this.selection);
        
        console.log(this.selection);
    }
}
```

---


## Entity Create Option Action | CMS

An "Entity Create Option Action" is an additional option that can be added when creating an entity. For example, options like "Create Document Type" or "Create Document Type with Template" can be available when a Document Type is being created.

These options will be displayed in a create options dialog when the "Create"-entity action is selected. The dialog will show the available options and allow the user to select one of them.

To enable a "Create"-entity action to show the options dialog, use the 'create'-kind in the manifest when setting up the "Create"-entity action. This will display the options dialog if multiple options are available, or it will automatically execute the first option if only one is available.

By using the "create"-kind for your create entity actions, you can ensure that your options are extendable by other developers. This also applies when you only have one option available

The following code shows you to register a "Create"-entity action that can display a dialog with options:

```
const manifest = {
    type: "entityAction",
    kind: "create",
    alias: "My.EntityAction",
    name: "My Create Entity Action",
    forEntityTypes: ["my-entity"],
};
```

The following code demonstrates how to register an Entity Create Option Action. If only one option is available, it will be executed immediately.

```
const manifest = {
    type: "entityCreateOptionAction",
    alias: "My.EntityCreateOptionAction",
    name: "My Create Option Action",
    weight: 100,
    api: () => import("./path-to-file.js"),
    forEntityTypes: ["my-entity"],
    meta: {
        icon: "icon-unplug",
        label: "My Create Option Action",
        additionalOptions: false,
    },
};
```

The following code shows how to implement the Create Action Option.

We currently support Create Options for the following entity types:

User


Last updated

Was this helpful?

---


## Global Context | CMS

Global contexts in Umbraco provide a clean, type-safe way to share functionality across the backoffice.

Registration of a Global Context

```
{
    "$schema": "../../umbraco-package-schema.json",
    "name": "My Global Context Package",
    "version": "1.0.0",
    "extensions": [
        {
            "type": "globalContext",
            "alias": "My.GlobalContext",
            "name": "My Global Context",
            "api": "/App_Plugins/my-global-context/dist/my-context.context.js"
        }
    ]
}
```

Creating Your Global Context

1. Define a Context Token

2. Implement the Context Class

Using Global Contexts

Last updated

Was this helpful?

---


## Header Apps | CMS

Place single-purpose extensions in the top-level navigation bar, next to the user profile avatar.

Button Header Apps as a link

Button Header Apps with deeper interactivity

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-85303a2099666e83d4ac78ffe083dd8b2f82d1da%252Fheader-apps-custom.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=83a3bf70&sv=2)

Last updated

Was this helpful?

Place single-purpose extensions in the top-level navigation bar, next to the user profile avatar.

Header App extensions appear next to the user profile and the global search icon in the top right of Umbraco’s Backoffice. Extension authors can create custom header apps to add globally accessible functionality to the Backoffice.

Button Header Apps as a link

Extension authors can create header apps that link to resource both inside and outside the backoffice. Header apps can be created using a manifest or using TypeScript.

To create a link-style header app, define a `headerApp`

extension in the `umbraco-package.json`

file. Be sure to include `meta.label`

and `meta.icon`

so that your header app appears when you reload the backoffice.

If `meta.href`

is defined, the header app will function as a link. Links will open in the same tab.

Header Apps can also be created using TypeScript. Examples of both approaches are shown below.

Button Header Apps with deeper interactivity

Extension authors can also create header apps that have more interactivity than a link.

By creating a custom component, extension authors can control how the button renders itself and how it behaves when clicked. This allows header apps to control navigation, open modals, or perform other actions.

For example, this is how the current user header app is able to present a modal when clicked.

In order for a header app to have some functionality, extension authors will need to define behavior by creating a JavaScript or TypeScript component. Once the component has been created, it will need to be registered in the header app's `element`

property.

This example assumes that the extension author has transpiled the above TypeScript code into a JavaScript file. The name and location of the transpiled file should match the `element`

property in the package manifest.

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
      "type": "headerApp",
      "alias": "My.HeaderApp",
      "name": "My Header App",
      "kind": "button",
      "meta": {
        "label": "Hello Umbraco",
        "icon": "icon-hearts",
        "href": "https://umbraco.com/"
      }
    }
  ]
}
```

my-element.ts

```
import { umbExtensionsRegistry } from '@umbraco-cms/backoffice/extension-registry';

const manifest: UmbExtensionManifest = {
  type: "headerApp",
  alias: "My.HeaderApp.Documentation",
  name: "My Documentation Header App",
  kind: "button",
  meta: {
    label: "Hello Documentation",
    icon: "icon-addressbook",
    href: "https://docs.umbraco.com/"
  }
};

umbExtensionsRegistry.register(manifest);
```

umbraco-package.json

```
{
  "$schema": "../../umbraco-package-schema.json",
  "name": "My Package",
  "version": "0.1.0",
  "extensions": [
    {
      "type": "headerApp",
      "alias": "My.HeaderApp.ServerServices",
      "name": "My Server Services Header App",
      "kind": "button",
      "element": "/App_Plugins/MyPackage/server-services-header-app.js"
    }
  ]
}
```

src/server-services-header.ts

```
import { html, customElement } from "@umbraco-cms/backoffice/external/lit";
import { UmbHeaderAppButtonElement } from "@umbraco-cms/backoffice/components";
import { umbOpenModal, UMB_CONFIRM_MODAL } from "@umbraco-cms/backoffice/modal";

@customElement("my-server-services-header-app")
export class MyServerServicesHeaderAppElement extends UmbHeaderAppButtonElement {
  async #handleUserClick() {
    umbOpenModal(this, UMB_CONFIRM_MODAL, {
      data: {
        headline: "Would you like to disable all Server Services?",
        content:
          "This action can be undone, but only after all services have stopped.",
        color: "danger",
        confirmLabel: "Disable all services",
      },
    })
      .then(() => {
        console.log("User has approved");
      })
      .catch(() => {
        console.log("User has rejected");
      });
  }

  override render() {
    return html`
      <uui-button
        @click=${this.#handleUserClick}
        look="primary"
        label="Server Services"
        compact
      >
        <uui-icon name="icon-server"></uui-icon>
      </uui-button>
    `;
  }
}

{ MyServerServicesHeaderAppElement as element };
```

---


## Icons | CMS

Create custom icon sets for use across the Umbraco backoffice.

Register a new set of icons

```
{
    "$schema": "../../umbraco-package-schema.json",
    "name": "My Package",
    "version": "0.1.0",
    "extensions": [
        {
            "type": "icons",
            "alias": "My.Icons.Unicorn",
            "name": "My Unicorn Icons",
            "js": "/App_Plugins/MyPackage/Icons/icons.js"
        }
    ]
}
```

```
export default [
    {
        name: "my-unicorn",
        path: () => import("./icon-unicorn.js"),
    },
    {
        name: "my-giraffe",
        path: () => import("./icon-giraffe.js"),
    }
]
```

Using Icons in your UI

Last updated

Was this helpful?

Create custom icon sets for use across the Umbraco backoffice.

Umbraco extension authors can create custom icon sets for use across the Umbraco backoffice using an extension type called `icons`.


Register a new set of icons

Icons must be registered in a manifest using the Extension API. The manifest can be added through the `umbraco-package.json`

file, as shown below.

umbraco-package.json

```
{
    "$schema": "../../umbraco-package-schema.json",
    "name": "My Package",
    "version": "0.1.0",
    "extensions": [
        {
            "type": "icons",
            "alias": "My.Icons.Unicorn",
            "name": "My Unicorn Icons",
            "js": "/App_Plugins/MyPackage/Icons/icons.js"
        }
    ]
}
```

The file set in the `js`

field contains the details of your icons. These definitions should resemble the following:

icons.js

```
export default [
    {
        name: "my-unicorn",
        path: () => import("./icon-unicorn.js"),
    },
    {
        name: "my-giraffe",
        path: () => import("./icon-giraffe.js"),
    }
]
```

Prefix each icon name to avoid collisions with other icons.

Each icon must define a path, either as a string or a dynamic import as shown above. This file must be a JavaScript file containing a default export of an SVG string. See an example below:

Using Icons in your UI

The `umb-icon`

element can automatically consume any registered icon.

Last updated

Was this helpful?

Was this helpful?

icon-unicorn.js

```
export default `<svg ...></svg>`;
```

```
<umb-icon name="my-unicorn"></umb-icon>
```

---


## Kinds | CMS

Create reusable, standardized configurations for extensions, helping to streamline development, ensure consistency, and reduce duplication.

Benefits of Using a Kind

Kind Registration

Example: Registering a Button Kind for Header Apps

Using the Kind in Other Extensions

Example: Header App Extension Using the Button Kind

Custom Kind Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4cd2cd7831deeb8633c43119da85065b437b4359%252Fkind-custom-header-app.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=403a429f&sv=2)

Create the Kind Extension

Create a Custom Component for

`welcome-header-app-message`

Derive Header Apps Using the Custom Kind Extension

Register the Derived Extension

Last updated

Was this helpful?

---


## Localization | CMS

Learn how to manage and use the Backoffice UI Localization files.

Last updated

Was this helpful?

Learn how to manage and use the Backoffice UI Localization files.

Registering Localization

When registering localizations to a language, you must add a new manifest to the Extension API. The manifest can be added through the `umbraco-package.json`

file.

The `umbraco-package.json`

file is only registered when placed directly in the `/App_Plugins/`

or `/App_Plugins/{YourPackageName}`

folder. It will not be recognized in nested subfolders.

Usually, the localization keys are provided through a JavaScript module. In this example, we will use a file named `en.js`:


umbraco-package.json

```
{
  "name": "MyPackage",
  "extensions": [
    {
      "type": "localization",
      "alias": "MyPackage.Localize.EnUS",
      "name": "English",
      "meta": {
        "culture": "en"
      },
      "js": "/App_Plugins/MyPackage/Localization/en.js"
    }
  ]
}
```

Read more about extensions in the [Package Manifest](/umbraco-cms/customizing/umbraco-package) article.

The Localization file

The localization files for the UI are JavaScript modules with a default export containing a key-value structure organized in sections.

The sections and keys will be formatted into a map in Umbraco with the format `section_key1`

and `section_key2.`

These form the unique key they are requested.

If you do not have many translations, you can also choose to include them directly in the meta-object using the `localizations`

property:

All keys must be wrapped within a single grouping level (for example `section`

) inside the `localizations`

object. You cannot place key-value pairs directly under `localizations`

, and further nesting is not supported.

In this case, the `en.js`

file is not required and we can remove the "js" property from the manifest. Only strings can be used in the meta-object.

Last updated

Was this helpful?

Was this helpful?

en.js

```
export default {
    section: {
        key1: 'value1',
        key2: 'value2',
    },
};
```

umbraco-package.json

```
{
  "name": "MyPackage",
  "extensions": [
    {
      "type": "localization",
      "alias": "MyPackage.Localize.EnUS",
      "name": "English",
      "meta": {
        "culture": "en",
        "localizations": {
          "section": {
            "key1": "value1",
            "key2": "value2"
          }
        }
      },
    }
  ]
}
```

---
