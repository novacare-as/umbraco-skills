# Tool Controller | AI in Umbraco

Controller for querying available AI tools and tool scopes from custom backoffice elements.

Import

```
import { UaiToolController, UaiToolScope, UaiToolItem } from "@umbraco-ai/core";
```

Constructor

```
new UaiToolController(host: UmbControllerHost)
```

| Parameter | Type | Description |
|---|---|---|
| `host` | `UmbControllerHost` | The controller host (usually `this` in a Lit element) |

Methods

getToolScopes

```
async getToolScopes(): Promise<{ data?: UaiToolScope[]; error?: unknown }>
```

`getTools`

```
async getTools(): Promise<{ data?: UaiToolItem[]; error?: unknown }>
```

getToolCountsByScope

Types

Example

Related

Last updated

Was this helpful?