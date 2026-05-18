# Extension Conditions | CMS

Learn how to use Extension Conditions when working with the Umbraco backoffice.

Utilizing Conditions in your Manifest

```
const manifest = {
    type: 'workspaceView',...
    conditions: [
        {
            alias: 'Umb.Condition.WorkspaceAlias',
            match: 'Umb.Workspace.Document',
        },
    ],
};
```

Built-in Conditions Types

Condition Configuration

Learn more

Last updated

Was this helpful?