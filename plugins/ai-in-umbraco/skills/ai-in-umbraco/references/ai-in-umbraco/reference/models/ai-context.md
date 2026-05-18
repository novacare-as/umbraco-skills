# AIContext | AI in Umbraco

Model representing an AI context with resources.

Namespace

```
using Umbraco.AI.Core.Contexts;
```

Definition

```
public sealed class AIContext : IAIVersionableEntity
{
    public Guid Id { get; internal set; }
    public required string Alias { get; set; }
    public required string Name { get; set; }
    public IList<AIContextResource> Resources { get; set; } = [];

    // Audit properties
    public DateTime DateCreated { get; init; } = DateTime.UtcNow;
    public DateTime DateModified { get; set; } = DateTime.UtcNow;
    public Guid? CreatedByUserId { get; set; }
    public Guid? ModifiedByUserId { get; set; }

    // Versioning
    public int Version { get; internal set; } = 1;
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Unique identifier (auto-generated) |
| `Alias` | `string` | Unique alias for programmatic lookup (required) |
| `Name` | `string` | Display name (required) |
| `Resources` | `IList<AIContextResource>` | Collection of resources |
| `DateCreated` | `DateTime` | When created (UTC) |
| `DateModified` | `DateTime` | When last modified (UTC) |
| `CreatedByUserId` | `Guid?` | User who created |
| `ModifiedByUserId` | `Guid?` | User who last modified |
| `Version` | `int` | Current version number |

Example

Related

AIContextResource

Definition

Properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Unique identifier (auto-generated) |
| `ResourceTypeId` | `string` | Type of resource (required, immutable) |
| `Name` | `string` | Display name (required) |
| `Description` | `string?` | Optional description |
| `SortOrder` | `int` | Order for injection |
| `Settings` | `object?` | Resource content (type-specific) |
| `InjectionMode` | `AIContextResourceInjectionMode` | When to inject |

Resource Types

| Type ID | Data Type | Description |
|---|---|---|
| `text` | `string` | Plain text content |
| `document` | `object` | Structured document |
| `url` | `string` | URL reference |

Injection Modes

Last updated

Was this helpful?