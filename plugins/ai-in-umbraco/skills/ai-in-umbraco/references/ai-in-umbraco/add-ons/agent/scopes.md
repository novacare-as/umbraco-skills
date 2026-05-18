# Scopes | AI in Umbraco

Categorise agents using surfaces, and control where they are available using scopes.

Surfaces

Built-in Surfaces

| Surface ID | Package | Icon | Description |
|---|---|---|---|
| `copilot` | Umbraco.AI.Agent.Copilot | `icon-chat` | Agents available in the copilot chat sidebar |

Assigning Surfaces to Agents

Via Backoffice

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-a5fea96a078cabb2bbfdf4883312814367d87001%252Fagent-scope-assignment.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fa326f86&sv=2)

Via API

Via Code

Querying Agents by Surface

List Agents by Surface

Get All Registered Surfaces

Via Service

Creating Custom Surfaces

1. Define the Surface Class

2. Automatic Registration

3. Manual Registration (Optional)

4. Query Agents by Your Surface

Frontend Localization

| Key Pattern | Purpose |
|---|---|
| `uaiAgentSurface_{surfaceId}Label` | Display name for the surface |
| `uaiAgentSurface_{surfaceId}Description` | Description shown in UI |

Scopes

Scope Rules

| Property | Type | Description |
|---|---|---|
| `AllowRules` | `IReadOnlyList<AIAgentScopeRule>` | If any rule matches, the agent is available (OR logic between rules). Empty means everywhere. |
| `DenyRules` | `IReadOnlyList<AIAgentScopeRule>` | If any rule matches, the agent is denied. Deny takes precedence over allow. |

| Property | Type | Description |
|---|---|---|
| `Sections` | `IReadOnlyList<string>?` | Section aliases (e.g., `"content"` , `"media"` ). Null/empty means any section. |
| `EntityTypes` | `IReadOnlyList<string>?` | Entity type aliases (e.g., `"document"` , `"media"` ). Null/empty means any type. |

Configuring Scopes

Scope Examples

Best Practices

Related

Last updated

Was this helpful?