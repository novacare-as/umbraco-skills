# Reference — Part 5: UmbracoMapper | CMS → Property Editor UIs | CMS

## UmbracoMapper | CMS

Often in code there is a need to 'map' one object's properties to another type of object. The 'type of objects' are not related by inheritance or interface. (Think database layer object, passing information to a presentation layer ViewModel etc). In these circumstances, it can save time and provide consistency to consolidate the logic to map between the options into one set of 'Mapping' rules.

UmbracoMapper replaced AutoMapper which was an external dependency. AutoMapper builds the mapping code dynamically, based upon mapping profiles, which are defined as C# expressions. UmbracoMapper relies on static code, that is, mappings need to be hand-written.

If you need to map `IPublishedContent`

, you might need a **custom implementation** or a **third-party solution like** **(**which has been renamed to ) rather than relying on Umbraco's `IUmbracoMapper.`


The IUmbracoMapper is registered with Dependency Injection (DI). It can therefore be injected into constructors of controllers, custom classes etc, wherever DI is used.

Mapping with the UmbracoMapper works in ways similar to AutoMapper:

```
// assuming source is ISource, create a new target instance
var target = umbracoMapper.Map<ITarget>(source);

// assuming both source and target already exists
target = umbracoMapper.Map(source, target);
```

The UmbracoMapper class also defines explicit methods to map enumerables:

```
// assuming sources is IEnumerable<ISource>, map to IEnumerable<ITarget>
var targets = umbracoMapper.MapEnumerable<ISource, ITarget>(sources);
```

Explicit mapping of enumerables enumerates the source items, and map each item individually.

It can also implicitly map enumerables. The following code is also valid:

If a mapping has been defined from `IEnumerable<ISource>`

to `IEnumerable<ITarget>`

, then it will be used. Otherwise, the UmbracoMapper will look for a mapping from the source type to the target type, pretty much like the explicit method.

Mappings are defined in `IMapDefinition`

instances. This interface defines one method:

