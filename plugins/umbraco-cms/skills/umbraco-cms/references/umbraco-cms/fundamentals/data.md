# Data

## Contents

- [Using Tabs | CMS](#using-tabs-cms)
- [Content Version Cleanup | CMS](#content-version-cleanup-cms)
- [Creating Media | CMS](#creating-media-cms)
- [Data Types | CMS](#data-types-cms)
- [Defining Content](#defining-content)
- [Dictionary Items | CMS](#dictionary-items-cms)
- [Members | CMS](#members-cms)
- [Relations | CMS](#relations-cms)
- [Scheduled Publishing | CMS](#scheduled-publishing-cms)
- [Users | CMS](#users-cms)

---

## Using Tabs | CMS

In this section, an overview is given of how to add and reorder tabs, convert a group to a tab and manage the “Generic” tab.

Using tabs, you can organize properties in the backoffice to provide a tailored and efficient workflow for editors creating and maintaining Content, Media and Members.

Tabs allow you to add horizontal organization in your Document Types, Media Types and Member Types. This is handy for types that need a more defined hierarchy or have many properties and groups.

To add a tab, follow these steps:

Go to

**Settings**.Create or select a

**Document Type/Media Type/Member Type**and click**Add tab**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-73e5077434efba521be9d2a5d10b213978d232dd%252FAdd-tab.png.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=63356db4&sv=2)

Add tab

When adding the first tab, all existing groups are automatically added to the tab.

To reorder tabs, follow these steps:

Go to

**Settings**.Select a

**Document Type/Media Type/Member Type**.Select

**Reorder**.You can drag the tab where you want, manually add a numeric value next to the tab name or use the arrows to set a value.

This is important when using compositions, as you want to always display a tab/group at a certain position by setting a manual numeric value.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f72d6585209e9587938e47130893f177c5723276%252FReorder-tabs.gif%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4927cb6&sv=2)

Reorder tabs Select

**I am done reordering**.Click

**Save**.

To convert a group to a tab, follow these steps:

Go to

**Settings**.Select a

**Document Type/Media Type/Member Type**.Select

**Reorder**.You can drag the group to the

**Convert to tab**option.Select

**I am done reordering**.Click

**Save**.

Converting a tab back into a group is not possible, as tabs can contain groups, and nested groups are unsupported. To overcome this, create a new group and transfer all tab properties into it, then delete the empty tab.

Once you start adding tabs, you might see a “Generic” tab appear. This is done to hold groups and properties that are not assigned to a tab. For example, a group of properties coming from a composition that has no tab. In order to display the groups and properties correctly and have a solid data structure, they will be displayed under the “Generic” tab.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8f0056f27c569fba01263e737f4de134a3358f8a%252FGeneric-tab.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=63a97f24&sv=2)

To manage the **Generic** tab on a **Document Type/Media Type**:

Go to the

**Composition**Document Type/Media Type.Click

**Add tab**and enter the**Name**for the tab. All existing groups and properties are added to the tab.Go to the

**Document Type/Media Type**, the**Generic**tab will now be replaced by the tab from the composition.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e37c0a3fee9d12fea9f2a93c41ef38b6f95b7061%252FComposition-add-tab.gif%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1c5080c2&sv=2)

Composition Add Tab

Last updated

Was this helpful?

---

## Content Version Cleanup | CMS

A new version is created whenever you save and publish a content item in Umbraco. This is how you can roll back to a previous version. Every saved version stores a record in the database, not only for the version but also for each content item property for that version. In a multi-lingual site, further rows are added for every culture variation. Over time this amount of data can build and swallow up the capacity of your SQL Server and slow the performance of the Umbraco backoffice.

The default cleanup policy will:

Not delete any versions created over the previous 4 days. The recent version history is preserved. See the

`KeepAllVersionsNewerThanDays`

setting.'Prune' versions 4 days after they are created. The last version of a content item saved on a particular day will be kept but earlier versions from that day will be deleted.

Delete all versions older than 90 days. See the

`KeepLatestVersionPerDayForDays`

setting.Never delete any versions that are currently 'published'.

Never delete any specific versions marked as 'Prevent Cleanup' in the Backoffice version history.


Based on the default cleanup policy, you can roll back content to the latest version saved on a particular day as long as it was

Created within the last 90 days, or

Marked as "Prevent Cleanup" in the Backoffice version history.


The **History** section, which acts as an audit log, is not cleared out, and will continue to show logs for versions older than 90 days.

The feature can be configured in the `appSettings.json`:


```
{
  "Umbraco": {
    "CMS": {
      "Content": {
        "ContentVersionCleanupPolicy": {
          "EnableCleanup": true,
          "KeepLatestVersionPerDayForDays": 90,
          "KeepAllVersionsNewerThanDays": 4
        }
      }
    }
  }
}
```

For sites with stricter requirements, it is possible to opt-out of both options globally, see [ContentSettings](/umbraco-cms/reference/configuration/contentsettings#content-version-cleanup-policy) and by Document Type.

Additionally, it is possible to keep the feature enabled but mark specific versions to keep forever.

It is worth noting that whilst we delete rows, we do not shrink database files or rebuild indexes. For upgraded sites with a lot of history you may wish to perform these tasks. If they are not part of your regular database maintenance plan already.

It is possible to override the global settings per Document Type in the backoffice to prevent unwanted cleanup. This can be managed in the "permissions" Content App for each Document Type.

![Content Version Cleanup - Document Type overrides](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-12d9deb094fea61b487ce25384b4b357081720c4%252Fimage%2520%2822%29.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=debd2a1c&sv=2)

It is possible to mark important content versions as "prevent cleanup" to ensure they are never removed. This happens via the new and improved rollback modal which can be found on the "info" content app for each document.

Open rollback modal.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e50e559391b6940d8ba1754b822bb84f9dfb125b%252Fprevent-cleanup-part-1.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4ccd5fe3&sv=2)

Click

**Prevent cleanup**button for each important version.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-55051c7c9acb88eed27d11397f22de9d68442efc%252Fprevent-cleanup-part-2.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f262d67&sv=2)


Last updated

Was this helpful?

---

## Creating Media | CMS

Learn how to work with different types of Media content on your Umbraco website.

Media in Umbraco CMS is handled the same way as content. You define **Media Types** that act as a base for media items. The following default Media Types are available:

Article - used for uploading and storing documents.

Audio - used for uploading and storing digital audio files.

File - used for uploading and storing different types of files in the Media section.

Folder - a container for organizing media items in the Media section tree.

Image - used for uploading and storing images.

Vector Graphics (SVG) - used for uploading and storing Scalable Vector Graphics (SVG) files which are text files containing source code to draw the desired image.

Video - used for uploading and storing video files.


The default Media Types aim to cover most needs for media on a website. You do not need to define your Media Types to start using the Media section. The tools for organizing and uploading the media are already in place.

If you have upgraded from an older version than 8.14 the Media Types listed above are not added automatically. You can add those types manually yourselves by following the steps below ['Creating a new Media Type'](/umbraco-cms/fundamentals/data/creating-media#creating-a-media-type). On the [default media types page](/umbraco-cms/fundamentals/data/creating-media/default-media-types), you will find a detailed overview of all Media Types.

You can upload media in two different ways:

From the **Media** section in the Umbraco backoffice, you can add new media items by following either of the approaches defined below:

Use the

**Create**dialog to create a new Media item in the Media sectionThe Media item will be created based on the type you choose.

Upload the image or file, give the Media item a name, and click

**Save**.

![Upload Media - Create Button](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b8e8bf6135cd3ad582cd17b7319ac7b3e06015fd%252Fimage%2520%2812%29.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=909ec425&sv=2)

Upload Media - Create Button Use the Drag and drop feature to add your files to the Media section.

Umbraco will automatically detect the Media Type and create the Media item.

You can drop entire folder structures to recreate that same structure in the Media section.


![Upload Media - Media section](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7fec9b4d8d0d7d7c243abe15f5d21f325f72d958%252Fimage%2520%2813%29.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fbc5551d&sv=2)

Upload Media - Media section

New media items can be added to your site without interrupting the content creation flow. This can be done following either of the two approaches outlined below.

Drag and drop the image(s) from your file explorer directly into the Media Picker property on the Content page.

Images added this way is automatically added to the user's start node in the Media section of the Umbraco backoffice.



![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9ffe47785c560dde0aaa1fd284297647104b98b2%252Fupload-images-from-content.gif%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1d4b83c4&sv=2)

Select the "+" icon to open the "Select media" dialog where you can add images from your file explorer directly or using drag and drop.


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1b44a15a995ea0de507075b8bf6b950bb0f75e01%252Fadd-image-from-dialog.gif%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f9838968&sv=2)

It is always a good idea to start by creating a folder for your media items. It can be a good idea to align these folders with the content on your website. This will give the editors a better overview of the files and enable them to upload media items in the correct place.

Follow these steps to create a folder in the Media section:

Go to the

**Media**section.Select

**...**next to**Media**.Select

**Create**.Select

**Folder**.Enter a name for the folder and select

**Save**in the bottom-right corner.

The **Image** Media Type has 5 properties: **Upload Image**, **Width**, **Height**, **Size**, and **Type**. These are populated once the image is uploaded. The properties can be viewed in the **Media** section and accessed in your Templates.

Except for the **Folder** Media Type, the other Media Types have 3 properties: **Upload Image**, **Type**, and **Size**.

Learn more about each Media Type in [the article about default Media Types](/umbraco-cms/fundamentals/data/creating-media/default-media-types).

The default view for the Media section is a card view that lets you preview the different files that have been uploaded.

![Media Section - Cardview](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-41aa73274463df9f34de82a641481d6c1b288820%252Fimage%2520%2814%29.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=790426c4&sv=2)

By selecting multiple media items it is possible to perform bulk operations like moving or deleting the items.

To edit properties on a single media item, click the name of the item, which you will see once you hover over the item.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5e5a75ec5d799d3055fcd008daab4986d2f9e991%252Fhover-over.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=42398d86&sv=2)

From the top-right corner of the Media section, you can toggle between the list and grid view. There is also an option to search for the items in the Media section.![Media Section - List view](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6fbc1af8ed8df0b3471786797d67de0b40f6523a%252Fswitch-view-v14.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=13fd537f&sv=2)


By adding a **Media Picker** property to a Document Type the editor will have the ability to select media items when creating content.

You can create custom Media Types and control the structure of the Media tree as you would with Document Types. This means you can store information that is specific to the media on the item itself.

A Media Type is created in the **Settings** section using the Media Type editor.

Go to the

**Settings**section.Click

**...**next to**Media Types**.Click

**Create**>**New Media Type**.Name the new Media Type

**Employee Image**.Choose an icon by selecting the icon left of the name field.


You will now see the Media Type editor. It is similar to the editor used for creating Document Types.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c553d42cca0bc1ba8f4d18183f8b5a282e8a905d%252Fcreate-new-media-type-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e58e06f1&sv=2)

Having different folders for different Media Types makes it possible to restrict where media items can be created and added. Only allowing PDF uploads in a certain folder and employee images in another make it easier to keep the Media section organized.

Before we start adding properties to the Media Type we need to add a group to put these in.

Click on

**Add group**.Call the group

*Image*.

We need to add the same properties as on the default **Image** Media Type. These are:

`umbracoFile`

`umbracoWidth`

`umbracoHeight`

`umbracoBytes`

`umbracoExtension`


Follow the steps outlined below to add the properties to the Media Type:

Click

**Add property**.Name it

*Upload image*.Change the alias to

*umbracoFile*.Click

**Select property editor**.Select

**Image cropper**.Rename the editor

*Employee Image Cropper*.Add two new crops called

*Thumbnail*(200px x 350px) and*wideThumbnail*(350px x 200px).

![Defining crops](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f3d1ddd61d8e3c4cf8984aa20179f342b147ba93%252Fnew-data-type-v14.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=a81f4114&sv=2)

**Save**.
9. Click **Add**.
10. Name the remaining four properties *Width*, *Height*, *Size*, and *Type*, and give them the aliases as mentioned above. They should all use the **Label** editor.

As mentioned before these properties will automatically be populated once an image has been uploaded.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7ae7b5eb115df0a71e8efeb6e076c9c3a6850191%252Ffinished-new-media-type-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=10a7e0a8&sv=2)

Next up, we will create a folder to hold the employee images. We could use the existing **Folder** Media Type but that would mean editors can upload employee images to any folder of that type. If we create a folder specifically for employee images there is only one place to put them.

Go back to the

**Settings**section and create a new Media Type.Name it

*Employee Images*.Select the folder icon by clicking the icon to the left of the name.

Navigate to the

**Structure**tab.Click

**Configure as a Collection**under**Presentation.**Choose

**List view - Media.**

![Configure Collection](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-bdc9ac877de55f32bd00802a0276a2b8815a70b5%252Fconfigure-collection-v14.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=f9f18442&sv=2)

**Save**.

The new folder is created under the Media Types folder. We also need to only allow the Employee Image Media Type in our new folder. Both of these configurations can be set on the **Structure** tab.

Go to the

**Structure**tab of the*Employee Images*folder.Toggle the

**Allow at root**.Click

**Choose**in the**Allowed Child Node Types**.Select

**Employee Image**.Click

**Choose**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-fd2bb2ffdb336cc989366e3ebdea3619f4c7be79%252Femployee-images-permissions.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d65388fd&sv=2)

Go to the

**Media**section.Select

**...**next to Media.Click

**Create**>**Employee Images**folder.![Employee Images](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f1e09a83d862f6b3d38c89dcbc9211c19ef3f785%252Femployee-images-folder.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=39c3170e&sv=2)

Name it

*Employee Images*.Click

**Save**.

Uncheck the **Allow at root** option on the **Employee Images** Media Type to prevent the creation of multiple folders of this type. This will only disable the creation of new ones and not affect existing folders.

If you select an image that has been uploaded to the folder you will see the full image and the two defined crops.

Moving the focal point circle on the image will update the crops to focus accordingly. You can also edit the individual crops by selecting them and moving the image or adjusting the slider to zoom.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ba6a9b601e5566af4dbdeb1b41f02f0b2b1c80c3%252Fcrops-and-focal-point-geo.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=edd6dd0&sv=2)

