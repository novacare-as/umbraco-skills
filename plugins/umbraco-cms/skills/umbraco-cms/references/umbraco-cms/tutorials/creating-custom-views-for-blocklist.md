# Custom Views for Block List | CMS

Custom Views are used to overwrite the presentation of a Block. The editing experience can be improved by providing a better representation of the Blocks content. It could be a presentation of how it will look on the front end or the specific properties available.

This article is a work in progress and may undergo further revisions, updates, or amendments. The information contained herein is subject to change without notice.

For this tutorial, you will set up a Document Type and create a new property using Block List as the property editor.

To create a Document Type:

Go to

**Settings**.Select the

**...**next to the**Document Types**in the**Settings**tree.Select

**Document Type with Template**.Using folders can help you organize your

**Document Types**.

Name the

**Document Type***Product*. You'll notice that the`product`

**alias**is automatically generated.Click

**Add Group**and name the group*Product Details*.Add the following properties:


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-36182dca4b104e388698eaaf42b992cea4fd133c%252Fdocument-properties.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d965ef92&sv=2)

Add another group called

**Features**and a property with the following specification:

| Name | Features |
|---|---|
| Alias | features |
| Data Type | Block List |

**Save**the Document Type.

Your Document Type will now look like:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ff2694ab293d7267c53240ce165fd9758d5738d9%252Fdocument-type.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e1096295&sv=2)

To create the Content Node, follow these steps:

Go to the

**Permissions**tab of the root content node.Select

**Add Child**in the**Allowed child node types**.Select the

**Product**Document Type and click**Save**.Go to

**Content**.Select

**...**next to the root content node.Choose

**Product**.**Name**the article*Product*.Fill the required details in the

**Product**page and**Save**it.

To configure the Block List editor:

Go to

**Settings**.Open the

**Product**Document Type.Click on the

**Block List**property you created earlier.

You'll see the Block list editor's configuration, as shown below:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5ddf8b571c1191fa2068091c57ab39b41f7e4b54%252Fblocklist-editor-settings.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=169ba8c2&sv=2)

The **Configuration** section allows you to perform the following actions:

Add

**Available Blocks**.Define the range of blocks that can be added.

Control the live and inline editing mode.

Set the property editor width.


The Available Blocks in the Block List editor configuration differentiate it from the other property editors. The list you create with the Block List editor is based on one or more blocks. Each block is based on an Element Type.

To add blocks to the Block List editor, follow these steps:

Click

**Add**in the**Available Blocks**to open the**Pick Element Type**window.

From here, you have the option to select an existing Element Type or create a new Element Type from the configuration screen.

Choose

**Create a new Element Type**.Set up a new Element type called

**Feature**and use the following configuration:

| Property Name | Alias | Editor |
|---|---|---|
| Name | featureName | Textstring |
| Details | details | Textarea |
| Image | image | Media Picker |

Click

**Save and Close**.

For more information on the block configuration, see the [Setup Block Types](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/block-editor/block-list-editor#setup-block-types) section.

Follow steps 1-4 to set up another block called

**Hero**.Toggle

**Live Editing mode**and select**Submit**.

You can enhance the editing experience by replacing the default representation of block entries with a custom view. This can be used to provide a more detailed representation of the block. You can make the content look as it will on the frontend or highlight specific values for a data overview.

A Custom View is a Web Component registered as a Backoffice Extension.

Create an `example-block-custom-view.ts`

file containing the following code:

This is a TypeScript file. It is recommended to follow the documentation on compiling TypeScript.

Now that you have created a Web Component, register it to show up on the block:

While the `forContentTypeAlias`

and `forBlockEditor`

parameters are optional, they also accept arrays. They can therefore be used to declare a custom view for multiple blocks and block editors. The code snippet below shows an example of such an array:

Depending on the values, the custom view is applied to the following data types:

`block-list`

- For more information, see the[Block List editor](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/block-editor/block-list-editor).`block-grid`

- For more information, see the[Block Grid editor](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/block-editor/block-grid-editor).`block-rte`

- Blocks used inline in the[Rich Text editor](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/rich-text-editor/blocks).

Read about [extension-manifest](/umbraco-cms/customizing/extending-overview/extension-registry/extension-manifest) to learn how to register an Extension Manifest.

Once registered, the Block will be represented by the given Web Component.

To add content to the blocks:

Go to the

**Content**section and select**Product**.Select

**Add Content**in the**Features**group. The**Add Content**displays the blocks created earlier.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9703d2185bd8228295e6f673a08a9aa170e41687%252FContent-block-list.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=2b8d6a5f&sv=2)

Select

**Feature**to open the**Feature**window.Enter the

**Name**and**Details**in the Feature window.

You will notice you can view the content as you type. This is because the **Live editing** mode is enabled.

Click

**Confirm**when the content is added.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6fc8d557416bd4fa14b96dd34c39d22bef9c141c%252FFeature-Content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=97d5123f&sv=2)

`Settings`

section for BlocksYou have now overwritten the default view for the block presentation by using your own custom view. Next, create a **Settings** section to control the data alignment of the block. To do this, you need to add a **Settings** model to our block configuration.

To add a Settings model:

Go to

**Product**in the**Settings**tree.Click the

`cog`

wheel next to**Features**.Select the

**Product - Features - Block List**to open the**Editor Settings**window.Select

**Feature**from the**Available Blocks**configuration.Select

**Settings Model**in the Data Models section to open the**Attach a settings Element Type**window.Select

**Create new Element Type**.**Enter a Name**for the element type:*Feature Settings*.Give it an icon.

Click

**Add Group**and**Enter a Name**:*Settings*.Click

**Add Property**and**Enter a Name**:*Block Alignment*. The`blockAlignment`

alias is automatically generated.Select

**Dropdown List**as the editor.Add

**left**,**center**and**right**as values to the Dropdown List.Click

**Submit**.


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6a29bf018056a53cc12b3ad669ad523861768e69%252Fprevalue-options-1.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f7dba722&sv=2)

Click

**Submit**.Click

**Save and Close**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-644ce418c92ae2e6fb5347ab6e43d8629708e518%252FFeature-Settings-1.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1eae87da&sv=2)

Click

**Submit**until you reach the Product Document Type.Click

**Save**.

You need to update the `example-block-custom-view.ts`

file with the following configuration:

You can make editing block content faster by making it possible to click anywhere in the preview to open the editing window. To do this, you need to update the `example-block-custom-view.ts`

file to get the link from Umbraco's configuration:

Link to `this.config?.editSettingsPath`

if you prefer to open the Settings window for the block.

If you are not able to use the URL, it is still possible to call a method to open the block workspace.

For this, you need to get the context of `UMB_BLOCK_ENTRY_CONTEXT`

, which holds the methods `edit()`

and `editSettings()`.


To render the stored value of your Block List editor on the frontend, see the [Rendering Block List Content](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/block-editor#block-list) section.

Last updated

Was this helpful?