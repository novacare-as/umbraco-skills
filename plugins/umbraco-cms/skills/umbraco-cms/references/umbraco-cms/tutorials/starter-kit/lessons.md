# Lessons

## Contents

- [Customize the Starter Kit | CMS](#customize-the-starter-kit-cms)
- [2 Add A Blog Post Publication Date](#2-add-a-blog-post-publication-date)
- [3 Add Open Graph](#3-add-open-graph)
- [Ask For Help and Join the Community | CMS](#ask-for-help-and-join-the-community-cms)

---

## Customize the Starter Kit | CMS

This lesson will teach you how to customize the Starter Kit.

A customized version of the site with your Home page image, site name, color theme, font, and perhaps a logo in the header.

Learn how to:

Navigate the editing area in the Content section.

Interact with content properties.

Upload images and use them with content items.

Preview your changes before publishing the content to the site.


Go to the

*Home*page in the Content section.Navigate to the

*Design*group by scrolling down.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c3ec678f32c85e0a27177badf49a725d8f2da2ad%252Fdesign-group_v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b275869a&sv=2)

Home page Design Group Choose a different font and color theme.

Try different combinations and see what fits your site.

Click

**Save**to save a draft of your changes.**Save**will not publish the changes to the website.Click

**Save and preview**to see how the page looks on different screen sizes.

Try changing the background image of the Home page.

Hover over the

*Hero Background*thumbnail and click the trash icon to remove the current image.You can now click the '+' to open a dialog where you can choose an image from the Media library or upload a new image.

Select the image you want and click

**Submit**.

Find the

*Sitename*property and change the name of the site.This is shown in the site navigation menu.

If you want a logo instead of the Site Name you can upload and/or choose an image from the Media Library.


Click

**Save and Publish**to publish the changes to the website.

To see the changes you've made go to the **Info** tab and click on the Link.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-908b589eac19bee4605d4af71242bc0631d7036f%252Flink-to-page_v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=65edabec&sv=2)

Nice job! In this lesson, you've learned to navigate and edit properties on a page. You've also learned the difference between the **Save**, **Preview**, and **Save and Publish** actions and how to use them.

Last updated

Was this helpful?

---

## 2 Add A Blog Post Publication Date

### Contents

- [Add a Blog Post Publication Date | CMS](#add-a-blog-post-publication-date-cms)
- [Add a Blog Post Publication Date | CMS](#add-a-blog-post-publication-date-cms)

---

### Add a Blog Post Publication Date | CMS

Last updated

Was this helpful?

In [Part One](/umbraco-cms/tutorials/starter-kit/lessons/2-add-a-blog-post-publication-date) we added a new property to the *Blogpost* Document Type.
Now in Part Two, we're going to display that instead of the default creation date.

Steps - Part Two

Find the blog posts on the

*Blog*in the**Content**section.Add publication dates to the blog posts.

Remember to publish your changes!

As this field is flagged as Mandatory you now can't save a post without it.


Go to the

**Settings**section.Expand the

**Templates**folder.Navigate to the

*Blogpost*template.This is the template that is rendering the full page view of a blog post


Find the element with the

`blogpost-date`

class and change it to use a nicely formatted Publication Date, i.e.:```
<small class="blogpost-date">@Model.PublicationDate.ToLongDateString()</small>
```

Click

**Save**to save the template. A confirmation message appears confirming the Template is saved.View the blog post page in the browser. Navigate to the page in the

**Content**tree and select the link on the**Info**tab.

Last updated

Was this helpful?

Was this helpful?

---

### Add a Blog Post Publication Date | CMS

In [Part Two](/umbraco-cms/tutorials/starter-kit/lessons/2-add-a-blog-post-publication-date/part-2), we displayed a nicely formatted publication date on the blog post page.

Finally, in Part Three we shall change the blog listing.

In the

**Settings**section, expand the**Partial Views**>**Components**>**LatestBlogPosts**folder.Select

*Default.cshtml*.

Scroll down to find the

`foreach`

loop.Declare a new

`publicationDate`

variable as the first thing within the loop:```
var publicationDate = post.Value<DateTime>("publicationDate");
```

Locate the

`blogpost-date`

element a bit further down and change it to use the new variable:```
<small class="blogpost-date">@publicationDate.ToLongDateString()</small>
```

The ToLongDateString() method is called on the

`publicationDate`

variable to format it as a long date string.

Redefine the

`blogposts`

variable before the first`div`

tag - this will be used for sorting the posts:```
@{
    var blogposts = Model.BlogPosts.OrderByDescending(x => x.Value<DateTime>("publicationDate")).ToList();
}
```

Because we are sorting by a custom property we need to use the generic

`Value`

method.


You can use **Query builder** to construct your queries in a more structured and reusable manner. Use the `UmbracoHelper`

or the `IPublishedContentQuery`

interface to build queries dynamically. For more information, see the article.

Locate the

`@foreach`

loop, and change`Model.Blostposts`

to the variable created above:`blogposts`

:**Save**the partial view - a confirmation message should appear confirming that the Partial view has been saved.

Now view both the Blog overview and the blog posts themselves in the browser to confirm that all is working as expected.

Nice job! In this lesson, you've learned what a **Document Type** is and how to add a new Property to it. You've also learned how to change Templates and sort by custom Properties.

#### See the entire file: Default.cshtml

Last updated

Was this helpful?

---

---

## 3 Add Open Graph

### Contents

- [Add Open Graph - Step 1 | CMS](#add-open-graph---step-1-cms)
- [Add Open Graph - Step 2 | CMS](#add-open-graph---step-2-cms)
- [Add Open Graph - Step 3 | CMS](#add-open-graph---step-3-cms)
- [Add Open Graph - Step 4 | CMS](#add-open-graph---step-4-cms)
- [Add Open Graph - Summary | CMS](#add-open-graph---summary-cms)

---

### Add Open Graph - Step 1 | CMS

Last updated

Was this helpful?

Adding support for Open Graph can be done in many ways. In this lesson, we'll create a reusable set of properties we can add to specific page types.

First we need to see what the expected outcome will be. Open Graph for web pages needs to contain at least the following:

```
<meta property="og:title" content="{Page or site title}" />
<meta property="og:type" content="website" />
<meta property="og:url" content="{URL to the content item}" />
<meta property="og:image" content="{URL to the open graph image}" />
```

Looking at the above we can pull a couple of things out automatically and then add ways to input the rest.

In this lesson, we'll only add Open Graph Content of the type "website", so we don't need input for that. We can also get the URL for the page we are currently on. This leaves us with two remaining properties to add: title and image.

Create a document type composition

Go to the

**Settings**section.Click on

**Document Types**.Select

**Create**>**Document Type**.Name the Document Type

*Open Graph*.Click

**Add Group**and name it*Open Graph*.**Add a property**to the group called*Open Graph Title*.Select

**Select property editor**and search for*textstring*.Click

**Add**.Add another property named

*Open Graph Image*and use the**Media Picker**as the editor.Click

**Add**.Click

**Save**.

Last updated

Was this helpful?

Was this helpful?

---

### Add Open Graph - Step 2 | CMS

Last updated

Was this helpful?

We will now add the group and properties to the Home page and Blog post of the site.

This is done by using compositions to add the functionality in multiple places.

Go to the

**Settings**section.Expand the

**Document Types**folder.Open the

`Home`

Document Type.Select

**Compositions...**in the top-right.Choose the

`Open Graph`

Document Type we created.Click

**Submit**.Click

**Save**.

This will add the group and properties from the **Open Graph** Document Type to the **Home** Document Type. Follow the same steps for the `Blogpost`

Document Type.

Reviewing the changes

If you go to the content section and select Home you can now see your changes (the same goes for the blog posts).

Last updated

Was this helpful?

Was this helpful?

---

### Add Open Graph - Step 3 | CMS

```
@if(Model is IOpenGraph){
        @Html.Partial("../Views/Partials/OpenGraph.cshtml")
    }
```


```
    <head>...

        @if(Model is IOpenGraph){
        @Html.Partial("../Views/Partials/OpenGraph.cshtml")
    }
    </head>
```

Last updated

Was this helpful?

Next step is to get the Open Graph code rendered on the website. This is done in the `head`

section of the HTML, so you need to find the template for this.

In the `Starter Kit`

the head is placed in the Master Template, which is responsible for wrapping all the other templates.

Because you've added the Open Graph feature as a composition you can check if the composition is present on the current page and then render meta tags.

Go to the

**Settings**section.Expand the

**Templates**folder.Select the

*Master*template.Find the

`<head>`

HTML tags at the top of the Template.Write the following before the closing

`</head>`

tag:```
@if(Model is IOpenGraph){
        @Html.Partial("../Views/Partials/OpenGraph.cshtml")
    }
```

Click

**Save**.

This will render a partial view *if* the composition is present on the current page. Currently that is the case for Home and Blog posts on the site.

`IOpenGraph`

is an interface created by adding the composition. When you know how that works you can see how powerful it can be. If not, enjoy the handy helper to check for the composition.

At the end, the head should look like this:

```
    <head>...

        @if(Model is IOpenGraph){
        @Html.Partial("../Views/Partials/OpenGraph.cshtml")
    }
    </head>
```

Last updated

Was this helpful?

Was this helpful?

---

### Add Open Graph - Step 4 | CMS

The final piece to the puzzle is adding the partial view that will be rendered when the composition is present. To do this:

Go to the

**Settings**section.Click on

**Partial Views**and select**Create...**>**New empty partial view**.**Enter a Name**for the partial view. Let's call it:*OpenGraph*Add the standard view model:

`@inherits Umbraco.Cms.Web.Common.Views.UmbracoViewPage`

We only render this view on pages where the composition exists, so we need to be more specific.


In the template editor, pass in the specific model you've created by adding

`<IOpenGraph>`

after the view model.Now you can start rendering the meta tags and adding in the values.


First add the title property

```
<meta property="og:title" content="@Model.OpenGraphTitle" />
```

Add the Open Graph meta tag for type of content - you can hardcode "website" in here:

```
<meta property="og:type" content="website" />
```

Next up is adding the URL for Open Graph.

For this you'll need the entire URL to the page, not relative to this page.

There is a handy method for getting this from a content item. Add:


```
<meta property="og:url" content="@Model.Url(mode: UrlMode.Absolute)" />
```

The final thing we need to do is render the image selected on the Open Graph Image property.

You'll still need to render the entire URL for the image.

First, we'll create a variable to get the image:


```
@{
    var ogImage = Model.Value<IPublishedContent>("openGraphImage");
}
```

Next, we add the

`meta`

property to get the path for the media item:

```
<meta property="og:image" content="@ogImage.Url(mode: UrlMode.Absolute)" />
```

Your partial view is now complete and should only render on pages that are using the Open Graph composition.


The final view should look like this:

If your meta properties do not show up on social media, make sure to inspect source HTML. Make sure there are no inline HTML tags in `og:title`

, `og:description`

etc.

**Pro tip:** To keep the lesson short and to the point, we have left out `null`

-checks from the code examples. So remember to fill in the Open Graph properties, in the content section, to avoid exceptions when viewing the page.

Last updated

Was this helpful?

---

### Add Open Graph - Summary | CMS

Last updated

Was this helpful?

All done, great job! Now test out if it works. Try adding it to more document types. Remember this is only one way of adding this functionality. You might want additional Open Graph tags or the properties to be on a different tab (e.g. *Navigation* or *SEO*).

Summary

In this lesson, you have learned:

To create a Document Type composition

How to create and render a Partial view

Compositions create an interface you can check on and use as a page model (

`IOpenGraph`

)How to get the full path (absolute URL) for both content and media items.


Last updated

Was this helpful?

Was this helpful?

---

---

## Ask For Help and Join the Community | CMS

Last updated

Was this helpful?

If you need some help, here's where to find it.

Outcome

You're a registered user of the Umbraco Community.

Maybe you have even signed up to attend a local meetup!

Steps

Search the , or browse the extensive if you prefer more structured learning.

Please create a forum post if you don't know the best way to proceed. There are experienced community members online 24/7 so hopefully you won't have to wait long for a reply. We are always very excited to help out newcomers!

Check the home page of Our for any upcoming meetups near you. If there aren't any, keep an eye out for any online community hangouts happening soon.

Finally, do think about . Even if it's pointing out something in the documentation that could be made clearer, we'd love to hear from you.


Summary

Welcome, you are now a valued member of the Umbraco community!

Last updated

Was this helpful?

Was this helpful?

---
