# Editors Manual

## Contents

- [Getting Started With Umbraco](#getting-started-with-umbraco)
- [Media Management](#media-management)
- [Tips And Tricks](#tips-and-tricks)
- [Version Management](#version-management)
- [Working with Rich Text Editor | CMS](#working-with-rich-text-editor-cms)

---

## Getting Started With Umbraco

### Contents

- [Copying a Page | CMS](#copying-a-page-cms)
- [Creating, Saving and Publishing Content Options | CMS](#creating-saving-and-publishing-content-options-cms)
- [Deleting and Restoring Pages | CMS](#deleting-and-restoring-pages-cms)
- [Editing Existing Content | CMS](#editing-existing-content-cms)
- [Finding Content | CMS](#finding-content-cms)
- [Logging In and Out | CMS](#logging-in-and-out-cms)
- [Moving a Page | CMS](#moving-a-page-cms)
- [Sorting Pages | CMS](#sorting-pages-cms)
- [Umbraco Interface | CMS](#umbraco-interface-cms)

---

### Copying a Page | CMS

Re-use a page or a tree structure you have previously created by copying the parent page and its child pages to a different section within the site structure.

When you copy a parent page all of its child pages are also copied, by default. You can choose if you want to copy the child pages or not. You can also choose whether the links should be automatically updated or continue to link to the original pages.

You can copy a page in two ways:

Go to

**Content**.Click

**...**next to the page you wish to copy.Select

**Duplicate to**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d40aee86cc3feb1019a6ca3d63eb2042ca39ea34%252Fduplicate.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=2c44d191&sv=2)

Copy Menu 1 A window appears on the right side of the screen. Here, you can choose where you want to copy the page in the tree structure.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-cb71b9fc229b4e0d3644b4c92b01f8db27581294%252Fduplicate-options.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d85c7eb4&sv=2)

Copy Option 1 Toggle

**Relate to original**button if you want to keep the links linked to the original page.Toggle

**Include descendants**if you want to copy the child pages alongside the parent page.Click

**Duplicate**.A confirmation message appears. Click

**OK**to dismiss the confirmation message.

Go to

**Content**.Select the page you wish to copy.

Click

**Actions**in the top-right corner of the screen.Select

**Duplicate to**from the**Actions**drop-down menu.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-db5be1b15384373837f8f3146e529f643fbae8f9%252Factions-duplicate-menu.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=bc78fdaa&sv=2)

Actions Menu A window appears on the right side of the screen. Here, you can choose where you want to copy the page in the tree structure.

Toggle

**Relate to original**button if you want to keep the links linked to the original page.Toggle

**Include descendants**if you want to copy the child pages alongside the parent page.Click

**Copy**.A confirmation message appears. Click

**OK**to dismiss the confirmation message.

When you select **Relate to original**, Umbraco will create a relationship between the original and copied page. This relationship can be used to programmatically link the pages - For example, linking two pages in a multilingual setup. This relationship **does not** sync the content between the original and copied page.

Last updated

Was this helpful?

---

### Creating, Saving and Publishing Content Options | CMS

In this section, you will get an overview of how to create and save pages. You will also learn more about how to publish and unpublish your content.

If you are a Cloud user, you will also learn how to compare and transfer content between environments. In Umbraco Cloud, an environment is a separate workspace such as Development, Staging, or Live/Production. It lets you preview and test changes before moving them to your live site. For more information about environments, see the article in the Umbraco Cloud documentation.

Select the parent page to create your new page. The parent page can be the home page or any of the sub-pages of the site.

If the parent page allows sub-pages underneath it, follow these steps:

Hover over the name of the parent page in the

**Content**section and click**•••**to view the types of pages you can create.Select the page type you wish to create. The new page is loaded in the editor on the right-hand side.

Enter a

**Name**for the page and click**Save**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5ee1fac059f297270606765281c47e85d9b51c3d%252Fcreating-new-page.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=55fbb08e&sv=2)

New Page

There are three different options for saving and publishing pages. The options vary depending on whether you’re still in the process of editing the page or have completed your edits and wish to publish your changes.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-113ccc8254d4e6b501b71485151508d6b56492aa%252FSave-and-publish-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=942581af&sv=2)

The **Save and preview** button allows you to save your changes and preview it before publishing the changes to the live site. The **Preview** feature shows you how the page will look once it is published. This **Save and preview** feature only saves your page and does not publish your contents to the live site.

The **Save** button is used for saving the page without publishing the changes to the live site. The **Save** feature is especially useful if you are working on changes over a period of time as you can save your changes frequently to prevent losing any data.

The **Save and publish** button is used to publish a previously saved page to the live website or to publish a page without previewing it. The **Save and publish** feature will save and publish the page to your live website.

The **Save and publish** button has three options:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5557a16f1a92d375abbc391eaf5090b3dcd17f77%252Fschedule.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1965dad5&sv=2)

The **Schedule** button allows you to set a time and a date for when your page should be published. With this option, you can continue working on your edits and the site will automatically be published at the time and date it was scheduled to.

To set up scheduled publishing, follow these steps:

Navigate to the page you want to publish.

Select the arrow next to the

**Save and Publish**button.Select

**Schedule**.In the

**Scheduled Publishing**window, set the date and time in the**Publish at**field.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-359ab6c03ab5ba5678770a4837630f94121b21e5%252Fscheduled-publishing.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6f377fa5&sv=2)

Scheduled publishing Select

**Schedule**.

The **Publish with descendants** button allows you to publish the current page and all the content linked to this page to the live site. Using this option, you can publish the current parent page and it's child nodes, previously published, and unpublished content items.

To publish the node with descendants, follow these steps:

Navigate to the page you want to publish.

Select the arrow next to the

**Save and Publish**button.Select

**Publish with descendants**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c6747b157e9352e7fc4e5036a13afc8fec22c7b3%252FPublish-with-descendants-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e5939ee0&sv=2)

Publish with descendants Toggle the option to

**Include unpublished content items**if you wish to. This option includes all unpublished content items for the selected page and the descendant pages.

The **Unpublish** button allows you to unpublish a page if you do not want a page to be publicly visible and do not want to delete it.

To unpublish a page, follow these steps:

Navigate to the page you want to unpublish.

Select the arrow next to the

**Save and Publish**button.Select

**Unpublish**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f89130a593592e4b1adede4aa7e1bbdca9b44174%252Funpublish.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7b0e71d1&sv=2)

You can also unpublish your page by setting the date and time using the **Schedule** feature.

To set up scheduled unpublishing, follow these steps:

Navigate to the page you want to unpublish.

Select the arrow next to the

**Save and Publish**button.Select

**Schedule**.In the

**Scheduled Publishing**window, set the date and time in the**Unpublish at**field.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-359ab6c03ab5ba5678770a4837630f94121b21e5%252Fscheduled-publishing.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6f377fa5&sv=2)

Scheduled unpublishing Select

**Schedule**.

**Compare** content is available in all Umbraco Cloud projects running the latest version of Umbraco Deploy for Umbraco versions 8 and 9.

Compare Content allows previewing content changes before transferring them to another environment. This is helpful to ensure that the correct updates are transferred when working with content in multiple environments.

You can see the **Summary Information** and **Field Comparison** values to understand what will change if you proceed to transfer the content to a higher environment or try restoring content to the current environment.

To compare content between environments, follow these steps:

Navigate to the page you want to compare.

Select the arrow next to the

**Save and Publish**button. Alternatively, you can click the**Actions**drop-down.Select

**Compare**to open the**Compare**window.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-cce433193e817e7c42dfde3d1604dc8f1eaadaae%252FCompare_option.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a47f273d&sv=2)

Compare option **Choose the workspace**from the drop-down field.View the

**Summary information**.In the

**Field Comparison**table, view the differences between the versions in the two workspaces at the node level of each field.Proceed to transfer the content using the

**Queue for transfer**or**Transfer now**options.Restore the content from the higher environment using the

**Partial restore**option.Click

**Close**to continue editing the content node.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-422e00bc0147f5e58a3f80cd5e8ee2d6efb0e3b3%252FComparing_Content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=cd32fdf1&sv=2)

Comparing Content

**Transfer now** is available in all Umbraco Cloud projects running the latest version of Umbraco Deploy for Umbraco versions 8 and 9.

You can transfer a specific content node directly to the higher environment without adding it to the **Queue for transfer**.

To transfer content between environments, follow these steps:

Navigate to the page you want to transfer.

Select the arrow next to the

**Save and Publish**button.Select

**Transfer now**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-062d92484d921ee9b6a23f5aa8575fff6b3ce1ed%252FTransfernow_option_v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=64899597&sv=2)

Transfer Option In the

**Transfer now**window, a message is displayed that you are about to transfer the content node directly to the higher environment, without adding it to the queue.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d70b5a4a47d7b0277132a08a0588cdb3fb2975b6%252FTransfer_Content_v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f5ddf902&sv=2)

