# AIProfile | AI in Umbraco

Profile configuration for AI model usage.

Namespace

```
using Umbraco.AI.Core.Profiles;
```

Class Definition

```
public sealed class AIProfile : IAIVersionableEntity
{
    public Guid Id { get; internal set; }
    public required string Alias { get; set; }
    public required string Name { get; set; }
    public AICapability Capability { get; init; } = AICapability.Chat;
    public AIModelRef Model { get; set; }
    public required Guid ConnectionId { get; set; }
    public IAIProfileSettings? Settings { get; set; }
    public IReadOnlyList<string> Tags { get; set; } = Array.Empty<string>();
    public int Version { get; internal set; }
    public DateTime DateCreated { get; init; }
    public DateTime DateModified { get; set; }
    public Guid? CreatedByUserId { get; set; }
    public Guid? ModifiedByUserId { get; set; }
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Unique identifier (assigned on save) |
| `Alias` | `string` | Unique alias for code references |
| `Name` | `string` | Display name |
| `Capability` | `AICapability` | Type of AI capability (Chat, Embedding, Speech-to-Text) |
| `Model` | `AIModelRef` | Reference to provider and model |
| `ConnectionId` | `Guid` | ID of the connection to use |
| `Settings` | `IAIProfileSettings?` | Capability-specific settings |
| `Tags` | `IReadOnlyList<string>` | Optional categorization tags |
| `Version` | `int` | Version number, starts at 1, increments with each save |
| `DateCreated` | `DateTime` | Creation timestamp |
| `DateModified` | `DateTime` | Last modification timestamp |
| `CreatedByUserId` | `Guid?` | ID of the user who created the profile |
| `ModifiedByUserId` | `Guid?` | ID of the user who last modified the profile |

Settings Types

AIChatProfileSettings

| Property | Type | Description |
|---|---|---|
| `Temperature` | `float?` | Randomness (0.0-1.0, default varies by model) |
| `MaxTokens` | `int?` | Maximum response tokens |
| `SystemPromptTemplate` | `string?` | Default system prompt |
| `ContextIds` | `IReadOnlyList<Guid>` | Context IDs for injection |
| `GuardrailIds` | `IReadOnlyList<Guid>` | Guardrail IDs for safety |

AIEmbeddingProfileSettings

| Property | Type | Description |
|---|---|---|
| `Dimensions` | `int?` | Number of dimensions for embeddings; uses the model's default when `null` |

AISpeechToTextProfileSettings

| Property | Type | Description |
|---|---|---|
| `Language` | `string?` | BCP-47 language hint for transcription (e.g., `en` , `de` , `ja` ) |

Creating a Profile

Notes

Last updated

Was this helpful?