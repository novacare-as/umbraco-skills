# Embeddings Controller | AI in Umbraco

Controller for generating text embeddings from custom backoffice elements.

Import

```
import { UaiEmbeddingsController, UaiEmbeddingOptions } from "@umbraco-ai/core";
```

Constructor

```
new UaiEmbeddingsController(host: UmbControllerHost)
```

| Parameter | Type | Description |
|---|---|---|
| `host` | `UmbControllerHost` | The controller host (usually `this` in a Lit element) |

Methods

generate

```
async generate(
    value: string,
    options?: UaiEmbeddingOptions
): Promise<{ data?: number[]; error?: unknown }>
```

| Parameter | Type | Description |
|---|---|---|
| `value` | `string` | The text to embed |
| `options` | `UaiEmbeddingOptions` | Optional configuration |

`generateMany`

| Parameter | Type | Description |
|---|---|---|
| `values` | `string[]` | The texts to embed |
| `options` | `UaiEmbeddingOptions` | Optional configuration |

Options

Result Types

Example

Related

Last updated

Was this helpful?