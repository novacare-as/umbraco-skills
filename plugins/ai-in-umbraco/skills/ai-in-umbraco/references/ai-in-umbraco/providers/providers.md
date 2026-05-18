# Overview | AI in Umbraco

Detailed configuration guides for each AI provider supported by Umbraco.AI.

Available Providers

| Provider | Package | Capabilities | Best For |
|---|---|---|---|
|

`Umbraco.AI.OpenAI`

[Anthropic](/ai-in-umbraco/providers/anthropic)`Umbraco.AI.Anthropic`

[Google Gemini](/ai-in-umbraco/providers/google)`Umbraco.AI.Google`

[Amazon Bedrock](/ai-in-umbraco/providers/amazon)`Umbraco.AI.Amazon`

[Microsoft AI Foundry](/ai-in-umbraco/providers/microsoft-foundry)`Umbraco.AI.MicrosoftFoundry`

Choosing a Provider

Capabilities Needed

| Capability | OpenAI | Anthropic | Amazon | MS Foundry | |
|---|---|---|---|---|---|
| Chat | Yes | Yes | Yes | Yes | Yes |
| Embedding | Yes | No | No | Yes | Yes |
| Speech-to-Text | Yes | No | No | No | No |

Use Case Fit

| Use Case | Recommended Provider |
|---|---|
| General content generation | OpenAI, Anthropic |
| Code assistance | OpenAI, Anthropic |
| Long document processing | Anthropic (200K context) |
| Semantic search/RAG | OpenAI, Amazon Bedrock |
| AWS infrastructure | Amazon Bedrock |
| Azure/Microsoft stack | Microsoft AI Foundry |
| Cost optimization | Google (Gemini Flash) |

Enterprise Considerations

| Factor | OpenAI | Anthropic | Amazon | MS Foundry | |
|---|---|---|---|---|---|
| Data residency options | Limited | No | Yes | Yes | Yes |
| SOC 2 compliance | Yes | Yes | Yes | Yes | Yes |
| HIPAA eligible | Yes | Contact | Contact | Yes | Yes |
| Self-hosted option | No | No | No | No | No |

Installing Multiple Providers

Provider Configuration Pattern

Custom Providers

Related

Last updated

Was this helpful?