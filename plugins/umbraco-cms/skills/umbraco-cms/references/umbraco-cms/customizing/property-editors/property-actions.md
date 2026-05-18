# Property Actions | CMS

Guide on how to implement Property Actions for Property Editors in Umbraco

Property Actions in the UI

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-15da7316fc895f00425c3975670934304210ccea%252Fproperty-actions-blocklist.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c29cebac&sv=2)

Registering a Property Action

Creating the Property Action Class

Last updated

Was this helpful?

Guide on how to implement Property Actions for Property Editors in Umbraco

Property Actions are a built-in feature of Umbraco that allows you to add extra functionality to a Property Editor. Think of them as small, secondary actions that you can attach to a property without modifying the editor itself.

Property Actions appear as a small button next to the property label, which expands to show the available actions.

Property Actions in the UI

Registering a Property Action

Before creating a Property Action, make sure you are familiar with the .

Here is how you can register a new Property Action:

Creating the Property Action Class

Every Property Action needs a class that defines what happens when the action is executed. You can extend the `UmbPropertyActionBase`

class for this.

Last updated

Was this helpful?

Was this helpful?

```
import { umbExtensionsRegistry } from '@umbraco-cms/backoffice/extension-registry';
const manifest =
  {
    type: 'propertyAction',
    kind: 'default',
    alias: 'My.propertyAction',
    name: 'My Property Action ',
    forPropertyEditorUis: ["my-property-editor"], // Target specific property editors
    api: () => import('./my-property-action.api.js'),
    weight: 10, // Order if multiple actions exist
    meta: {
      icon: 'icon-add', // Icon to display in the UI
      label: 'My property action', // Label shown to editors
    }
  };

umbExtensionsRegistry.register(manifest);
```

```
import { UmbPropertyActionBase } from '@umbraco-cms/backoffice/property-action';
import { UMB_PROPERTY_CONTEXT } from '@umbraco-cms/backoffice/property';

export class MyPropertyAction extends UmbPropertyActionBase {
  // The execute method is called when the user triggers the action.
  async execute() {
    // Retrieve the property’s current state,
    const propertyContext = await this.getContext(UMB_PROPERTY_CONTEXT);

    // Here it's possible to modify the property or perform other actions.  In this case, setting a value.
    propertyContext.setValue("Default text here");
  }
}
export { MyPropertyAction as api };
```