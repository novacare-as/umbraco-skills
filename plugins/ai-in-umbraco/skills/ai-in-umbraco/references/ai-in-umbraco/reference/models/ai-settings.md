# AISettings | AI in Umbraco

Model representing global AI settings.

Namespace

```
using Umbraco.AI.Core.Settings;
```

Definition

```
public class AISettings : IAIAuditableEntity
{
    // Fixed settings ID (singleton)
    public static Guid SettingsId = new("672BF83C-97E0-4D04-9D33-23FC2E5EBE42");

    public Guid Id => SettingsId;

    [AISetting]
    public Guid? DefaultChatProfileId { get; set; }

    [AISetting]
    public Guid? DefaultEmbeddingProfileId { get; set; }

    [AISetting]
    public Guid? DefaultSpeechToTextProfileId { get; set; }

    [AISetting]
    public Guid? ClassifierChatProfileId { get; set; }

    // Audit properties
    public DateTime DateCreated { get; internal set; }
    public DateTime DateModified { get; internal set; }
    public Guid? CreatedByUserId { get; internal set; }
    public Guid? ModifiedByUserId { get; internal set; }
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Fixed identifier (always the same value) |
| `DefaultChatProfileId` | `Guid?` | Default profile for chat operations |
| `DefaultEmbeddingProfileId` | `Guid?` | Default profile for embedding operations |
| `DefaultSpeechToTextProfileId` | `Guid?` | Default profile for speech-to-text operations |
| `ClassifierChatProfileId` | `Guid?` | Optional profile for classification tasks (falls back to default chat) |
| `DateCreated` | `DateTime` | When settings were first created |
| `DateModified` | `DateTime` | When settings were last modified |
| `CreatedByUserId` | `Guid?` | User who created |
| `ModifiedByUserId` | `Guid?` | User who last modified |

Notes

Example

Related

Last updated

Was this helpful?