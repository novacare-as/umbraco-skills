---
name: umbraco-ai
description: >
  Reference for Umbraco.AI — the provider-agnostic AI integration layer for Umbraco CMS, built on Microsoft.Extensions.AI. Use whenever the user mentions Umbraco.AI or AI in Umbraco; any `Umbraco.AI.*` package (Core, OpenAI, Anthropic, Google, MicrosoftFoundry, Amazon); injecting `IAIChatService`, `IAIEmbeddingService`, `IAIProfileService`, `IAIConnectionService`, `IAIGuardrailService`, `IAIContextService`, `IAIAuditLogService`, `IAIUsageAnalyticsService`, or `IAIAgentService`; profiles and aliases (`WithAlias(...)`), connections, contexts and the context picker, guardrails, AI middleware, tool calling, chat / embeddings / speech-to-text; the backoffice AI section; the AI Management API; the frontend AI controllers; AI testing and evaluation; and the add-ons Umbraco Agent, Agent Copilot, Prompt, Search, and Deploy.
---

# Umbraco Ai

Umbraco.AI is a first-party package that adds a **provider-agnostic** AI layer on top of Umbraco CMS. It wraps `Microsoft.Extensions.AI` so that application code asks for a named **profile** (e.g. `chat.WithAlias("content-chat")`) and the profile decides which provider, model, and settings are used. Most integration work falls into three surfaces — the **Umbraco backoffice** (configuring connections, profiles, guardrails, contexts), the **C# service layer** (`IAIChatService` and siblings injected into controllers and services), and the **Management API** + **frontend AI controllers** (for custom backoffice UI). Capabilities covered: chat, embeddings, speech-to-text, and tool calling.

## How to use this skill

This skill has 2 layers. Read only what you need for the task at hand.

### Layer 1: This file (SKILL.md)
Always in context. Use the routing table below to decide which files to read next.

### Layer 2: Documentation (references/)
Conceptual documentation — how things work, best practices, guides.
Read these when the user asks "how does X work" or "what's the best way to do Y".

## Core mental model — Provider → Connection → Profile → Alias

Four abstractions, distinct and easy to conflate — always use them in this order when answering:

- **Provider** — a class of AI service, shipped as its own NuGet: `Umbraco.AI.OpenAI`, `Umbraco.AI.Anthropic`, `Umbraco.AI.Google`, `Umbraco.AI.MicrosoftFoundry`, `Umbraco.AI.Amazon` (Bedrock). Installing a provider registers its capabilities; you can run multiple providers side by side.
- **Connection** — credentials + endpoint for **one** provider. A single provider can have many connections (e.g. OpenAI: Development, Production, Team-A-billing). Managed in the backoffice or via the Management API.
- **Profile** — a Connection + model + capability-specific settings (temperature, max tokens, embedding dimensions, voice, etc.), identified by a human-readable **alias**. A profile is scoped to **one capability** (chat **or** embedding **or** speech-to-text). Different aliases can use different providers behind the scenes — this is the indirection that lets you swap providers without changing code.
- **Alias** — the string application code passes to `WithAlias("…")`. Aliases must be globally unique within their capability. Treat aliases as a stable API contract: renaming one is a breaking change for every callsite.

Rule of thumb: **code references aliases; the backoffice owns the mapping from alias → connection → provider**. If a dev asks "which model is used?", the answer lives in the Profile configuration, not the C# code.

Capabilities: `Chat`, `Embedding`, `SpeechToText`. Each maps to a matching `Microsoft.Extensions.AI` interface under the hood.

## C# service surfaces — which interface for which job

Injected via constructor DI. All live in `Umbraco.AI.Core.*` and are available once the Core package is installed.

