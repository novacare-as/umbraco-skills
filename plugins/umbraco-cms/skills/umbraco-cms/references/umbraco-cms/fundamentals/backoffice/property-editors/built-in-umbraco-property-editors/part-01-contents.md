# Built In Umbraco Property Editors — Part 1: Contents → Content Picker | CMS

## Contents

- [Block Editor](#block-editor)
- [Checkbox List | CMS](#checkbox-list-cms)
- [Code Editor | CMS](#code-editor-cms)
- [Collection | CMS](#collection-cms)
- [Color Picker | CMS](#color-picker-cms)
- [Content Picker | CMS](#content-picker-cms)
- [Date Time Editor](#date-time-editor)
- [DateTime | CMS](#datetime-cms)
- [Decimal | CMS](#decimal-cms)
- [Document Picker | CMS](#document-picker-cms)
- [Dropdown | CMS](#dropdown-cms)
- [Email Address | CMS](#email-address-cms)
- [Entity Data Picker | CMS](#entity-data-picker-cms)
- [Eye Dropper Color Picker | CMS](#eye-dropper-color-picker-cms)
- [File Upload | CMS](#file-upload-cms)
- [Image Cropper | CMS](#image-cropper-cms)
- [Label | CMS](#label-cms)
- [Markdown Editor | CMS](#markdown-editor-cms)
- [Media Picker | CMS](#media-picker-cms)
- [Member Group Picker | CMS](#member-group-picker-cms)
- [Member Picker | CMS](#member-picker-cms)
- [Multi Url Picker | CMS](#multi-url-picker-cms)
- [Repeatable Textstrings | CMS](#repeatable-textstrings-cms)
- [Numeric | CMS](#numeric-cms)
- [Radiobutton List | CMS](#radiobutton-list-cms)
- [Rich Text Editor](#rich-text-editor)
- [Slider | CMS](#slider-cms)
- [Tags | CMS](#tags-cms)
- [Textarea | CMS](#textarea-cms)
- [Textbox | CMS](#textbox-cms)
- [Toggle | CMS](#toggle-cms)
- [User Picker | CMS](#user-picker-cms)

---


## Block Editor

### Contents

- [Block Grid | CMS](#block-grid-cms)
- [Block Level Variance | CMS](#block-level-variance-cms)
- [Block List | CMS](#block-list-cms)

---

### Block Grid | CMS

`Schema Alias: Umbraco.BlockGrid`


`UI Alias: Umb.PropertyEditorUi.BlockGrid`


`Returns: BlockGridModel`


The **Block Grid** property editor enables editors to layout their content in the Umbraco backoffice. The content is made of Blocks that can contain different types of data.

The Block Grid property editor is configured via the **Data Types** backoffice interface.

To set up the Block Grid property editor, follow these steps:

Navigate to the

**Settings**section in the Umbraco backoffice.Click

**...**next to the**Data Types**folder.Select

**Create**->**New Data Type**.Select

**Block Grid**from the list of available property editors.

You will see the configuration options for adding Block Types to the Grid as shown below.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-fe5fec9d0dfa3cb6ce66f2b4db4e986edc501400%252FBlockGridEditor_Configuration.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e4848d92&sv=2)

You will also see the following additional configuration options.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-291627f49787168c3859f79593efaa7929d45f4c%252FBlockGridEditor_Configuration-2.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b7f3da79&sv=2)

The Data Type editor allows you to configure the following properties:

**Blocks**- Defines the Block Types available for use in the property. For more information, see[Setup Block Types](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/block-editor/block-grid-editor#setup-block-types). Blocks can also be grouped. This is then visible to editors in the Block Catalogue when populating content, and can also be used to allow a group of Blocks in an Area.**Amount**- Sets the minimum and/or the maximum number of Blocks that should be allowed at the root of the layout.**Live editing mode**- Enabling this option will allow you to see the changes as you are editing them.**Editor width**- Overwrites the width of the property editor. This field takes any valid CSS value for "max-width". For example: 100% or 800px.**Create Button Label**- Overwrites the label on the Create button.**Grid Columns**- Define the number of columns in your Block Grid. The default is 12 columns.**Layout Stylesheet**- Replaces the built-in Layout Stylesheet. Additionally, you can retrieve the default layout stylesheet to use as a base for your own inspiration or for writing your own stylesheet.

Block Types are based on [Element Types](/umbraco-cms/fundamentals/data/defining-content/default-document-types#element-type). These can be created beforehand or while setting up your Block Types.

Once you have added an Element Type as a Block Type on your Block Grid Data Type you have the option to configure it.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5509be958d59695123a86597c67f471f3eb9a357%252FBlockGridEditor_DataType_Blocks.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fc175242&sv=2)

Each Block has a set of properties that are optional to configure. These are described below.

Customize the user experience for your content editors when they work with the Blocks in the Content section.

**Label**- Defines a label for the appearance of the Block in the editor. The label can use[Umbraco Flavoured Markdown](/umbraco-cms/reference/umbraco-flavored-markdown)to display values of properties. The label is also used for search in the**Add Block**dialog during content editing. If no label is defined, the block will not be searchable. The search does not fall back to the block’s name.**Content model**- Presents the Element Type used as model for the Content section of this Block. This cannot be changed but you can open the Element Type to perform edits or view the properties available. Useful when writing your Label.**Settings model**- Adds a Settings section to your Block based on a given Element Type. When selected you can open the Element Type or choose to remove the Settings section again.

**Allow in root**- Determines whether the Block can be created at the root of your layout. Turn this off if you only want a Block to appear within Block Areas.**Allow in areas**- Determines whether the Block can be created inside Areas of other Blocks. If this is turned off it can still be allowed in Block Areas by defining specific allowed Blocks.

Customize the Blocks size in the Grid. If you define multiple options, the Block becomes scalable.

By default, a Block takes up the available width.

A Block can be resized in two ways:

When a Block is placed in an Area, it will fit to the Areas width. Learn more about

[Areas](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/block-editor/block-grid-editor#areas).A Block can have one or more Column Span options defined.


A Column Span option is used to define the width of a Block. With multiple Column Span options defined, the Content Editor can scale the Block to fit specific needs.

Additionally, Blocks can be configured to span rows, this enables one Block to be placed next to a few rows containing other Blocks.

**Available column spans**- Defines one or more columns, the Block spans across. For example: in a 12 columns grid, 6 columns is equivalent to half width. By enabling 6 columns and 12 columns, the Block can be scaled to either half width or full width.**Available row spans**- Defines the amount of rows the Block spans across.

See the [scaling blocks](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/block-editor/block-grid-editor#scaling-blocks) section of this article for an example of how scaling works.

Blocks can nest other Blocks to support specific compositions. These compositions can be used as a layout for other Blocks.

To achieve nesting, a Block must have one or more Areas defined. Each Area can contain one or more Blocks.

Each Area has a size, defined by column and rows spans. The grid for the Areas are based on the same amount of columns as your root grid, unless you choose to change it.

To scale an Area, click and drag the scale-button in the bottom-right corner of an Area.

**Grid Columns for Areas**- Overwrites the amount of columns used for the Area grid.**Areas**- Determines whether the Block can be created inside Areas of other Blocks.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ae25f727ec1076160e4ebcf5a94a2d6136168513%252FBlockGridEditor_Areas.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d4a9be99&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-27a9a510790e07e332bb6dfe70522f6fae76a521%252FBlockGridEditor_AreasConfiguration.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=cc3d6a7a&sv=2)

**Alias**- The alias is used to identify this Area. It is being printed by`GetBlockGridHTML()`

and used as name for the Area slot in Custom Views. The alias is also available for CSS Selectors to target the HTML-Element representing an Area.**Create Button Label**- Overwrites the Create Button Label of the Area.**Number of blocks**- Determines the total number of Blocks in an Area.**Allowed block types**- When this is empty, all Blocks with Permissions for creation in Areas, will be available. This can be overwritten by specifying the allowed Blocks. Define the types of Blocks or Groups of Blocks that are allowed. Additionally, you can also set how many Blocks of each type/group should be present.

When allowing a Group of Blocks, you might want to require a specific amount for a certain Block of that Group. This can be done by adding that Block Type to the list as well, and setting the requirements accordingly.

Advanced properties are also available for each Block, as shown below.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b4ae68e40edcb9cae74d3a3a70a66bbe66222778%252FBlockGridEditor_AreasConfigurationAdvanced.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c6ef11d&sv=2)

**Overlay editor size**- Sets the size for the Content editor overlay for editing this block.**Inline editing mode**- Enabling this will change editing experience to inline, meaning that editing the data of blocks happens at sight as accordions.**Hide content editor**- Hides the UI for editing the content in a Block Editor. This is only relevant if you made a custom view that provides the UI for editing of content.

**Custom view**- Overwrites the view for the block presentation in the Content editor. Building Custom Views for Block representations in Backoffice is the same for all Block Editors.[Read about building a Custom View for Blocks here](/umbraco-cms/customizing/extending-overview/extension-types/block-custom-view)

These properties refer to how the Block is presented in the Block catalogue, when editors choose which Blocks to use for their content.

**Background color**- Define a background color to be displayed beneath the icon or thumbnail. Eg.`#424242`

.**Icon color**- Change the color of the Element Type icon. Eg.`#242424`

.**Thumbnail**- Pick an image or SVG file to replace the icon of this Block in the catalogue.

The thumbnails for the catalogue are displayed at a maximum height of 150px and will scale proportionally to maintain their original aspect ratio. Any standard image format (PNG, JPG, SVG) will work effectively.

Configuring the catalogue appearance improves the content editor experience. A well-designed block catalogue with colors and thumbnails makes it easier for editors to quickly identify and select the right blocks for their content.

When viewing a **Block Grid** property editor in the **Content** section for the first time, you will be presented with the option to **Add content**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b77fcfc125732d5d189edcdfd918410854a5d0b4%252FBlockGridEditor_AddContent.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7203741d&sv=2)

Clicking the **Add content** button opens up the **Block Catalogue**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b519f0b755b68203bac8a61856ed04122932e30a%252FBlockGridEditor_BlockPicker.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=cb72d214&sv=2)

The Block Catalogue looks different depending on the amount of available Blocks and their catalogue appearance.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-826d46925e447679133aaef2829cd77a926723d2%252FBlockGridEditor_BlockPicker_exsetup.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5413a5be&sv=2)

Click the Block Type you wish to create and a new Block will appear in the layout.

More Blocks can be added to the layout by clicking the Add content button. Alternatively, use the Add content button that appears on hover to add new Blocks between, besides, or above the existing Blocks.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-644ec9d1b1a7c7ec8c2b638bc603667009967b64%252FBlockGridEditor_AddContentInline.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a2aa427a&sv=2)

To delete a Block, click the trash icon which appears on the mouse hover.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-aee9a56f88a302639a177a138d8bcf942298bbf2%252FBlockGridEditor_DeleteContent.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c35ce198&sv=2)

Blocks can be rearranged using the click and drag feature. Move them up or down to place them in the desired order.

Moving a Block from one Area to another is done in the same way. If a Block is not allowed in the given position, the area will display a red color and not allow the new position.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b5a762aad5d41735a8da57a4bb3f456f401dbdfe%252FSorting_BlockGrid_Blocks.gif%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c4911924&sv=2)

If a Block has multiple size options it can be scaled via the UI. This appears in the bottom left corner of the Block.

The Block is resized using a click-and-drag feature. Moving the mouse will change the size to the size options closest to the mouse pointer.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f56d714d12bac484be99108827783cd920c3d567%252Fresizing-block-block-grid.gif%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f82ae3a7&sv=2)

Rendering the stored value of your **Block Grid** property editor can be done in two ways:

You can choose to use the built-in rendering mechanism for rendering Blocks using a Partial View for each block.

The default rendering method is named `GetBlockGridHtmlAsync()`

and comes with a few options - for example:

In the sample above `"myGrid"`

is the alias of the Block Grid editor.

If you are using ModelsBuilder, the example will look like this:

To use the `GetBlockGridHtmlAsync()`

method, you will need to create a Partial View for each Block Type. The Partial View must be named using the alias of the Element Type that is being used as Content Model for the Block Type.

These Partial View files need to go into the `Views/Partials/blockgrid/Components/`

folder.

Example: `Views/Partials/blockgrid/Components/MyElementTypeAliasOfContent.cshtml`.


The Partial Views will receive a model of type `Umbraco.Cms.Core.Models.Blocks.BlockGridItem`

. This model contains `Content`

and `Settings`

from your block, as well as the configured `RowSpan`

, `ColumnSpan`

, and `Areas`

of the Block.

The Partial View for the Block is responsible for rendering its own Block Areas. This is done using another built-in rendering mechanism:

Here you will need to create a Partial View for each Block Type within the Block Area. For the name, use the alias of the Element Type that is being used as Content Model for the Block Type.

These Partial Views must be placed in the same folder as before, (`Views/Partials/blockgrid/Components/`

), and will receive a model of type `Umbraco.Cms.Core.Models.Blocks.BlockGridItem`.


The following is an example of a Partial View for a Block Type of type `MyElementTypeAliasOfContent`.


If you are using ModelsBuilder, you can make the property rendering strongly typed by letting your view accept a model of type `BlockGridItem<T>`

. For example:

Using the default rendering together with your layout stylesheet will provide what you need for rendering the layout.

To use the Default Layout Stylesheet, copy the stylesheet to your frontend. You can download the default layout stylesheet from the link within the DataType, we recommend putting the file in the `css`

folder, example: `wwwroot/css/umbraco-blockgridlayout.css`.


A set of built-in Partial Views are responsible for rendering the Blocks and Areas in a Block Grid. If you want to tweak or change the way the Block Grid is rendered, you can use the built-in Partial Views as a template:

Clone the views from . They can be found in

`/src/Umbraco.Web.UI/Views/Partials/blockgrid/`

.Copy the cloned views to the local folder

`Views/Partials/blockgrid/`

.Make changes to your copied views. The entry point for

`GetBlockGridHtmlAsync()`

is the view`default.cshtml`.


The built-in value converter for the Block Grid property editor lets you use the block data as you like. Call the `Value<T>`

method with a type of `BlockGridModel`

to have the stored value returned as a `BlockGridModel`

instance.

`BlockGridModel`

contains the Block Grid configuration (like the number of columns as `GridColumns`

) whilst also being an implementation of `IEnumerable<BlockGridItem>`

(see details for `BlockGridItem`

above).

The following example mimics the built-in rendering mechanism for rendering Blocks using Partial Views:

If you do not want to use Partial Views, you can access the block item data directly within your rendering:

When using Block Grid in a headless scenario with the [Content Delivery API](/umbraco-cms/reference/content-delivery-api), the property outputs a structured JSON representation instead of rendered HTML.

The JSON structure includes:

`gridColumns`

- The number of columns configured for the grid (typically 12)`items`

- An array of block items, each containing:`content`

- The block's content data`settings`

- The block's settings data (if configured)`rowSpan`

and`columnSpan`

- Layout dimensions for the block`areaGridColumns`

- Number of columns for nested areas`areas`

- Array of nested areas within the block, each containing their own items


Your frontend application is responsible for:

Parsing the grid layout structure

Implementing CSS Grid or an equivalent layout system

Rendering blocks recursively to handle nested areas

Handling responsive behavior


For detailed information about the JSON structure and property expansion options, see [Property expansion and limiting](/umbraco-cms/reference/content-delivery-api/property-expansion-and-limiting#block-grid).

The default layout stylesheet is using CSS Grid. This can be modified to fit your implementation and your project.

To make additions or overwrite parts of the default layout stylesheet, import the default stylesheet at the top of your own file.

You need to copy the Default Layout Stylesheet to your frontend. You can download the default layout stylesheet from the link within the DataType, we recommend putting the file in the `css`

folder, example: `wwwroot/css/umbraco-blockgridlayout.css`.


In this case, you would have to write the layout from scratch.

You are free to pick any style, meaning there is no requirement to use CSS Grid. It is, however, recommended to use CSS Grid to ensure complete compatibility with the Umbraco backoffice.

When extending or writing your own layout, you need to know the structure and what data is available.

For example: You can use the below HTML structure:

Building Custom Views for Block representations in Backoffice is based on the same API for all Block Editors.

[Read about building a Custom View for Blocks here](/umbraco-cms/customizing/extending-overview/extension-types/block-custom-view)

In this example, we will be creating content programmatically for a "spot" Blocks in a Block Grid.

Create an element type to represent block content called

**Spot Element**with the following properties:

A property called

**title**with the editor of**Textstring**A property called

**text**with the editor of**Textstring**

Create an element type to represent block content called

**Spot Settings**with the following properties:

A property called

**featured**with the editor of**True/false**.

Add a property called

**blockGrid**in a Document Type.Select

**Block Grid**as the property editor.Click

**Add**in the**Blocks**Settings and select**Spot Element**.Select

**Spot Settings**in the**Settings model**field.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-949ae88fff55a0db297e593e35777434fa392218%252FBlockEditorConfigurationProgramatically.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e7252544&sv=2)

The raw input data for the spots looks like this:

The resulting JSON object stored for the Block Grid will look like this:

For each item in the raw data, we need to create:

One

`contentData`

entry with the*title*and*text*.One

`settingsData`

entry with the*featured*value (the checkbox expects`"0"`

or`"1"`

as data value).One

`layout`

entry with the desired column and row spans.

All `contentData`

and `layoutData`

entries need their own unique `Udi`

as well as the ID (key) of their corresponding Element Types. In this sample, we only have one Element Type for content (`spotElement`

) and one for settings (`spotSettings`

). In a real life scenario, there could be any number of Element Type combinations.

Create a class called

**Model.cs**containing the following to transform the raw data into Block Grid-compatible JSON:

By injecting and into an API controller, we can transform the raw data into Block Grid JSON. It can then be saved to the target content item. Create a class called

**BlockGridTestController.cs**containing the following:

For the above code `IContent? content = _contentService.GetById(Guid.Parse("efba7b97-91b6-4ddf-b2cc-eef89ff48c3b"));`

change the id with your content node that is using the Block Grid.

To test this implementation, run the project and send a

`POST`

request to`/umbraco/api/blockgridtest/create`

after your domain name. If the result shows as**Saved**, then check your content node, and you will see the 2 spotElement contents.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4edfd5aba871c2719c106da2e15a6da06aecc00b%252FBlockEditorContentCreated.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=be1514e4&sv=2)

*This can also be tested via Postman as well if preferred.*

Last updated

Was this helpful?

---

### Block Level Variance | CMS

An intro to achieving content variance at block level.

In a variant context, a Block Editor behaves like any other Umbraco property editor by default. The Blocks contained within the editor "belong" to the Document variant, and there is no connection between Blocks across variants.

In other words, both Block content and structure can vary between each Document variant.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-437c13e81e82f09a61a1cd1bfd51552b93d79960%252Fblock-level-variance-1.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7a6b4cc7&sv=2)

This is the desired behavior for many cases. However, in some cases it is preferable to have a shared Block structure across all variants, where only the Block content varies.

This is known as Block Level Variance:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e20614bac8a3af796a03b28d9c3bd1723716c877%252Fblock-level-variance-2.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5bc0cd12&sv=2)

Block Level Variance is achieved when:

The

[Document Type](/umbraco-cms/fundamentals/data/defining-content/default-document-types#document-type)is configured for variance, andThe Block Editor property is

*not*configured for variance, andThe Block Editor property editor is configured to use

[Element Types](/umbraco-cms/fundamentals/data/defining-content/default-document-types#element-type)that*do*vary.

When adding a new *variant* Block to one Document variant, it is automatically added to all variants of the Document.

The Block will start out in an "unexposed" state for all other Document variants than the one where it was added. It will remain like that for each variant until it is edited in that variant.

The "unexposed" state is visualized by a dimmed-down icon and title (or likely a missing title, if [Umbraco Flavored Markdown](/umbraco-cms/reference/umbraco-flavored-markdown) is used):

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-35b5a386e49e0c81f71e873c0d7d7287020e1959%252Fblock-level-variance-3.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=bffb018d&sv=2)

"Unexposed" Blocks are omitted from the published Document output. So, you do not need to worry about defensive coding to avoid rendering these Blocks.

It is entirely possible to mix and match variance and invariance within the scope of Block Level Variance. Invariance is fully supported, both at Block level and at Block property level.

Invariance within Block Level Variance follows the same rules as invariance at Document level:

Invariant content is added to and updated across all Document variants.

Invariant content is explicitly published for all published Document variants when one or more variants are published.


Consider a Document with English and Danish language variants, which is published in both languages.

An editor opens the English variant.

They add an invariant Block, and

They re-publish the English variant.


**Result:** The new block will appear in both the English and Danish published content.

An editor opens the Danish variant.

They update an invariant property value in a variant Block, and

They re-publish the Danish variant.


**Result:** The updated property value appears in both the English and Danish published content.

The Block Editor structure is *invariant* for Block Level Variance. This means that the structure follows the same rules for invariance as outlined in the section above.

In other words: If an editor changes the order of the Blocks in one Document variant, it changes for all Document variants. The change is applied to all published Document variants, as soon as one or more variants are published.

Last updated

Was this helpful?

---

### Block List | CMS

`Schema Alias: Umbraco.BlockList`


`UI Alias: Umb.PropertyEditorUi.BlockList`


`Returns: IEnumerable<BlockListItem>`


**Block List** is a list editing property editor, using [Element Types](/umbraco-cms/fundamentals/data/defining-content/default-document-types#element-type) to define the list item schema.

The *Block List* replaces the obsolete *Nested Content* editor.

The Block List property editor is configured in the same way as any standard property editor, via the *Data Types* admin interface.

To set up your Block List Editor property, create a new *Data Type* and select **Block List** from the list of available property editors.

Then you will see the configuration options for a Block List as shown below.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-10e35dcea7b7c3c67a6adce9accd1b5fcd2577d9%252FBlockListEditor_DataType.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f02da992&sv=2)

The Data Type editor allows you to configure the following properties:

**Available Blocks**- Here you will define the Block Types to be available for use in the property. For more information, see[Setup Block Types](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/block-editor/block-list-editor#setup-block-types).**Amount**- Sets the minimum and/or maximum number of blocks that should be allowed in the list.**Single block mode**- When in Single block mode, the output will be`BlockListItem<>`

instead of`BlockListModel`

**Live editing mode**- Enabling this will make editing of a block happening directly to the document model, making changes appear as you type.**Inline editing mode**- Enabling this will change editing experience to inline, meaning that editing the data of blocks happens at sight as accordions.**Property editor width**- Overwrite the width of the property editor. This field takes any valid css value for "max-width".

Block Types are **Element Types** which need to be created before you can start configuring them as Block Types. This can be done directly from the property editor setup process. You can also set them up beforehand and add them to the block list after.

Once you have added an element type as a Block Type on your Data Type you will have the option to configure it further.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-917af153ea68bb7e050242887bc0bc6c2e8b557f%252FBlockListEditor_DataType_Blocks.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=88cbb807&sv=2)

Each Block has a set of properties that are optional to configure. They are described below.

You can configure the properties in the group to customize the user experience for your content editors. This helps them to quickly identify and select the right blocks for their content.

**Label**- Define a label for the appearance of the Block in the editor. The label uses[Umbraco Flavoured Markdown](/umbraco-cms/reference/umbraco-flavored-markdown)to display values of properties. The label is also used for search in the**Add Block**dialog during content editing. If no label is defined, the block will not be searchable. The search does not fall back to the block’s name.**Overlay editor size**- Set the size for the Content editor overlay for editing this block.

It is possible to use two separate Element Types for your Block Types. Its required to have one for Content and optional to add one for Settings.

**Content model**- This presents the Element Type used as model for the content section of this Block. This cannot be changed, but you can open the Element Type to perform edits or view the properties available. Useful when writing your Label.**Settings model**- Add a Settings section to your Block based on a given Element Type. When picked you can open the Element Type or choose to remove the settings section again.

These properties refer to how the Block is presented in the Block catalogue, when editors choose which Blocks to use for their content.

**Background color**- Define a background color to be displayed beneath the icon or thumbnail. Eg.`#424242`

.**Icon color**- Change the color of the Element Type icon. Eg.`#242424`

.**Thumbnail**- Pick an image or SVG file to replace the icon of this Block in the catalogue.

The thumbnails for the catalogue are displayed at a maximum height of 150px and will scale proportionally to maintain their original aspect ratio. Any standard image format (PNG, JPG, SVG) will work effectively.

Configuring the catalogue appearance improves the content editor experience. A well-designed block catalogue with colors and thumbnails makes it easier for editors to quickly identify and select the right blocks for their content.

These properties are relevant when you work with custom views.

**Force hide content editor**- If you made a custom view that enables you to edit the content part of a block and you are using default editing mode (not inline) you might want to hide the content-editor from the block editor overlay.

When viewing a **Block List** editor in the Content section for the first time, you will be presented with the option to add content.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a92b78f20c53650163c4ea982c85441b4ac7dae8%252FBlockListEditor_AddContent.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=99054937&sv=2)

Clicking the "Create new" button brings up the Block Catalogue. If you only have a single block configured, this button will display "Add {block type name}".

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ea77a24f1be54dee0b3a99d0d157640b6c8b4ceb%252FBlockListEditor_BlockPicker_simplesetup.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e2af0d6b&sv=2)

The Block Catalogue looks different depending on the amount of available Blocks and their catalogue appearance.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-48ca8012ceb6499227d127c9595a3226b971b423%252FBlockListEditor_BlockPicker.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=752e5af0&sv=2)

Click the Block Type you wish to create and a new Block will appear in the list.

Depending on whether your Block List Editor is setup to use default or inline editing mode you will see one of the following things happening:

In default mode you will enter the editing overlay of that Block:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-72dfd74bcebc9411b42b9f70ddb52bdc2e39c214%252FBlockListEditor_EditingOverlay.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=63a66db9&sv=2)

In inline editing mode the new Blocks will expand to show its inline editor:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1885624076da1068d03460e3071a64379fa17bb8%252FBlockListEditor_InlineEditing.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b549f71a&sv=2)

More Blocks can be added to the list by clicking the "Create new" button. You can also use the inline Add button that appears on hover between or above existing Blocks.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8b20c59740b53d275b09ada3770408d242ed9494%252FBlockListEditor_AddContentInline.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c33750ec&sv=2)

To reorder the Blocks, click and drag a Block up or down to place in the desired order.

To delete a Block click the trash-bin icon appearing on hover.

Rendering the stored value of your **Block List** property can be done in two ways.

You can choose to use the built-in rendering mechanism for rendering blocks via a Partial View for each block.

The default rendering method is named `GetBlockListHtml()`

and comes with a few options to go with it. The typical use could be:

"MyBlocks" above is the alias for the Block List editor.

If using ModelsBuilder the example can be simplified:

Example:

To make this work you will need to create a Partial View for each block. The partial view should be named by the alias of the Element Type that is being used as Content Model.

These partial views must be placed in this folder: `Views/Partials/BlockList/Components/`

. Example: `Views/Partials/BlockList/Components/MyElementTypeAliasOfContent.cshtml`.


A Partial View will receive the model of `Umbraco.Core.Models.Blocks.BlockListItem`

. This gives you the option to access properties of the Content and Settings section of your Block.

In this example of a Partial view for a Block Type, the `MyElementTypeAliasOfContent`

and `MyElementTypeAliasOfSettings`

should correspond with the selected Element Type Alias for the given model.

Example:

With ModelsBuilder:

A built-in value converter is available to use the data as you like. Call the `Value<T>`

method with a generic type of `IEnumerable<BlockListItem>`

and the stored value will be returned as a list of `BlockListItem`

entities.

Example:

Each item is a `BlockListItem`

entity that contains two main properties `Content`

and `Settings`

. Each of these is a `IPublishedElement`

which means you can use all the value converters you are used to using.

Example:

Sometimes, you might want to use the Block List Editor to hold some data and not necessarily render a view. This applies when the data should be presented in different areas on a page. An example could be a product page with variants stored in a Block List Editor.

In this case, you can extract the variant's data using the following, which returns `IEnumerable<IPublishedElement>`.


Example:

If using ModelsBuilder the example can be simplified:

Example:

If your Block List Editor only uses a single block, you can cast the collection to a specific type. Supply a type `T`

using `.OfType<T>()`

, otherwise the return value will be `IEnumerable<IPublishedElement>`.


Building Custom Views for Block representations in Backoffice is the same for all Block Editors. [Read about building a Custom View for Blocks here](/umbraco-cms/customizing/extending-overview/extension-types/block-custom-view)

Last updated

Was this helpful?

---

---


## Checkbox List | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-798ccd419be2f139dd2d37a01ac7c63cfd813f32%252Fcheckbox-list-setup.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4a0f70e2&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-091b76744a6b77968cb054d0907e149a99c3935b%252Fcheckbox-list-content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3446152a&sv=2)

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.CheckBoxList`


`UI Alias: Umb.PropertyEditorUi.CheckBoxList`


`Returns: IEnumerable<string>`


Displays a list of preset values as a list of checkbox controls. The text saved is an IEnumerable collection of the text values.

Unlike other property editors, the Option IDs are not directly accessible in Razor.

Data Type Definition Example

You can use dictionary items to translate the options in a Checkbox List property editor in a multilingual setup. For more details, see the [Creating a Multilingual Site](/umbraco-cms/tutorials/multilanguage-setup#translating-multi-value-property-editors) article.

Content Example

MVC View Example

Without Models Builder

With Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@{
    if (Model.HasValue("superHeros"))
    {
        <ul>
            @foreach (var item in Model.Value<IEnumerable<string>>("superHeros"))
            {
                <li>@item</li>
            }
        </ul>
    }
}
```

```
@{
    if (Model.SuperHeros.Any())
    {
        <ul>
            @foreach (var item in Model.SuperHeros)
            {
                <li>@item</li>
            }
        </ul>
    }
}
```

```
@using Umbraco.Cms.Core.Serialization
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@inject IJsonSerializer Serializer
@{
    // Create a variable for the GUID of the page you want to update
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Set the value of the property with alias 'superHeroes'.
    content.SetValue("superHeroes", Serializer.Serialize(new[] { "Umbraco", "CodeGarden"}));

    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234);
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'superHeroes'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.SuperHeroes).Alias, Serializer.Serialize(new[] { "Umbraco", "CodeGarden"}));
}
```

---


## Code Editor | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ddd16be02348c874b3483c319a906ebec561fcc3%252FCode-Editor-definition-example.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e1a16f0a&sv=2)

Configuration

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-061c5e3c5ebeb96642ae8846665f2c6bc597fb18%252FCode-Editor-content-example.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=828d6ecc&sv=2)

MVC View Example

Without Models Builder

With Modelsbuilder

Add values programmatically

Last updated

Was this helpful?

`Schema Alias: Umbraco.CodeEditor`


`UI Alias: Umb.PropertyEditorUi.CodeEditor`


`Returns: String`


The Code Editor property editor provides an interface for entering and editing code snippets. It offers features like syntax highlighting, line numbering, wrapping code and so on.

Data Type Definition Example

Configuration

The Code Editor can be configured with the following settings:

**Language**: A dropdown to select the syntax highlighting and validation rules for the editor. Supported languages include`C#`

,`CSS`

,`HTML`

,`JavaScript`

,`JSON`

,`Markdown`

,`Razor (CSHTML)`

, and`TypeScript`

.**Height**: Allows you to specify the height of the editor in pixels (for example., 400px). This ensures the editor fits well within your content entry forms.**Line Numbers**: A toggle to enable or disable the line number on the left side of the editor.**Minimap**: A toggle to enable a high-level, zoomed-out visual overview of the code on the right side of the editor for faster navigation in long files.**Word Wrap**: A toggle that determines if long lines of code should wrap to the next line or require horizontal scrolling.

Content Example

MVC View Example

Without Models Builder

With Modelsbuilder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

Last updated

Was this helpful?

Was this helpful?

```
@if (Model.HasValue("codeEditor"))
{
    var codeSnippet = Model.Value<string>("codeEditor");
    <pre><code>@codeSnippet</code></pre>
}
```

```
@if (Model != null && !string.IsNullOrEmpty(Model.CodeEditor))
{
    <pre><code>@Model.CodeEditor</code></pre>
}
```

```
@using Umbraco.Cms.Core.Services;

@inject IContentService Services;
@{
    // Get access to ContentService
    var contentService = Services;

    // Create a variable for the GUID of your page
    var guid = new Guid("ca4249ed-2b23-4337-b522-63cabe5587d1");

    // Get the page using the GUID you've just defined
    var content = contentService.GetById(guid);

    // Define your code string
    string newCode = "body {\n  background-color: red;\n}";

    // Set the value of the property with alias 'codeEditor'
    content.SetValue("codeEditor", newCode);

    // Save the change
    contentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = contentService.GetById(1234);
}
```

---


## Collection | CMS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-63e85069886c8025c020e20d5b8221eea006d742%252Flistview-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=81368532&sv=2)

Configure Collection

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f15477d46b6eddacdfdad47a270039a236dca652%252Fenable-listview-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5195818a&sv=2)

Settings

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9b989d6017663212ae464d626e70cb544a3cf3ec%252Fcollection-settings-example-15-1.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4864b820&sv=2)

Columns Displayed

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-375af70dc02e9e08b40408ed85876582ca776199%252Fcollection-property-picker.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d8b461e&sv=2)

Layouts

Order By

Order Direction

Page Size

Workspace View icon

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e9ed8be01f58b8d603b43afdc7864738c2f993e1%252Flist-icon.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ea14ae4c&sv=2)

Workspace View name

Show Content Workspace View First

Content Example

Generic field value

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-30d0e0033ec3b8b988e2b60a64d1f3028b8151ad%252Fcollection-label-template.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4bcf4321&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d54e5d4a712a9b3bf32b8a151a00daebb2d83606%252Fcollections-display-email.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6944dbac&sv=2)

Content name

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a20251e88768c5ace588baef372103336e1f6473%252Fcontent-picker-property.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ac06061a&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f0e664a416bbebe8a94aa8c8c59d1b6d99e91366%252Fcollection-column-content-picker.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=200cff7b&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9726d5c05ea804c3635e82c8a0b293497964fa18%252Fcontent-picker-picked-value.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7e2839dd&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-cfb2e51eb9f1f7b1d74820fedfd891b0747f8cd4%252Fcollection-view-cards-content-picker.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4b73c74c&sv=2)

Last updated

Was this helpful?

---


## Color Picker | CMS

Data Type Definition Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c6ea4a2cd1fe32212668dbb0d9cf0899cf5e9972%252FColor-Picker-DataType.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c12d1e31&sv=2)

Content Example

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1bf70361a19ee2437a319c746665624068523fe8%252FColor-Picker-Content-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ca503e51&sv=2)

Example with Models Builder

Example without Models Builder

Add values programmatically

Without labels

With labels

Last updated

Was this helpful?

`Schema Alias: Umbraco.ColorPicker`


`UI Alias: Umb.PropertyEditorUi.ColorPicker`


`Returns: String (Hexadecimal)`


`Returns: Umbraco.Cms.Core.PropertyEditors.ValueConverters.ColorPickerValueConverter.PickedColor (When using labels)`


The Color picker allows you to set some predetermined colors that the editor can choose between.

It is possible to add a label to use with the color.

Data Type Definition Example

Content Example

Example with Models Builder

Example without Models Builder

Add values programmatically

See the example below to see how a value can be added or changed programmatically. To update a value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Without labels

With labels

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

Was this helpful?

```
@{
     // Model has a property called "Color" which holds a Color Picker editor
    var hexColor = Model.Color;
    // Define the label if you've included it
    String colorLabel = Model.Color.Label;

    if (hexColor != null)
    {
        <div style="background-color: @hexColor">@colorLabel</div>
    }
}
```

```
@using Umbraco.Cms.Core.PropertyEditors.ValueConverters
@{
    // Model has a property called "Color" which holds a Color Picker editor
    var hexColor = Model.Value("Color");
    // Define the label if you've included it
    var colorLabel = Model.Value<ColorPickerValueConverter.PickedColor>("Color").Label;

    if (hexColor != null)
    {
        <div style="background-color: @hexColor">@colorLabel</div>
    }
}
```

```
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Set the value of the property with alias 'color'. 
    // The value set here, needs to be one of the colors on the Color Picker
    content.SetValue("color", "38761d");

    // Save the change
    ContentService.Save(content);
}
```

```
@using Umbraco.Cms.Core.Services
@inject IContentService ContentService
@{
    // Create a variable for the GUID of the page you want to update
    var guid = Guid.Parse("32e60db4-1283-4caa-9645-f2153f9888ef");

    // Get the page using the GUID you've defined
    var content = ContentService.GetById(guid); // ID of your page

    // Set the value of the property with alias 'color'. 
    // The value set here, needs to be one of the colors on the Color Picker
    content.SetValue("color", "{'value':'000000', 'label':'Black', 'sortOrder':1, 'id':'1'}");

    // Save the change
    ContentService.Save(content);
}
```

```
@{
    // Get the page using it's id
    var content = ContentService.GetById(1234); 
}
```

```
@using Umbraco.Cms.Core.PublishedCache
@inject IPublishedContentTypeCache PublishedContentTypeCache
@{
    // Set the value of the property with alias 'color'
    content.SetValue(Home.GetModelPropertyType(PublishedContentTypeCache, x => x.Color).Alias, "38761d");
}
```

---


## Content Picker | CMS

`Schema Alias: Umbraco.ContentPicker`


`UI Alias: Umb.PropertyEditorUi.DocumentPicker`


`Returns: IEnumerable<IPublishedContent>`


The Content Picker enables choosing the type of content tree to display and which specific part to render. It also allows you to set a dynamic root node for the content based on the current document using the Content Picker.

The Content Picker was formerly known as the **Multinode Treepicker** in version 13 and below.

The renaming is purely a client-side UI change, meaning the property editor still uses the `Umbraco.MultiNodeTreePicker`

schema alias.

The change was made as the word **Content** in the backoffice acts as an umbrella term covering Documents, Media, and Members.

**Are you looking for the original Content Picker?**

The Content Picker from version 13 and below has been renamed [Document Picker](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/document-picker).

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4079d60ffc6e48e1c6ef4400170dcbb78bb126ad%252FContentPicker-data-type-definition.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=beb2f866&sv=2)

Define a limit on the number of items allowed to be selected.

Checking this field allows users to choose nodes they normally cannot access.

This option allows for configuring what type of content is available when using the Data Type. The available types of content are Content, Members, or Media items.

When selecting Content from the dropdown, the option to specify a root node, also called the **origin**, becomes available.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6fa69a0a132a31d2fadd3879a78dc2bc1daac418%252Fspecify-root-node.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7a14d5f0&sv=2)

When picking the **origin** there are several different options available:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4ddf2b83716638ad64e537bcf5918b7cb6fe9edf%252Fpick-origin-root-node.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d7b166bf&sv=2)

The following options are available when picking the origin:

**Content Root**: The root of the content tree.**Root**: The root is the first level item of the sub-tree of the current node.**Parent**: The parent is the nearest ancestor of the current node.**Current**: The current node.A picker that uses the current node, cannot pick anything when the current node is created, as it will not have any children.


**Site**: The nearest ancestor of the current node with a domain assigned.**Specific node**: A specific node selected from the existing content.

When an origin has been specified, it becomes possible to continue to build a *Dynamic Root* by adding additional query steps.

Navigate the content tree relative to the specified origin to execute multiple query steps and find the root node needed.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e180bb29a747d471e7415dafc37a3d88ca60bceb%252Fappend-step-to-query.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=82f86fe1&sv=2)

The following options are available:

**Nearest Ancestor or Self:**Find the nearest ancestor or current item that fits with one of the configured Document Types.**Furthest Ancestor or Self:**Find the furthest ancestor or current item that fits with one of the configured Document Types.**Nearest Descendant or Self:**Find the nearest descendant or current item that fits with one of the configured Document Types.**Furthest Descendant or Self:**Find the furthest descendant or current item that fits with one of the configured Document Types.

The options above are all based on navigating the document hierarchy by locating ancestors and descendants. It is possible to execute **custom steps** to build even more complex queries. Once a custom query is available it will be added to the bottom of the *Append steps to query* dialog. Learn more about [adding custom query steps in the section below](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/content-picker#adding-a-custom-query-step).

Each query step takes the output from the origin or the previous step as input. It is only ever the result of the last query step that is passed to the next step.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0204da0e2a632e1ddd2dfbbbccba2cbf8d6a69f3%252Fcontent-picker-query-steps.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=2f57315b&sv=2)

Custom query steps can be used to solve specific use cases, such as traversing sibling documents or matching property values. Before the custom query steps can be selected in the Data Type settings, they must be defined via code.

When implementing a query step it requires a collection of origins and information about the query step. The collection is taken from where the name specified in the UI can be found.

**Specifying the origin is required** for the custom query step to become available.

Read the [Node Type section](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/content-picker#node-type) above to learn more about this.

You can inject dependencies into the constructor. These dependencies could be custom repositories or the `IVariationContextAccessor`

, if you want to use the current culture.

The `ExecuteAsync`

method receives a set of content keys from the last executed query step or the origin. It has to return a new set of content keys.

To register the custom query step, append it to the existing query steps, `DynamicRootSteps()`

. This is done from a composer as shown below.

Finally, register the custom query step on the client side and provide a brief description.

You can do this in an `umbraco-package.json`

file, as shown below:

Choose which types of content should be available to pick using the Content Picker.

This is done by selecting one or more Document Types.

Consider the following tree structure where the Document Type alias is presented in square brackets.

Codegarden

2023 [

`year`

]Talks [

`talks`

]...

Umbraco anno MMXXIII [

`talk`

]

Stages [

`stages`

]Social Space [

`stage`

]No 10 [

`stage`

]No 16 [

`stage`

]The Theatre [

`stage`

]


2022 [

`year`

]Talks [

`talks`

]...


Stages [

`stages`

]Main Stage [

`stage`

]The Barn [

`stage`

]The Theatre [

`stage`

]




Consider configuring a Content Picker on the `talk`

Document Type to select a `stage`

for the `talk`

. Here, you want to display only the stages for the actual year. To do this, you need to set the parent as the origin.

For instance, if you are on the `Umbraco anno MMXXIII`

node, the collection of content keys passed into the first query step will only contain the `Talks`

content node.

First, query for the nearest ancestors of the type

`year`

. This will return`2023`

.Second, query for the nearest descendants of the type

`stages`.


When opening the picker on the `Umbraco anno MMXXIII`

node, it will now show the children of the node on the path `Codegarden > 2023 > Stages`.


See the example below to see how a value can be added or changed programmatically. To update the value of a property editor you need the .

The example below demonstrates how to add values programmatically using a Razor view. However, this is used for illustrative purposes only and is not the recommended method for production environments.

Although the use of a GUID is preferable, you can also use the numeric ID to get the page:

If Models Builder is enabled you can get the alias of the desired property without using a magic string:

Last updated

Was this helpful?

---
