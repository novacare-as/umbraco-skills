# Creating A Basic Website

## Contents

- [Adding Language Variants | CMS](#adding-language-variants-cms)
- [Articles and Article Items | CMS](#articles-and-article-items-cms)
- [Conclusions | CMS](#conclusions-cms)
- [Creating a Master Template | CMS](#creating-a-master-template-cms)
- [Creating Pages and Using the Master Template | CMS](#creating-pages-and-using-the-master-template-cms)
- [Creating Your First Template | CMS](#creating-your-first-template-cms)
- [CSS and Images | CMS](#css-and-images-cms)
- [Displaying the Document Type Properties | CMS](#displaying-the-document-type-properties-cms)
- [Document Types | CMS](#document-types-cms)
- [Getting Started | CMS](#getting-started-cms)
- [Setting the Navigation Menu | CMS](#setting-the-navigation-menu-cms)

---

## Adding Language Variants | CMS

Adding a new language

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-79700da4df36f36c29fffac2048afa13715733f5%252Fadding-a-language-v15.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=30a2b5cd&sv=2)

Adding a language

Enabling Language Variants on Document Types and Properties

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ea0e0611550f7c53d7aa26964e999566e7a794e7%252Fenable-vary-by-culture.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e5335a4d&sv=2)

Enable Vary by Culture ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ae762ffc5914f1b9d7045cb066b07f0abeea8bd7%252Fenable-vary-by-culture-property-v16.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c14fecaa&sv=2)

Allow property editor Language Variants

Adding Culture and Hostnames to the root node of the website

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5cebe96c9241e71db9062c4bbc101b67c4df3b47%252Fculture-and-hostnames-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b9b3e74c&sv=2)

Culture and Hostnames

Adding Language Variants to the Content

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-4a5e1ae20ef18185772c87858ad072a43ac40cde%252Flanguage-content-tree-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9b20bb31&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-fc2d5b9e44f79c5a03d4d67f617e728eab09da75%252Flanguage-dropdown-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=99ed7d00&sv=2)

Language Variant dropdown ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6525f47684182503fbb751ead5aead488f343842%252Fopen-in-splitview-v15.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=90ee0569&sv=2)

Open Language in Splitview ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ce64bbed63c8cd121b68027e55df4b4b5302d5bd%252Fsplitview-editing-v15.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=83df01f3&sv=2)

Splitview editing ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1602ec08e15990e70bcff29a974414b0ca5927ab%252Fpublishing-variant-content-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=40928066&sv=2)

Publishing Variant content

Viewing the Language Variant on the Browser

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-33498c706ab064d2503d342a48d87da8f295a641%252Fviewing-langvariant-browser-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=cf0e7591&sv=2)

Viewing the Language Variant Link

More Information

Last updated

Was this helpful?

---

## Articles and Article Items | CMS

Having a parent page with child pages provides a good example of Umbraco's features. For example, our fictional company, Widgets Ltd, publishes about ten articles per month and therefore wants the parent page to function as a blog. This setup works for articles, posts, and other collections that require multiple content items based on the same content type.

Create two new Document Types with template: **Articles Main** and **Articles Item**.

To create **Articles Main** Document Type, follow these steps:

Go to

**Settings**.Click

**...**next to the**Document Types**in the**Settings**tree.Select

**Create...**.Select

**Document Type with Template**.Enter a

**Name**for the**Document Type**. Let's call it*Articles Main*.Let's add two fields with the following specifications:

Group Field Name Alias Data Type Intro Articles Title articlesTitle Textstring Intro Articles Body Text articlesBodyText Rich Text Editor ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d679adbf29e8409f8850d0c807d08f6a4fa7d355%252Farticles-main.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=df233b83&sv=2)

Articles Main Document Type Data Properties Click

**Save**

To create **Articles Item** Document Type, follow these steps:

Go to

**Settings**.Click

**...**next to the**Document Types**in the**Settings**tree.Select

**Create...**.Select

**Document Type with Template**.Enter a

**Name**for the**Document Type**. Let's call it*Articles Item*.Let's add two fields with the following specifications:

Group Field Name Alias Data Type Content Article Title articleTitle Textstring Content Article Content articleContent Rich Text Editor ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6dcdc31744f4df4744223dff009d067146d1a5be%252Farticles-item.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d7d94610&sv=2)

