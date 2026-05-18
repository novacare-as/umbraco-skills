# AIGuardrail | AI in Umbraco

Model representing an AI guardrail with evaluation rules.

Namespace

```
using Umbraco.AI.Core.Guardrails;
```

Definition

```
public sealed class AIGuardrail : IAIVersionableEntity
{
    public Guid Id { get; internal set; }
    public required string Alias { get; set; }
    public required string Name { get; set; }
    public IList<AIGuardrailRule> Rules { get; set; } = [];

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
| `Rules` | `IList<AIGuardrailRule>` | Ordered collection of evaluation rules |
| `DateCreated` | `DateTime` | When created (UTC) |
| `DateModified` | `DateTime` | When last modified (UTC) |
| `CreatedByUserId` | `Guid?` | User who created |
| `ModifiedByUserId` | `Guid?` | User who last modified |
| `Version` | `int` | Current version number |

Example

Related

AIGuardrailRule

Definition

Properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Unique identifier (auto-generated) |
| `EvaluatorId` | `string` | Registered evaluator ID (required, immutable) |
| `Name` | `string` | Display name (required) |
| `Phase` | `AIGuardrailPhase` | When to evaluate (default: PostGenerate) |
| `Action` | `AIGuardrailAction` | What to do when flagged: Block, Warn, or Redact (default: Block) |
| `Config` | `JsonElement?` | Evaluator-specific configuration |
| `GuardrailName` | `string?` | Name of the parent guardrail (set during resolution) |
| `SortOrder` | `int` | Controls evaluation order within the guardrail |

Enums

AIGuardrailPhase

AIGuardrailAction

Last updated

Was this helpful?