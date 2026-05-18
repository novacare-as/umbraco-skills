# Property Editor Data Source Types | CMS

Umbraco Documentation

file-lines Docs Overview

folder-grid CMS

Picker Data Source Type chevron-right

Previous Property Editor Data Source chevron-left

Next Picker Data Source Type chevron-right

Last updated 5 months ago

Was this helpful?

## Picker

## Contents

- [Collection Data Source | CMS](#collection-data-source-cms)
- [Tree Data Source | CMS](#tree-data-source-cms)

---

## Collection Data Source | CMS

Last updated

Was this helpful?

The interface below is simplified for clarity and omits return types and arguments. See full interfaces in the

```
interface UmbPickerPropertyEditorCollectionDataSource {
  requestCollection();
  requestItems();
  search?();
  setConfig?();
  getConfig?();
}
```

Example

```
import { UmbControllerBase } from '@umbraco-cms/backoffice/class-api';
import type { UmbCollectionFilterModel, UmbCollectionItemModel } from '@umbraco-cms/backoffice/collection';
import type {
	UmbPickerCollectionDataSource,
	UmbPickerSearchableDataSource,
} from '@umbraco-cms/backoffice/picker-data-source';
import type { UmbSearchRequestArgs } from '@umbraco-cms/backoffice/search';

interface ExampleCollectionItemModel extends UmbCollectionItemModel {
	isPickable: boolean;
}

export class MyCustomPickerCollectionPropertyEditorDataSource
	extends UmbControllerBase
	implements UmbPickerCollectionDataSource<ExampleCollectionItemModel>, UmbPickerSearchableDataSource
{
	collectionPickableFilter = (item: ExampleCollectionItemModel) => item.isPickable;

	async requestCollection(args: UmbCollectionFilterModel) {
		const data = {
			items: customItems,
			total: customItems.length,
		};

		return { data };
	}

	async requestItems(uniques: Array<string>) {
		const items = customItems.filter((x) => uniques.includes(x.unique));
		return { data: items };
	}

	async search(args: UmbSearchRequestArgs) {
		const items = customItems.filter((item) => item.name?.toLowerCase().includes(args.query.toLowerCase()));
		const total = items.length;

		const data = {
			items,
			total,
		};

		return { data };
	}
}

export { ExampleCustomPickerCollectionPropertyEditorDataSource as api };

const customItems: Array<ExampleCollectionItemModel> = [
	{
		unique: '1',
		entityType: 'example',
		name: 'Example 1',
		icon: 'icon-shape-triangle',
		isPickable: true,
	},
	{
		unique: '2',
		entityType: 'example',
		name: 'Example 2',
		icon: 'icon-shape-triangle',
		isPickable: false,
	},
	{
		unique: '3',
		entityType: 'example',
		name: 'Example 3',
		icon: 'icon-shape-triangle',
		isPickable: true,
	},
];
```

Last updated

Was this helpful?

Was this helpful?

---

## Tree Data Source | CMS

Last updated

Was this helpful?

The interface below is simplified for clarity and omits return types and arguments. See full interfaces in the

```
interface UmbPickerPropertyEditorCollectionDataSource {
  requestTreeRoot();
  requestTreeRootItems();
  requestTreeItemsOf();
  requestTreeItemAncestors();
  requestItems();
  search?();
  setConfig?();
  getConfig?();
}
```

Example

```
import { UmbControllerBase } from '@umbraco-cms/backoffice/class-api';
import type {
	UmbPickerSearchableDataSource,
	UmbPickerTreeDataSource,
} from '@umbraco-cms/backoffice/picker-data-source';
import type { UmbSearchRequestArgs, UmbSearchResultItemModel } from '@umbraco-cms/backoffice/search';
import type { UmbTreeChildrenOfRequestArgs, UmbTreeItemModel } from '@umbraco-cms/backoffice/tree';

export class ExampleCustomPickerTreePropertyEditorDataSource
	extends UmbControllerBase
	implements UmbPickerTreeDataSource, UmbPickerSearchableDataSource
{
	treePickableFilter: (treeItem: UmbTreeItemModel) => boolean = (treeItem) =>
		!!treeItem.unique && treeItem.entityType === 'example';

	searchPickableFilter: (searchItem: UmbSearchResultItemModel) => boolean = (searchItem) =>
		!!searchItem.unique && searchItem.entityType === 'example';

	async requestTreeRoot() {
		const root = {
			unique: null,
			name: 'Examples',
			icon: 'icon-folder',
			hasChildren: true,
			entityType: 'example-root',
			isFolder: true,
		};

		return { data: root };
	}

	async requestTreeRootItems() {
		const rootItems = customItems.filter((item) => item.parent.unique === null);

		const data = {
			items: rootItems,
			total: rootItems.length,
		};

		return { data };
	}

	async requestTreeItemsOf(args: UmbTreeChildrenOfRequestArgs) {
		const items = customItems.filter(
			(item) => item.parent.entityType === args.parent.entityType && item.parent.unique === args.parent.unique,
		);

		const data = {
			items: items,
			total: items.length,
		};

		return { data };
	}

	async requestTreeItemAncestors() {
		// TODO: implement when needed
		return { data: [] };
	}

	async requestItems(uniques: Array<string>) {
		const items = customItems.filter((x) => uniques.includes(x.unique));
		return { data: items };
	}

	async search(args: UmbSearchRequestArgs) {
		const result = customItems.filter((item) => item.name.toLowerCase().includes(args.query.toLowerCase()));

		const data = {
			items: result,
			total: result.length,
		};

		return { data };
	}
}

export { ExampleCustomPickerTreePropertyEditorDataSource as api };

const customItems: Array<UmbTreeItemModel> = [
	{
		unique: '1',
		entityType: 'example',
		name: 'Example 1',
		icon: 'icon-shape-triangle',
		parent: { unique: null, entityType: 'example-root' },
		isFolder: false,
		hasChildren: false,
	},
	{
		unique: '2',
		entityType: 'example',
		name: 'Example 2',
		icon: 'icon-shape-triangle',
		parent: { unique: null, entityType: 'example-root' },
		isFolder: false,
		hasChildren: false,
	},
	{
		unique: '3',
		entityType: 'example',
		name: 'Example 3',
		icon: 'icon-shape-triangle',
		parent: { unique: null, entityType: 'example-root' },
		isFolder: false,
		hasChildren: false,
	},
	{
		unique: '4',
		entityType: 'example',
		name: 'Example 4',
		icon: 'icon-shape-triangle',
		parent: { unique: '6', entityType: 'example-folder' },
		isFolder: false,
		hasChildren: false,
	},
	{
		unique: '5',
		entityType: 'example',
		name: 'Example 5',
		icon: 'icon-shape-triangle',
		parent: { unique: '6', entityType: 'example-folder' },
		isFolder: false,
		hasChildren: false,
	},
	{
		unique: '6',
		entityType: 'example-folder',
		name: 'Example Folder 1',
		parent: { unique: null, entityType: 'example-root' },
		isFolder: true,
		hasChildren: true,
	},
];
```

Last updated

Was this helpful?

Was this helpful?

---