| Interface | Namespace | Use for |
|---|---|---|
| `IAIChatService` | `Umbraco.AI.Core.Chat` | Chat completions; pass a `List<ChatMessage>` and a profile alias. Supports tool calling via middleware. |
| `IAIEmbeddingService` | `Umbraco.AI.Core.Embeddings` | Generate embeddings for content / query text. Choose profile by alias. |
| Speech-to-text service | `Umbraco.AI.Core` | Transcribe audio (see the using-the-API docs for the concrete interface). |
| `IAIProfileService` | `Umbraco.AI.Core.Profiles` | Read/CRUD profiles programmatically (e.g. provisioning). |
| `IAIConnectionService` | `Umbraco.AI.Core` | Read/CRUD connections. |
| `IAIContextService` | `Umbraco.AI.Core` | Resolve contexts (Umbraco content surfaced as grounding data) — used when building prompts. |
| `IAIGuardrailService` | `Umbraco.AI.Core` | Query and administer guardrails (pre/post-processing policies). |
| `IAISettingsService` | `Umbraco.AI.Core` | Global AI settings. |
| `IAIAuditLogService` | `Umbraco.AI.Core` | Read audit entries (who called which alias, when). |
| `IAIUsageAnalyticsService` | `Umbraco.AI.Core` | Token usage / cost aggregation. |
| `IAIAgentService` | `Umbraco.AI.Agent` | Agent-style workflows — requires the Agent add-on. |

Minimal chat call pattern:

```csharp
var response = await _chatService.GetChatResponseAsync(
    chat => chat.WithAlias("quick-chat"),
    new List<ChatMessage> { new(ChatRole.User, message) });
return Ok(response.Text);
```

Use `ChatRole.System` for system prompts, `ChatRole.User` / `ChatRole.Assistant` for turns. Streaming, tool calling, and context injection go through the same service via option lambdas.

## Three integration layers — backoffice, Management API, frontend controllers

Pick the layer based on *who* the integration serves:

- **Backoffice UI** — for Umbraco admins. Built-in screens for managing connections, profiles, guardrails, contexts, and settings; viewing audit logs, usage analytics, and version history. No code needed for day-to-day admin.
- **C# service layer** — for server-side application code (API controllers, content event handlers, scheduled jobs). Inject the interfaces from the previous section. This is the primary surface for most feature work.
- **AI Management API** — REST endpoints for headless admin / provisioning: chat, embeddings, connections, profiles, contexts, context-resource-types, guardrails, tools, providers, settings, analytics, audit-logs, versions. Use this to script profile provisioning across environments or build alternative admin UIs.
- **Frontend AI controllers** — Lit-based backoffice web-component controllers that extensions can consume: chat, embeddings, speech-to-text, tool, plus shared types. Use these when building custom backoffice dashboards or property editors that talk to Umbraco.AI from the client side — do **not** call providers directly from the browser.

Extension points: custom **providers** (`Umbraco.AI.MyProvider` pattern), custom **middleware**, custom **guardrails**, custom **tools**, and **notifications** for hooking into request / response lifecycle events.

## Scope of this skill — what's in and what isn't

**In scope** — everything under the Umbraco.AI documentation: Core package, all five first-party providers, the backoffice admin UI, the Management API, the frontend controllers, extensibility (providers, middleware, guardrails, tools, notifications), testing & evaluation, and the five add-ons (Agent, Agent Copilot, Prompt, Search, Deploy).

**Not in scope:**

- General Umbraco CMS documentation (content types, templates, Umbraco Forms, Umbraco Commerce, etc.).
- The underlying `Microsoft.Extensions.AI` API — Umbraco.AI wraps it, but low-level M.E.AI questions belong to Microsoft's docs. This skill does document which M.E.AI interface each capability maps to.
- Raw provider APIs (OpenAI, Anthropic, etc.) — this skill covers the **Umbraco** integration wrapper, not the provider APIs themselves. When a user asks "what does parameter X do on OpenAI's chat endpoint?", note that the answer is upstream from this skill.
- Prompt engineering best practices in general — out of scope except where Umbraco.AI's Prompt add-on prescribes structure.

## Routing table

Use this table to determine which file(s) to read based on the user's question.

### Documentation → references/

Routing is split by area — read the index for the area you need (every area has the full topic list for that subdirectory):

- **Ai In Umbraco** → `references/ai-in-umbraco/index.md` (223 topics)
