# Server Events From SignalR | CMS

Describes server events emitted via a SignalR hub and available for consumption in the backoffice

Umbraco registers a SignalR event hub that broadcasts events related to the update of entities. These can be used in the backoffice to respond to changes made by users other than the current editor.

Each server event is triggered via a notification handler. So for example, when a document is saved, the `ContentSavedNotification`

is published. This is handled by a class responsible for issuing a server event.

Not all server events should be broadcast to all users. For example, if a user doesn't have access to the Media section, they shouldn't receive notifications on updates to media. For core entities, Umbraco uses the same permission system that defines access in the backoffice. In this way, only events appropriate for the currently logged in editor are exposed.

Each event emitted contains the following fields:

`EventType`

- the event type, which might be`Created`

,`Updated`

,`Deleted`

etc.`EventSource`

- the event source, which might be`Document`

,`Media`

etc.`Key`

- the unique GUID that identifies the entity changed.

The currently authorized user will have one or more claims indicating the access they have to different areas of the backoffice. When first connecting to the SignalR hub, these details are used to assign the user to one or more SignalR groups.

Which groups they have access to is determined by the collection of registered `IEventSourceAuthorizer`

instances.

For example, there is a `DocumentEventAuthorizer`

that ensures users with access to the documents (content) tree are assigned to the `Umbraco:CMS:Document`

event source. As a result, when server events are emitted for documents, only those users with this access will receive them.

Using the same patterns as the core CMS, server events for other entities defined in packages or custom solutions can be emitted.

Firstly, a `IEventSourceAuthorizer`

should be registered. This will likely hook into what you already have in place for controlling access to the backoffice section where the entity is managed.

For example, if you had a `Product`

entity managed in a custom CMS section, the authorizer might look like this:

The authorizer should be registered with Umbraco using something like the following, called from a composer, or otherwise in application start up:

You then need to emit the event from a notification handler which handles notifications published when the entity is updated.

For example, assuming an existing `ProductSavedNotification`

that is published with the product is saved:

Again, the notification handler will need to be registered with Umbraco:

Last updated

Was this helpful?