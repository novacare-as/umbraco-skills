# Workspaces | CMS

Key Concepts

Extension Types

Last updated

Was this helpful?

Workspaces provide dedicated editing environments for specific entity types in Umbraco. They create isolated areas where users can edit content, media, members, or other entities with specialized interfaces and functionality.

Key Concepts

**Entity-Based Structure**: Each workspace is designed for a specific entity type (content, media, member, etc.). It is identified by a unique string (such as a key or ID).

**Draft State Management**: Workspaces maintain a draft copy of entity data that can be modified without affecting the published version until explicitly saved.

**Flexible Interface**: Workspaces can range from single-view interfaces to complex multi-tabbed editors with specialized functionality.

**Shared Communication**: Workspaces host workspace contexts that enable all extensions within the workspace to communicate and share state.

Extension Types

Workspaces support different extension types that work together to create comprehensive editing experiences. These extensions communicate through shared workspace contexts to provide integrated functionality:

The foundation extension that provides shared state management and communication between all workspace extensions. Start here when building workspace functionality.

Create tab-based content areas within workspaces for organizing different aspects of entity editing. These appear as tabs in the main workspace area.

Add primary action buttons to workspace footers for user interactions like save, publish, or custom operations.

Extend workspace actions with dropdown menu items to provide additional functionality without cluttering the footer.

Display persistent status information and contextual data in the workspace footer area for always-visible information.

Last updated

Was this helpful?

Was this helpful?

```
interface UmbWorkspaceElement {}
```