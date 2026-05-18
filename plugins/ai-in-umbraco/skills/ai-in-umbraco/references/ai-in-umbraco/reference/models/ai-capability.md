# AICapability | AI in Umbraco

Enumeration of AI capability types.

Namespace

```
using Umbraco.AI.Core.Models;
```

Definition

```
public enum AICapability
{
    Chat = 0,
    Embedding = 1,
    SpeechToText = 4
}
```

Values

| Value | Int | Description | Status |
|---|---|---|---|
| `Chat` | 0 | Conversational AI / chat completions | Available |
| `Embedding` | 1 | Text to vector embeddings | Available |
| `SpeechToText` | 4 | Audio transcription and voice input | Available |

Usage

Filtering Profiles

Getting Available Capabilities

Creating Profiles

Checking Provider Support

Notes

Last updated

Was this helpful?