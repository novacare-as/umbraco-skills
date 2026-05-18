# Tracking References | CMS

Guide on how to implement tracking entity references for Property Editors in Umbraco

Viewing References

For Media Items

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-504116f0e2adc48b11d40d5236157bb924c21286%252Fmedia-references.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b88aa91c&sv=2)

For Content Nodes

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-504116f0e2adc48b11d40d5236157bb924c21286%252Fmedia-references.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b88aa91c&sv=2)

For Data Types

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d09a0db0f0219114c48e91bab176a02563ab825f%252Fdata-types-references.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=67efb1ae&sv=2)

Example

Last updated

Was this helpful?

Guide on how to implement tracking entity references for Property Editors in Umbraco

Property editors can be extended further to track entity references that may be selected or referenced inside the property editor. For example in the core of the CMS we have added this to numerous property editors.

A good example of this is the Media Picker. The CMS stores a reference to the selected media item, enabling the identification of content nodes that use that particular media item. This avoids it being accidentally deleted if it is being used.

When a content node is saved it will save the entity references as relations.

Viewing References

For Media Items

Go to the

**Media**section.Select a media item and click the

**Info**tab.

For Content Nodes

Go to the

**Settings**section.Under the

**Relations**from the**Advanced**section, select**Related Document**relations.

For Data Types

Go to the

**Settings**section.Expand the

**Data Types**folder.Select the

**Data Type**you wish to view the references.Navigate to the

**Info**tab.

Example

The following example shows how to implement tracking for the inbuilt CMS property editor **Content Picker**. It will always add a specific media reference, regardless of what value is picked in the content picker. In your own implementations, you will need to parse the value stored from the property editor you are implementing. You will also need to find any references to picked items in order to track their references.

You'll need a Composer to enable the tracking example:

Last updated

Was this helpful?

Was this helpful?

TrackingExample.cs

```
using Umbraco.Cms.Core;
using Umbraco.Cms.Core.Models;
using Umbraco.Cms.Core.Models.Editors;
using Umbraco.Cms.Core.PropertyEditors;

namespace UmbracoDocs.Samples;

public class TrackingExample : IDataValueReferenceFactory, IDataValueReference
{
    public IDataValueReference GetDataValueReference() => this;

    // Which Data Editor (Data Type) does this apply to - in this example it is the built in content picker of Umbraco
    public bool IsForEditor(IDataEditor? dataEditor)
        => dataEditor?.Alias.InvariantEquals(Constants.PropertyEditors.Aliases.ContentPicker) is true;

    public IEnumerable<UmbracoEntityReference> GetReferences(object? value)
    {
        // Value contains the raw data that is being saved for a property editor
        // You can then analyse this data be it a complex JSON structure or something more trivial
        // To add the chosen entities as references (as any UDI type including custom ones)

        // A very simple example
        // This will always ADD a specific media reference to the collection list
        // When it's a ContentPicker datatype
        var references = new List<UmbracoEntityReference>();
        var udiType = UmbracoObjectTypes.Media.GetUdiType();
        var udi = Udi.Create(udiType, Guid.Parse("fbbaa38d-bd93-48b9-b1d5-724c46b6693e"));
        var entityRef = new UmbracoEntityReference(udi);
        references.Add(entityRef);
        return references;
    }
}
```

TrackingExampleComposer.cs

```
using Umbraco.Cms.Core.Composing;

namespace UmbracoDocs.Samples;

public class TrackingExampleComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
        => builder.DataValueReferenceFactories().Append<TrackingExample>();
}
```