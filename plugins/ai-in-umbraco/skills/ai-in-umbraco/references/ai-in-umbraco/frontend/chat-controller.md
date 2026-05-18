# Chat Controller | AI in Umbraco

High-level controller for chat completions in custom elements.

Import

```
import { UaiChatController } from "@umbraco-ai/core";
```

Constructor

```
new UaiChatController(host: UmbControllerHost)
```

| Parameter | Type | Description |
|---|---|---|
| `host` | `UmbControllerHost` | The controller host (usually `this` in a Lit element) |

Methods

complete

```
async complete(
    messages: UaiChatMessage[],
    options?: UaiChatOptions
): Promise<{ data?: UaiChatResult; error?: unknown }>
```

| Parameter | Type | Description |
|---|---|---|
| `messages` | `UaiChatMessage[]` | The conversation messages |
| `options` | `UaiChatOptions` | Optional configuration |

Options

Complete Example

Last updated

Was this helpful?