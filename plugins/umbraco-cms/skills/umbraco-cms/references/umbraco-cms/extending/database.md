# Creating a Custom Database Table | CMS

A guide to creating a custom Database table in Umbraco

Umbraco ships with , which enables mapping the results of database queries to Common Language Runtime (CLR) objects. NPoco allows custom database tables to be added to your site to store additional data that should not be stored as normal content nodes.

The end result looks like this:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f5bae6652167e776ebfde12d72396efb7b3569e5%252Fdb-table%2520%281%29.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=21eed915&sv=2)

The following code sample shows how this is done using a composer and component.

When migrating from version 8 there are a few changes to be aware of. The first change is that namespace updates are dependencies that need to be passed to the `Upgrader.Execute()`

method. Another is a change to the access modifier of the `Migrate()`

method.

If building a new solution, you can adopt a new pattern. With this pattern you create and run a similar migration but trigger it in response to a [notification handler](/umbraco-cms/fundamentals/code/subscribing-to-notifications).

The code for this approach is as follows:

The notification handler can be registered in a composer:

In short, it's up to you. If you are migrating from version 8 and want the quickest route to getting running with the latest version, then using a component makes sense.

You will be using the notification pattern elsewhere. This could be when responding to Umbraco events that run many times in the lifetime of the application, like when content is saved. And so you may also prefer to align with that pattern for start-up events.

It is also worth noting that components offer both `Initialize`

and `Terminate`

methods. With these you will need to handle two notifications to do the same with the notification handler approach (`UmbracoApplicationStartingNotification`

and `UmbracoApplicationStoppingNotification`

). A single handler class can be used for both notifications though.

**Important!** The `BlogCommentSchema`

class nested inside the migration is purely used as a database schema representation class. It should not be used as a Data Transfer Object (DTO) to access the table data. Equally, you shouldn't use your DTO classes to define the schema used by your migration. Instead, you should create a duplicate snapshot for the purpose of creating or working with your database tables in the current migration. The name of the class is not important as you will be overriding it using the TableName attribute. You should choose a name that makes it clear that this class is purely for defining the schema in this migration.

Whilst this adds a level of duplication, it is important that migrations and the code/classes within a migration remain immutable. If the DTO was to be used for both, it could cause unexpected behaviour. Should you later modify your DTO used in your application but you have previous migrations expecting the DTO to be in its unmodified state.

Once a snapshot has been created, and once your code has been deployed, the snapshot should never be changed directly. Instead, you should use further migrations to alter the database table into the state you require. This ensures that migrations can be run in sequence and that each migration can expect the database to be in a known state before executing.

When adding further migrations and if you need to reuse the schema class, it is a good idea to duplicate this in those particular migrations. You want the migrations to be immutable. Having separate classes in separate namespaces, reduces the risk of modifying a schema class from your initial migration.

When storing data in custom database tables, this is by default not manageable by Umbraco at all. This can be great for many purposes such as storing massive amounts of data that you do not need to edit from the backoffice. Decoupling part of your data from being managed by Umbraco as content can be a way of achieving better performance for your site. It will no longer take up space in indexes and caches, and the Umbraco database.

This also means that if you do need to edit or display this data, you need to implement the underlying functionality to support this. The same if the case if you need this data to be transferred or kept synchronized between multiple sites or environments. Data stored in custom tables are not supported by default by add-ons such as Umbraco Deploy and will not be deployable by default.

Figuring out how to manage data across multiple environments can be different between individual sites and there is not one solution that fits all. Some sites may have automated database synchronization set up to ensure specific tables in multiple databases are always kept in sync. Other sites may be better off with scripts moving data around manually on demand.

To create, read, update or delete data from your custom database tables, you can use the `IScopeProvider`

to get access to the database operations.

The following example creates a `Controller`

that uses `[Route]`

annotations to create API endpoints for fetching and inserting blog comments.

This example does not use the aforementioned `BlogCommentSchema`

class but rather a separate (yet duplicate) class that is not part of the example. Also, be aware that things like error handling and data validation have been omitted for brevity.

Last updated

Was this helpful?