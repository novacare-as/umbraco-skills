# Property Level UI Permissions | CMS

Use the UI Property Permissions to restrict access to specific properties in the Backoffice UI.

Document Property Value User Permissions

Write custom Property Level Permissions

Register a Workspace Context

```
import { UMB_WORKSPACE_CONDITION_ALIAS } from "@umbraco-cms/backoffice/workspace";
import { UMB_DOCUMENT_WORKSPACE_ALIAS } from "@umbraco-cms/backoffice/document";

const manifest: UmbExtensionManifest = {
    type: "workspaceContext",
    name: "My Document Property Permission Workspace Context",
    alias: "My.WorkspaceContext.DocumentPropertyPermission",
    api: () => import("./my-document-property-permission.workspace-context.js"),
    conditions: [
        {
            alias: UMB_WORKSPACE_CONDITION_ALIAS,
            match: UMB_DOCUMENT_WORKSPACE_ALIAS,
        },
    ],
};
```

Write a general rule

Write a rule for a specific property

Write a rule for a specific property or a specific variant

Last updated

Was this helpful?