Article Item Document Type Data Properties Click

**Save**

To add **Articles Main** as a child node:

Navigate to the

**Home Page**Document Type.Go to the

**Structure**tab.Select

**Choose**in the**Allowed child node types**.Select

**Articles Main**.Click

**Choose**.Click

**Save**.

To update **Articles Main** Document Type permissions:

Navigate to the

**Articles Main**Document Type.Go to the

**Structure**tab.Select

**Choose**in the**Allowed child node types**.Select

**Articles Item**.Click

**Choose**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-309044a1c82217630c4271fdbd57dd50d417265e%252Fadding-child-node.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=2db97b0c&sv=2)

Adding child Node Click

**Configure as a collection**.Select

**List View - Content**.Click

**Save**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f1d3a19600d74ac13a77cbefc156599587c5b7b6%252Flist-view-enabled.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f6027f91&sv=2)

Enabling Collection

To add a content node:

Go to

**Content**.Select

**...**next to the**HomePage**node.Click

**Create**.Select

**Articles Main**.Enter the name for the article. We are going to call it

*Articles*.Enter the content in the

**Article Title**and**Article Body Text**fields.Click

**Save and Publish**. When you click on Save and Publish, you will notice an empty Collection is created.We still need to add the child nodes which will be displayed in the Collection making it easier to view them. You can create new nodes from this section.

{% hint style="info" %} If you do not see the Collection, try refreshing the page. {% endhint %}

Click

**Create Articles Item**.Enter the name for the article. We are going to call it

*Article 1*.Enter the content in the

**Article Title**and**Article Content**fields.Repeat steps 8 to 10 to create

*Article 2*.Click

**Save and Publish**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-885dfd4e5a81228678eb6afa99a8efe0ac50720b%252Ffigure-40-articles-created-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a71e212c&sv=2)

Content Tree with Articles

To update the **Articles Main** template, follow these steps:

Go to

**Settings**.Expand the

**Templates**folder in the**Templating**section.Open the

**Articles Main**template.Select

**Master**in the**Master template:No Master**field.Click

**Choose**.Click

**Save**.Open the

**Custom Umbraco Template**folder.Copy the contents of

**Blog.html**.Paste the content into

**Articles Main**below the closing curly brace "}".Remove everything from the

`<html>`

(around line 8) to the end of the`</div>`

tag (around line 43) which is the`header`

and`navigation`

of the site since it is already mentioned in the Master template.Remove everything from the

`<!-- Footer -->`

tag (around line 83) to the end of the`</html>`

tag (around line 130)Replace the static text within the

`<h1>`

tags (around line 12) with the Model.Value reference to.**articlesTitle**Replace the static text within the

`<div>`

tags (from line 23 to 29) with the Model.Value reference to.**articlesBodyText**![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b9940ed727206e020b329bf5ae1f878a9b2719da%252Farticles-main-template.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e6f0bee0&sv=2)

Articles Main Template Define a query for all articles below the

`<h3>`

tag (around line 30) of the`<!-- Latest blog posts -->`

section.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d49be6c69335f01074218b2dd93ef878eb547e6f%252Fquery-builder.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=cba412ab&sv=2)

Query Builder You can set conditions to get specific articles or decide the order of the articles. For the purpose of this guide, we are using the following parameters:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6df17907397ee5e884bf410be45ab8b47370e678%252Fquery-parameters-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e5354626&sv=2)

Query parameters If you've set the correct parameters, you will get a preview of the items being selected with the query.

Click

**Submit**.You will see a similar code snippet added to your template:

The above code will output a list of all the

as links using the name.**Article Items**We will modify the template a little, to add more information about the articles.

Replace the

`HTML`

in the*foreach*loop with this snippet:Remove the

`<ul>`

tags surrounding the*foreach*loop.Click

**Save**.

### See the entire file: Articles Main

To update the **Articles Item** template, follow these steps:

Go to

**Settings**.Expand the

**Templates**folder in the**Templating**section.Open the

**Articles Item**template.Select

**Master**in the**Master template:No master**field.Click

