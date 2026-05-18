# Repositories | CMS

Repositories provide a structured way to manage data operations in the Backoffice. They abstract the data access layer, allowing for easier reuse and scalability.

Repositories create separation between domain logic and data access. By providing a known interface for data requests, we can reuse UI components across different domains. For example, we have a generic UX flow for deleting an entity. By supplying this flow with a repository that has a known interface for deletion, we can use the same UX flow to delete any entity. The same applies to Trees, Collections, Workspaces, and more.

Additionally, repositories can utilize different data sources depending on the application's state. These sources may include:

A REST API

Offline storage

A local cache

And more.


This abstraction ensures that consumers don’t need to worry about how to access data. The repository serves as the Backoffice’s entry point for requesting new data. As a result, we achieve a loosely coupled connection between consumers and data storage procedures, effectively hiding complex implementations.

**Repository:**defines what data operations are available (get, add, update, delete).**Data Source:**defines how data is fetched or stored.

A repository must be instantiated where it is used. It should take an [UmbController](/umbraco-cms/customizing/foundation/umbraco-controller) as part of the constructor. This ensures that any contexts consumed in the repository are scoped correctly.

A repository can be initialized directly from an element, but will often be instantiated in a [context](/umbraco-cms/customizing/foundation/context-api), like the Workspace Context.

The data flow when using a repository can be illustrated as follows:

```
(Data Source) -> Repository -> (Controller/Context) -> Element
```

Often, you will find that data is already available and observable in a [context](/umbraco-cms/customizing/contexts). In that case, subscribing to the context [state](/umbraco-cms/customizing/foundation/states) will be the right approach to take. This way, you will receive all runtime updates that occur to the data throughout the session.

If the needed data isn’t available in a context, use a repository to request the data. This will give you the correct data no matter the current application state.

In the example below, we instantiate the `UmbDocumentItemRepository`

directly in a custom element to request Document Item data by its unique key.

Alternatively, you can instantiate the repository in a [controller](/umbraco-cms/customizing/foundation/umbraco-controller) or [context](/umbraco-cms/customizing/foundation/context-api), store the data in a [state](/umbraco-cms/customizing/foundation/states), and then observe that state in your element. This is often the preferred approach as it allows for better separation of concerns and reusability across different components.

By registering your repository in the [Extension Registry](/umbraco-cms/customizing/extending-overview/extension-registry), you make it available to use in different extension kinds that require a repository alias.

Some of the common repository interfaces are:

[UmbDetailRepository](/umbraco-cms/customizing/foundation/repositories/repository-types/detail-repository)- for detail views of a single entity.[UmbCollectionRepository](/umbraco-cms/customizing/foundation/repositories/repository-types/collection-repository)- for collection views of multiple entities.UmbTreeRepository - for tree structures of entities.

[UmbItemRepository](/umbraco-cms/customizing/foundation/repositories/repository-types/item-repository)- for item requests.

See the example below of how to register a custom repository:

Last updated

Was this helpful?

## Repository Types

## Contents

- [Collection Repository | CMS](#collection-repository-cms)
- [Detail Repository | CMS](#detail-repository-cms)
- [Item Repository | CMS](#item-repository-cms)

---

## Collection Repository | CMS

```
interface UmbCollectionRepository {
  requestCollection();
}
```

Last updated

Was this helpful?

A collection repository is a specific type of repository designed to handle operations related to collections of items. It provides methods to request collections of data in a filtered and paginated manner.

The interface below is simplified for clarity and omits return types and arguments. See full interfaces in the .

```
interface UmbCollectionRepository {
  requestCollection();
}
```

Last updated

Was this helpful?

Was this helpful?

---

## Detail Repository | CMS

```
interface UmbDetailRepository {
  createScaffold();
  create();
  requestByUnique();
  save();
  delete();
}
```

Last updated

Was this helpful?

A detail repository is a specific type of repository designed to handle operations related to individual entities. It provides methods to create, retrieve, update, and delete single entities.

The interface below is simplified for clarity and omits return types and arguments. See full interfaces in the .

```
interface UmbDetailRepository {
  createScaffold();
  create();
  requestByUnique();
  save();
  delete();
}
```

Last updated

Was this helpful?

Was this helpful?

---

## Item Repository | CMS

```
interface UmbItemRepository {
  requestItems();
}
```

Last updated

Was this helpful?

An item repository is a specific type of repository designed to handle operations related to multiple individual items. It provides methods to request multiple items based on unique identifiers.

The interface below is simplified for clarity and omits return types and arguments. See full interfaces in the .

```
interface UmbItemRepository {
  requestItems();
}
```

Last updated

Was this helpful?

Was this helpful?

---