Transfer Content Click

**Transfer now**.

Last updated

Was this helpful?

---

### Deleting and Restoring Pages | CMS

Deleting a Page

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-957654af5ae9ad4228563853ee8fab26366aa2a6%252Ftrash.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=cf16fea0&sv=2)

Delete Menu 1 ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-108e7b498e19ff27126df2327212c18c846aa666%252Factions-trash-menu.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b2d8124c&sv=2)

Delete Menu 2 ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-eb75884db0880db65770934e9d32523c6314b50f%252FDelete-warning-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b6883776&sv=2)

Delete Warning

Restoring a Deleted Page from the Recycle Bin

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1eb2664f344b72f38af1970b407988f0564ce460%252FRestore-menu-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=faba68b9&sv=2)

Move Menu 1 ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-725e787d1398968b3208cfd554911cfe28bffcb2%252Faction-restore-menu.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9fd3537d&sv=2)

Move Menu 2 ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-09a52bfb7a2e3c54cec34916645de3d9a4a05e58%252Frestore-option.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=634b6f23&sv=2)

Move Select Structure

Emptying the Recycle Bin

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2b8c35c2f8589f8129d8864bb7f49f57743f64ac%252FEmpty-recycle-bin-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e6ebd876&sv=2)

Empty Recycle Bin ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-beb4bdd48756a8d60b66558c6bb5a1dac295825b%252FEmpty-warning-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=99914edc&sv=2)

Empty Recycle Bin Warning

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f56ed9a571459d799324b79430a79897a6b475da%252FDelete-single-page-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f8f44d64&sv=2)

Delete single page ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-735298584f396d60a315796df7973460ca164574%252Factions-delete-menu.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b09ea34c&sv=2)

Delete single page option 2 ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-43be38709b6a15fafe81be9edff7635701cd7582%252FDelete-single-page-warning-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=933f2b6c&sv=2)

Delete Warning

Last updated

Was this helpful?

---

### Editing Existing Content | CMS

Content Within the Tree View

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ec5b5d68931eea6c3187b1110853598e41b0434f%252FView-page-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ddbd74ae&sv=2)

View Page Layout

