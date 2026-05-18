# Creating an XML Sitemap | CMS

Learn how to build, configure, and add an XML sitemap to your Umbraco website.

An XML sitemap is a guide for search engines to discover and index your content. Each page on your site that you wish to feature will be represented by a `<url>`

entry in the list.

Adding an XML sitemap to your site makes it easier for search engines such as Google to find and index the pages of your website. Having a sitemap will improve the Search Engine Optimization (SEO) for your website.

This tutorial will take you through the steps of building and configuring a sitemap that fits your Umbraco website.

If you are in a hurry, there is a community package that can do the job for you:

An XML sitemap is a list of URLs for the content on your site.

See the about the XML schema, the sitemap needs to conform to.

Below is an XML sample of a typical sitemap entry:

```
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    <url>
        <loc>https://www.example.com/</loc>
        <lastmod>2005-01-01</lastmod>
        <changefreq>monthly</changefreq>
        <priority>0.8</priority>
    </url>
</urlset>
```

There are different ways of approaching this task. The best approach will be determined by the size of your site and your preference for implementing functionality in Umbraco.

In this tutorial, we are going to write the code directly in a Template using Razor and `IPublishedContent`

. You may want to take a different approach, like using route hijacking to write the code in an MVC controller.

Throughout this tutorial, we will:

Create a new Document Type called 'XmlSiteMap' that is to be used for the sitemap content page,

Create a Document Type composition, containing a consistent set of sitemap-related properties, and

Build a Razor template view to generate the sitemap entries based on different criteria and filters.


In this first step of the tutorial, we will be creating a new Document Type for our sitemap page.

Navigate to the

**Settings**section in the Umbraco backoffice.Create a new

**Document Type with Template**under the Document Types folder.Name the new Document Type

**XmlSiteMap**.Add a TextString property called

**Excluded Document Types**(alias:`excludedDocumentType`

).Save the XmlSiteMap Document Type.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-85db89e37935c60bc79245a79fa34f70119cc696%252Fcreate-sitemap-doctype.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1367e7c7&sv=2)

View of the properties defined on the finished XmlSiteMap Document Type Open the Document Type used at the root of your website (Example:

**HomePage**).Go to the

**Structure**tab.Add the new XmlSiteMap under

**Allowed child node types**.Save the

*HomePage*Document Type.Navigate to the

**Content**section.Create a new XmlSiteMap page as a subpage to the root/home page in your Content tree.

Use the alias to add the XmlSiteMap Document Type to the "Excluded Document Type" list:

`xmlSiteMap`

.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ebbfe924b6d99a8e1f8c39bff6987c1d1498cd7c%252Fcreate-sitemap-page.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b989a2b7&sv=2)

View of the Content Tree after a Sitemap page has been added

In this step, we will be creating a Composition Document Type. This Document Type will be used to add sitemap options to all Document Types used to add content pages to the website.

The following options will be added:

**Relative priority**: A sitemap entry will allow you to state the*relative priority*of any particular page in terms of its importance within your site. A value of 1.0 is the highest level of importance and 0.1 is at the other end of the scale.**Change Frequency**: You can add a*change frequency*to define how often the content on a particular page is expected to change. This will help the search engine know when to return to reindex any regularly updated content.

Create and configure the Document Type Composition by following these steps:

Navigate to the

**Settings**section in the Umbraco backoffice.Create a new

**Composition**under the Document Types folder.Name the new Document Type

**XmlSiteMapSettings**.Add the following properties: a. Slider named

**Search Engine Relative Priority**(searchEngineRelativePriority): MinValue: 0.1, MaxValue: 1, Step Increments 0.1, InitialValue 0.5. b. Dropdown named**Search Engine Change Frequency**(searchEngineChangeFrequency): Always, hourly, daily, weekly, monthly, yearly, and never. c. Toggle named**Hide From Xml Sitemap**(hideFromXmlSitemap).

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c2fe55327eef4fb58bea7e556d561e2b117782f9%252Fcreate-sitemap-settings-composition-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9ca4b9a1&sv=2)

Add the XmlSiteMapSettings composition to all Document Types used to create content pages in the Content section.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-59e585071509f6400523a86b175bc3f1e4de2239%252Fxml-sitemap-add-composition-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=31a6dc71&sv=2)

This will give editors the ability to set a priority and a change frequency for each page on the site. We will use the values from the parent or parent's parent page in case the values are not specified on a particular page. This enables the values to be set in one place for a particular section.

In this step, we will be building the XmlSiteMap template to display the XML schema on the sitemap page.

Editing the template can be done in two different ways:

Locate the XmlSiteMap Template in the

**Settings**section of the Umbraco backoffice and use the editor to make the changes, orOpen and work with the

`Views/XmlSiteMap.cshtml`

file in your preferred Integrated Development Environment (IDE) on your machine.

We will start by adding the XML schema for the sitemap. Since we do not want our template to inherit any 'master' HTML layouts we will set the `layout`

to be `null`.


Navigate to the

**Settings**section of the Umbraco backoffice.Find and open the XmlSiteMap Template.

