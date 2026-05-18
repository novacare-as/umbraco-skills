# Concepts | AI in Umbraco

Core concepts for Prompt Management.

What is a Prompt?

Prompt Properties

| Property | Description |
|---|---|
| `Alias` | Unique identifier for code references |
| `Name` | Display name in the backoffice |
| `Description` | Optional description |
| `Instructions` | Prompt template text |
| `ProfileId` | Associated AI profile (optional) |
| `ContextIds` | AI Contexts to inject |
| `GuardrailIds` | Guardrails to evaluate during execution |
| `Tags` | Organization tags |
| `IsActive` | Whether the prompt is available |
| `IncludeEntityContext` | Include entity info in system message |
| `OptionCount` | Number of result options (0 = informational, 1 = single, 2+) |
| `DisplayMode` | Where the prompt is shown (`PropertyAction` or `TipTapTool` ) |
| `Scope` | Allow/deny rules for where the prompt runs |

How Prompts Work

Variable Resolution

Prompt Scoping

Version History

Best Practices

Related

Last updated

Was this helpful?