List

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-103b7c76ae2a702f03403cffdabc367d36c216c6%252FList-view-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=35238169&sv=2)

Grid

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1721c39449c64d51a07a27bb5de9a84823501a8b%252Fgrid-view-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=25249a91&sv=2)

Enabling Collection

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1d66e865a109c175ea0fa3dee4f63ecbb8651b1d%252Fconfigure-collection-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=64b55512&sv=2)

Last updated

Was this helpful?

Content Within the Tree View

When you are looking to edit content, locate the * page* you want to edit in the Content tree on the left-side of the screen.

To edit existing content, follow these steps:

Go to the

**Content**section.Select the page in the section tree you wish to edit. The content of the page is loaded in the right-side editor.

Edit the contents of the page.

Click

**Save**to save the edits without publishing it.Click

**Save and preview**to preview the changes.Click

**Save and publish**to publish the changes. For more information, see the[Save and Publishing Pages](/umbraco-cms/tutorials/editors-manual/getting-started-with-umbraco/creating-saving-and-publishing-content#saving-and-publishing-pages)article.

View Page Layout

By default, you can view Page layouts in two ways: in a List or in a Grid.

List

When you [enable Collection](/umbraco-cms/tutorials/editors-manual/getting-started-with-umbraco/editing-existing-content#enabling-collection) on a page, its child pages are no longer shown as nested items in the content tree. Instead, the parent page appears as a single node in the tree. Selecting it displays all of its child pages in a list view within the main content area. For more information, see the [Collection](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/collection) article.

Grid

You can switch to the grid view by clicking the ![layout](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d11e88494cea1a1888ad6f6ff6dc8fa15b32fd51%252Flayout.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=c06ebe2b&sv=2)


Enabling Collection

To enable Collection:

Go to

**Settings**.Navigate to the Document Type you wish to configure as a Collection.

Go to the

**Structure**tab.Click

**Configure as a Collection**in the Collections field.Select

**List View - Content**.Click

**Save**.

Click

**Save**.

Additionally, you can sort the list items by the **Name**, **Last Edited**, and **Updated By** columns in either ascending or descending order.

Last updated

Was this helpful?

Was this helpful?

---

### Finding Content | CMS

Last updated

Was this helpful?

The Umbraco content tree view allows you to navigate web pages through a logical site hierarchy. You can find a page by navigating through the tree itself if you know where the page is stored.

Searching in Umbraco

A quicker way to search across all the content, files, or folders in Umbraco is to click the Magnifier icon in the top-right of the screen. Alternatively, you can use the keyboard shortcut **CTRL + SPACE** to access the **Search** bar.

Using the search bar, you can enter a search term and Umbraco will search for pages and media containing the term.

Last updated

Was this helpful?

Was this helpful?

---

### Logging In and Out | CMS

Last updated

Was this helpful?

Logging in

To access the Umbraco Backoffice:

Open your web browser and enter your website domain name followed by

`/umbraco`

(for example: http://www.company.com/umbraco/). A login screen appears.Enter your

**Email**and**Password**provided by your system administrator.Click

**Login**.

The address at which you access Umbraco may vary so check with your system administrator.

Logging Out

To log out of the Umbraco Backoffice:

Select the profile picture in the top-right of the screen.

Click

**Logout**.

Last updated

Was this helpful?

Was this helpful?

---

### Moving a Page | CMS

Last updated

Was this helpful?

Move pages within the website through the tree view. Not all pages can be moved depending on your set-up or page permissions. If you need clarification, contact your system administrator.

You can move a page in two ways:

Option 1

Go to

**Content**.Click

**...**next to the page you wish to move.Select

**Move to**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b0a196943d9e5117eb93d46ebd5ef0a285108171%252FMove-menu-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6fafd48f&sv=2)

Move Menu 1 A window appears on the right side of the screen. Here, you can choose where you want to move the page in the tree structure.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9d4904553dd7f1fa5718d3fa3ca81baf394798ed%252FMove-options-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b0957d8a&sv=2)

Move Option 1 Click

**Move**.A confirmation message appears. Click

**OK**to dismiss the confirmation message.

Option 2

Go to

**Content**.Select the page you wish to move.

Click

**Actions**in the top-right corner of the screen.Select

**Move to**from the**Actions**drop-down menu.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c9659889cde51cf253ef0e3ee8726f2fdd31a694%252Fmove-actions-menu.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3a229704&sv=2)

Actions Menu A window appears on the right side of the screen. Here, you can choose where you want to move the page in the tree structure.

Click

**Move**.A confirmation message appears. Click

**OK**to dismiss the confirmation message.

Last updated

Was this helpful?

Was this helpful?

---

### Sorting Pages | CMS

Last updated

Was this helpful?

The pages in Umbraco are placed in the tree structure according to a predefined sort order. The most recently created page is placed at the bottom of the tree structure. You can change the order of the pages by using the **Sort** function.

You can sort pages in two ways:

Option 1

Go to

**Content**.Navigate to the parent node whose child nodes you wish to sort.

Click

**...**next to the page you wish to sort.Select

**Sort children of**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8acc25907f04d4acc3110b74ee541629d22d834d%252FSort-menu-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1c5f7d4a&sv=2)

Sort Menu 1 A window appears on the right-side of the screen. Here, you can arrange the child nodes in the order you want by dragging them up or down.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-43730a24d6a0ea53f54e2a0cfa570ee52f050ea9%252FSort-options-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=2671aebd&sv=2)

Sort Option 1 Click

**Save**and then**Close**.

Option 2

Go to

**Content**.Select the parent node whose child nodes you wish to sort.

Click

**Actions**in the top-right corner of the screen.Select

