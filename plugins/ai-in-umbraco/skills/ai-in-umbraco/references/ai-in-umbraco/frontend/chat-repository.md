# Chat Repository | AI in Umbraco

Access AI chat functionality from TypeScript using the chat repository pattern.

UaiChatRepository

```
import { UaiChatRepository } from "@umbraco-ai/core";

const repository = new UaiChatRepository(host);
```

When to Use

| Scenario | Use |
|---|---|
| Chat completions with cancellation | `UaiChatController` |
| Direct API calls for chat data | `UaiChatRepository` |
| Custom chat implementations | `UaiChatRepository` |

Related

Last updated

Was this helpful?