# Managing Guardrails | AI in Umbraco

Create and manage AI guardrails in the Umbraco backoffice.

Accessing Guardrails

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-f3bae8f4e52c3eeb7830d6947241157644d656f5%252Fbackoffice-guardrails-list.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=5eed74c5&sv=2)

Creating a Guardrail

| Field | Description |
|---|---|
| Alias | Unique identifier for code references (URL-safe, no spaces) |
| Name | Display name shown in the backoffice |

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-ffb8f493b4c9603ac4bc761fce02c06111b7c7ad%252Fbackoffice-create-guardrail-form.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8275fb22&sv=2)

Adding Rules

| Field | Description |
|---|---|
| Evaluator | The evaluator to use (Contains, Regex Match, or LLM Safety Judge) |
| Name | Display name for the rule |
| Phase | When to evaluate: Pre-Generate or Post-Generate |
| Action | What to do when flagged: Block, Warn, or Redact |
| Config | Evaluator-specific settings |

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-cac67db4159b2fe5439a4a5bf145b8f1e2e075b6%252Fbackoffice-create-guardrail-add-guardrail.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b034d78a&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-fdd18b8f5b45c7b355692b345b45d19c8cc3742a%252Fbackoffice-create-guardrail-add-guardrail-details.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b4a4da48&sv=2)

Evaluation Phases

| Phase | Description |
|---|---|
| Pre-Generate | Evaluates user input before sending to the AI provider. |
| Post-Generate | Evaluates the AI response before returning to the user. |

Actions

| Action | Description |
|---|---|
| Block | Stops processing and returns an error to the caller. |
| Warn | Allows the content through unchanged and logs a warning. |
| Redact | Replaces flagged content with `[REDACTED]` before it reaches the AI model or caller. |

Available Evaluators

| Evaluator | ID | Type | Description | Supports Redact |
|---|---|---|---|---|
| Contains | `contains` | Code-based | Flags content containing a specific substring. | Yes |
| Regex Match | `regex` | Code-based | Flags content matching a regular expression pattern. | Yes |
| LLM Safety Judge | `llm-judge` | Model-based | Uses an AI model to evaluate content for safety, misinformation, and compliance. | No |

Contains Evaluator

| Setting | Description |
|---|---|
| Search Pattern | The substring to find in the content |
| Ignore Case | Case-insensitive search (default: on) |

Regex Match Evaluator

| Setting | Description |
|---|---|
| Regex Pattern | Regular expression to match against content |
| Ignore Case | Case-insensitive matching (default: on) |
| Multiline | Enable multiline mode where `^` and `$` match line boundaries |

LLM Safety Judge Evaluator

| Setting | Description |
|---|---|
| Judge Profile ID | AI profile to use for evaluation (leave empty for default) |
| Evaluation Criteria | What aspects to evaluate (safety, compliance, brand voice, etc.) |
| Safety Threshold | Content is flagged if the safety score is below this value (0-1, default: 0.7). |

Reordering Rules

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-e094a8140ce674eb8bf199ed68df4844a140aa6b%252Fbackoffice-guardrail-rules.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e476f82&sv=2)

Editing a Guardrail

Deleting a Guardrail

Example: Content Safety Guardrail

Example: PII Redaction Guardrail

Assigning Guardrails

Assigning to a Profile

Assigning to a Prompt

Assigning to an Agent

Version History

Related

Last updated

Was this helpful?