**Sort children of**from the**Actions**drop-down menu.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b6b667389a12c7c36e5a2229da37f82e91576f22%252FActions-menu-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fb5bc8eb&sv=2)

Actions Menu A window appears on the right-side of the screen. Here, you can arrange the child nodes in the order you want by dragging them up or down.

Click

**Save**and then**Close**.

Last updated

Was this helpful?

Was this helpful?

---

### Umbraco Interface | CMS

After logging in to an Umbraco project you will be presented with a dashboard containing a wide array of buttons and features. Let's quickly go through what each feature does.

By default, there are two dashboards available:

The

**Getting Started**dashboard provides helpful information about Umbraco.The

**Redirect URL Management**dashboard displays the original and redirected links of the published pages which are moved to a new location in your project.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6c51b15f03573a67968fec360909fa5dbd6422aa%252FUI-dashboard.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8aaf046b&sv=2)

The

**Search**bar allows you to search for the content in your entire project.The

**Help**icon provides different Help options such as Tours, Umbraco Learning Base YouTube videos, Umbraco Documentation, and your System Information.The

**profile**icon allows you to edit your profile, change the password, and Logout from the application.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-009c3ffa14edc735ad975dc7a6129bebfa0983c9%252Fsearchmenu.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e8304c17&sv=2)

The following sections are available in the backoffice:

**Content**- allows to manage your content.**Media**- allows to manage images and other media files.**Settings**- allows to handle your meta data such as document types.**Packages**- allows to manage and install packages.**Users**- allows to manage the users on the project. To learn more about users, see the[Users](/umbraco-cms/fundamentals/data/users)article.**Members**- allows to handle the members of the project. If you want to learn more about Members, see the[Members](/umbraco-cms/fundamentals/data/members)article.**Forms**- allows to create and manage your forms.**Translation**- allows to manage dictionary items.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-91b2612400d93183b4b62cb6066c3ea5a0d61db3%252FThe-Section-Menu-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1f9752b4&sv=2)

The menu list will differ depending on your permissions for the project. For example: if you are an editor, then you will only have access to **Content**, **Media**, and **Forms** as per the default settings.

The section tree is different depending on the section you are in.

In this example, you are looking at the content section. The section provides an overview of the nodes contained in the tree.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a997bea505c2a9be736030ffa1254de2e4f0de18%252FThe-Section-Tree-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fa5c8aa9&sv=2)

The **Content** tab allows you to create content nodes and manage your content tree. When you hover over the sections, it is highlighted with a darker color indicating that you are hovering over it. A button with three dots will show up, left-click or click the + icon to view additional options.

The **Recycle Bin** contains the deleted content and is available only in the **Content** and the **Media** section.

[Previous Logging In and Out chevron-left](/umbraco-cms/tutorials/editors-manual/getting-started-with-umbraco/logging-in-and-out)

[Next Creating, Saving and Publishing Content Options chevron-right](/umbraco-cms/tutorials/editors-manual/getting-started-with-umbraco/creating-saving-and-publishing-content)

Last updated

Was this helpful?

---

---

## Media Management

### Contents

- [Cropping Images | CMS](#cropping-images-cms)
- [Working with Folders | CMS](#working-with-folders-cms)
- [Working with Media Types | CMS](#working-with-media-types-cms)

---

### Cropping Images | CMS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4c0f4928de23e6cae0d123f24fbc0798b6dd341a%252Fcropping-images-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=38f41706&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4d4e692fdb2cd2aff557b65a24600f67985059cd%252Fpreset-crops-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ff0eb211&sv=2)

Editing a pre-defined crop

Last updated

Was this helpful?

If your system administrator has set up cropping for your images, you will see a similar interface when you edit your images:

The circle in the middle of the image is the default focal point. The focal point defines the primary area or focus of the image which will be the center point of any image re-sizing. You can move the focal point by clicking and dragging it to the desired part of the image.

Next to the image, you may see specific crops of the image depending on your setup. In the above example, you can see that 2 crops have been set-up. To add or update the image crops, see [Adding properties](/umbraco-cms/fundamentals/data/creating-media#adding-properties) section in the [Creating media](/umbraco-cms/fundamentals/data/creating-media) article.

To manually alter the pre-defined crops:

Select one of the crops - you will see an enlarged version of the crop.

Drag the image around and zoom in or out until you have the desired result.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4d4e692fdb2cd2aff557b65a24600f67985059cd%252Fpreset-crops-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ff0eb211&sv=2)

Editing a pre-defined crop Once you are happy with your changes, click

**Done**to save the changes.If you wish to reset the crop to default view, click

**Reset crop**.Once you have finished editing the crops, click

**Save and close**.

Last updated

Was this helpful?

Was this helpful?

---

### Working with Folders | CMS

Creating a Folder

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8cb0c87ca25e9b21a1eabae351132d677d6a5b93%252Fcreate-folder-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ea7daf82&sv=2)

Create Folder

Editing a Folder

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b0b16b139f084b8b5762a92b4f05a87608618022%252FEdit-folder-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=140aab8e&sv=2)

Edit Folder

Deleting a Folder

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0507e029514be6f2fc25b84692d26b0f3f570034%252FDelete-folder-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=abec2f83&sv=2)

Delete Folder

Restoring a Folder from the Recycle Bin

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f38f1fa9f41692d4531b6c03c69b5ed1b5926cea%252FmediaRecycle-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=dc05d5db&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d8675f8d24d12552d7919328e4291fc76ee1e57c%252FRestore-Folder-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3dae94b2&sv=2)

Restore Folder