Last updated

Was this helpful?

### Default Data/Media Types | CMS

Data Types

UploadArticle

UploadAudio

UploadVectorGraphics

UploadVideo

Media Types

UmbracoMediaArticle

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-fff82eeba5baa590554aaa6910f50717cf0eaf69%252Fumbraco-media-article-media-type.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=224521d7&sv=2)

UmbracoMediaAudio

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-194c4dc201a1125334e6b22f82df167e6365c5a9%252Fumbraco-media-audio-media-type.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ac03b3eb&sv=2)

UmbracoMediaVectorGraphics

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e5957f78e7987a0a6c7362d52c282103808d4aec%252Fumbraco-media-vector-graphicsmedia-type.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=eb3511a6&sv=2)

UmbracoMediaVideo

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a0cdd81bcf09c12a89b7b1c545d7391ba39f77a7%252Fumbraco-media-video-media-type.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3f1defd0&sv=2)

Last updated

Was this helpful?

On this page you will find the media types and Data Types in Umbraco. These types are not created automatically after an upgrade. If you want to use the new types, you can create them yourself.

After upgrading, the default media types are not created automatically. If you create them manually, make sure to:

Set the permission for each of the media types to

**Allow at root**.Ensure that the

**Folder**media type allows the new media types as children.

Data Types

