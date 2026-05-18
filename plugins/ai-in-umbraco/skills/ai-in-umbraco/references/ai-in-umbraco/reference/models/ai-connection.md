# AIConnection | AI in Umbraco

Connection to an AI provider with credentials.

Namespace

```
using Umbraco.AI.Core.Connections;
```

Class Definition

```
public class AIConnection : IAIVersionableEntity
{
    public Guid Id { get; internal set; }
    public required string Alias { get; set; }
    public required string Name { get; set; }
    public required string ProviderId { get; init; }
    public object? Settings { get; set; }
    public bool IsActive { get; set; } = true;
    public DateTime DateCreated { get; init; } = DateTime.UtcNow;
    public DateTime DateModified { get; set; } = DateTime.UtcNow;
    public int Version { get; internal set; } = 1;
    public Guid? CreatedByUserId { get; set; }
    public Guid? ModifiedByUserId { get; set; }
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Unique identifier (assigned on save) |
| `Alias` | `string` | Unique alias for lookups |
| `Name` | `string` | Display name |
| `ProviderId` | `string` | ID of the provider (for example, `"openai"` ) |
| `Settings` | `object?` | Provider-specific settings |
| `IsActive` | `bool` | Whether connection is enabled |
| `DateCreated` | `DateTime` | Creation timestamp (UTC) |
| `DateModified` | `DateTime` | Last modification timestamp (UTC) |
| `Version` | `int` | Version number, starts at 1, increments with each save |
| `CreatedByUserId` | `Guid?` | ID of the user who created the connection |
| `ModifiedByUserId` | `Guid?` | ID of the user who last modified the connection |

Settings

OpenAI Example

Configuration References

Creating a Connection

Notes

Last updated

Was this helpful?