Moving a Folder from the Recycle Bin

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a2f852e92c712b8dfa5ee09f2e35019d38ae7ac0%252FMove-Folder-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ad40e2fa&sv=2)

Move Folder ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e6609809f8d94384cf64c82660e2e1c8f2ec58e4%252FMove-media-location-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=df95415a&sv=2)

Move Media.png

Sorting the Contents of a Folder

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9121cdfa94c82f631f7364500d127fd90802a720%252FSort-Folder-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6b673a1f&sv=2)

Sort Folder ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d3396f529b6dd2723b9afc9b37b393a60acbf992%252Fsort-items-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a31b0d21&sv=2)

Sort Items

Last updated

Was this helpful?

---

### Working with Media Types | CMS

Uploading a Media Item

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e73e86019c5ac995b56fe6011c360977af9c3589%252Fupload-images-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c2b42da5&sv=2)

mediaUpload.jpg

Deleting a Media Item

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5298481902a13fd5fc7f1e704ace2987f369caa6%252Fdelete-media-item-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b4417f4e&sv=2)

mediaUpload.jpg

Restoring a Media Item from the Recycle Bin

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-3d6b8261529f4efcc6f9a6a5791fc5fd4b8b4397%252FmediaRecycle-single-imagev14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3fda3685&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-49795699a9c073019475866df3782948e1bbba81%252FRestore-MediaItem-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e62ebd51&sv=2)

Restore Folder

Moving an Image or File

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-586486fcf4853863ef1c164bbb5e361b33586594%252Fmove-images-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5a5cb433&sv=2)

Move media items ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e6609809f8d94384cf64c82660e2e1c8f2ec58e4%252FMove-media-location-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=df95415a&sv=2)

Move Media.png

More Information

Last updated

Was this helpful?

---

---

## Tips And Tricks

### Contents

- [Audit Trail | CMS](#audit-trail-cms)
- [Notifications | CMS](#notifications-cms)
- [Preview Pane Responsive View | CMS](#preview-pane-responsive-view-cms)
- [Session Timeout | CMS](#session-timeout-cms)
- [Refreshing the Tree View | CMS](#refreshing-the-tree-view-cms)

---

### Audit Trail | CMS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-14f1ace061d9d9bba3f70ad9a5b589a7625376d9%252FauditTrail-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3041442d&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ccb3f108411437c4b98c3ea57f0f196a2b2c6178%252Fview-audit-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7d5815dc&sv=2)

View audit Trail

Last updated

Was this helpful?

Within the **Info** content app for pages you can find the **Audit Trail** in the **History** section. Here, you can get a quick overview of the actions performed on that node, by whom, when and any additional comments.

The Audit Trail is useful to find out who made changes on a certain date.

To view the audit trail:

Go to the

**Content**section.Navigate to the page you wish to see the audit trail.

Go to the

**Info**tab.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ccb3f108411437c4b98c3ea57f0f196a2b2c6178%252Fview-audit-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7d5815dc&sv=2)

View audit Trail

Last updated

Was this helpful?

Was this helpful?

---

### Notifications | CMS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5a2acbfabf744bc1d0396f193ed3648105774414%252FNotifications-menu-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7a33c6c3&sv=2)

Notifications Menu ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c4427df675b8ffe4b65213618a01305b417e7752%252Fnotifications-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=76b79ef4&sv=2)

notifications.jpg

Last updated

Was this helpful?

You can set up notifications to receive an email when an action is performed on a given content item. To receive notifications, you need to add your email address to your user profile.

To set up notifications for a content item:

Click

**...**next to the page or select the page and click**Actions**in the top-right corner of the screen.Choose

**Notifications**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5a2acbfabf744bc1d0396f193ed3648105774414%252FNotifications-menu-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7a33c6c3&sv=2)

Notifications Menu Check the actions in which you are interested and you will receive notifications each time the given action occurs.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c4427df675b8ffe4b65213618a01305b417e7752%252Fnotifications-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=76b79ef4&sv=2)

notifications.jpg Click

**Save**.

The notification settings apply to the chosen content item as well as any child items that appear below the item in the content tree.

If the notifications option does not appear, the SMTP settings are probably incorrect. In this case, contact the administrator of your website.

Last updated

Was this helpful?

Was this helpful?

---

### Preview Pane Responsive View | CMS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-3fef3ae4b555b6eb56ef573c97a014d442b4fdd2%252FresponsivePreview-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c33f767e&sv=2)

responsivePreview.png

Last updated

Was this helpful?

When viewing page content in preview mode you have the option to scale the preview window to various device sizes:

Once you have finished editing the page content, click

**Save and preview**.Select

**Fit browser**to view the different preview modes.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-3fef3ae4b555b6eb56ef573c97a014d442b4fdd2%252FresponsivePreview-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c33f767e&sv=2)

responsivePreview.png Select the device you would like to scale the preview pane to.


Last updated

Was this helpful?

Was this helpful?

---

### Session Timeout | CMS

Session Timeout Configuration for Developers

Last updated

Was this helpful?

Umbraco is set up to automatically log a user out if they have been inactive for over 20 minutes. Don't worry if you are logged out of Umbraco. Log back in using your credentials and continue editing.

Session Timeout Configuration for Developers

The session timeout can be configured in Umbraco's `appsettings.json`

file. You can modify the setting to extend or reduce the timeout duration based on your site's needs.

Last updated

Was this helpful?

Was this helpful?

---

### Refreshing the Tree View | CMS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-49553cca52fd2a1e4f6d2099077e4305af11e448%252FReload-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=db5dc824&sv=2)

