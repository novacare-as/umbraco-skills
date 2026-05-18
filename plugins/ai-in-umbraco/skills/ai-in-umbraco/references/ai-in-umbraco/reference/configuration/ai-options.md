# AIOptions | AI in Umbraco

Configuration options for AI services (fallback mechanism).

Namespace

```
using Umbraco.AI.Core.Models;
```

Class Definition

```
public class AIOptions
{
    public string? DefaultChatProfileAlias { get; set; }
    public string? DefaultEmbeddingProfileAlias { get; set; }
    public string? ClassifierChatProfileAlias { get; set; }
    public string? DefaultSpeechToTextProfileAlias { get; set; }
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `DefaultChatProfileAlias` | `string?` | Fallback default profile alias for chat operations |
| `DefaultEmbeddingProfileAlias` | `string?` | Fallback default profile alias for embeddings |
| `ClassifierChatProfileAlias` | `string?` | Fallback profile alias for classification tasks |
| `DefaultSpeechToTextProfileAlias` | `string?` | Fallback default profile alias for speech-to-text |

Configuration

Precedence

Usage

Setting Defaults

Accessing Options

Behavior When Not Set

Environment Variables

Related

Last updated

Was this helpful?