UploadArticle

The `UploadArticle`

Data Type has the following configuration:

Property editor:

`FileUpload`

Accepted file extensions:

`pdf`

,`docx`

,`doc`


UploadAudio

The `UploadAudio`

Data Type has the following configuration:

Property editor:

`FileUpload`

Accepted file extensions:

`mp3`

,`weba`

,`oga`

,`opus`


UploadVectorGraphics

The `UploadVectorGraphics`

Data Type has the following configuration:

Property editor:

`FileUpload`

Accepted file extensions:

`svg`


UploadVideo

The `UploadVideo`

Data Type has the following configuration:

Property editor:

`FileUpload`

Accepted file extensions:

`mp4`

,`webm`

,`ogv`


Media Types

UmbracoMediaArticle

The `UmbracoMediaArticle`

media type has the following properties:

`umbracoFile`

- Upload File`umbracoExtension`

- Label (string)`umbracoBytes`

- Label (bigint)

UmbracoMediaAudio

The `UmbracoMediaAudio`

media type has the following properties:

`umbracoFile`

Upload Audio`umbracoExtension`

Label (string)`umbracoBytes`

Label (bigint)

UmbracoMediaVectorGraphics

The `UmbracoMediaVectorGraphics`

media type has the following properties:

`umbracoFile`

- Upload Vector Graphics`umbracoExtension`

Label (string)`umbracoBytes`

Label (bigint)

UmbracoMediaVideo

The `UmbracoMediaVideo`

media type has the following properties:

`umbracoFile`

- Upload Video`umbracoExtension`

- Label (string)`umbracoBytes`

- Label (bigint)

You can also create localization files for Media Types. You can read more about this in the [Document Type Localization](/umbraco-cms/fundamentals/data/defining-content/document-type-localization) article.

Last updated

Was this helpful?

Was this helpful?

---

## Data Types | CMS

Learn about the data types in Umbraco.

*A Data Type defines the type of input for a property. So when adding a property (on Document Types, Media Types and Members) and selecting the Type you are selecting a Data Type. There are preconfigured Data Types available in Umbraco and more can be added in the Settings section.*

