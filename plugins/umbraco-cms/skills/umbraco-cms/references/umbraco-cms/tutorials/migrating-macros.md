# Migrating Macros | CMS

Get started with developing a custom migration path for Macros to Blocks in the Rich Text Editors (RTE).

There are a multitude of options for migrating away from macros to use blocks in the Rich Text Editor instead. This article showcases a solution that lets you scan and then fix each macro one by one (or in batches).

This tutorial serves primarily as inspiration for how to migrate the macros in your Umbraco website.

The code supplied should not be used in a production environment without proper testing. It can however be used to kickstart your custom solution.

At the end of the article a few [other ways of running a larger migration is explained](/umbraco-cms/tutorials/migrating-macros#alternative-approaches).

Through the following tutorial, a macro will be converted one-to-one to a block. Each macro parameter will match the same named property on an Element Type. Text strings will be used as values.

If your migration deals with complex types, it's advised to create instances of the new data format and compare the old and new values. There might be more differences between the Parameter Type on the macro and the Property Editor/Data Type on the Element Type.

**Upgrading from Umbraco 13**

As most people will be dealing with this migration when upgrading from Umbraco 13, that will be including in this tutorial. Specifically from 13.7.2 to 15.2.3.

This will also work when migrating directly from 13 to 17.

The following covers how to configure a macro.

You need to:

Define a macro and its parameters.


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-86ef8da0b41fa5a690e08cab672d483d84a67eb1%252Fmacro-settings.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7207c9a9&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-83b0d4840d95cdcdd2c8d5299404f3594cfc5b1a%252Fmacro-parameters.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9794a23d&sv=2)

Have a macro partial view that is used to render the macro on the website. It is also used in the backoffice rendering if enabled in the macro settings.


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-15fc33b62c17fd04762481b149f4e464d690e8d2%252Fmacro-backoffice.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=413cbd4a&sv=2)

Enable the Richtext Editor (TinyMce) to allow the insertion of macros.


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d06bd3a49feaab121b0b7f5c8ed10dc8e87b6b84%252Fmacro-tinymce.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c85ae0cf&sv=2)

Below you can find the relevant items used in our example:

The block setup is similar but with a few changes:

Switch the property editor of the Richtext Data Type from TinyMce to Tiptap.


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b5c902118d037292b2bd28baebd613c18646fddc%252Frte-tiptap.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=58321774&sv=2)

Set up an Element Type with the same properties as the macro parameters.


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-c83e4e101663398f70113f90efa458c217a8a854%252Fblock-definition.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fb0cc223&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-01518c0b874bbbbc3dfcaf7edc0fd53f98c10f46%252Fblock-backoffice.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=96b583c1&sv=2)

Allow the Tiptap editor to insert blocks and configure the newly created block to be one of the options.


![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-a3fbe6a044dc552a911019b1c76bc4106160f9b5%252Ftiptap-blocks.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3eaf9891&sv=2)

Transform the macro view into a web component for the backoffice custom view.


Register the web component.


Transform the macro view in to a Richtext block view.


However you retrieve the relevant data you have with a raw string or a `RichTextEditorValue`

that you need to convert. The following looks at a sample value.

The value holds JSON with:

Empty block information.

The markup with the actual RTE value and the inline macro data.

The macro consists off:

The tag used as a placeholder where to render its output.

An alias to find the correct render/update logic.

Two parameters with values entered by the user.



The first step in transforming the data is taking the JSON value and deserializing it into a `RichTextEditorValue`

. This way you have a class to work with to store the updated data in.

You can deserialize it yourself, or you can use the `RichTextPropertyEditorHelper`

to do the job for you. It will also try to catch non-JSON values that have not been migrated to the new format.

The next step is to get all (relevant) macro tags out of the markup. One way of doing this is through a regular expression.

The sample regex does not take into account that the order of parameters, which might be different from tag to tag. One way of dealing with this is to not take out the parameters in the first match. Instead move each parameter to a separate regex that runs on the first match.

Every macro conversion will be different based on which parameters get matched to which properties on the block. As such it is advised to create a converter per macro that deals with the specific data handling.

Now that the relevant information has been extracted, it's time to decide what the data should look like.

Note that:

The markup still contains a tag placeholder but this time with only the

`data-content-key`

.That key references an item inside the blocks

`contentData`

that holds the values of the properties and a reference to the Element Type set up earlier.The same key is added to the

`expose`

collection and the Rich text`layout`

collection.This means that if you have multiple blocks in the same value, more

`contentData`

items will be added in the blocks collection. They will be referenced in the`expose and`

Layout accordingly.

The example below shows the full handling of an invariant macro to an invariant block.

This migrator starts and ends with a raw (serialized) string. If you choose a different path, you might have to change the code to work with the supplied value types instead.

In this setup, the values are received straight from the database using custom Data Transfer Objects (DTOs). This allows for getting get the data needed. This example does not take nested data into account. For an example on how to to do this, [check out one of the alternatives](/umbraco-cms/tutorials/migrating-macros#alternative-approaches) at the bottom of this article.

This example also only fetches the active (draft/current) version of the affected data to reduce processing time.

Once the data is transformed it needs to be stored. Custom SQL is used to perform this.

If you need to perform validation on the updated value, you either have to use a higher level services (`IContentValidationService`

/`IContentEditingService`

) or use the `RichTextPropertyValueEditor.Validate()`

method. Because this example fetches the current data and overwrites it, the old value will not show up in the version history of the affected node. If you do need this to happen then it is advised to use the `IContentValidationService`

or `IContentService`

instead.

Now that you have a converter you need a way to call the correct one depending on the macros found in an RTE value. For this, create a `MacroMigrationService`

that holds the following method:

The method above takes in an `IEnumerable<int>`

. How to get those will be determined later.

To access the database, you need a scope from the scope provider.

The next step is to fetch the value from the database using our custom `MacroPropertyDto`

and a custom SQL query.

For each of the items found, run a regular expression that matches on the tag and alias.

The next step is to look in the list of migrators to find the correct one based on the alias found in the match. Then this needs to run.

When all macros have been converted for a given property, the updated value is saved in the database.

To get all the property IDs, the following `Report`

method is used. The method returns a paginated report of all items that need to be migrated. It includes relevant document data and which migrator will run. This allows you test and debug specific values and migrators.

The last steps are to:

Register the services and their interfaces into the DI container using a composer.

Create a management API controller to call the service.


A full list of files including the full version of the `MacroMigrationService`

and its dependencies can be found below. Once all of this is in place you will have some Swagger docs available at `/umbraco/swagger/index.html?urls.primaryName=Macro+Migrations+Api+v1`

to test the migrators.

## Full MacroMigrator System

**CtaButtonMacroMigrator.cs**

**IMacroMigrationService.cs**

**IMacroMigrator.cs**

**MacroController.cs**

**MacroMigrationComposer.cs**

**MacroMigrationService.cs**

If you want the conversion to happen automatically as you upgrade, you can define a

For an example that takes into account RTE values inside of block properties, have a look at our and its related

The proposed conversion logic should be adaptable to the system used in the local links migration.

If you are using Umbraco Deploy in your solution, you can use its infrastructure to run the migration logic defined above.

To make this work, update the alias of the rich text editor to something else. On import, a migration is triggered. See the in the `Umbraco.Deploy.Contrib`

package.

Create a migrator to handle any value that is of the special alias and convert them into a property with the updated value. For an example see the matching .

Last updated

Was this helpful?