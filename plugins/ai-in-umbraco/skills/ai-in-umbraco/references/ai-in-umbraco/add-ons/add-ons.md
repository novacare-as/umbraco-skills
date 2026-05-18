# Overview | AI in Umbraco

Add-on packages that extend Umbraco.AI with additional capabilities.

Available Add-ons

| Add-on | Package | Description |
|---|---|---|
|

`Umbraco.AI.Prompt`

[Agent Runtime](/ai-in-umbraco/add-ons/agent)`Umbraco.AI.Agent`

[Agent Copilot](/ai-in-umbraco/add-ons/agent-copilot)`Umbraco.AI.Agent.Copilot`

[Semantic Search](/ai-in-umbraco/add-ons/search)`Umbraco.AI.Search`

[Deploy Support](/ai-in-umbraco/add-ons/deploy)`Umbraco.AI.Deploy`

Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                      Your Application                            │
├─────────────────────────────────────────────────────────────────┤
│                                  ┌──────────────────────────┐   │
│                                  │ Umbraco.AI.Agent.Copilot │   │
│                                  │     (Chat UI Add-on)     │   │
│                                  └────────────┬─────────────┘   │
│                                               │                 │
│   ┌───────────────────┐      ┌────────────────▼───────────┐     │
│   │ Umbraco.AI.Prompt │      │     Umbraco.AI.Agent       │     │
│   │   (Prompt Mgmt)   │      │     (Agent Runtime)        │     │
│   └────────┬──────────┘      └─────────────┬──────────────┘     │
│            │                               │                    │
│            └───────────────┬───────────────┘                    │
│                            │                                    │
│                  ┌─────────▼─────────┐                          │
│                  │    Umbraco.AI     │                          │
│                  │      (Core)       │                          │
│                  └─────────┬─────────┘                          │
│                            │                                    │
│           ┌────────────────┼───────────────┐                    │
│           │                │               │                    │
│      ┌────▼─────┐    ┌─────▼─────┐    ┌────▼─────┐              │
│      │ OpenAI   │    │ Anthropic │    │ Google   │  ...        │
│      │ Provider │    │ Provider  │    │ Provider │              │
│      └──────────┘    └───────────┘    └──────────┘              │
└─────────────────────────────────────────────────────────────────┘
```

Installing Add-ons

Common Features

Add-on Databases

| Add-on | Migration Prefix |
|---|---|
| Prompt | `UmbracoAIPrompt_` |
| Agent | `UmbracoAIAgent_` |
| Search | `UmbracoAISearch_` |

Related

Last updated

Was this helpful?