A Data Type can be something basic such as TextString, Number, True/False and so on. Or it can be more complex such as Multi Node Tree Picker, Image Cropper, Block Grid and so on.

The Data Type references a Property Editor and if the Property Editor has settings these are configured on the Data Type. This means you can have multiple Data Types referencing the same Property Editor.

An example of this could be to have two dropdown Data Types both referencing the same dropdown Property Editor. One configured to show a list of cities, the other a list of countries.

Follow these steps to create a new Dropdown Data Type:

Go to the

**Settings**section within the backoffice.Select the

**+**icon to the right of the**Data Types**folder.Choose

**New Data Type...**.Name the Data Type.

Click on

**Select a property editor**.Find and click on the

**Dropdown**editor.Click

**Select**.Choose whether to enable multiple selections.

Add

**options**.**Save**the Data Type once you have added the required configuration.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-741b15b8d3bf8bf8baa276d8855a3931a0e9f356%252Fdropdown-data-type-sample.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1f8044cd&sv=2)

**Data Type configuration**

**Property Editor** This is where you pick the Property Editor UI that the Data Type will be referencing. By default, Umbraco ships with a wide selection to choose from. Learn more about each of them in the [Default Data Types](/umbraco-cms/fundamentals/data/data-types/default-data-types) article.

In the **Settings** box below, the configuration options specific to the chosen Property Editor UI will be available. Some Property Editors have many configuration options while some only have a few.

When you're happy with the list press **Save**. It is now possible to select this Data Type for a property on Document Types, Media Types, and Members. Doing this will then create a dropdown list for the editor to choose from and save the choice as a string.

To customize an existing Data Type go to the **Settings** section, expand the **Data Types** folder and select the **Data Type** you want to edit.

Besides the Data Types that are available out of the box there are some additional **Property Editors**. For example, think of the **Slider** and **Block List**.

To view the Data Type reference, go to the **Settings** section and expand the **Data Types** folder. Select the **Data Type** you wish to view the reference for and click the **Info** tab.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e911c377f9fbd56303b9c03afcd1e508d4f13d3e%252Fviewing-data-type-reference.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=667ff60e&sv=2)

This gives you an overview of the Types that currently use the Data Type.

Learn more about viewing references or implementing tracking in the [Tracking References](/umbraco-cms/customizing/property-editors/tracking) article.

Last updated

Was this helpful?

### Default Data Types | CMS

Learn about the default data types in Umbraco.

Here's a list of the default Data Types that come installed with Umbraco. There are plenty more that you can create based on the installed [Property Editors](/umbraco-cms/fundamentals/backoffice/property-editors).

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f7341191ae5005b9fb91d97a1ad2ea6583c0de91%252Fdefault-data-types-9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=62413a2f&sv=2)

Adds a list of approved colors. The approved colors are added as hex values by using the color picker. Optionally, you can enable labels to give the colors different names.

Displays a list of preset options as a list of checkbox controls. The preset options are added when configuring a Property Editor using the Data Type. Alternatively, the options can also be updated in the **Settings** section under **Data Types**. The value saved is a comma-separated string of IDs.

The Content Picker opens a modal to pick a specific page from the content structure. The value saved is the selected page's ID.

Displays a calendar UI for selecting date and time. The value saved is a standard DateTime value but does not contain time information.

Displays a calendar UI for selecting date and time. The value saved is a standard DateTime value.

Displays a list of preset options as a list where only a single value can be selected. The default Data Type does not contain any predefined options. The value saved is the selected value as a string.

Displays a list of preset options as a list where multiple values can be selected. The default Data Type does not contain any predefined options. The value saved is a comma-separated string of IDs.

Allows to upload and crop images by using a focal point. Specific crop definitions can also be added. This Data Type is used by default on the Image Media Type.

The Image Media Picker opens a modal to pick images from the **Media** tree or images from your Computer. The value saved is the selected media node UDI.

Is a non-editable control and can be used to *only* display the value. It can also be used in the **Media** section to load in values related to the node, such as width, height and file size.

There are six Label Data Types:

Label (bigint) - Allows to save a big integer value for a Label.

Label (datetime) - Allows to set a DateTime value for a Label.

Label (decimal) - Allows to set a decimal value for a Label.

Label (integer) - Allows to set an integer value for a Label.

Label (string) - Allows to set a long string value for a Label.

Label (time) - Allows to set time for a Label


This Data Type is used by **Document Types** that are set to display as a Collection.

This Data Type is used by **Media Types** that is set to display as a Collection.

This Data Type is used by **Member Types** that is set to display as a Collection.

The picker opens a modal to pick a specific media item from the Media tree. The value saved is the selected media node UDI.

Displays a dropdown with all the available members. A single member can be selected. The value saved is the ID of the member.

This Data Type allows an editor to add an array of links. These can either be internal Umbraco pages external URLs or links to media in the Media section. The Data Type can be configured by limited number of links it is possible to add.

The picker opens a modal to pick multiple images from the **Media** tree. The value saved is a comma separated string of media node UDIs.

The picker opens a modal to pick multiple media items from the **Media** tree. The value saved is a comma separated string of media node UDIs.

A textbox to input a numeric value.

This Data type enables editors to choose from a list of radiobuttons.

A TipTap-based What You See Is What You Get (WYSIWYG) editor. This is the standard editor used to edit a larger amount of text. The editor has a lot of settings, which can be changed on the Richtext editor Data Type in the Settings section.

Learn more about the configuration options in the [Rich Text Editor articles](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/rich-text-editor).

A textbox that allows you to use multiple tags on a **Document Type**. You can specify a Tag Group for the Data Type, if you need to use Tags on different sections of your site.

A textarea provides a multi-line plain-text editing control. You can set the maximum allowed characters for the textarea and the number of rows, if any.

A normal HTML input text field.

