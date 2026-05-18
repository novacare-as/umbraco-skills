# UI Library | CMS

Find out more about Umbraco Backoffice UI Library, Backoffice UI API and Storybook.

With the UI Library, you get a collection of visual building blocks that consists of pieces to build any UI in Umbraco. Each component is a building block updating its display according to the data passed to it.

**Are you looking for the AngularJS documentation?**

With Umbraco 14 the Umbraco backoffice has been rebuilt using Web Components and TypeScript. This means that AngularJS is no longer being used in Umbraco CMS, hence the removal of the corresponding documentation.

With the UI API, you get a set of collections related to modules export, interfaces, and hierarchy. This includes code examples and much more that you can use to extend the backoffice.

![Cover](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-07e0d5c35ebb2091afedbe2deba5bf13d163f565%252FDocumentations%2520Icons_Umbraco_CMS_Fundamentals_Backoffice.png%3Falt%3Dmedia&width=752&dpr=3&quality=100&sign=fadcf50d&sv=2)

See, test, and get a feel for the familiar backoffice components built using the new UI components.

![Cover](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6258bb83e76c6849276f0a4e4230f8dd940a38d6%252FDocumentations%2520Icons_Umbraco_CMS_Fundamentals_Code.png%3Falt%3Dmedia&width=752&dpr=3&quality=100&sign=600d328d&sv=2)

Find reference documentation about all types and contexts in the Backoffice.

The Umbraco UI Library is a set of web components that can be used to build Umbraco User Interfaces. The UI Library separates the user interface from Umbraco’s business logic and creates a unified user experience. This is done with coherent styling and naming, across all the Umbraco platforms and projects including the ones developed by you.

is an application that gathers all the components together of the UI Library. It holds the documentation for the components and showcases different use case scenarios. You can explore all the components through stories reflecting their use cases.

Each story has interactive controls that allow you to change the state of the component in real time. Every publicly available property is editable in Storybook, so you can test out custom configurations and use cases.

You can also modify the custom properties in the stylesheet to see how the component will look. Every story has a code example that you can copy and paste into your project. This will allow you to implement the components in your own packages and extensions.

The is the starting point for working with the Umbraco UI Library. The Storybook contains two tabs:

Canvas - The Canvas tab allows to use the interactive controls.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1e6b0c0730a7a1835410eb51bf2955e1f9a6d197%252FCanvas_tab.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ace446b0&sv=2)

Documentation - Here, you can find code examples for all the stories and use them in your markup. You can look it up by tag name or head to the project repository, where, in the packages folder, you will find all the component packages with all the necessary scripts and examples in the readme files.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ac21325f1728886a8dbd7236d70ffe8577b627f5%252FDocs_tab.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=71b26da3&sv=2)


You can also work with the components on a code level. If you want to do so here is how you import it:

This requires that your Package has the `@umbraco-cms/backoffice`

dependency.

Last updated

Was this helpful?