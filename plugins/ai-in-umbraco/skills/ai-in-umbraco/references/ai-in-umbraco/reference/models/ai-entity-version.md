# AIEntityVersion | AI in Umbraco

Model representing an entity version history record.

Namespace

```
using Umbraco.AI.Core.Versioning;
```

Definition

```
public sealed class AIEntityVersion
{
    public Guid Id { get; init; }
    public Guid EntityId { get; init; }
    public string EntityType { get; init; } = string.Empty;
    public int Version { get; init; }
    public string Snapshot { get; init; } = string.Empty;
    public DateTime DateCreated { get; init; }
    public Guid? CreatedByUserId { get; init; }
    public string? ChangeDescription { get; init; }
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Version record identifier |
| `EntityId` | `Guid` | ID of the versioned entity |
| `EntityType` | `string` | Type discriminator |
| `Version` | `int` | Sequential version number |
| `Snapshot` | `string` | JSON serialization of entity state |
| `DateCreated` | `DateTime` | When this version was created |
| `CreatedByUserId` | `Guid?` | User who created this version |
| `ChangeDescription` | `string?` | Optional description of changes |

Entity Types

| Type String | Entity | Package |
|---|---|---|
| `"connection"` | `AIConnection` | Umbraco.AI |
| `"profile"` | `AIProfile` | Umbraco.AI |
| `"context"` | `AIContext` | Umbraco.AI |
| `"guardrail"` | `AIGuardrail` | Umbraco.AI |
| `"prompt"` | `AIPrompt` | Umbraco.AI.Prompt |
| `"agent"` | `AIAgent` | Umbraco.AI.Agent |

Example

AIVersionComparison

AIValueChange

AIVersionCleanupResult

IAIVersionableEntity

Related

Last updated

Was this helpful?