A checkbox which saves either 0 or 1, depending on the checkbox being checked or not. A common use is to create a property with the 'umbracoNaviHide' alias and the Data Type True/False. This will provide editors with the option to hide nodes in the navigation menu on the website.

Adds an upload field, which allows documents or images to be uploaded to Umbraco. This does not add them to the media library, they are added to the document data.

There are five Upload Data Types:

Upload Article - Used for uploading and storing documents.

Upload Audio - Used for uploading and storing digital audio files.

Upload File - Used for uploading and storing different types of files in the Media section

Upload Vector Graphics - Used for uploading and storing Scalable Vector Graphics (svg) files which are text files containing source code to draw the desired image.

Upload Video - Used for uploading and storing video files.


Last updated

Was this helpful?

---

## Defining Content

### Contents

- [Default Document Types | CMS](#default-document-types-cms)
- [Document Type Localization | CMS](#document-type-localization-cms)

---

### Default Document Types | CMS

On this page, you will find the default Document Types in Umbraco. If you want to use these document types, you can create them in the Settings section.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2ff143255d47ca5a591484791f41830cc7de2205%252FCreateDoctype.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ddd44501&sv=2)

Document Type

Document Type with Template

Element Type

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e568ea61e176ebbbb6c1527b02ab9f843d1400af%252FElement-Type.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f3234a1c&sv=2)

Folder

Last updated

Was this helpful?

---

### Document Type Localization | CMS

Setup localization for Document Types in the Umbraco backoffice.

Registering Document Type localization Files

```
{
  "name": "Document Type Localization",
  "extensions": [
    {
      "type": "localization",
      "alias": "DocumentType.Localize.En",
      "name": "English",
      "meta": {
        "culture": "en"
      },
      "js": "/App_Plugins/DocumentTypeLocalization/doctype-en.js"
    }
  ]
}
```

Creating localizations

Applying localizations

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c14a6bb5ca35e3f03417c5bf2c37bd14378f5e13%252Flocalization-document-type-editor-validation-v15.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3d2b8d37&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9f3533c9eab90560a568451d5cbe788d108fa117%252Flocalization-document-type-editor-v15.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6a02654&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-58b02eb6b1c7fc91622b40689087dc92743bb36c%252Flocalization-document-editor-create.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b03827d3&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-47ed19ed8814e61b96535bc918c525dd14df4c99%252Flocalization-document-editor-v15.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e713e0b3&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a81ce08060873ef2f487955a1375576e419ab570%252Flocalization-document-editor-validation.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e1cb0f2c&sv=2)

Last updated

Was this helpful?

Setup localization for Document Types in the Umbraco backoffice.

The Umbraco backoffice is localized to match the [user's configured UI Culture](/umbraco-cms/tutorials/multilanguage-setup#changing-the-default-backoffice-language-of-a-user).

When defining a Document Type, you can apply localization to:

Document Type names and descriptions.

Property names and descriptions.

Custom property validation messages.

Tab and group names.


Setting up localization for Document Types is a three-step process:

Register the Document Type localization files via

[a new manifest 'umbraco-package.json' file](/umbraco-cms/customizing/extending-overview/extension-types/localization#registering-localization).Create the localizations in

[user defined Document Type localization files](/umbraco-cms/customizing/extending-overview/extension-types/localization#the-localization-file).Apply the localizations to the Document Type.


Everything in this article also applies to defining [Media Types](/umbraco-cms/fundamentals/backoffice#media-types) and [Member Types](/umbraco-cms/fundamentals/backoffice#member-types).

Registering Document Type localization Files

To register Document Type localizations, you must create a new manifest using an `umbraco-package.json`

file.

The `umbraco-package.json`

file is only registered when placed directly in the `/App_Plugins/`

or `/App_Plugins/{SubFolderName}`

folder. It will not be recognized in nested subfolders.

umbraco-package.json

```
{
  "name": "Document Type Localization",
  "extensions": [
    {
      "type": "localization",
      "alias": "DocumentType.Localize.En",
      "name": "English",
      "meta": {
        "culture": "en"
      },
      "js": "/App_Plugins/DocumentTypeLocalization/doctype-en.js"
    }
  ]
}
```

Creating localizations

Once you have registered the Document Type localization, you can add your localization texts for use in Document Types. The following localizations are used for the samples in this article:

Umbraco must be restarted to register the localization manifest. Any subsequent localization text changes will need to be reloaded within the browser.

Applying localizations

The localizations are applied by using the syntax `#{area alias}_{key alias}`.


Create a

**Document Type with Template**called`#contentTypes_article`

with the**alias**:`articlePage`

.Under the newly created Document Type, follow these steps:

Set the

**description**to`#contentTypes_article-desc`

.Create a new

**tab**called`#tabs_content`

.Add a new

**group**called`#groups_titles`

.Add a

**property**called`#properties_title`

with**alias**`title`

.Set the description to

`{#properties_title-desc}`

.Use a

`TextString`

editor.Set the field validation to

`mandatory`

.Under validation add

`#properties_title-message`.




Property descriptions support [Umbraco Flavored Markdown](/umbraco-cms/reference/umbraco-flavored-markdown), which uses a different syntax (wrapped in brackets) to avoid conflicts with Markdown headers.

Add a

**property**called`#properties_subTitle`

with**alias**`subTitle`

.Set the description to

`{#properties_subTitle-desc}`

.Use a

`TextString`

editor.

Enable

`Allow at root`

in the**Structure**tab.

When creating and editing the content, you will see that the backoffice now uses the configured localizations.

Create a new "Article" node:


When trying to save the node without adding the mandatory content, you will see a warning as expected:


Last updated

Was this helpful?

Was this helpful?

doctype-en.js

```
export default {
    contentTypes: {
        article: 'Article page',
        'article-desc': 'A textual, article-like page on the site. Use this as the main type of content.',
        landing: 'Landing page',
        'landing-desc': 'An inviting, very graphical page. Use this as an entry point for a campaign, and supplement with Article pages.'
    },
    tabs: {
        content: 'Page content',
        seo: 'SEO configuration',
    },
    groups: {
        titles: 'Page titles'
    },
    properties: {
        title: 'Main title',
        'title-desc': 'This is the main title of the page.',
        'title-message': 'The main title is required for this page.',
        subTitle: 'Sub title',
        'subTitle-desc': 'This is the sub title of the page.',
    }
};
```

---

---

## Dictionary Items | CMS

Creating Dictionary Items in Umbraco

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b69dbefae0e5adeb3b8b3bbcbec37fbb29e39cdc%252Fdictionary-item.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=685f698a&sv=2)

Adding a Dictionary Item

Grouping Dictionary Items

Editing Dictionary Items

Fetching Dictionary Values in the Template

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0e03646e5a2b0030dfcdfd4031e1ed66ec60fa48%252Frendering-dictionary-item.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5ea98423&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e43fc16234cc2a7096fcfcb4c93b3642bc62a9b0%252Frendering-altvalue-dictionary-item.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=2ed0850e&sv=2)

Importing and exporting Dictionary Items

Exporting Dictionary Items

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c9c209d1ce5214bebb64a84d8ed4b690d2d41ea5%252Fexport.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=195a9758&sv=2)

Importing Dictionary Items

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-97c5508a8f8c556058fb63427f9498dc3a41700a%252Fimport.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d941fed6&sv=2)