**Choose**.Click

**Save**.Open the

**Custom Umbraco Template**folder.Copy the contents of

**Blogpost.html**.Paste the content into

**Articles Item**below the closing curly brace "}".Remove everything from the

`<html>`

(around line 8) to the end of the`</div>`

tag (around line 43) which is the`header`

and`navigation`

of the site since it is already mentioned in the Master template.Remove everything from the

`<!-- Footer -->`

tag (around line 113) to the end of the`</html>`

tag (around line 160)Replace the static text within the

`<h1>`

tags (around line 13) with the Model.Value reference to.**articleTitle**Replace the static text within the

`<div>`

tags (from line 25 to 39) with the Model.Value reference to.**articleContent**![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-971ad2938caa5427f1ec16a7bb7f1feac971a7fe%252Farticles-item-template-v9.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=77add9f3&sv=2)

Articles Item Template Click

**Submit**.Click

**Save**.

### See the entire file: Articles Item

Check your browser, you should now see something similar to the screen below.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-46da0ea2da60d3f7ebfe997414d5ed67d56e35c4%252Farticle-main-frontend-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=81a6e30c&sv=2)

Last updated

Was this helpful?

---

## Conclusions | CMS

Last updated

Was this helpful?

Congratulations! You now have a fully functional website. Hopefully, this guide has provided you with all the basics needed to create your own site in Umbraco.

This is only the beginning — there is much more to explore in Umbraco beyond what we have covered here.

**Video Tutorials:**Check out the .**Training and Certification:**Attend an official Umbraco Master Class or .**Documentation:**Browse the for detailed guidance.**Support:**For help with topics not covered in this guide, connect with the community on the .

Happy Umbraco-ing

Last updated

Was this helpful?

Was this helpful?

---

## Creating a Master Template | CMS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1f64247bda8b05aaa3420281bdd2e8879a268000%252Fmaster-template-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1238c653&sv=2)

Master Template

Using the Master Template

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ec2dfd460b8fa7b7a16a70266b8feb5d28501539%252Fhomepage-has-master-template.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4eb0f98e&sv=2)

Adding Master Template to HomePage

Updating Templates With the New Master Template

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-339486cd8e9857dc836831be852aa1b79a649dc7%252Fhomepage-after-cutting-the-header.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d585c604&sv=2)

Header and navigation tags selected in the HomePage template ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-61b2b7b82d7609530b5df08711a4e338003a25e4%252Fmaster-after-adding-the-header.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=dfd09dc2&sv=2)

Header and navigation tags added in the Master template ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ba2acf0a517c90b62b00cd2082cf1d8aaea485f7%252Fadding-renderbody.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b211eb8d&sv=2)

Adding renderbody in the Master template ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-20750dd3516a34912d0bacb5ab79e6ba7b1760d7%252Fmaster-template-complete.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=17d40381&sv=2)

End of the Master template


[Previous Displaying the Document Type Properties chevron-left](/umbraco-cms/tutorials/creating-a-basic-website/displaying-the-document-type-properties)

[Next Creating Pages and Using the Master Template chevron-right](/umbraco-cms/tutorials/creating-a-basic-website/creating-master-template-part-2)

Last updated

Was this helpful?

---

## Creating Pages and Using the Master Template | CMS

Creating a Contact Us Page

Creating the Document Type and Template

Group Field Name Alias Data Type Content Page Title pageTitle Textstring Content Body Text bodyText Rich Text Editor ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-39fb76a98d280bcfaa9ae36105f6672f584b0c4f%252Fcontact-us-template-with-data-fields.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=91909ea4&sv=2)

Simple Content Page Template with Data Fields

Updating the Document Type Permissions

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1f08ef49e716363b48a1cdb2819a307e0fef410c%252Fhomepage-allowed-child.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=50b76b0b&sv=2)

Allow child nodes in HomePage

Creating the content node

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2d4f85ca9ec531bedfaabd330db73744343137fe%252Fadding-child-node-Content.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c3b00595&sv=2)

Adding Content Page as Child node

Adding the Document Type Properties

Viewing the Contact Us Page

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1845a6297c70ee40667893854b9a78d3ea4c86ba%252Fviewing-contact-us.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b015f13f&sv=2)