Reload Tree

Last updated

Was this helpful?

When editing content, the content tree will refresh itself when the content is saved.

If the tree does not refresh or if multiple editors are working on the site, and you want to have their changes loaded into your content tree - you can do so by reloading parts of the content tree.

To reload a section of the content tree:

Click

**...**next to an item in the tree.Choose

**Reload**. The parent and child nodes are now reloaded and will reflect any new changes.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-49553cca52fd2a1e4f6d2099077e4305af11e448%252FReload-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=db5dc824&sv=2)

Reload Tree

Last updated

Was this helpful?

Was this helpful?

---

---

## Version Management

### Contents

- [Comparing Versions | CMS](#comparing-versions-cms)
- [Rollback to a Previous Version | CMS](#rollback-to-a-previous-version-cms)

---

### Comparing Versions | CMS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ec8ed11c6893c92dd486a3f431e56bd423904294%252FRollback-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fb8c605e&sv=2)

Rollback ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a842a6260f13aa148b9c4194ba8b9b851fb4bfe5%252FRollback-changes-v10.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5af6cc84&sv=2)

Rollback Changes

Last updated

Was this helpful?

You will never lose changes on a page because all the old versions of the page are saved in **History**.

To compare a page on the site with its previous versions:

Navigate to the page whose versions you wish to view.

Go to the

**Info**tab.Click on the

**Rollback**button in the**History**section.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ec8ed11c6893c92dd486a3f431e56bd423904294%252FRollback-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fb8c605e&sv=2)

Rollback The Rollback window opens. Select a version you wish to compare with.

After selecting the version, a comparison of the current page with the version you selected is displayed. The text highlighted in red and striked-out will not appear in the selected version and the text highlighted in green means the text that will be added, should you choose to rollback to that version of the page.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a842a6260f13aa148b9c4194ba8b9b851fb4bfe5%252FRollback-changes-v10.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5af6cc84&sv=2)

Rollback Changes

Last updated

Was this helpful?

Was this helpful?

---

### Rollback to a Previous Version | CMS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ec8ed11c6893c92dd486a3f431e56bd423904294%252FRollback-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fb8c605e&sv=2)

Rollback ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a842a6260f13aa148b9c4194ba8b9b851fb4bfe5%252FRollback-changes-v10.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5af6cc84&sv=2)

Confirm Rollback

Last updated

Was this helpful?

You have the opportunity to access and re-publish older versions, if necessary.

To rollback to a previous version of the page:

Navigate to the page whose versions you wish to view.

Go to the

**Info**tab.Click on the

**Rollback**button in the**History**section.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ec8ed11c6893c92dd486a3f431e56bd423904294%252FRollback-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fb8c605e&sv=2)

Rollback The Rollback window opens. Select a version of the page you wish to Rollback to.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a842a6260f13aa148b9c4194ba8b9b851fb4bfe5%252FRollback-changes-v10.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5af6cc84&sv=2)

Confirm Rollback Click

**Rollback**to proceed with the changes. Your content has now been rolled back to the selected version of the page and is saved as a**Draft**version.To publish the draft version, click

**Save and publish**.

Last updated

Was this helpful?

Was this helpful?

---

---

## Working with Rich Text Editor | CMS

The Umbraco Rich Text Editor (RTE) is a field where you, as an editor, can be creative. You can select how much you want to do yourself. You can work on text content, format the text, or leave it the way it is. If you want to do more, you can insert images, create tables, or create links to other pages/documents.

The functionality varies depending on how the editor is set up. Here, we describe the default editor with all the options enabled. Contact your system administrator for details regarding your editor.

By default, the following editor buttons are available. Your system administrator can determine which buttons are displayed in different templates. You therefore might have access to more or fewer buttons than those shown here.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2207792f2a2062be5bf421a00c9f1644a4e747ac%252Feditor_bar_v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e098c8eb&sv=2)

The Rich Text Editor is like any other word-processing program. You write the text and the text wraps around when the line reaches the end. Use the following keyboard shortcuts in the editor to add:

Space between paragraphs - press

`ENTER`

.Line breaks - press

`SHIFT + ENTER`.


To make your work easier, there are shortcut keys for certain editor functions. Use the following shortcut keys to carry out certain commands:

| Windows/Linux | MacOS | Action |
|---|---|---|
| Ctrl + A | Cmd + A | Select all |
| Ctrl + B | Cmd + B | Bold |
| Ctrl + I | Cmd + I | Italic |
| Ctrl + U | Cmd + U | Underline |
| Ctrl + C | Cmd + C | Copy |
| Ctrl + V | Cmd + V | Paste |
| Ctrl + Shift + V | Cmd + Shift + V | Paste without formatting |
| Ctrl + X | Cmd + X | Cut |
| Ctrl + Z | Cmd + Z | Undo |
| Ctrl + Shift + Y | Cmd + Shift + Z | Redo |

Only a few keyboard shortcuts are listed here. For a detailed list of available shortcuts, see the .

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-37760d445b5ce97fa175e8b706a3e614456e1262%252Fview-source-code-v11.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=edc54f63&sv=2)

If you are proficient in HTML, you can switch to HTML mode to create your page. You can also check the code and make minor adjustments to get the page exactly as you want.

Certain elements such as scripts are not recognized by the HTML view of the Rich Text Editor. You can enter the scripts directly in the text view of the editor.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9cf550da427c744ab946b6f095b1675a82ce7fc5%252FFormats-Button-v11.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e5062852&sv=2)

You can apply formatting via the **Formats** drop-down list. The Formats drop-down list provides predefined styles that can be applied to text while maintaining a consistent look and feel throughout the site.