Using Dictionary Item in a Multilingual website

Related Links

Last updated

Was this helpful?

---

## Members | CMS

Members are used for registering and authentication external / frontend users of an Umbraco installation. This could be Forum members and Intranet members.

Members are used for registering and authenticating external users of an Umbraco installation (ie. forum members, intranet users and so forth).

This guide will explain how to define and create members in the backoffice. If you want to work with members using the service APIs, links can be found at the end of the document.

There is a default Member Type that can be used to create members. You can customize this to fit your needs or create your own Member Type from scratch.

Go to the **Members** section and click **Create**.

Members have a number of mandatory properties that need to be filled in before a member can be saved. Some of the properties are **Username**, **Email**, two **Password fields** and so on.

There are also a number of default properties which are stored in the database in the tables `Member`

and`TwoFactorLogin`:


`umbracoMemberFailedPasswordAttempts`

`umbracoMemberApproved`

`umbracoMemberLockedOut`

`umbracoTwoFactorLogin`

`umbracoMemberLastLockoutDate`

`umbracoMemberLastLogin`

`umbracoMemberLastPasswordChangeDate`


Once the Member is created and saved you can access it by expanding the Members tree and clicking **All Members** to get a collection. You can also view members of a specific type by selecting the member type in the Members tree.

Sensitive properties on a members data will not be displayed to backoffice users unless they have appropriate permissions. In order to see the values of the default properties in the **Member** tab you need to have the Sensitive data User Group. By having this group added to a user they will also have the option to mark member type properties as sensitive.

More information can be found under [security](/umbraco-cms/reference/security/sensitive-data-on-members).

You can create your own Member Types and add tabs, groups and properties as you would with Document Types.

Go to the **Settings** section, click **...** next to **Member Types** and select **Create**. You will now be taken to the Member Type editor that is used to define and edit the Member Type. Name the new Member Type and click **Save**.

Once created, the Member Type will have no properties, so you have the freedom to add your own properties or compositions.

When creating a Member Type you can assign compositions. Compositions allow you to inherit tabs and properties from existing member types instead of creating them from scratch.

For example on the member type that you have created, click on **Composition**. Then you can choose the existing **Member** type which then you will inherit its tabs, groups, and properties.

The default **Member** type has a **Membership** group which includes `umbracoMemberComments`

property along with the other default properties. The other properties can be seen only in the **Member** tab when creating a member.

It is possible to add more groups and more properties to each of the Member Types you create, as well as the default Member Type.

Member Groups define roles for your members that can be used for role-based protection. A member can be in multiple groups.

To create a new Member Group click the menu icon next to the **Member Groups** node in the Members section. Choose **Create**, name the group, and save the group.

To assign a member to a specific group find the member you wish to assign and find the **Properties** group. Here you can see which groups the member is already part of. You can also add the member to more groups or remove the member from already assigned groups:

As a developer you are able to leverage your website when you build on the Members section of Umbraco. The member's section is by default in the Umbraco backoffice, but you can still use it to implement some work on your front end. Members are created using ASP.NET Core Identity, so there are some provider settings that can be set in appsettings.json - here are the defaults:

You can find out more about the services methods in the reference section of the documentation by following the links below.

Last updated

Was this helpful?

---

## Relations | CMS

Learn about relations and how to create and manage them.

Umbraco sections are built around the concept of 'trees' and there is an implicit relationship between items in a section tree.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1ace04fdb615474f953cca3f8ff2ce24f29bd4d8%252Fparent-siblings-children.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=903ad66c&sv=2)

We refer to these relationships in the manner of a 'Family Tree'. One content item might be the 'Parent' of some content items, and those items would be referred to as the 'Children' of that parent. Items within the same branch of the tree can also be described as 'Ancestors' or 'Descendants' of an item.

There are methods available to support querying content items by their relative position to the current page. This is possible using the following concepts: `Model.Ancestors()`

, `Model.Children()`

, or `Model.Descendants()`.


In some cases there are no direct relationships between two items in a tree, but they are still somehow 'related'. This could be the alternate language translation pages of a content page.

In other cases there is a 'relation' between different types of entities. This could be a relation between Content and Member, or Member and MediaFolder. You might need to be able to retrieve and display the uploaded images from a specific logged-in Member.

These are the scenarios where the concept of **Umbraco Relations** provides a solution.

Umbraco Relations allow you to relate almost any object in Umbraco to almost any other Umbraco object. This is done by defining a new *Relation Type*.

With a Content, Member, or Media picker the relationship only works as a 1-way street. The content item knows it has 'picked' another content item but that other content item does not know where it has been picked.