Viewing Contact Us Page

Using Document Type Properties from the Homepage

Last updated

Was this helpful?

---

## Creating Your First Template | CMS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5498867f46eee062b04dc75b088bc149f792282f%252Fempty-homepage-template.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4ee22d1e&sv=2)

Home Page Template

Creating Your First content node

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-122cd7b2ec8b1fd35652ed45546a1afa42fcdc64%252Fcreate-a-homepage-content-node.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=506ab5a3&sv=2)

Home Page Content Node Name Description Page Title Welcome to Widgets Ltd Body Text **Lorem ipsum**Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam et aliquet ante, ut eleifend libero.- Proin eleifend consequat nunc id vulputate.
- Ut eget lobortis metus, non congue lorem.
- Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.
- Maecenas tempus non lectus rhoncus efficitur.

*Morbi pharetra pulvinar arcu non gravida.*Footer Text Copyright Widgets Ltd 2024 ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-345df7a178e4a1ec1d94a9fb53074357dc977ff7%252Fhomepage-in-content-tree.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d8af792c&sv=2)

Home Page in Content Tree

Accessing the Frontend

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b86d17b4c1c389cdc8c4d68e4c76d3adc54c4ad8%252Ffigure-16-unstyled-homepage-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=98362fe3&sv=2)

Last updated

Was this helpful?

---

## CSS and Images | CMS

Last updated

Was this helpful?

Our homepage is currently missing the CSS and image files. To include these files:

Open File Explorer and navigate to both your Umbraco project folder and the Custom Umbraco Template folder.


The Umbraco project folder refers to the folder created during the [Umbraco installation](/umbraco-cms/fundamentals/setup/install).

Copy the

**css**and**images**folders from the*Custom Umbraco template*folder.Paste them inside the

**wwwroot**folder of your Umbraco project.Go to the

**HomePage**template in the**Settings**section.Make sure the stylesheet reference in the HTML is

`/css/main.css`

.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a1bede0b3b371b216fbda09033e07a58b7de474b%252Fstylesheet-reference.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4e7c6529&sv=2)

Stylesheet reference

Stylesheet Reference

Use the Developer Tools in Chrome/Firefox/Edge and refresh `http://localhost:xxxx.`


Check the

**Network**tab to confirm no CSS or image files are missing.If you see any errors, double-check for typos and confirm the folders are placed correctly inside the

**wwwroot**folder of your Umbraco project.

How Static Files Are Served

Umbraco serves static files such as stylesheets and images from the **wwwroot** folder. This folder acts as the web root in ASP.NET Core applications. Any files placed here are publicly accessible and can be served directly by the application when requested by the browser.

Last updated

Was this helpful?

Was this helpful?

---

## Displaying the Document Type Properties | CMS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ce958c8aacdc9f8bccf7eb7091641a0af8ce2ff2%252Ffigure-17-where-our-data-fields-go-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7a41ad14&sv=2)

Setting the Document Type Properties

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2a7b2f2eb86c1c8dfbd6f74781759545c480e941%252Freplace-hardcoded-text-with-umbraco-page-field.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7b0c5b60&sv=2)

Replace page Title value ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f82b17b1abda70007bff9eeaa13e1fa7644e1b8e%252Fumbraco-page-field.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6a6e1f12&sv=2)

Page Title field ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7bed28cc2809d7b6ec031492bfc2d0bad71ba635%252Freplace-bodytext-with-page-field.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=db9ba2ef&sv=2)

Replace Body Text value ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5c6d3640d5ac0740a095fe9a167f22eb144fb9d8%252Ffooter-text.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c28b5706&sv=2)

Replace Footer Text value

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-81ca7973afb08025592804a72befae5888e94e0d%252Ffigure-22-displaying-document-type-properties.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=dd04f1e8&sv=2)

Last updated

Was this helpful?

You might have noticed that the content we've added to the homepage is not being displayed. We need to wire up the Data Type properties to the template.

Let’s look at our template and identify where the content should be displayed.

The top arrow in this image is the *Page Title* and the bottom arrow is the *Body Text*. The Footer is all the way at the bottom of the page.

Setting the Document Type Properties