These styles incorporate advanced formatting functionality which can be applied to provide a different look for certain elements such as links, headings, and sub-headings. For example, you can use a format style to change a link into a call-to-action button.

To apply pre-defined styles:

Select the text you want to apply the style.

Choose the style from the

**Format**drop-down list.

For more information on how to create the Styles, see the [Rich Text Editor Styles](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/rich-text-editor/style-menu) article.

You do not normally need to spend much time formatting text because Umbraco takes care of the formatting. However, the editor provides some options for controlling the text styles.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d2bafa5e64f67513fa60f2764f97b420567f9f17%252FFormatting-Buttons-v11.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6c39fd22&sv=2)

The most familiar way to control formatting is by using the formatting buttons. With these buttons, you can apply basic formatting such as Bold, Italic, aligning text, creating bulleted and numbered lists, and applying indents.

To apply a format using the formatting buttons:

Select the text you want to apply the formatting.

Click the desired format button.


When you write content in another editor and copy it into a Rich Text Editor, you may encounter style issues on your website.

While pasting content, the original text styles are preserved which can lead to different font faces, sizes, and colors displaying on the website when viewed.

To prevent formatting issues, we recommended pasting the content first into a markdown editor such as Notepad, then copying and pasting it into your Rich Text Editor.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f7f9194cd05d06ba8b29c42cf24aab9b7e805e01%252FRemove-Format-v11.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=97c9d592&sv=2)

If you have already formatted a paragraph or selection using the formatting buttons, you can remove the formatting rule.

To remove formatting:

Select the text you want to remove the style from.

Click the relevant formatting button to remove the formatting rule.


You can also add a **Remove format** button in your toolbar. To add the **Remove format** button:

Navigate to your Rich Text Editor in the Document Type.

Click the cog wheel.

Click

**Edit**next to the Rich Text Editor Data Type.Select

**Remove format**under the**Toolbar Configuration**.Click

**Submit**.Click

**Save**.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-eff09368f5abfe9b3634b04b53dea05a621c9ee1%252FLink-Button-v11.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=324ec8ba&sv=2)

The **Insert/Edit Link** button is used to add or update links to internal pages, external pages, media files, email links, and anchors. The process for inserting a hyperlink differs depending on the type of hyperlink you wish to create.

To insert different types of hyperlinks, follow these steps:

### Link to a Page on Another Website

![Link to a Page on another Website](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-471995fc1919525e9701215a92dac9915f3d6c5e%252FLink-to-an-external-Page-v11.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=6b65d08e&sv=2)


Select the text that will form the hyperlink.

Click the

**Insert/Edit Link**button to open the link properties slide-out menu.Enter the URL of the web page you wish to link to in the

**Link**field.Enter the text that will be displayed as the link title in the

**Link Title**field.This is important information for everyone reading the website with different accessibility aids.


Select the

**Target**field to open the link in a new window or tab.Click

**Submit**.

### Link to a Page in Umbraco

![Link to a Page in Umbraco](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e53758ab08390f21fd6e2c05d10b0199df3197fd%252FLink-to-a-Page-v11.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=cd9a8bde&sv=2)


Select the text that will form the hyperlink.

Click the

**Insert/Edit Link**button to open the link properties slide-out menu.Select a page from the

**Link to page**field.This will populate the

**Link**and**Link Title**fields automatically.

Select the

**Target**field to open the link in a new window or tab.Click

**Submit**.

### Link to a Media File in Umbraco

![Link to a Media File in Umbraco](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-037f6c2a694fcc90d11eccb3f0a998ead2da0ca9%252FLink-to-Media-File-v11.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=ef5b1c05&sv=2)


Select the text that will form the hyperlink.

Click the

**Insert/Edit Link**button to open the link properties slide-out menu.Select the

**Link to Media**button to select the media item.Click

**Select**.This will automatically populate the

**Link**and**Link Title**fields with the media item information.By default, the

**Link**field contains the media file name and cannot be edited.

Select the

**Target**field to open the link in a new window or tab.Click

**Submit**.

### Link to an Email Address in Umbraco

![Link to an Email Address in Umbraco](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-10530d28af47f8d6214f410f9ffe013576359b2f%252FLink-to-Email-Address-v11.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=b9829a96&sv=2)


Select the text that will form the hyperlink.

Click the

**Insert/Edit Link**button to open the link properties slide-out menu.Enter the text

`mailto:`

followed by the email address you wish to link to in the**Link**field. For example,`mailto:`

.[[email protected]](/cdn-cgi/l/email-protection)Enter the text that will be displayed as the link title in the

**Link Title**field.Select the

**Target**field to open the link in a new window or tab.Click

**Submit**.

### Link to an Anchor on the Same Page

An anchor allows you to create internal page links that enable users to navigate within a page. There are two parts to setting up an anchor: the anchor itself and the link to the anchor.

**Creating an Anchor**

![Creating an Anchor](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2b8917bd9fae57512260342a144f78321b77c5ab%252FCreating-an-anchor-v11.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=1a4ba162&sv=2)


Click the editor cursor where you wish to create the anchor.

Click the

**Anchor Button**which will launch the Anchor creation dialog.Enter your anchor name in the

**ID**field.You should avoid special characters and spaces.


Click

**Save**.You will see a small anchor icon where you previously had the editor cursor.



To delete the anchor:

Select the anchor icon.

Press your

**Delete**key.

![Deleting an Anchor](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d3d15aaed333105e2995d638ca07ffb094b0c72a%252FDelete-an-anchor-v11.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=2e949094&sv=2)