Umbraco Relations works as a 2-way street. When creating a relation between two different types of entities, it will be possible to find one entity from the other and vice versa. As an example this provides the option to list out all the pages that a content banner had been picked on.

A Relation Type specifies how two types of entities are related. Two items might be related under multiple Relation Types, and you might only be interested in your 'Related Language Page' Relation Type.

It is possible to view the existing Relation Types from the Umbraco backoffice:

Access the Umbraco Backoffice.

Navigate to the

**Settings**section.Locate the

**Advanced**group in the sidebar.Select

**Relations**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2a55e85f9b05be5cdb7188ff8b86b0d3d665bf99%252FRelations-in-the-backoffice.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f8861e9a&sv=2)

On the dashboard all defined relations will be listed. Select a Relation to view a list of all the objects that have been related for that specific Relation Type.

You can create Relations using the RelationService API via code.

[Some examples are provided here in the RelationService Documentation Page](/umbraco-cms/reference/management/using-services/relationservice)

You might want to create a 'Relation' between two objects either as:

A response to a backoffice event. For example, a content item being published that has picked other content items. Storing a relationship between these items would make querying between them easier. Perhaps show all the pages on which a particular 'banner' has been picked.

A logged-in member on the front end of an Umbraco website might have the facility to upload images. In response, the implementation could store the photos programmatically in the Media Section and at the same time, create a Relation to record the relationship between the member and their uploaded pictures. On an image gallery page, it would be possible to display all the gallery images for the current logged-in Member using the relations.


Some of the community packages that use Relations are listed below:

- a content picker that automatically creates Relations.

- allows you to relate two items via the Backoffice.

- Provides a LinkedPages context item to show, edit, and add relations between content pages.


Last updated

Was this helpful?

---

## Scheduled Publishing | CMS

Each document in Umbraco can be scheduled for publishing and unpublishing on a pre-defined date and time.

Each document in Umbraco can be scheduled for publishing and unpublishing on a pre-defined date and time.

You can find the options to do this click on the arrow next to the **Save and publish** button and pick **Schedule...**

![Scheduled publishing](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0c35835d2070624dc53fe55388aac77faa8c4871%252Fimage%2520%2819%29.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=cd5dff8d&sv=2)

This will open a **Schedule Publishing** dialog where you can specify dates and time.

Your server may be in a different timezone than where you are located. You are able to select a date and time in your timezone and Umbraco will make sure that the item gets published at that time. So, if you select 12 PM then the item will be published at 12PM in the timezone you are in. This may be 8 PM on the server, which is indicated when you select the date and time.

![Scheduled publishing time](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7d9e34527fcaebeaf6b0ca2e608081678a7f3f46%252Fimage%2520%2820%29.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c8eca459&sv=2)

If you are in the same timezone as the server, this message will not appear under the date picker.

In Umbraco versions lower than 7.5, the time you select has to be the time on the server. These older versions of Umbraco do not detect your local time zone.

All users with access to the Content section in the Umbraco backoffice are able to schedule content for publishing/unpublish.

In some cases you will need to adjust your configuration to ensure that scheduled publishing/unpublishing works. The schedule works by the server sending an HTTP(S) request to itself.

If you are in a load balanced environment special care must be given to ensure you've configured this correctly, [see the docs here](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/file-system-replication)

If you are not load balancing, the way that Umbraco determines the base URL to send the scheduled HTTP(S) request to is as follows:

umbracoSettings:settings/web.routing/@umbracoApplicationUrl if it exists

*(see*[these docs](/umbraco-cms/reference/configuration/webroutingsettings)*for details)*Else umbracoSettings:settings/scheduledTasks/@baseUrl if it exits

*(deprecated)*Else umbracoSettings:distributedCall/servers if we have the server in there

*(deprecated, see load balance docs)*Else it's based on the first request that the website receives and uses the base URL of this request

*(default)*

If the `umbracoApplicationUrl`

is used, the value also specifies the scheme (either HTTP or HTTPS). The request for scheduled publishing will always be sent over HTTPS if the appSettings `umbracoUseSSL`

is set to `true`.


If your scheduled publishing/unpublishing is not working as expected it is probably an issue that your server cannot communicate with the scheduled publishing endpoint. This can be caused by a number of reasons such as:

Url rewrites in place that prevent the endpoint from being reached

DNS misconfiguration not allowing the server to communicate to the base URL used in the first request that the website receives - which could be directly affected by a firewall/Network Address Translation (NAT)/load balancer that your server sites behind

Secure Sockets Layer (SSL) and/or umbracoUseSSL misconfiguration not allowing the server to communicate to the scheduled publishing endpoint on the correct http/https scheme


To better diagnose the issue you can temporarily change your log4net config settings to be `DEBUG`

instead of `INFO`

. This will give you all sorts of information including being able to see whether or not the scheduled publishing endpoint is being reached or not.

In some cases it might be easiest to specify the [umbracoSettings:settings/web.routing/@umbracoApplicationUrl](/umbraco-cms/reference/configuration/webroutingsettings) setting. This is to ensure that your server is communicating to itself on the correct URL.

Last updated

Was this helpful?

---

## Users | CMS

Learn how to create, manage, and assign permissions to users in the Umbraco backoffice.

Users are people who have access to the Umbraco backoffice (not to be confused with [Members](/umbraco-cms/fundamentals/data/members)). These could include Content Editors, Translators, Web Designers, and Developers.

This guide will walk you through how to create and invite users, manage user profiles, work with User Groups and permissions in the backoffice.

To create or invite a User:

Go to the

**Users**section in the backoffice.Select

**Create -> User**. Alternatively, click**Invite...**.Enter the

**Name**and**Email**of the new user.Select which

**User group**the new user should be added to.*[Optional]*Enter a**Message**for the invitation.Click

**Create user**or**Send invite**.

Once you have created the user, the new user will receive a system-generated password for their initial login. This password needs to be used to access the account.

