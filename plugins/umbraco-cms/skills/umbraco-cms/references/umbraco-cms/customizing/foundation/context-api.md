# Context Api

## Contents

- [Consume a Context | CMS](#consume-a-context-cms)
- [Context API Fundamentals | CMS](#context-api-fundamentals-cms)
- [Provide a Context | CMS](#provide-a-context-cms)

---

## Consume a Context | CMS

Learn how to consume contexts in Umbraco elements using one-time references or subscriptions to access data and functionality through the Context API.

There are two ways to consume a context: get a **one-time reference** to the context, or get a **subscription** for handling context changes. The Context API is a flexible system where contexts can get disconnected or replaced. A subscription allows for the handling of these changes. However, subscriptions use more resources. They are typically consumed in the constructor, a time when the computer is already processing a lot. Which way to go depends on your use case.

A one-time reference approach is suitable for fire-and-forget events. The key here is that the context is not needed on initialization, but is only needed when a specific criteria is met. For instance, events that occur after user interaction or when a specific function is called. In that case, you need to get a context, do something and forget about the context after that.

If you need a context during initialization which is then set as a variable, you should always use a subscription. Otherwise, you risk holding on to a context that could be disconnected or replaced without you knowing.

An [Umbraco Element](/umbraco-cms/customizing/foundation/umbraco-element) is **any web component** that extends `UmbLitElement`

or uses the `UmbElementMixin`

to wrap its base class. Whether you are building with Lit, vanilla JavaScript, or any other web component framework, you can make it an Umbraco Element. This gives it full access to the Context API.

Umbraco Elements provide two methods for consuming contexts:


- Retrieves a one-time reference to a context**getContext(token)**

- Creates a reactive subscription to a context**consumeContext(token, callback)**

Both methods accept a Context Token (or string alias) to identify which context to consume.

The first example uses Lit and that is the way Umbraco builds their elements. If you do not want to use Lit, there is also an example using vanilla JavaScript. Both examples do not have any TypeScript specific code. You can use them in either a JavaScript or a TypeScript file.

```
import { UMB_NOTIFICATION_CONTEXT } from '@umbraco-cms/backoffice/notification';
import { html } from '@umbraco-cms/backoffice/external/lit';
import { UmbLitElement } from '@umbraco-cms/backoffice/lit-element';

//The example element extends the UmbLitElement (which is the same as UmbElementMixin(LitElement))
//This gives us all the helpers we need to get or consume contexts
export default class ExampleElement extends UmbLitElement {

    /** Notification handler for the notification button */
    async #notificationButtonClick() {
        //We try to get an instance of the context
        const notificationContext = await this.getContext(UMB_NOTIFICATION_CONTEXT);
        if (!notificationContext) {
            throw new Error('Notification context not found!');
        }
        
        notificationContext?.peek("positive", {
            data: {
                headline: "Success",
                message: "The notification button was clicked successfully!"
            }
        });

        //The notification is sent, now forget the context
    }

    /**
     * Renders the lit component
     * @see https://lit.dev/docs/components/rendering/
     */
    render() {
        return html`
            <uui-button look="primary" color="default" @click="${this.#notificationButtonClick}">
                Click me for a notification!
            </uui-button>
        `;
    }
}

// Register the custom element
customElements.define('example-element', ExampleElement);
```

When you are dealing with a subscription, it is good practice to consume the context in the constructor for the following reasons:

The constructor runs once when the element is created. This ensures your context subscription is set up before the element connects to the DOM. This guarantees you will not miss any context updates that occur during the element's initialization.

Context consumers created in the constructor are automatically connected when the element enters the DOM (

`connectedCallback`

). They are disconnected when it is removed (`disconnectedCallback`

). You do not need to manually manage this lifecycle as Umbraco's controller system handles it for you.By establishing context subscriptions in the constructor, your element's state is consistent from the moment it is created. This prevents race conditions where the element might render or perform actions before its required contexts are available.

Creating context consumers in the constructor is more efficient than creating them in lifecycle methods that are called multiple times. For example,

`connectedCallback`

fires every time the element is added to the DOM.

The first example uses Lit and that is the way Umbraco builds their elements. If you do not want to use Lit, there is also an HTML element example. Both examples do not have any TypeScript specific code. You can use them in either a JavaScript or a TypeScript file.

Not all code that needs contexts lives in UI elements (web components). Services, managers, repositories, and helper classes often need access to contexts. These may include notifications, workspaces, or application state. However, they do not exist as elements in the DOM.

For these non-UI classes, extend `UmbControllerBase`

to gain the same context consumption capabilities as elements. This base class provides `getContext()`

and `consumeContext()`

methods. This allows any class with a controller host to access the Context API.

This example creates an example service that can show a notification in the backoffice of Umbraco based on the given text.

This example consumes the document workspace context and saves it to a variable to be used later.

In rare cases, you may need complete manual control over context consumption. This means not extending `UmbControllerBase`

or using element mixins. This is typically necessary when:

Integrating with third-party libraries or frameworks

Working with legacy code that cannot be refactored

Building custom architectural patterns outside Umbraco's standard controller system


For these scenarios, use `UmbContextConsumer`

directly. This low-level API gives you full control but requires manual lifecycle management. You must call `hostConnected()`

, `hostDisconnected()`

, and `destroy()`.


**Use this approach only when necessary.** The methods shown in previous sections handle lifecycle management automatically. These include `UmbLitElement`

, `UmbElementMixin`

, and `UmbControllerBase`

. They are suitable for most use cases.

To create the one-time reference, you don't provide a callback when calling the UmbContextConsumer. This makes it destroy itself when going out of scope.

In contrast to the one-time reference, a callback is provided. This makes it a subscription. You need to disconnect and destroy the context consumer yourself. This example creates a custom `DocumentService`

that consumes the Document Workspace Context.

To use this service, the host element must call the lifecycle methods:

Last updated

Was this helpful?

---

## Context API Fundamentals | CMS

Learn about the Context API fundamentals, terminology, and how it enables communication between elements in the Umbraco backoffice through hierarchy.

The Context API is a powerful communication system in Umbraco's backoffice. It enables elements to share data and functionality without tight coupling. This article covers the core concepts, terminology, and flow mechanisms you need to understand before working with contexts.

Whether you're building custom property editors, workspace extensions, or complex UI components, understanding the Context API is essential. It provides a structured way to access shared state, services, and functionality throughout the element hierarchy.

The Umbraco backoffice is a collection of DOM elements like any web application. Elements can be anything: a button, a property editor, a section, a menu option, or a tree. These elements have a hierarchy and form the entire DOM tree that makes up the Umbraco application.

The Context API in Umbraco is a communication system. It allows elements to share data and functionality through their hierarchy in a `context`

. Parent elements can provide contexts that their descendant elements can request and use.

When an element needs access to some data or functionality, it requests the appropriate context. It does this by using the context's identifier. The system finds the nearest provider up the element hierarchy. This creates loose coupling between elements. Descendants don't need direct references to their dependencies as they can declare what type of context they need and the system handles the connection.

This approach is similar to dependency injection in managing dependencies automatically. However, the Context API works specifically through the element structure rather than a central container. For example, a custom property editor can request the `workspace context`

to access information about the current document. Information that can be accessed includes the document's name, content type, or publication status.

The Context API exists to solve common problems in complex user interfaces:

Avoiding prop drilling: Instead of passing data through multiple layers of components, child elements can directly request what they need.

Loose coupling: Elements don't need direct references to their dependencies. This makes the codebase more modular and maintainable.

Shared state management: Multiple elements can access and react to the same state without complex wiring.


To understand the Context API, it's important to understand the terminology that is used in the rest of the documentation.

An object that encapsulates both data and methods to interact with that data. This object can be provided to descending DOM elements. A context represents a specific capability or state that multiple elements might need to access. Examples include workspace context, content data, user permissions, or specialized services. Contexts encapsulate both data and methods, making them more than data containers. Unlike repositories, a context is always only available within the scope of a certain element and its descendants.

An element that creates and makes a context available to its descending elements. The provider is responsible for the context's lifecycle. One element can provide multiple different contexts if needed.

Any element that requests and consumes a context provided by one of its ancestor elements. An element becomes a consumer by requesting a context. The element does not need to know which specific ancestor provides the context nor implement any special interfaces. The consuming element receives callbacks when the requested context becomes available or unavailable. This allows the element to react appropriately to changes in the element hierarchy.

A unique identifier used to request a specific context. Context tokens serve as contracts between providers and consumers. They define exactly which context is being requested and ensure that the right provider responds. Using a context token prevents conflicts when multiple contexts might have similar names and makes clear what functionality is being shared.

Each DOM element can be a context provider. Each descendant in the DOM hierarchy can consume that context if desired. When an element wants to consume a context, the following happens:

An element requests a context by a given Context Token.

The Context API dispatches an event that starts at the element that requested the context. The event bubbles up the DOM tree to each parent element until an element is found that responds to the event.

An instance of the context is provided back to the element that requested the context.


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-adb44ad0f24575a1dccb7eb184f890bd49643a36%252Fumbraco_context_api_flow.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e9c18f17&sv=2)

If no context could be found and the event reaches the top-level element (the document), no context is consumed.

Although every element can be a context provider, the most important contexts are registered at specific hierarchy levels. These levels are also explicit extension points in the Umbraco manifest.

The most common hierarchy levels to which the contexts can be registered are:

Global

Section

Workspace

Property


**Global contexts** are registered at the highest level and are always available anywhere in the backoffice. Examples of global contexts:

`Notification context`

: used for displaying notifications in the backoffice. This context is consumable in elements anywhere in the DOM tree.`Current user context`

: has information about the currently logged in user. This context is consumable anywhere in the DOM tree.

**Section contexts** are available in the context of a section. That is everything in the backoffice except the menubar. Examples of section contexts:

`Section context`

: provides information about the section, like path, alias, and label.`Sidebar menu section context`

: holds information about the sidebar menu, like which menu is currently selected.

**Workspace contexts** work on a workspace, the part of Umbraco that is next to the tree. Example for this level:

`Workspace context`

: holds information about the current entity being edited in the workspace. This holds minimal information about an entity and the entity type. There are specific workspace contexts per entity type. For instance, the`Document workspace context`

for documents and`Media workspace context`

for media.

**Property contexts** are contexts that work at the property level. They can work on one or more property editors. An example is the clipboard functionality where blocks can be copied and pasted between block grids and block lists. Because these contexts are scoped at the property level, they are typically not consumed directly.

Last updated

Was this helpful?

---

## Provide a Context | CMS

Providing a Context enables distant code to communicate with it, ideal way to incorporate central logic.

Last updated

Was this helpful?

Providing a Context enables distant code to communicate with it, ideal way to incorporate central logic.

Provide a Context API

The recommended approach is to base your Context API on the `UmbContextBase`

class, which provides automatic context registration. The following example shows how it's used:

```
import { UmbContextBase } from '@umbraco-cms/backoffice/class-api';

export class MyCustomContext extends UmbContextBase {
	constructor(host: UmbControllerHost) {
		super(host, MY_CUSTOM_CONTEXT);
	}
}

export const MY_CUSTOM_CONTEXT = new UmbContextToken<MyCustomContext, MyCustomContext>(
	'MyCustomContextUniqueAlias',
);
```

For a practical implementation example, see the [Extension Type Workspace Context](/umbraco-cms/customizing/extending-overview/extension-types/workspaces/workspace-context) article.

You can provide a Context API from any Umbraco Element or Umbraco Controller:

```
this.provideContext('myContextAlias', new MyContextApi());
```

Or provide it from a Controller using a `host`

reference to the Controller Host (Umbraco Element/Controller):

```
new UmbContextProviderController(host, 'myContextAlias', new MyContextApi());
```

Last updated

Was this helpful?

Was this helpful?

---
