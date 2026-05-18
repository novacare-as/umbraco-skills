# AIModelRef | AI in Umbraco

Reference to a specific AI model.

Namespace

```
using Umbraco.AI.Core.Models;
```

Definition

```
public readonly struct AIModelRef
{
    public AIModelRef(string providerId, string modelId);

    public string ProviderId { get; }
    public string ModelId { get; }

    public override string ToString() => $"{ProviderId}/{ModelId}";
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `ProviderId` | `string` | The provider's unique identifier |
| `ModelId` | `string` | The model's unique identifier |

Constructor

| Parameter | Type | Description |
|---|---|---|
| `providerId` | `string` | Provider ID (required, non-null) |
| `modelId` | `string` | Model ID (required, non-null) |

Usage

Creating a Model Reference

Using with Profiles

String Representation

Common Model IDs

OpenAI Chat Models

| Model ID | Description |
|---|---|
| `gpt-4o` | GPT-4o (Omni) |
| `gpt-4o-mini` | GPT-4o Mini (faster, cheaper) |
| `gpt-4-turbo` | GPT-4 Turbo |
| `gpt-3.5-turbo` | GPT-3.5 Turbo |

OpenAI Embedding Models

| Model ID | Description |
|---|---|
| `text-embedding-3-small` | Small embedding model (1536 dims) |
| `text-embedding-3-large` | Large embedding model (3072 dims) |
| `text-embedding-ada-002` | Ada v2 (legacy) |

Notes

Last updated

Was this helpful?