Open a user’s profile from the **Users** section to update:

Profile photo.

Email address of the user.

UI Culture (sets the backoffice language of the user account).

User Group (determines the scope of access in the backoffice).

Start nodes for both Content and Media sections to limit access.


When working with multiple users in Umbraco, the user screen provides tools to help you quickly locate and manage users using filters and layout options.

At the top of the Users section, use the search bar to quickly find a user by typing their name or email address.

Use the **Status** filter to narrow down users based on their current state:

Active – Users who have logged in and are enabled.

Disabled – Users whose access has been explicitly turned off.

Locked out - User has been automatically blocked from logging in after too many failed login attempts.

Invited - User has been invited to access the Umbraco backoffice.

Inactive – Users who haven't logged in or have been disabled.


The **Groups** filter lets you view users based on the user groups they belong to. For example, Administrators, Editors, Sensitive data, Translators, and Writers.

Use **Order by** to sort users by:

Name (A–Z)

Name (Z-A)

Newest

Oldest

Last Login


Users are displayed in Grid format by default, showing:

Initials, full name, and group membership.

Login status (for example, “Inactive” label).

Last login time (if applicable).


Click the table/grid icon (top-right corner) to switch to a more compact, column-based layout.

By default, the User Groups available to new users are **Administrators**, **Editors**, **Sensitive Data**, **Translators,** and **Writers**.

**Administrators**: Can do anything when editing nodes in the content section (has all permissions).**Editors**: Allowed to create and publish content items or nodes on the website without approval from others or restrictions (has permissions to**Public Access**,**Rollback**,**Browse Node**,**Create Content Template**,**Delete**,**Create**,**Publish**,**Unpublish**,**Update**,**Copy**,**Move**and**Sort**).**Sensitive data**: Any users added to this User group will have access to view any data marked as sensitive. Learn more about this feature in the[Sensitive Data](/umbraco-cms/reference/security/sensitive-data-on-members)article.**Translators**: These are used for translating your website. Translators are allowed to browse and update nodes as well as grant dashboard access. Translations of site pages must be reviewed by others before publication (has permissions to**Browse Node**and**Update**).**Writers**: Allowed to browse nodes, create nodes, and save content. Not allowed to publish directly but has permissions to**Browse Node**,**Create**, and**Update**.

In previous versions of Umbraco, "Send to publish" was enabled for Writers. Since Umbraco 16, approval processes can be configured using the official .

You can also create your own custom User Groups and add properties and tabs as you would with Document Types and Member Types.

Go to the

**Users**section.Select

**User Groups**.Click

**Create**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9fff1b7f592f1856ab34ba89ed180d8b6fe164f6%252Fuser-groups-menu-v16.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=655503dc&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9eaef60cbe2c9153600e62d86350439665dd4f3d%252Fuser-groups-v16.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=42bc4e2b&sv=2)

Enter the information about the User Group and settings for custom properties:

**Name**: The name of the User Group.**Alias**: Used to reference the User Group in code - the alias will be auto-generated based on the name.**Assign access**: Define which sections and languages the users will have access to. Also, if the users should have access to only some or all content and media.**Default Permissions**: Select the default permissions granted to users of the User Group.**Granular permissions**: Define a specific node the users in the group should have access to.

Depending on which User Group a user is added to, each user has a set of permissions associated with their accounts. These permissions either enable or disable a user's ability to perform their associated function.

The available user Permissions are defined under **Default Permissions** in the User group.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f16114eafb828ad4503e3606cefcdc5ae17d2793%252Fdefault-permissions-v16.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4716076f&sv=2)

As an addition to the Default Permissions, it is also possible to add more granular permissions on a User Group level.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-cc1455ca16da3c672260e6d72c93a2e34fee52c7%252Fgranular-permissions.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e53e0303&sv=2)

With the **Documents** permission, you can define granular permissions on specific documents. This is useful when a User Group should only have limited access to a certain page on the website. Clicking **Add** opens a dialog where you can choose between documents from the Content section.

With the **Document Property Values** permission, you can define both read and write permissions for individual properties on a Document Type. This is useful if a User Group should have limited access to edit the content on a specific type of document. Clicking **Add** opens a dialog where you select a Document Type, choose a Property, and, finally, set the read and write permissions.

When a new user is created, you can set specific permissions for that user on different domains and subdomains. You can also set permissions on different User Groups, even for the default types.

As a developer, you are only able to leverage your website from the backoffice when you build on the Users section of Umbraco. This is because the Users section is restricted to the Umbraco backoffice.

Umbraco Forms has a backoffice security model integrated with Umbraco Users. You can manage the details in the **Users** section of the backoffice, within a tree named **Forms Security**.

Last updated

Was this helpful?

### API Users | CMS

This guide will explain the concept of API Users, how they differ from regular Users, and how to define them

Last updated

Was this helpful?

This guide will explain the concept of API Users, how they differ from regular Users, and how to define them

API Users allow for authorizing [external access](/umbraco-cms/reference/management-api/external-access) to the Management API.

An API User is identical to a [regular User](/umbraco-cms/fundamentals/data/users) except for one thing: It has no password. In fact, API Users are not allowed to log into the backoffice like regular Users.

Instead, API Users hold the Client Credentials used to authorize against the Management API. When an external source authorizes using Client Credentials, it effectively assumes the identity of the API User.

Since API Users are identical to regular Users their backoffice access can be controlled in the same way. This allows for imposing detailed access control on the external sources connected to the Management API.

Client IDs for API Users are explicitly prefixed with `umbraco-back-office-`

. This guards against API Users accidentally taking over one of the Client IDs used by the Umbraco core.

Creating an API User

To create an API User:

Go to the

**Users**section in the backoffice.Select

**Create -> API User**.Enter the

**Name**and**Email**of the new API user.Select which

**User group**the new user should be added to.Click

**Create user**.

Last updated

Was this helpful?

Was this helpful?

---