Set

`Layout`

to`null`

.Add

`Context.Response.ContentType = "text/xml";`

within the curly brackets.Add the following code snippet below the closing curly bracket in the template:

Save the template.


The sitemap should start at the homepage at the root of the site. Since our XmlSiteMap page is created as a subpage page to the root, we can use the `Root()`

helper to define the starting point as `IPublishedContent`.


Add

`IPublishedContent siteHomePage = Model.Root();`

within the first set of curly brackets in the template.Save the template.


We will retrieve each page in the site as **IPublishedContent** and read in the `SearchEngineChangeFrequency`

and `SearchEngineRelativePriority`

properties. We will also read the URL of the page as well as when it was last modified.

You can include HTML markup in the body of a method declared in a code block. This is a great way to organize your razor view implementation and to avoid repeating code and HTML in multiple places.

Add the following code snippet below the XML schema:

Update the XML schema to include

`RenderSiteMapUrlEntry(siteHomePage)`:


We are using `IPublishedContent`

in this example. Using **ModelsBuilder** instead will enable you to take advantage of the fact that the XML Sitemap Settings composition will create an interface called `IXmlSiteMapSettings`

. This will allow you to adjust the helper to accept `RenderSiteMapUrlEntry(IXmlSiteMapSettings node)`

and read properties without the `Value`

helper. You would still need to create an extension method on `IXmlSiteMapSettings`

to implement the recursive functionality we make use of on the `SearchEngineChangeFrequency`

property.

Visit the URL of your sitemap page (`http://yoursite.com/sitemap`

) to render a single sitemap entry for the homepage.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-eac01d0e45d83e290e0abcb4f132b1a4f20c7d2e%252Fsitemap.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=64363bdd&sv=2)

We need to go through each page created beneath the homepage to see if they should be added to the sitemap.

We will add a `RenderSiteMapUrlEntriesForChildren`

helper which accepts a 'Parent Page' parameter as the starting point. Then we will find the children of this Parent Page and write out their sitemap entry. Finally, we will call this same method again from itself.

Add the following code snippet below the

`RenderSiteMapUrlEntry`

helper and before the closing curly bracket:Update the XML schema to include

`RenderSiteMapUrlEntriesForChildren(siteHomePage)`:


You will now see the XML sitemap rendered for the entire site.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6d173120dae1339fc4c999f44280312c0def21f8%252FsitemapWithChildren.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=21dc4d1f&sv=2)

In this step, we will use different parameters for filtering the content on the sitemap.

As everything is currently added on the sitemap, we have yet to take into account the pages that should be hidden.

We added a **HideFromXmlSitemap** checkbox to all Document Types via our `XmlSiteMapSettings`

composition. This configuration needs to be included when rendering the sitemap. The helper needs to only return pages that do not have the HideFromXmlSitemap checked.

Update the

`RenderSiteMapUrlEntriesForChildren`

helper as shown below:

Revisit a page in the Content tree, and check the HideFromXmlSitemap option. This page will now be excluded from the sitemap.

To further control which and how many pages are shown in the sitemap you can filter by **depth**. We will provide the helper with a number that defines how deep into the Content tree the sitemap should look.

Navigate to the

**Settings**section in the Umbraco backoffice.Find and open the XmlSiteMap Document Type.

Add a Numeric property and call it

**Max Site Map Depth**(alias:`maxSiteMapDepth`

).Save the Document Type.

Open the XmlSiteMap Template.

Add the following line within the first set of curly brackets:

Update the

`RenderSiteMapUrlEntriesForChildren`

helper as shown below:Navigate to the

**Content**section in the Umbraco backoffice.Open the Sitemap page and set the

**Max Site Map Depth**to`2`

.Save and publish the content.


Your sitemap will now only contain entries for the top two levels. Leaving the value blank will mean that no maximum depth restriction will be applied.

Finally, we need the helper to check the **Excluded Document Types** list on the XmlSiteMap Document Type.

Open the XmlSiteMap Template.

Add the following code snippets within the first set of curly brackets:

Update the

`RenderSiteMapUrlEntriesForChildren`

helper as shown below to pass in the array:

Visit the URL of your sitemap page (`http://yoursite.com/sitemap`

) to render a complete sitemap for your site.

It contains an entry for each page that is

Not

**hidden**,Not based on an

**excluded Document Type**, andLocated within the bounds of the defined

**depth**.

Once you have added a sitemap to your site it is recommended that you also reference it in your `robots.txt`

file.

Locate and open the

`robots.txt`

file in your preferred IDE.Add the following code snippet:

Save the file.


Once you introduce a sitemap for the first time, you might find yourself being crawled by multiple different search engine bots. This is expected and exactly what you want.

It can be a good idea to add a **crawl-rate** to the `robots.txt`

as well. This will instruct well-behaved search engine bots to increase the time between requests to your site.

Add

`Crawl-delay: 10`

to a new line in your`robots.txt`

file.Save the file.


Visit to test the validity of your generated XML sitemap.

Last updated

Was this helpful?