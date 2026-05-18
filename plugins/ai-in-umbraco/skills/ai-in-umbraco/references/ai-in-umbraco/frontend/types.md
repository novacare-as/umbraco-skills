# Types | AI in Umbraco

TypeScript type definitions for all frontend AI operations.

```
import type {
    UaiChatRole,
    UaiChatMessage,
    UaiChatUsage,
    UaiChatResult,
    UaiChatStreamChunk,
    UaiChatOptions,
    UaiChatRequest,
    UaiEmbeddingOptions,
    UaiEmbeddingResult,
    UaiEmbeddingItem,
    UaiSpeechToTextOptions,
    UaiSpeechToTextResult,
    UaiToolScope,
    UaiToolItem,
} from "@umbraco-ai/core";
```

| Value | Description |
|---|---|
| `'user'` | Message from the user |
| `'assistant'` | Message from the AI |
| `'system'` | System instructions |

| Value | Description |
|---|---|
| `'stop'` | Model finished naturally |
| `'length'` | Hit max tokens limit |
| `'content_filter'` | Content was filtered |
| `null` | Reason not provided |

Last updated

Was this helpful?