# Permissions | AI in Umbraco

Configure tool permissions for agents using scopes, explicit tool lists, and user group overrides.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-9892cfe4742226b5fcb2e64ab5d527fc786e7cf7%252Fagent-governance-tab.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b0bca75&sv=2)

Permission System Overview

Tool Scopes

Built-in Tool Scopes

| Scope ID | Icon | Destructive | Description |
|---|---|---|---|
| `content-read` | `icon-article` | No | Read operations on content items |
| `content-write` | `icon-article` | Yes | Create, update, or delete content |
| `media-read` | `icon-picture` | No | Read operations on media items |
| `media-write` | `icon-picture` | Yes | Upload, update, or delete media |
| `search` | `icon-search` | No | Search content, media, and Umbraco resources |
| `navigation` | `icon-navigation` | No | Access current page info and context resources |
| `web` | `icon-globe` | No | Fetch external web pages and content |

Configuring Scope Permissions

Explicit Tool Permissions

When to Use Explicit Permissions

Configuring Explicit Tool Permissions

Combining Scopes and Explicit Permissions

User Group Permission Overrides

Use Cases

How Overrides Work

Configuring User Group Overrides

User Group Permission Properties

| Property | Type | Description |
|---|---|---|
| `AllowedToolIds` | `IReadOnlyList<string>` | Tool IDs added to the allowed set for this user group. |
| `AllowedToolScopeIds` | `IReadOnlyList<string>` | Tool scope IDs added to the allowed set for this user group. |
| `DeniedToolIds` | `IReadOnlyList<string>` | Tool IDs removed from the allowed set. Takes precedence over allow rules. |
| `DeniedToolScopeIds` | `IReadOnlyList<string>` | Tool scope IDs removed from the allowed set. Takes precedence over allow rules. |

Permission Resolution Flow

Frontend Tool Metadata

Tool Metadata Properties

| Property | Type | Description |
|---|---|---|
| `scope` | `string?` | Tool scope ID for permission grouping (e.g., "content-write") |
| `isDestructive` | `boolean` | Whether tool performs destructive operations (create/update/delete) |

Checking Permissions Programmatically

Check if a Tool is Allowed

Get All Allowed Tools

Permission Filtering at Runtime

Security Considerations

Best Practices

Related

Last updated

Was this helpful?