To set the Document Type properties:

Go to

**Settings**.Open the

**Homepage**template.Scroll down to the

`<!-- Jumbotron, w title -->`

section (around line 45) and highlight the text`“Welcome - UmbracoTV”`

(around line 48).![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-2a7b2f2eb86c1c8dfbd6f74781759545c480e941%252Freplace-hardcoded-text-with-umbraco-page-field.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7b0c5b60&sv=2)

Replace page Title value Click

**Insert**and select**Value**.Select

**Document Type**from the**Choose field**dropdown list.Select

**HomePage**.Click

**Choose**.Select

**pageTitle**field from the**HomePage**dropdown list.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f82b17b1abda70007bff9eeaa13e1fa7644e1b8e%252Fumbraco-page-field.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6a6e1f12&sv=2)

Page Title field Click

**Submit**.Go to the content between the

`<div class="container">`

tags (around line 60 to 77):Highlight the content as shown in the figure.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7bed28cc2809d7b6ec031492bfc2d0bad71ba635%252Freplace-bodytext-with-page-field.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=db9ba2ef&sv=2)

Replace Body Text value Repeat steps 4 to 9 to insert the

**bodyText**field.Go to the content between the

`<div class="container-fluid footer">`

tag (around line 148 to 181):Highlight the content between the

`<div class="container">`

tags.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5c6d3640d5ac0740a095fe9a167f22eb144fb9d8%252Ffooter-text.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c28b5706&sv=2)

Replace Footer Text value Repeat steps 4 to 9 to insert the

**footerText**field.Click

**Save**.

Reload your homepage to view the content. You should see something similar like the image below:

Now, you can go back and add additional fields or update existing fields in the Document Type. Fill them out in the content node and then add them in the template to display the data in the website.

Last updated

Was this helpful?

Was this helpful?

---

## Document Types | CMS

Creating a Document Type

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-01aef2268e46ae9cda91da766184ed0d75bb8991%252Fcreating-a-document-type.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3bd71c19&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-afe0c947015a941f4bb3b8639f85ddd2252508fd%252Fsaving-a-document-type.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f79b1a98&sv=2)

Customizing the Document Type

Adding icons

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-37112c1d4d4b89aec28a7917038c016c45ed8ee0%252Fselecting-an-icon.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a8ad5780&sv=2)

Selecting an icon

Setting Permissions

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-3eb16006ef68ffd13beafb21276327f09073bda1%252Fallow-document-type-as-root.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=29d647bc&sv=2)

Allow Document Type as root

Adding Properties

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-09a29ef8d1cc6ee1cef05e015ee3b0de6664eeaf%252Fadd-group-document-type.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7c602ff4&sv=2)

Adding a Group ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-508ae70eae1a5cad17d537812a3ad97e202d2d86%252Fcreating-our-pagetitle-property.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ec1b518d&sv=2)

Adding a property ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-99547de435912df0848c9a50b9638cfd75443ca1%252Fselecting-textstring-data-type.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9d5b3cee&sv=2)

Selecting a Data Type

| Name | Body Text |
|---|---|
| Description | The main content of the page. |
| Data Type | Richtext Editor |

| Name | Footer Text |
|---|---|
| Description | Copyright notice for the footer. |
| Data Type | Textstring |

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-eab39fc4a25ae151f82ea90a16da8401deb26f8a%252Fhomepage-document-type-with-properties.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=14c5ac70&sv=2)

Last updated

Was this helpful?

---

## Getting Started | CMS

**What You Need**

Installing Umbraco

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f8a0f32cb52337e1c7e356a6d3c8e0f6c9de5f81%252Finstalling-umbraco.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1c9328c3&sv=2)

Installing Umbraco

Preparing the Custom Umbraco Template Site

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1a5470c8fb2c6198eb7754e7434ac998dbee60fd%252Ffigure-5-retrospect-template-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=57a55958&sv=2)

Default template homepage

Logging in to Umbraco

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-692ecc891f760238f61efced1c7acc319a479a0c%252Fbackoffice-landing-page.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a2f0edee&sv=2)

Umbraco Backoffice

Last updated

Was this helpful?