**Linking to an Anchor**

![Linking to an anchor](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9711528cfdffc768e91be4ab9317d687c37a1706%252FLinking-to-Anchor-v11.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=32db5a6&sv=2)


Select the text to which you wish to add the anchor link to.

Click the

**Insert link**button to open the link properties slide-out menu.Add a hash symbol (#) followed by the name of your anchor in the

**Anchor/querystring**field.Enter the text that will be displayed as the link title in the

**Link Title**field.Click

**Submit**.

### Create a Link from an Image

You can make images into clickable links in Umbraco:

![Create a Link from an Image](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0b9291b4737f311b8adc4e2ae008d6c4fa70ae63%252FLink-from-Image-v11.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=bdc2571d&sv=2)


Insert an image into the Rich Text Editor.

For more information, see the

[Working with Images](/umbraco-cms/tutorials/editors-manual/working-with-content#working-with-images)section.

Select the image that will form the hyperlink.

Enter the URL of the web page you wish to link to in the

**Link**field.Enter the text that will be displayed as the link title in the

**Link Title**field.Select the

**Target**field to open the link in a new window or tab.Click

**Submit**.

### Removing a Link

![Remove link Button](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a2cbd44b1078d916489463bffa2eb3b0b2b7e4d0%252FRemove-link-v11.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=bd02da7c&sv=2)


To remove a link:

Select the link in the Rich Text Editor.

For text links, click the cursor anywhere within the link text. For an image, click the image itself.


Click the

**Remove Link**button which will remove the hyperlink.Alternatively, you can click the

**Insert/Edit Link**button and remove the link from the**Link**field.

To display images on a page the images must be uploaded to your Umbraco media library.

Many administrators set up a media library containing images that editors can use on their pages. Others allow their editor's free use of their images. The procedure for uploading an image varies slightly depending on which method your administrators have setup. Check with your system administrator for more information about this.

### Inserting an Image from the Media Library

![Inserting an Image from the Media Library](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-79ba71c8e5d2fcb14c975c03aa22bdb97947a5d8%252FInserting-Image-from-the-Media-Library-v11.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=99070a59&sv=2)


Place the cursor in the Rich Text Editor where you want to insert your image.

Click the

**Media Picker**button from the toolbar.Select the folder in which the image is.

Click the thumbnail of your chosen image to open the image properties menu.

Enter a name/description for the image in the

**Caption (optional)**field.It is important to add descriptive titles to images as these are used to assist visually impaired users.


Click

**Select**.

### Inserting an Image from your Computer

You can upload images directly from the Rich Text Editor on the page you are editing. These images will be stored in the Umbraco Media Library. Therefore, it would be best to ensure the image is placed in the correct location within the library. If you click the plus icon underneath the search bar in the media picker slide-out menu you can create folders in the media library.

![Inserting an Image from your Computer](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-94f0ee5cc75c42b67e3efedf4bd722f7cb27dca9%252FInserting-an-Image-from-Computer-v11.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=30fac593&sv=2)


Place the cursor in the Rich Text Editor where you want to insert your image.

Click the

**Media Picker**button from the toolbar.Click the

**Upload**button which is located in the top right-hand corner of the menu.Select the chosen image from the pop-up window.

Enter a name/description for the image in the

**Caption (optional)**field.Click

**Select**.

### Editing an Inserted Image

After inserting an image, you can edit its alt text, caption, and dimensions without removing and re-inserting it.

Click on the image in the Rich Text Editor to select it.

Click the

**Media Picker**button in the toolbar.The Media Picker is skipped and the

**Edit selected media**panel opens directly.

Update any of the following properties:

**Alt text**— A description used by screen readers. Pre-filled with the media item name.**Caption**— Optional text displayed below the image. Adding a caption wraps the image in a figure element.**Width**and**Height**— Display dimensions in pixels. A lock icon constrains the aspect ratio by default. Changing one value adjusts the other automatically. Click the lock icon to set each value independently. Click**Reset**to restore original dimensions.

Click

**Submit**to apply the changes.

The Rich Text Editor setting **Maximum size for inserted images** may limit image dimensions. Images exceeding the configured **Maximum size for inserted images** are scaled down proportionally.

### Deleting an Image from the Page

To delete an image from the page:

Select the image.

Press the

**Delete**button on your keyboard.The image disappears from the page but is not deleted from the Umbraco Media library.



![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8020e292d180dd61315fca9b8b40a12d36bd0183%252FInsert-a-table-v11.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6c99b01f&sv=2)

Tables are used to format information in a grid-based structure. When you insert a table, you select how many rows and columns the table should comprise of. Additionally, you can fill in some optional formatting properties. These values can be changed later, so it is not important to know exactly what your table will look like when you create it.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-259f12eb87ab1879969fccaab2aa6273cb911915%252FEditing-an-existing-table-v11.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=af85d31&sv=2)

To edit the table after creating it, click on the table. A pop-up appears with different table properties and options. Alternatively, you can click on the **Table** button in the Rich Text Editor toolbar.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b52931a72f02d8d2da5bcf6deb2aa80300a54547%252Ftable-properties-v11.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=22636e25&sv=2)

Clicking on **Table Properties** gives you different options for modifying the table’s appearance. However, the developer of the website may have already created table styles for you so you may not need to adjust these settings.

There are other options available for modifying cells, rows, and columns such as width, height, alignment, border, and so on.

The Rich Text Editor in Umbraco can be configured in many different ways.

For more information, see the [Rich Text Editor Configuration](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/rich-text-editor/configuration) article.

Last updated

Was this helpful?

---
