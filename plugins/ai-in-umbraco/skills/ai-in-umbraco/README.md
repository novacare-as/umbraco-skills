# Umbraco Ai Skill

A Claude Code skill that provides Reference for Umbraco.AI — the provider-agnostic AI integration layer for Umbraco CMS, built on Microsoft.Extensions.AI. Use whenever the user mentions Umbraco.AI or AI in Umbraco; any `Umbraco.AI.*` package (Core, OpenAI, Anthropic, Google, MicrosoftFoundry, Amazon); injecting `IAIChatService`, `IAIEmbeddingService`, `IAIProfileService`, `IAIConnectionService`, `IAIGuardrailService`, `IAIContextService`, `IAIAuditLogService`, `IAIUsageAnalyticsService`, or `IAIAgentService`; profiles and aliases (`WithAlias(...)`), connections, contexts and the context picker, guardrails, AI middleware, tool calling, chat / embeddings / speech-to-text; the backoffice AI section; the AI Management API; the frontend AI controllers; AI testing and evaluation; and the add-ons Umbraco Agent, Agent Copilot, Prompt, Search, and Deploy.

## Structure

```
SKILL.md              # Skill definition and routing table (always in context)
references/           # Documentation
```

## Installation

Add this skill to your Claude Code setup by placing it in your skills directory
or referencing it in your configuration.