The **Creating a Basic Site** tutorial provides step-by-step instructions to build an Umbraco website using a set of HTML, CSS, and JavaScript files. This tutorial enables you to use a website template, modify it, and connect the sections that require content management in the Umbraco CMS.

To begin this tutorial, download the Custom Umbraco Template folder attached below:

Installing Umbraco

To download the latest version of Umbraco, refer to the [Installation article](/umbraco-cms/fundamentals/setup/install). On the installation wizard, follow the steps:

Enter your

**Name**,**Email**, and**Password**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f8a0f32cb52337e1c7e356a6d3c8e0f6c9de5f81%252Finstalling-umbraco.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1c9328c3&sv=2)

Installing Umbraco Click

**Next**.Choose the level of

**Consent for telemetry data**for your Umbraco installation.Click

**Next**.Select the

**Database Type**from the drop-down list.Enter the

**Database Name**.Click

**Install**.

The installation will take a couple of minutes to complete.

Preparing the Custom Umbraco Template Site

Unzip the Custom Umbraco Template to a folder on your system.

Open the

**index.html**from the folder in your preferred browser to see the template.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1a5470c8fb2c6198eb7754e7434ac998dbee60fd%252Ffigure-5-retrospect-template-v8.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=57a55958&sv=2)

Default template homepage

The template contains some text with dummy links. We’re going to turn this into a fully-fledged, Umbraco-powered site!

Logging in to Umbraco

You can log in to Umbraco in two steps:

Once the installation is complete, you will see the

**Login**screen.Enter the

**Name**and**Password**used during the installation process. You should see a similar Umbraco Backoffice as the image below:![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-692ecc891f760238f61efced1c7acc319a479a0c%252Fbackoffice-landing-page.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a2f0edee&sv=2)

Umbraco Backoffice

Last updated

Was this helpful?

Was this helpful?

---

## Setting the Navigation Menu | CMS

You can set up the navigation menu in two ways:

[Dynamically](/umbraco-cms/tutorials/creating-a-basic-website/setting-the-navigation-menu#dynamic-navigation): Umbraco can automatically generate a navigation menu based on the pages in the Content Tree. When you create or modify a page, it will automatically appear in the navigation menu. This dynamic approach eliminates the need to manually add or update menu items when pages are added, removed, or renamed.[Hardcoded](/umbraco-cms/tutorials/creating-a-basic-website/setting-the-navigation-menu#hardcode-navigation): Alternatively, you can hardcode the navigation menu. However, this approach requires more maintenance, as any changes to the pages—such as adding, removing, or renaming—would need to be manually reflected in the menu.

To create dynamic navigation links from the published content nodes, follow these steps:

Go to

**Settings**.Expand the

**Templates**folder from the**Templating**section.Open the

**Master**template.Locate the

`<!-- Navigation -->`

tag (around line 20).Right below it, place the cursor on an empty line.

Select

**Query builder...**in the top-right side of the editor.Make sure it is set to say "I want

**all content**from**my website**".Click

**Submit**.

You now have the following snippet in your **Master** Template:

```
@{
var selection = Umbraco.ContentAtRoot().FirstOrDefault()
	.Children()
	.Where(x => x.IsVisible());
}
<ul>
	@foreach (var item in selection)
	{
		<li>
			<a href="@item.Url()">@item.Name()</a>
		</li>
	}
</ul>
```

This snippet needs to be merged with the navigation above it.

Wrap the

`<ul>`

tag inside the`<div class="container">`

and`<nav>`

tags.

The final result will look like this:

Click

**Save**.

To add a basic hardcoded navigation, follow these steps:

Go to

**Settings**.Expand the

**Templates**folder from the**Templating**section.Open the

**Master**template.Go to the

`<!-- Navigation -->`

tag (around line 20).Copy the content within the

`<div>`

tags (around line 21 to 43) and replace it with the following code:

Click

**Save**.

The IsVisible() helper method

If you add a checkbox property to a Document Type with an alias of umbracoNaviHide, the IsVisible() helper method can be used to exclude these from being shown in any collection.

Let's test the menu. You'll find that clicking on the Articles link throws an Umbraco error as we've not created this page yet. We'll create the Articles page in the next chapter.

Last updated

Was this helpful?

---
