# Concepts

## Contents

- [Capabilities | AI in Umbraco](#capabilities-ai-in-umbraco)
- [Core Concepts | AI in Umbraco](#core-concepts-ai-in-umbraco)
- [Connections | AI in Umbraco](#connections-ai-in-umbraco)
- [Context Picker | AI in Umbraco](#context-picker-ai-in-umbraco)
- [Contexts | AI in Umbraco](#contexts-ai-in-umbraco)
- [Guardrails | AI in Umbraco](#guardrails-ai-in-umbraco)
- [Middleware | AI in Umbraco](#middleware-ai-in-umbraco)
- [Observability | AI in Umbraco](#observability-ai-in-umbraco)
- [Profiles | AI in Umbraco](#profiles-ai-in-umbraco)
- [Providers | AI in Umbraco](#providers-ai-in-umbraco)
- [Settings | AI in Umbraco](#settings-ai-in-umbraco)
- [Version History | AI in Umbraco](#version-history-ai-in-umbraco)

---

## Capabilities | AI in Umbraco

Capabilities represent the types of AI operations that providers can support.

Available Capabilities

| Capability | Description | M.E.AI Interface |
|---|---|---|
| Chat | Conversational AI, text generation, completions | `IChatClient` |
| Embedding | Vector embeddings for semantic search | `IEmbeddingGenerator<string, Embedding<float>>` |
| Speech-to-Text | Audio transcription and voice input | `ISpeechToTextClient` |

Chat Capability

```
var messages = new List<ChatMessage>
{
    new(ChatRole.System, "You are a helpful assistant."),
    new(ChatRole.User, "What is Umbraco?")
};

var response = await _chatService.GetChatResponseAsync(
    chat => chat.WithAlias("content-chat"),
    messages);
```

Embedding Capability

Speech-to-Text Capability

Capability and Profile Relationship

Checking Provider Capabilities

Capability Interfaces

Related

Last updated

Was this helpful?

---

## Core Concepts | AI in Umbraco

Understand the core concepts that make up Umbraco.AI's architecture.

The Configuration Hierarchy

Key Concepts

Built on Microsoft.Extensions.AI

In This Section

Last updated

Was this helpful?

Understand the core concepts that make up Umbraco.AI's architecture.

Umbraco.AI is built around a hierarchical configuration model that separates concerns and enables flexibility. Understanding these concepts helps you make the most of the platform.

The Configuration Hierarchy

Each level adds configuration that flows down to the actual AI request.

Key Concepts

**Providers**

Installable plugins that connect to AI services like OpenAI or Azure

**Connections**

Store credentials and endpoint settings for a provider

**Profiles**

Combine a connection with model settings for specific use cases

**Capabilities**

The types of AI operations available: Chat, Embedding, and more

**Middleware**

Extensible pipeline for logging, caching, and custom behavior

**Guardrails**

Rules that evaluate AI inputs and responses for safety and compliance

Built on Microsoft.Extensions.AI

Umbraco.AI is built on , Microsoft's official abstraction for AI services. Building on M.E.AI provides:

Standard types like

`IChatClient`

,`ChatMessage`

, and`ChatResponse`

Familiar patterns for .NET developers

Compatibility with the broader M.E.AI ecosystem

Compatible with future M.E.AI releases


The service layer in Umbraco.AI is lightweight - it adds Umbraco-specific features (profiles, connections, backoffice UI) while exposing standard M.E.AI types.

In This Section

Last updated

Was this helpful?

Was this helpful?

---

## Connections | AI in Umbraco

Connections store the credentials and settings needed to authenticate with an AI provider.

What Connections Store

| Property | Description |
|---|---|
| `Id` | Unique identifier (GUID) |
| `Alias` | Unique string for programmatic lookup |
| `Name` | Display name shown in the backoffice |
| `ProviderId` | Which provider this connection uses |
| `Settings` | Provider-specific settings (API key, endpoint, and so on) |
| `IsActive` | Whether the connection is enabled |
| `Version` | Current version number, increments with each save |

Connection vs Provider

```
OpenAI Provider
    ├── Connection: "Development" (dev API key)
    ├── Connection: "Production" (prod API key)
    └── Connection: "Team A" (separate billing)
```

Creating Connections

Configuration References

Accessing Connections in Code

Related

Last updated

Was this helpful?

---

## Context Picker | AI in Umbraco

The AI Context Picker property editor enables dynamic context resolution based on content hierarchy.

How It Works

```
┌─────────────────────────────────────────────────────────────┐
│                     Content Tree                            │
│                                                             │
│   Home (context: "corporate-brand")                         │
│   ├── About Us                                              │
│   │   └── Team ← AI operation here                          │
│   │       (inherits "corporate-brand" from Home)            │
│   │                                                         │
│   └── Products (context: "product-focused")                 │
│       └── Widget Pro ← AI operation here                    │
│           (uses "product-focused" from Products)            │
└─────────────────────────────────────────────────────────────┘
```

Adding the Property Editor

Create a Data Type

Configuration Options

| Option | Description |
|---|---|
| Allow Multiple | Enable selection of multiple contexts |
| Minimum Items | Minimum contexts required (optional) |
| Maximum Items | Maximum contexts allowed (optional) |

Add to Document Type

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-fe09a81ae6fc38127ace72ddae705cb5c018499e%252Fcontent-node-context-picker.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5b2a10d5&sv=2)

Context Resolution

Resolution Order

| Source | Priority | Description |
|---|---|---|
| Content | 1 (highest) | Context picker property on content (inherited up tree) |
| Profile | 2 | Context IDs configured on the AI profile |

Content Resolution Details

Using Contexts in Code

Reading Context from Content

Manual Context Resolution

Resolved Context Structure

| Property | Description |
|---|---|
| `InjectedResources` | Resources with `Always` injection mode (included in system prompt) |
| `OnDemandResources` | Resources with `OnDemand` injection mode (available as tools) |
| `AllResources` | All resolved resources |
| `Sources` | Tracking information for debugging |

Injection Modes

Always Mode

OnDemand Mode

Profile-Level Contexts

Related

Last updated

Was this helpful?

---

## Contexts | AI in Umbraco

Contexts define brand voice, guidelines, and additional content that get injected into AI operations.

What Contexts Store

| Property | Description |
|---|---|
| `Id` | Unique identifier (GUID) |
| `Alias` | Unique string for programmatic lookup |
| `Name` | Display name shown in the backoffice |
| `Resources` | Collection of context resources |
| `Version` | Current version number (for version history) |

Context Resources

| Property | Description |
|---|---|
| `Id` | Unique identifier (GUID) |
| `ResourceTypeId` | The type of resource (e.g., "text", "document") |
| `Name` | Display name for the resource |
| `Description` | Optional description |
| `SortOrder` | Controls injection order |
| `Settings` | Type-specific settings |
| `InjectionMode` | When the resource is injected |

Injection Modes

| Mode | Description |
|---|---|
| `Always` | Resource is always included (default) |
| `OnDemand` | Resource is included only when explicitly requested |

Using Contexts in Code

Getting a Context

Creating a Context

How Context Injection Works

Managing Contexts

Via Backoffice

Via Code

Version History

Related

Last updated

Was this helpful?

---

## Guardrails | AI in Umbraco

Guardrails evaluate and filter AI inputs and responses for safety, compliance, and quality enforcement.

What Guardrails Store

| Property | Description |
|---|---|
| `Id` | Unique identifier (GUID) |
| `Alias` | Unique string for programmatic lookup |
| `Name` | Display name shown in the backoffice |
| `Rules` | Ordered collection of evaluation rules |
| `Version` | Current version number (for version history) |

Guardrail Rules

| Property | Description |
|---|---|
| `Id` | Unique identifier (GUID) |
| `EvaluatorId` | The registered evaluator to use (e.g., "contains") |
| `Name` | Display name for the rule |
| `Phase` | When the rule runs: `PreGenerate` or `PostGenerate` |
| `Action` | What happens when flagged: `Block` , `Warn` , or `Redact` |
| `Config` | Evaluator-specific configuration (JSON) |
| `SortOrder` | Controls evaluation order within the guardrail |

Phases

| Phase | Description |
|---|---|
| `PreGenerate` | Evaluated before the request is sent to the AI provider. |
| `PostGenerate` | Evaluated after the AI provider returns a response. |

Actions

| Action | Description |
|---|---|
| `Block` | Stop processing and throw `AIGuardrailBlockedException` . |
| `Warn` | Allow the content through unchanged and log a warning. |
| `Redact` | Replace flagged content with `[REDACTED]` before it reaches the AI model or caller. |

Example Guardrail Configurations

| Guardrail | Use Case | Rules |
|---|---|---|
| `content-safety` | General safety | Contains for competitor brands (Block), Regex for SSNs (Block) |
| `brand-compliance` | Brand voice enforcement | LLM Safety Judge with brand criteria (Warn) |
| `data-protection` | Data protection | Regex for emails pre-generate (Redact), Regex for phone numbers post (Redact) |
| `quality-assurance` | Output quality | LLM Safety Judge for accuracy (Warn) |

Built-in Evaluators

| Evaluator | ID | Type | Redact | Description |
|---|---|---|---|---|
| Contains | `contains` | Code-based | Yes | Flags content containing a specific substring. Config: `SearchPattern` , `IgnoreCase` |
| Regex Match | `regex` | Code-based | Yes | Flags content matching a regular expression pattern. Config: `Pattern` , `IgnoreCase` , `Multiline` |
| LLM Safety Judge | `llm-judge` | Model-based | No | Uses an AI model to evaluate content against configurable criteria. Config: `ProfileId` , `EvaluationCriteria` , `SafetyThreshold` |

Evaluator Types

| Type | Description |
|---|---|
| `CodeBased` | Deterministic evaluation using patterns and rules. Fast, runs during streaming |
| `ModelBased` | Uses an AI model for evaluation. More nuanced, runs after stream completes |

Using Guardrails in Code

Getting a Guardrail

Creating a Guardrail

Assigning Guardrails to a Profile

How Guardrail Evaluation Works

Streaming Behavior

Handling Blocked Content

Managing Guardrails

Version History

Related

Last updated

Was this helpful?

---

## Middleware | AI in Umbraco

Middleware provides an extensible pipeline for adding cross-cutting concerns to AI requests.

How Middleware Works

Middleware Types

Chat Middleware

```
public interface IAIChatMiddleware
{
    IChatClient Apply(IChatClient client);
}
```

Embedding Middleware

Example: Logging Middleware

Registering Middleware

Middleware Ordering

M.E.AI Built-in Middleware

Creating Custom Middleware

Related

Last updated

Was this helpful?

---

## Observability | AI in Umbraco

Monitor AI operations with OpenTelemetry tracing and metrics.

How It Works

```
Request → [Middleware Pipeline] → Provider
                ↓                     ↓
         Umbraco tags added     gen_ai.* span created
                ↓
         Application Performance Monitoring (APM) dashboard (Jaeger, Application Insights, etc.)
```

Enabling OpenTelemetry

```
using Umbraco.AI.Core.Telemetry;

builder.Services.AddOpenTelemetry()
    .WithTracing(t => t.AddSource(AITelemetry.SourceName))
    .WithMetrics(m => m.AddMeter(AITelemetry.SourceName));
```

Traces

| Span Name | Kind | Description |
|---|---|---|
| `gen_ai.chat {model}` | Client | Chat completion request |
| `gen_ai.embeddings {model}` | Client | Embedding generation request |

Umbraco Enrichment Tags

| Tag | Description |
|---|---|
| `umbraco.ai.profile.id` | AI profile GUID |
| `umbraco.ai.profile.alias` | AI profile alias |
| `umbraco.ai.entity.id` | CMS entity ID the operation targets |
| `umbraco.ai.entity.type` | CMS entity type (document, media, etc.) |
| `umbraco.ai.feature.type` | Feature that initiated the call (prompt, agent, etc.) |
| `umbraco.ai.feature.id` | Specific prompt or agent ID |
| `umbraco.ai.audit.id` | Linked audit log entry ID |
| `umbraco.ai.user.id` | Umbraco user who initiated the operation |

Metrics

| Metric | Type | Description |
|---|---|---|
| `gen_ai.client.token.usage` | Histogram | Input and output token counts |
| `gen_ai.client.operation.duration` | Histogram | Operation latency |
| `gen_ai.client.time_to_first_chunk` | Histogram | Time to first streaming chunk |
| `gen_ai.client.time_per_output_chunk` | Histogram | Per-chunk streaming latency |

Audit Log Correlation

Example: Application Insights

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-b84fefaf25e101b6b9b1dba11754bd7638a074e1%252Fobservability-trace-example.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=113f4aa6&sv=2)

Example: Jaeger

Related

Last updated

Was this helpful?

---

## Profiles | AI in Umbraco

Profiles combine a connection with model settings to create reusable AI configurations.

What Profiles Store

| Property | Description |
|---|---|
| `Id` | Unique identifier (GUID) |
| `Alias` | Unique string for programmatic lookup |
| `Name` | Display name shown in the backoffice |
| `Capability` | The type of AI capability (Chat, Embedding, Speech-to-Text, and so on) |
| `ConnectionId` | Which connection provides credentials |
| `Model` | The specific AI model to use |
| `Settings` | Capability-specific settings |
| `Tags` | Optional tags for organization |

Profile Settings by Capability

Chat Profiles

| Setting | Description | Type |
|---|---|---|
| `Temperature` | Controls randomness (0-2) | float |
| `MaxTokens` | Maximum response length | int |
| `SystemPromptTemplate` | Instructions sent with every request | string |

Embedding Profiles

| Setting | Description | Type |
|---|---|---|
| `Dimensions` | Number of dimensions for the generated embeddings (model default if null) | int |

Speech-to-Text Profiles

| Setting | Description | Type |
|---|---|---|
| `Language` | BCP-47 language hint for transcription (e.g., "en", "de") | string |

Example Profile Configurations

| Profile | Use Case | Model | Temperature | System Prompt |
|---|---|---|---|---|
| `content-writer` | Blog posts | gpt-4o | 0.8 | "You are a helpful content writer..." |
| `code-assistant` | Code help | gpt-4o | 0.2 | "You are a code assistant..." |
| `translator` | Translation | gpt-4o-mini | 0.3 | "Translate to {language}..." |
| `embeddings` | Search indexing | text-embedding-3-small | - | - |

Using Profiles in Code

Default Profile

Named Profile

Override Settings

Profile Resolution

Managing Profiles

Via Backoffice

Via Code

Related

Last updated

Was this helpful?

---

## Providers | AI in Umbraco

Providers are installable plugins that connect Umbraco.AI to AI services.

How Providers Work

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                                 Umbraco.AI                                      │
│    ┌─────────────────────────────────────────────────────────────────────────┐  │
│    │                          Provider Registry                              │  │
│    │  ┌──────────┐ ┌───────────┐ ┌──────────┐ ┌─────────┐ ┌───────────────┐  │  │
│    │  │  OpenAI  │ │ Anthropic │ │ Google   │ │ Amazon  │ │ MS AI Foundry │  │  │
│    │  │ Provider │ │  Provider │ │ Provider │ │ Bedrock │ │   Provider    │  │  │
│    │  └──────────┘ └───────────┘ └──────────┘ └─────────┘ └───────────────┘  │  │
│    └─────────────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────────────┘
```

Available Providers

| Provider | Package | Capabilities |
|---|---|---|
| OpenAI | `Umbraco.AI.OpenAI` | Chat, Embedding, Speech-to-Text |
| Anthropic | `Umbraco.AI.Anthropic` | Chat |
| Google Gemini | `Umbraco.AI.Google` | Chat |
| Amazon Bedrock | `Umbraco.AI.Amazon` | Chat, Embedding |
| Microsoft AI Foundry | `Umbraco.AI.MicrosoftFoundry` | Chat, Embedding |

Provider Discovery

Provider Settings

| Setting | Description |
|---|---|
| API Key | Authentication credential |
| Endpoint | API URL (for custom endpoints) |
| Organization | Organization identifier (if applicable) |

Provider Capabilities

Accessing Providers in Code

Creating Custom Providers

[Custom Providers chevron-right](/ai-in-umbraco/extending/providers)

Related

Last updated

Was this helpful?

---

## Settings | AI in Umbraco

Global AI settings configure default profiles and system-wide behavior.

What Settings Store

| Property | Description |
|---|---|
| `Id` | Fixed identifier (always the same GUID) |
| `DefaultChatProfileId` | The profile used when no profile is specified for chat operations |
| `DefaultEmbeddingProfileId` | The profile used when no profile is specified for embedding operations |
| `DefaultSpeechToTextProfileId` | The profile used when no profile is specified for speech-to-text operations |
| `ClassifierChatProfileId` | Optional profile for internal classification tasks (e.g., agent routing). Falls back to default chat profile |

Configuring Default Profiles

Using Settings in Code

Getting Current Settings

```
public class SettingsExample
{
    private readonly IAISettingsService _settingsService;

    public SettingsExample(IAISettingsService settingsService)
    {
        _settingsService = settingsService;
    }

    public async Task<AISettings> GetCurrentSettings()
    {
        return await _settingsService.GetSettingsAsync();
    }
}
```

Updating Settings

How Default Profiles Work

Classifier Chat Profile

Fallback Chain

Configuration File Fallback

Managing Settings

Via Backoffice

Via Management API

Related

Last updated

Was this helpful?

---

## Version History | AI in Umbraco

Version history tracks changes to AI entities and enables rollback to previous states.

Supported Entity Types

| Entity Type | Package | Description |
|---|---|---|
| `connection` | Umbraco.AI | API credentials and provider settings |
| `profile` | Umbraco.AI | Model configuration and settings |
| `context` | Umbraco.AI | Brand voice and content resources |
| `prompt` | Umbraco.AI.Prompt | Prompt templates |
| `agent` | Umbraco.AI.Agent | AI agent definitions |

How Versioning Works

Version Record Properties

| Property | Description |
|---|---|
| `Id` | Unique identifier for the version record |
| `EntityId` | The ID of the versioned entity |
| `EntityType` | Discriminator (e.g., "profile", "context") |
| `Version` | Sequential version number |
| `Snapshot` | JSON serialization of the entity state |
| `DateCreated` | When this version was created |
| `CreatedByUserId` | Who created this version |
| `ChangeDescription` | Optional description of changes |

Using Version History in Code

Getting Version History

Getting a Specific Version

Comparing Versions

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-23d3d8049b9ea66b334fb648ac648b9c15493d48%252Fbackoffice-version-compare.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=97b19327&sv=2)

Rolling Back

Version Cleanup

| Property | Default | Description |
|---|---|---|
| `Enabled` | `true` | Whether automatic version cleanup is enabled |
| `MaxVersionsPerEntity` | `50` | Maximum versions to retain per entity (set to `0` to disable) |
| `RetentionDays` | `90` | Days to retain version history (set to `0` to disable) |

Manual Cleanup

Viewing Version History

Via Backoffice

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-63d531a0722632addf790757c5b5f7b287347206%252Fbackoffice-version-history.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=53126ffa&sv=2)

Via Management API

Related

Last updated

Was this helpful?

---