Mappings are registered (and must be registered) via a [collection builder](/umbraco-cms/implementation/composing#collections):

A definition provides a constructor, and a map:

The constructor function is used to create an instance of the target class. The most basic implementation would be:

The mapping action is used to map an instance of the source class, to an instance of the target class. The most basic implementation would be:

The constructor function is used whenever the mapper is asked to create a target instance. Then, the mapping action is used.

In other words, `umbracoMapper.Map<ITarget>(source)`

will first run the construction function, and then the mapping action. On the other hand, `umbracoMapper.Map(source, target)`

where target already exists, would only run the mapping action.

The UmbracoMapper class provides multiple overloads of the Define method:

An overload accepting a constructor function and a mapping action, as presented above.

An overload accepting a mapping action only, which tells the mapper how to map to an existing target (but the mapper will not be able to create new target instances).

An overload accepting a construction function, which tells the mapper how to create new target instances (but the mapper will not perform any additional mapping).

A parameter-less overload, which defines a "no-operation" mapping (the mapper cannot create new target instance, and mapping does nothing).


Both constructor functions and map actions presented above expose a context parameter which is an instance of MapperContext and provides two types of services:

An

`Items`

dictionary which can store any type of object, using string keys, and can be used to carry some context along mappings;Some Map and MapEnumerable functions that can be used in mapping functions, to recursively map nested elements, while propagating the context.


The context provides a `HasItem`

property. To check whether the context has items, without allocating an extra empty dictionary, use this property.

The context is used, for instance, to carry the culture when mapping content items with variants. See the `MapperContextExtensions`

class, which contains methods such as:

And

Every `Map`

and `MapEnumerable`

method exposed by the UmbracoMapper have overloads that can manipulate the context before executing the mapping. For instance,

Umbraco.Code is an assembly which should contain coding utilities for Umbraco. At the moment, it contains only one Roslyn analyzer, the `MapAllAnalyzer`

, which is used to help writing mapping methods.

The code lives in the and the tool is available via . It is included as a development dependency in Umbraco.

The analyzer examines every method mapping from a source to a target, and being marked with the `// Umbraco.Code.MapAll`

comment block:

The analyzer verifies that every publicly settable property of target is assigned a value. If a property is not assigned a value, the tool raises a build error (ie. the code will not compile).

Since, contrary to AutoMapper, mapping is not implicit nor automatic, this ensures that an error would be raised. Should a new property be added to ISource, the corresponding mappings must be updated.

It is possible to exclude some properties from the check:

And the comment can be repeated if the list of excluded properties is long:

The analyzer follows the standard analyzer development patterns, and building the code in Release mode produces the appropriate NuGet package.

Below you will find a full example showing you how to map a collection of type Product to a collection of type ProductDto.

Result from `/umbraco/api/products/getall`:


Result from `/umbraco/api/products/getfirstproduct`:


Last updated

Was this helpful?

---


## Markdown to HTML Conversion | CMS

Describes how markdown to HTML is carried out within Umbraco.

Last updated

Was this helpful?

Describes how markdown to HTML is carried out within Umbraco.

Umbraco requires Markdown to be converted into HTML. Primarily, this is to support the [Markdown property editor](/umbraco-cms/fundamentals/backoffice/property-editors/built-in-umbraco-property-editors/markdown-editor). There are also internal use cases, for example, in rendering email notification content for [health checks](/umbraco-cms/extending/health-check).

The conversion is managed via the `IMarkdownToHtmlConverter`

interface.

Umbraco registers a default implementation of `HeyRedMarkdownToHtmlConverter`

, which is based on the .

Also provided is an unregistered, alternate implementation of `MarkdigMarkdownToHtmlConverter`

, based on the .

Both implementations convert standard markdown into HTML, but there are some subtle differences in the output produced.

Modifying the Default Behavior

If you prefer to use the Markdig-based implementation, replace the default registration by adding the following composer:

```
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.Strings;
using Umbraco.Cms.Infrastructure.Strings;

public class MarkdownToHtmlComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.Services.AddUnique<IMarkdownToHtmlConverter, MarkdigMarkdownToHtmlConverter>();
    }
}
```

Alternatively, the interface itself can be implemented directly, enabling you to use the library and custom behavior you prefer:

Planned Updates

The Hey Red Markdown library is now deprecated. We expect to make the implementation based on Markdig the default one registered from Umbraco 18. The Hey Red Markdown library implementation will be removed in Umbraco 19.

Last updated

Was this helpful?

Was this helpful?

```
namespace Umbraco.Cms.Core.Strings;

public interface IMarkdownToHtmlConverter
{
    /// <summary>
    /// Converts the specified Markdown-formatted text to an HTML-encoded string.
    /// </summary>
    /// <param name="markdown">The input string containing Markdown syntax to be converted.</param>
    /// <returns>A string containing the HTML representation of the input Markdown.</returns>
    public string ToHtml(string markdown);
}
```

---


## Notifications

### Contents

- [CacheRefresher Notifications Example | CMS](#cacherefresher-notifications-example-cms)
- [ContentService Notifications Example | CMS](#contentservice-notifications-example-cms)
- [Creating And Publishing Notifications | CMS](#creating-and-publishing-notifications-cms)
- [Determining if an entity is new | CMS](#determining-if-an-entity-is-new-cms)
- [Hot vs. cold restarts | CMS](#hot-vs-cold-restarts-cms)
- [MediaService Notifications Example | CMS](#mediaservice-notifications-example-cms)
- [MemberService Notifications Example | CMS](#memberservice-notifications-example-cms)
- [Notification Handler | CMS](#notification-handler-cms)
- [Umbraco Application Lifetime Notifications | CMS](#umbraco-application-lifetime-notifications-cms)

---

### CacheRefresher Notifications Example | CMS

Example of how to use a CacheRefresher Notification

```
public abstract class CacheRefresherNotification : INotification
{
    public CacheRefresherNotification(object messageObject, MessageType messageType)
    {
        MessageObject = messageObject ?? throw new ArgumentNullException(nameof(messageObject));
        MessageType = messageType;
    }

    public object MessageObject { get; }

    public MessageType MessageType { get; }
}
```

```
public enum MessageType
{
    RefreshAll,
    RefreshById,
    RefreshByJson,
    RemoveById,
    RefreshByInstance,
    RemoveByInstance,
    RefreshByPayload,
}
```

Last updated

Was this helpful?

Example of how to use a CacheRefresher Notification

Before starting with cache refresher notifications it's a good idea to ensure you need to use them. If you want to react to changes in content, for instance, there's no real reason to use these notifications. This is due to the [content service notifications](/umbraco-cms/reference/notifications/contentservice-notifications) being easier to work with. If you need to react to changes in the cache, then these are the notifications for you.

Cache refresher notifications are sent when the cache has refreshed. There are multiple different types of cache refresher notifications. These types are based on what type has been updated in the cache, for instance, content or media. All these notifications inherit from the same base notification: `CacheRefresherNotification`.


The base notification is implemented in the following way:

```
public abstract class CacheRefresherNotification : INotification
{
    public CacheRefresherNotification(object messageObject, MessageType messageType)
    {
        MessageObject = messageObject ?? throw new ArgumentNullException(nameof(messageObject));
        MessageType = messageType;
    }

    public object MessageObject { get; }

    public MessageType MessageType { get; }
}
```

As you can see this notification contains two properties, a `MessageObject`

and a `MessageType`

. The `MessageType`

specifies what kind of cache operation was performed, for example `RemoveById`

. The possible message types is as follows:

```
public enum MessageType
{
    RefreshAll,
    RefreshById,
    RefreshByJson,
    RemoveById,
    RefreshByInstance,
    RemoveByInstance,
    RefreshByPayload,
}
```

The other parameter `MessageObject`

will depend on what type of cache refresher notification you're handling. If you for instance handle the `ContentCacheNotification`

, the message object will be `ContentCacheRefresher.JsonPayload[]`.


This object contains the Id and key of the item being updated, as well as an enum specifying how the tree is updated:

An example of working with the `ContentCacheNotification`

can be seen here:

Last updated

Was this helpful?

Was this helpful?

```
[Flags]
public enum TreeChangeTypes : byte
{
    None = 0,

    // all items have been refreshed
    RefreshAll = 1,

    // an item node has been refreshed
    // with only local impact
    RefreshNode = 2,

    // an item node has been refreshed
    // with branch impact
    RefreshBranch = 4,

    // an item node has been removed
    // never to return
    Remove = 8,
}
```

```
using Umbraco.Cms.Core.Cache;
using Umbraco.Cms.Core.Events;
using Umbraco.Cms.Core.Notifications;
using Umbraco.Cms.Core.Services;
using Umbraco.Cms.Core.Services.Changes;

namespace Umbraco.Cms.Web.UI;

public class ContentCacheRefresherExample : INotificationHandler<ContentCacheRefresherNotification>
{
    private readonly IContentService _contentService;

    public ContentCacheRefresherExample(IContentService contentService)
    {
        _contentService = contentService;
    }

    public void Handle(ContentCacheRefresherNotification notification)
    {
        if (notification.MessageObject is not ContentCacheRefresher.JsonPayload[] payloads)
        {
            return;
        }

        foreach (ContentCacheRefresher.JsonPayload payload in payloads)
        {
            if (payload.ChangeTypes is not TreeChangeTypes.RefreshNode or TreeChangeTypes.RefreshBranch)
            {
                return;
            }

            // You can do stuff with the ID of the refreshed content, for instance getting it from the content service.
            var refreshedContent = _contentService.GetById(payload.Id);
        }
    }
}
```

---

### ContentService Notifications Example | CMS

Find out more about ContentService Notifications and explore some example of how to use it

The ContentService class is the most commonly used type when extending Umbraco using notifications. ContentService implements IContentService. It provides access to operations involving IContent.

Example usage of the ContentPublishingNotification:

```
using Umbraco.Cms.Core.Events;
using Umbraco.Cms.Core.Notifications;

namespace Umbraco.Docs.Samples.Web.Notifications;

public class DontShout : INotificationHandler<ContentPublishingNotification>
{
    public void Handle(ContentPublishingNotification notification)
    {
        foreach (var node in notification.PublishedEntities)
        {
            if (node.ContentType.Alias.Equals("announcement"))
            {
                var newsArticleTitle = node.GetValue<string>("title");
                if (!string.IsNullOrWhiteSpace(newsArticleTitle) && newsArticleTitle.Equals(newsArticleTitle.ToUpper()))
                {
                    notification.CancelOperation(new EventMessage("Corporate style guideline infringement",
                        "Don't put the announcement title in upper case, no need to shout!",
                        EventMessageType.Error));
                }
            }
        }
    }
}
```

Umbraco V8 introduced the concept of Variants for Document Types, initially to allow different language variants of particular properties within a Document Type to be edited/translated based on the languages configured in your instance of Umbraco.

These variants can be saved, published, and unpublished independently of each other. (Unpublishing a 'mandatory language' variant of a content item - will trigger all culture variants to be unpublished).

This poses a problem when handling notifications from the ContentService - for example which culture got published? Do I want to run my 'custom' code that fires on save if it's only the Spanish version that's been published? Also, if only the Spanish variant is 'unpublished' - that feels like a different situation than if 'all the variants' have been 'unpublished'. Depending on which event you are handling there are helper methods you can call to find out.

When handling the ContentSavingNotification which will be published whenever a variant is saved. You can tell 'which' variant has triggered the save using an extension method on the ContentSavingNotification called 'IsSavingCulture'

As an example, you could check which cultures are being saved (it could be multiple if multiple checkboxes are checked)

With the Saved notification you can similarly use the 'HasSavedCulture' method of the 'ContentSavedNotification' to detect which culture caused the Save.

When handling the Unpublishing notification, it might not work how you would expect. If 'all the variants' are being unpublished at the same time (or the mandatory language is being unpublished, which forces this to occur) then the Unpublishing notification will be published as expected.

However, if only one variant is being unpublished, the Unpublishing event will not be triggered. This is because the content item itself is not fully 'unpublished' by the action. Instead, what occurs is a 'publish' action 'without' the unpublished variant.

You can therefore detect the Unpublishing of a variant in the publishing notification - using the IsUnpublishingCulture extension method of the `ContentPublishingNotification`


Again, the Unpublished notification does not get published when a single variant is Unpublished, instead, the Published notification can be used, and the 'HasUnpublishedCulture' extension method of the ContentPublishedNotification can determine which variant being unpublished triggered the publish.

When handling the ContentPublishingNotification which will be triggered whenever a variant is published (or unpublished - see note in the Unpublishing section above).

You can tell 'which' variant has triggered the publish using a helper method on the ContentPublishingNotification called IsPublishingCulture.

For example, you could check which cultures are being published and act accordingly (it could be multiple if multiple checkboxes are checked).

In the Published notification you can similarly use the HasPublishedCulture and HasUnpublishedCulture methods of the 'ContentPublishedEventArgs' to detect which culture caused the Publish or the UnPublish if it was only a single non-mandatory variant that was unpublished.

In each of these notifications, the entities being Saved, Published, and Unpublished are `IContent`

entities. There are some useful helper methods on IContent to discover the status of the content item's variant cultures:

#### What happened to Creating and Created events?

Both the ContentService.Creating and ContentService.Created events were removed, and therefore never moved to notifications. Why? Because these events were not guaranteed to trigger and therefore should not be used. This is because these events would only trigger when the ContentService.CreateContent method was used which is an entirely optional way to create content entities. It is also possible to construct a new content item - which is generally the preferred and consistent way - and therefore the Creating/Created events would not execute when constructing content that way.

Furthermore, there was no reason to listen to the Creating/Created events. They were misleading since they didn't trigger before and after the entity persisted. They are triggered inside the CreateContent method which never persists the entity, it constructs a new content object.

**What do we use instead?**

The ContentSavingNotification and ContentSavedNotification will always be published before and after an entity has been persisted. You can determine if an entity is brand new in either of those notifications. In the Saving notification - before the entity is persisted - you can check the entity's HasIdentity property which will be 'false' if it is brand new. In the Saved notification you can [check to see if the entity 'remembers being dirty'](/umbraco-cms/reference/notifications/determining-new-entity)

#### What happened to `raiseEvent`

method parameters?

RaiseEvent method service parameters have been removed from v9 and to name some reasons why:

Because it's entirely inconsistent, not all services have this as method parameters and maintaining that consistency is impossible especially if 3rd party libraries support events/notifications.

It's hacky. There's no good way to suppress events/notifications this way at a higher (scoped) level.

There's also hard-coded logic to ignore these parameters sometimes which makes it even more inconsistent.

There are events below services at the repository level that cannot be controlled by this flag.


**What do we use instead?**

We can suppress notifications at the scope level which makes things consistent and will work for all services that use a Scope. Also, there's no required maintenance to make sure that new service methods will also work.

**How to use scopes**:

Create an explicit scope and call scope.Notifications.Suppress().

The result of Suppress() is IDisposable, so until it is disposed, notifications will not be added to the queue.


Child scope will inherit the parent Scope's notification object which means if a parent scope has notifications suppressed, then so does the child scope. You cannot call Suppress() more than once for the same outer scope instance else an exception will be thrown. This ensures that you cannot un-suppress notifications at a child level for an outer scope. It also ensures that suppressing events is an explicit thing to do.

**Why would one want to suppress events?**

The main reason for ever doing this would be performance for bulk operations. The callers should be aware that suppressing events will lead to an inconsistent content cache state (if notifications are suppressed for content or media services). This is because notifications are used by the Published Content Cache to populate the `cmsContentNu`

table and populate the content caches. They are also used to populate the Examine indexes.

So if you did suppress events, it will require you to rebuild the Published Content Cache and examine data manually.

Last updated

Was this helpful?

---

### Creating And Publishing Notifications | CMS

How to create and publish your own custom notifications

There may be many reasons why you would like to create your own custom notifications, in this article we'll use the CleanUpYourRoom [recurring hosted service](/umbraco-cms/reference/scheduling) as an example, which empties the recycle bin every 5 minutes. You might want to publish a notification once the task has started, and maybe once the task has successfully cleared the recycle bin.

For a notification to be publishable there's only one requirement, it must implement the empty marker interface `INotification`

, the rest is up to you. For instance, we might want to create a notification that just signals that the clean your room task has started and nothing else, in this case, we'll create an empty class implementing `INotification`


```
using Umbraco.Cms.Core.Notifications;

namespace Umbraco.Docs.Samples.Web.RecurringBackgroundJobs;

public class CleanYourRoomStartedNotification : INotification
{

}
```

This notification can now be published, and we can create a notification handler to receive it with, see [MediaService-Notifications](/umbraco-cms/reference/notifications/mediaservice-notifications) for an example of how to implement a notification handler. But this notification alone might not be super helpful, we might want to be able to send some additional information with the notification, however, since this is, in essence, just a normal class, we can include whatever information we want. Let's try and create a `RoomCleanedNotification`

which contains the number of nodes removed from the recycle bin:

```
using Umbraco.Cms.Core.Notifications;

namespace Umbraco.Docs.Samples.Web.RecurringBackgroundJobs;

public class RoomCleanedNotification : INotification
{
    public int ItemsDeleted { get; }

    public RoomCleanedNotification(int itemsDeleted)
    {
        ItemsDeleted = itemsDeleted;
    }
}
```

Now you can create a handler that receives the amount of items deleted through the notification.

Just creating the notification classes is not enough, we also want to be able to publish them. There's two ways of publishing notifications:

`IEventAggregator`

- Notifications published with`IEventAggregator`

will always be published immediately.`IScope.Notifications`

- Notifications published with a scope will only be published once the scope has been completed and disposed.

The method you use to publish notifications depends on what your needs are, the benefits of publishing notifications with a scope is that the notification will only be published if you complete the scope, and then only once the scope is disposed of. This can be useful if you access the database, or do some other operation that might fail causing you to do a rollback, disposing of the scope without completing it, in this case, you might not want to publish a notification that signals that the operation was a success, using scopes will handle this for you. On the other hand, you might want to publish the notification immediately no matter what, for instance with the `CleanYourRoomStartedNotification`

, for this, the `IEventAggregator`

is the right choice.

In this case, the `CleanYourRoomStartedNotification`

will always be published immediately, however, `RoomCleanedNotification`

will only be published once the operation is done, and if you remove the `scope.Complete();`

line it will never be published, the recycle bin won't be emptied either.

Last updated

Was this helpful?

---

### Determining if an entity is new | CMS

Example of how to determine if an entity is new

Last updated

Was this helpful?

Example of how to determine if an entity is new

Many of the Umbraco services publishes a 'Saved' notification (or similar). In some cases, it is beneficial to know if this entity is a brand new entity that has been persisted in the database. This is how you can determine this.

Checking if it's new

We know that if an entity is new and hasn't been persisted that it will not have an ID. Therefore we know if an entity has been newly persisted to the database by checking if its ID was changed before being persisted.

Here's the snippet of code that does that:

```
var dirty = (IRememberBeingDirty)entity;
var isNew = dirty.WasPropertyDirty("Id");
```

To check if an entity is new in the ContentSavingNotification use the following:

```
var isNew = entity.HasIdentity is false;
```

Since the IContent has not been saved yet, it's not necessary to cast it to `IRememberBeingDirty`

. It won't have an identity if it's new, since it hasn't been committed yet.

How it works

This is all possible because of the `IRememberBeingDirty`

interface. Indeed the name of this interface is hilarious but it describes exactly what it does. All entities implement this interface which is really handy. It tracks not only the property data that has changed because it inherits from yet another hilarious interface called `ICanBeDirty`

. It also tracks the property data that was changed before it was committed.

Last updated

Was this helpful?

Was this helpful?

---

### Hot vs. cold restarts | CMS

When rebooting an Umbraco CMS website it is common to distinguish between hot and cold restarts depending on your setup.

Hot start

Cold start

Troubleshooting slow startup

In Memory Auto

Legacy Umbraco

[Previous Umbraco Application Lifetime Notifications chevron-left](/umbraco-cms/reference/notifications/umbracoapplicationlifetime-notifications)

[Next Inversion of Control / Dependency injection chevron-right](/umbraco-cms/reference/using-ioc)

Last updated

Was this helpful?

---

### MediaService Notifications Example | CMS

Example of how to use a MediaService Notification

The MediaService class implements IMediaService. It provides access to operations involving IMedia.

Example usage of the MediaService notifications:

```
using Microsoft.Extensions.Logging;
using Umbraco.Cms.Core.Events;
using Umbraco.Cms.Core.Notifications;

namespace MySite;

public class MediaNotificationHandler : INotificationHandler<MediaSavedNotification>
{
    private readonly ILogger<MediaNotificationHandler> _logger;

    public MediaNotificationHandler(ILogger<MediaNotificationHandler> logger)
    {
        _logger = logger;
    }
    
    public void Handle(MediaSavedNotification notification)
    {
        foreach (var mediaItem in notification.SavedEntities)
        {
            if (mediaItem.ContentType.Alias.Equals("Image"))
            {
                // Do something with the image, maybe send to Azure for AI analysis of image contents or something.
                _logger.LogDebug($"Sending {mediaItem.Name} to analysis");
                SendToAzure(mediaItem);
            }
        }
    }
}
```

You can return a custom message to the user. Use this to show information, a warning or maybe an error.
This is achieved using the `Messages`

property of the notification and a composer.

This example returns an informational message to the user when a Media item is saved.

#### What happened to Creating and Created events?

Both the MediaService.Creating and MediaService.Created events have been obsoleted. Because of this, these were not moved over to notifications, and no longer exist. Why? Because these events were not guaranteed to trigger and therefore should not have been used. This is because these events *only* triggered when the MediaService.CreateMedia method was used which is an entirely optional way to create media entities. It is also possible to construct a new media item - which is generally the preferred and consistent way - and therefore the Creating/Created events would not execute when constructing media that way.

Furthermore, there was no reason to listen for the Creating/Created events because they were misleading. They didn't trigger before and after the entity had been persisted. Instead they triggered inside the CreateMedia method which never persists the entity. It constructs a new media object.

**What do we use instead?**

The MediaSavingNotification and MediaSavedNotification will always be published before and after an entity has been persisted. You can determine if an entity is brand new with either of those notifications. With the Saving notification - before the entity is persisted - you can check the entity's HasIdentity property which will be 'false' if it is brand new. In the Saved event you can [check to see if the entity 'remembers being dirty'](/umbraco-cms/reference/notifications/determining-new-entity)

#### What happened to `raiseEvent`

method parameters?

RaiseEvent method service parameters have been removed from v9 and to name some reasons why:

Because it's entirely inconsistent, not all services have this as method parameters and maintaining that consistency is impossible especially if 3rd party libraries support events/notifications.

It's hacky. There's no good way to suppress events/notifications this way at a higher (scoped) level.

There's also hard-coded logic to ignore these parameters sometimes which makes it even more inconsistent.

There are events below services at the repository level that cannot be controlled by this flag.


**What do we use instead?**

We can suppress notifications at the scope level which makes things consistent and will work for all services that use a Scope. Also, there's no required maintenance to make sure that new service methods will also work.

**How to use scopes**:

Create an explicit scope and call scope.Notifications.Suppress().

The result of Suppress() is IDisposable, so until it is disposed, notifications will not be added to the queue.


Child scope will inherit the parent Scope's notification object which means if a parent scope has notifications suppressed, then so does the child scope. You cannot call Suppress() more than once for the same outer scope instance else an exception will be thrown. This ensures that you cannot un-suppress notifications at a child level for an outer scope. It also ensures that suppressing events is an explicit thing to do.

**Why would one want to suppress events?**

The main reason for ever doing this would be performance for bulk operations. The callers should be aware that suppressing events will lead to an inconsistent content cache state (if notifications are suppressed for content or media services). This is because notifications are used by the Published Content Cache to populate the `cmsContentNu`

table and populate the content caches. They are also used to populate the Examine indexes.

So if you did suppress events, it will require you to rebuild the Published Content Cache and examine data manually.

Last updated

Was this helpful?

---

### MemberService Notifications Example | CMS

Example of how to use a MemberService Notification

The MemberService implements IMemberService and provides access to operations involving IMember.

```
using Microsoft.Extensions.Logging;
using Umbraco.Cms.Core.Events;
using Umbraco.Cms.Core.Notifications;

namespace MySite;

public class MemberNotificationHandler : INotificationHandler<MemberSavedNotification>
{
    private readonly ILogger<MemberNotificationHandler> _logger;

    public MemberNotificationHandler(ILogger<MemberNotificationHandler> logger)
    {
        _logger = logger;
    }
    
    public void Handle(MemberSavedNotification notification)
    {
        foreach (var member in notification.SavedEntities)
        {
            // Write to the logs every time a member is saved.
            _logger.LogInformation("Member {member} has been saved and notification published!", member.Name);
        }
    }
}
```

#### What happened to `raiseEvent`

method parameters?

RaiseEvent method service parameters have been removed from v9 and to name some reasons why:

Because it's entirely inconsistent, not all services have this as method parameters and maintaining that consistency is impossible especially if 3rd party libraries support events/notifications.

It's hacky. There's no good way to suppress events/notifications this way at a higher (scoped) level.

There's also hard-coded logic to ignore these parameters sometimes which makes it even more inconsistent.

There are events below services at the repository level that cannot be controlled by this flag.


**What do we use instead?**

We can suppress notifications at the scope level which makes things consistent and will work for all services that use a Scope. Also, there's no required maintenance to make sure that new service methods will also work.

**How to use scopes**:

Create an explicit scope and call scope.Notifications.Suppress().

The result of Suppress() is IDisposable, so until it is disposed, notifications will not be added to the queue.


Child scope will inherit the parent Scope's notification object which means if a parent scope has notifications suppressed, then so does the child scope. You cannot call Suppress() more than once for the same outer scope instance else an exception will be thrown. This ensures that you cannot un-suppress notifications at a child level for an outer scope. It also ensures that suppressing events is an explicit thing to do.

**Why would one want to suppress events?**

The main reason for ever doing this would be performance for bulk operations. The callers should be aware that suppressing events will lead to an inconsistent content cache state (if notifications are suppressed for content or media services). This is because notifications are used by the Published Content Cache to populate the `cmsContentNu`

table and populate the content caches. They are also used to populate the Examine indexes.

So if you did suppress events, it will require you to rebuild the Published Content Cache and examine data manually.

[Previous MediaService Notifications Example chevron-left](/umbraco-cms/reference/notifications/mediaservice-notifications)

[Next Umbraco Application Lifetime Notifications chevron-right](/umbraco-cms/reference/notifications/umbracoapplicationlifetime-notifications)

Last updated

Was this helpful?

---

### Notification Handler | CMS

Learn about notification handlers lifetime, async notification handler and how to register the notification handlers.

```
public void Handle(TemplateSavingNotification notification)
{
 notification.State["SomeKey"] = "Some Value Relevant to the \"after\" notification handler";
}


public void Handle(TemplateSavedNotification notification)
{
  var valueFromSaving = notification.State["SomeKey"];
}
```

Registering notification handlers

Registering notification handlers in the program class

Registering notification handlers in a composer

Async Notification Handler

Notification handler

Notification registration

Last updated

Was this helpful?

---

### Umbraco Application Lifetime Notifications | CMS

Represents an Umbraco application lifetime (starting, started, stopping, stopped) notification

Last updated

Was this helpful?

Represents an Umbraco application lifetime (starting, started, stopping, stopped) notification

Umbraco application lifetime notifications are published for the starting, started, stopping, and stopped events of the Umbraco runtime. These events implement the `IUmbracoApplicationLifetimeNotification`

interface that contains a single `IsRestarting`

property.

An Umbraco application is restarted after an install or upgrade has been completed. You can use this property to prevent running code twice: on initial boot and restart. To prevent running code when the application is in the install or upgrade state, inject an `IRuntimeState`

instance in your notification and inspect the `Level`

property instead.

Usage

Example usage of the UmbracoApplicationLifetime notifications:

```
using Microsoft.Extensions.Logging;
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.Events;
using Umbraco.Cms.Core.DependencyInjection;
using Umbraco.Cms.Core.Notifications;

public class UmbracoApplicationNotificationComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.AddNotificationHandler<UmbracoApplicationStartingNotification, UmbracoApplicationNotificationHandler>();
        builder.AddNotificationHandler<UmbracoApplicationStartedNotification, UmbracoApplicationNotificationHandler>();
        builder.AddNotificationHandler<UmbracoApplicationStoppingNotification, UmbracoApplicationNotificationHandler>();
        builder.AddNotificationHandler<UmbracoApplicationStoppedNotification, UmbracoApplicationNotificationHandler>();
    }
}

public class UmbracoApplicationNotificationHandler : INotificationHandler<UmbracoApplicationStartingNotification>, INotificationHandler<UmbracoApplicationStartedNotification>, INotificationHandler<UmbracoApplicationStoppingNotification>, INotificationHandler<UmbracoApplicationStoppedNotification>
{
    private readonly ILogger _logger;

    public UmbracoApplicationNotificationHandler(ILogger<UmbracoApplicationNotificationHandler> logger) => _logger = logger;

    public void Handle(UmbracoApplicationStartingNotification notification) => Log(notification, notification.IsRestarting);

    public void Handle(UmbracoApplicationStartedNotification notification) => Log(notification, notification.IsRestarting);

    public void Handle(UmbracoApplicationStoppingNotification notification) => Log(notification, notification.IsRestarting);

    public void Handle(UmbracoApplicationStoppedNotification notification) => Log(notification, notification.IsRestarting);

    private void Log(INotification notification, bool isRestarting) => _logger.LogInformation("{Type} - {IsRestarting}", notification.GetType().Name, isRestarting);
}
```

Last updated

Was this helpful?

Was this helpful?

---

---


## Plugins

### Contents

- [Creating Resolvers | CMS](#creating-resolvers-cms)
- [Finding types | CMS](#finding-types-cms)

---

### Creating Resolvers | CMS

*A Resolver should be created for any plugin type. Resolvers are the standard way to retrieve/create/register plugin types.*

As an example, we'll create a resolver to resolve an application error logger:

```
/// <summary>
/// An object resolver to return the IErrorLogger
/// </summary>
public class ErrorLoggerResolver : SingleObjectResolverBase<ErrorLoggerResolver, IErrorLogger>
{
    internal ContentStoreResolver(IErrorLogger errorLogger)
        : base(errorLogger)
    {
    }

    /// <summary>
    /// Can be used by developers at runtime to set their IErrorLogger at app startup
    /// </summary>
    /// <param name="contentStore"></param>
    public void SetErrorLogger(IErrorLogger errorLogger)
    {
        Value = errorLogger;
    }

    /// <summary>
    /// Returns the IErrorLogger
    /// </summary>
    public IErrorLogger ErrorLogger
    {
        get { return Value; }
    }
}
```

All you need to do is inherit from `Umbraco.Core.ObjectResolution.SingleObjectResolverBase<TResolver, TResolved>`

and then add whatever constructors, properties and methods you would like to expose.

In the example above we have a constructor that accepts a default `IErrorLogger`

. Normally in Umbraco this resolver will be constructed in a `IBootManager`

with a default object. The we expose a method to allow developers to change to a custom `IErrorLogger`

at runtime called `SetErrorLogger`

. Then we create a property to expose the `IErrorLogger`

called ErrorLogger.

Example:

Creating a multiple object resolver is similar. As an example we'll create a LanguageConvertersResolver.

The naming convention for multiple objects resolvers are plural: We've named this LanguageConverter**s**Resolver with a pluralized 'Converters' to denote that this resolver returns multiple objects

When creating a multiple object resolver you need to decide what lifetime scope the objects created and returned will have which is defined in the constructor created. The default constructor of the `ManyObjectsResolverBase`

specifies that the objects created will have an Application based lifetime scope which means the objects will be singletons only one instance of each one will exist for the lifetime of the application. There are 3 lifetime scopes that can be specified:

ObjectLifetimeScope.Application

One instance of each object will be created for the entire lifetime of the application (singleton)


ObjectLifetimeScope.Transient

A new instance of each object will be created each time the 'Values' collection is accessed


ObjectLifetimeScope.HttpRequest

One instance of each object will be created for the lifetime of the current http request



Last updated

Was this helpful?

---

### Finding types | CMS

*Whenever types need to be found in assemblies in order to add them to resolvers, the PluginManager should be used. The TypeFinder should never be used directly in any code except for in PluginManager extension methods or in the PluginManager itself.*

The `Umbraco.Core.PluginManager`

class is responsible for finding and caching all plugin types. It is also responsible for instantiating these types. It contains 4 important methods:

`IEnumerable<Type> ResolveTypes<T>()`

Generic method to find the specified type and cache the result


`IEnumerable<Type> ResolveTypesWithAttribute<T, TAttribute>()`

Generic method to find the specified type that has an attribute and cache the result


`IEnumerable<Type> ResolveAttributedTypes<TAttribute>()`

Generic method to find any type that has the specified attribute and cache the result


`T CreateInstance<T>(Type type, bool throwException = false)`

Used to create an instance of the specified type based on the resolved/cached plugin types



It is definitely possible to use the methods above to find types in your code but this is not recommended practice. It is recommended to create extension methods for the PluginManager named accordingly to find specific types. For example:

```
PluginManager.Current.ResolveTrees();
```

The code for this method is as follows:

The code calls the PluginManager's ResolveTypes method but this method is human readable and distinguishable.

Last updated

Was this helpful?

---

---


## Property Editor UIs | CMS

Learn about the different Property Editor UI elements that ship with Umbraco out of the box.

This document provides a comprehensive list of all Property Editor UI elements registered via manifests (`propertyEditorUi`

) available in Umbraco CMS. These elements define the user interface components for property editors used throughout the system.

Property Editor UI manifests define how property editors appear and behave in the Umbraco backoffice. Each manifest includes properties like alias, label, icon, group, and configuration settings.

**Alias:**`Umb.PropertyEditorUi.TextBox`

**Icon:**`icon-autofill`

**Group:**`common`

**Schema:**`Umbraco.TextBox`

**Read-only Support:**✅**Location:**`/packages/property-editors/text-box/manifests.ts`

**Settings:**`inputType`

- Configure input type (text, email, URL, and so on)


**Alias:**`Umb.PropertyEditorUi.EmailAddress`

**Icon:**`icon-message`

**Group:**`common`

**Schema:**`Umbraco.EmailAddress`

**Read-only Support:**✅**Location:**`/packages/property-editors/text-box/manifests.ts`

**Settings:**`inputType`

- Input type configuration


**Alias:**`Umb.PropertyEditorUi.TextArea`

**Icon:**`icon-edit`

**Group:**`common`

**Schema:**`Umbraco.TextArea`

**Read-only Support:**✅**Location:**`/packages/property-editors/textarea/manifests.ts`

**Settings:**`rows`

- Number of rows to display


**Alias:**`Umb.PropertyEditorUi.Toggle`

**Icon:**`icon-checkbox`

**Group:**`common`

**Schema:**`Umbraco.TrueFalse`

**Read-only Support:**✅**Location:**`/packages/property-editors/toggle/manifests.ts`

**Settings:**`default`

- Preset value`showLabels`

- Show on/off labels`labelOn`

- Custom "on" label`labelOff`

- Custom "off" label`ariaLabel`

- Screen reader label


**Alias:**`Umb.PropertyEditorUi.Integer`

**Icon:**`icon-autofill`

**Group:**`common`

**Schema:**`Umbraco.Integer`

**Read-only Support:**✅**Location:**`/packages/property-editors/number/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.Decimal`

**Icon:**`icon-autofill`

**Group:**`common`

**Schema:**`Umbraco.Decimal`

**Read-only Support:**✅**Location:**`/packages/property-editors/number/manifests.ts`

**Settings:**`placeholder`

- Placeholder text


**Alias:**`Umb.PropertyEditorUi.Slider`

**Icon:**`icon-navigation-horizontal`

**Group:**`common`

**Schema:**`Umbraco.Slider`

**Read-only Support:**✅**Location:**`/packages/property-editors/slider/manifests.ts`

**Settings:**`enableRange`

- Enable range selection`initVal1`

- Initial value`initVal2`

- Second initial value (for range)`step`

- Step increments


**Alias:**`Umb.PropertyEditorUi.DatePicker`

**Icon:**`icon-time`

**Group:**`pickers`

**Schema:**`Umbraco.DateTime`

**Read-only Support:**✅**Location:**`/packages/property-editors/date-picker/manifests.ts`

**Settings:**`format`

- Date format string


**Alias:**`Umb.PropertyEditorUi.ColorPicker`

**Icon:**`icon-colorpicker`

**Group:**`pickers`

**Schema:**`Umbraco.ColorPicker`

**Read-only Support:**✅**Location:**`/packages/property-editors/color-picker/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.EyeDropper`

**Icon:**`icon-colorpicker`

**Group:**`pickers`

**Schema:**`Umbraco.ColorPicker.EyeDropper`

**Location:**`/packages/property-editors/eye-dropper/manifests.ts`

**Settings:**`showAlpha`

- Show alpha channel`showPalette`

- Show color palette


**Alias:**`Umb.PropertyEditorUi.Dropdown`

**Icon:**`icon-list`

**Group:**`lists`

**Schema:**`Umbraco.DropDown.Flexible`

**Read-only Support:**✅**Location:**`/packages/property-editors/dropdown/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.Select`

**Icon:**`icon-list`

**Group:**`pickers`

**Location:**`/packages/property-editors/select/manifests.ts`

**Settings:**`items`

- Add selectable options


**Alias:**`Umb.PropertyEditorUi.RadioButtonList`

**Icon:**`icon-target`

**Group:**`lists`

**Schema:**`Umbraco.RadioButtonList`

**Read-only Support:**✅**Location:**`/packages/property-editors/radio-button-list/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.CheckBoxList`

**Icon:**`icon-bulleted-list`

**Group:**`lists`

**Schema:**`Umbraco.CheckBoxList`

**Read-only Support:**✅**Location:**`/packages/property-editors/checkbox-list/manifests.ts`

**Settings:**`items`

- Add checkbox options


**Alias:**`Umb.PropertyEditorUi.MultipleTextString`

**Icon:**`icon-ordered-list`

**Group:**`lists`

**Schema:**`Umbraco.MultipleTextString`

**Read-only Support:**✅**Location:**`/packages/property-editors/multiple-text-string/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.ContentPicker`

**Icon:**`icon-page-add`

**Group:**`pickers`

**Schema:**`Umbraco.MultiNodeTreePicker`

**Read-only Support:**✅**Location:**`/packages/property-editors/content-picker/manifests.ts`

**Settings:**`filter`

- Filter by content type


**Alias:**`Umb.PropertyEditorUi.DocumentPicker`

**Icon:**`icon-document`

**Group:**`pickers`

**Schema:**`Umbraco.ContentPicker`

**Read-only Support:**✅**Location:**`/packages/documents/documents/property-editors/document-picker/manifests.ts`

**Settings:**`startNodeId`

- Set start node


**Alias:**`Umb.PropertyEditorUi.MultiUrlPicker`

**Icon:**`icon-link`

**Group:**`pickers`

**Schema:**`Umbraco.MultiUrlPicker`

**Read-only Support:**✅**Location:**`/packages/multi-url-picker/property-editor/manifests.ts`

**Settings:**`overlaySize`

- Overlay size`hideAnchor`

- Hide anchor/query string input


**Alias:**`Umb.PropertyEditorUi.MediaPicker`

**Icon:**`icon-picture`

**Group:**`media`

**Schema:**`Umbraco.MediaPicker3`

**Read-only Support:**✅**Location:**`/packages/media/media/property-editors/media-picker/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.UploadField`

**Icon:**`icon-download-alt`

**Group:**`media`

**Schema:**`Umbraco.UploadField`

**Location:**`/packages/media/media/property-editors/upload-field/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.ImageCropper`

**Icon:**`icon-crop`

**Group:**`media`

**Schema:**`Umbraco.ImageCropper`

**Location:**`/packages/media/media/property-editors/image-cropper/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.Tiptap`

**Icon:**`icon-browser-window`

**Group:**`richContent`

**Schema:**`Umbraco.RichText`

**Location:**`/packages/tiptap/property-editors/tiptap/manifests.ts`

**Settings:**`extensions`

- Extensions configuration`toolbar`

- Toolbar configuration`stylesheets`

- Stylesheet selection`dimensions`

- Editor dimensions`maxImageSize`

- Maximum image size`overlaySize`

- Overlay size


**Alias:**`Umb.PropertyEditorUi.MarkdownEditor`

**Icon:**`icon-code`

**Group:**`richContent`

**Schema:**`Umbraco.MarkdownEditor`

**Read-only Support:**✅**Location:**`/packages/markdown-editor/property-editors/markdown-editor/manifests.ts`

**Settings:**`preview`

- Enable preview`defaultValue`

- Default value`overlaySize`

- Overlay size


**Alias:**`Umb.PropertyEditorUi.CodeEditor`

**Icon:**`icon-brackets`

**Group:**`richContent`

**Schema:**`Umbraco.Plain.String`

**Location:**`/packages/code-editor/property-editor/manifests.ts`

**Settings:**`language`

- Programming language`height`

- Editor height`lineNumbers`

- Show line numbers`minimap`

- Show minimap`wordWrap`

- Enable word wrap


**Alias:**`Umb.PropertyEditorUi.BlockList`

**Icon:**`icon-thumbnail-list`

**Group:**`lists`

**Schema:**`Umbraco.BlockList`

**Read-only Support:**✅**Location:**`/packages/block/block-list/property-editors/block-list-editor/manifests.ts`

**Settings:**`useSingleBlockMode`

- Single block mode`useLiveEditing`

- Live editing mode`useInlineEditingAsDefault`

- Inline editing as default`maxPropertyWidth`

- Maximum property width


**Alias:**`Umb.PropertyEditorUi.BlockGrid`

**Icon:**`icon-layout`

**Group:**`richContent`

**Schema:**`Umbraco.BlockGrid`

**Read-only Support:**✅**Location:**`/packages/block/block-grid/property-editors/block-grid-editor/manifests.ts`

**Settings:**`blockGroups`

- Block groups configuration`useLiveEditing`

- Live editing mode`maxPropertyWidth`

- Editor width`createLabel`

- Create button label`gridColumns`

- Number of grid columns`layoutStylesheet`

- Layout stylesheet


**Alias:**`Umb.PropertyEditorUi.UserPicker`

**Icon:**`icon-user`

**Group:**`people`

**Schema:**`Umbraco.UserPicker`

**Location:**`/packages/user/user/property-editor/user-picker/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.MemberPicker`

**Icon:**`icon-user`

**Group:**`people`

**Schema:**`Umbraco.MemberPicker`

**Read-only Support:**✅**Location:**`/packages/members/member/property-editor/member-picker/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.MemberGroupPicker`

**Icon:**`icon-users-alt`

**Group:**`people`

**Schema:**`Umbraco.MemberGroupPicker`

**Read-only Support:**✅**Location:**`/packages/members/member-group/property-editor/member-group-picker/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.Tags`

**Icon:**`icon-tags`

**Group:**`common`

**Schema:**`Umbraco.Tags`

**Read-only Support:**✅**Location:**`/packages/tags/property-editors/tags/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.Label`

**Icon:**`icon-readonly`

**Group:**`common`

**Schema:**`Umbraco.Label`

**Read-only Support:**✅**Location:**`/packages/property-editors/label/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.IconPicker`

**Icon:**`icon-autofill`

**Group:**`common`

**Location:**`/packages/property-editors/icon-picker/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.Collection`

**Icon:**`icon-layers`

**Group:**`lists`

**Schema:**`Umbraco.ListView`

**Location:**`/packages/property-editors/collection/manifests.ts`

**Settings:**`layouts`

- Layout configuration`orderBy`

- Order by field`orderDirection`

- Order direction`pageSize`

- Page size`icon`

- Workspace view icon`tabName`

- Workspace view name`showContentFirst`

- Show content workspace view first


These property editors are used for configuring other property editors and don't typically have schema aliases:

**Alias:**`Umb.PropertyEditorUi.StylesheetPicker`

**Location:**`/packages/templating/stylesheets/property-editors/stylesheet-picker/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.StaticFilePicker`

**Location:**`/packages/static-file/property-editors/static-file-picker/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.MediaTypePicker`

**Location:**`/packages/media/media-types/property-editors/media-type-picker/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.DocumentTypePicker`

**Location:**`/packages/documents/document-types/property-editors/document-type-picker/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.ValueType`

**Location:**`/packages/property-editors/value-type/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.OverlaySize`

**Location:**`/packages/property-editors/overlay-size/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.OrderDirection`

**Location:**`/packages/property-editors/order-direction/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.NumberRange`

**Location:**`/packages/property-editors/number-range/manifests.ts`


**Alias:**`Umb.PropertyEditorUi.ColorSwatchesEditor`

**Location:**`/packages/property-editors/color-swatches-editor/manifests.ts`


Property editors are organized into the following groups:

`common`

- Basic, frequently-used editors`lists`

- Editors for managing lists and collections`pickers`

- Editors for selecting/picking items`media`

- Media-related editors`richContent`

- Rich text and content editors`people`

- User and member pickers

Each property editor UI manifest follows this structure:

Property Editor UIs are referenced when creating data types through their alias. For example:

Use

`Umb.PropertyEditorUi.TextBox`

for a text input fieldUse

`Umb.PropertyEditorUi.MediaPicker`

for media selectionUse

`Umb.PropertyEditorUi.BlockGrid`

for complex grid layouts

**Read-only Support:**Property editors marked with ✅ support read-only mode**Location:**File paths are relative to`/src/Umbraco.Web.UI.Client/src/`

**Settings:**Most property editors can be configured through their settings properties**Schema Alias:**Links the UI to the underlying data schema/value converter

Last updated

Was this helpful?

---
