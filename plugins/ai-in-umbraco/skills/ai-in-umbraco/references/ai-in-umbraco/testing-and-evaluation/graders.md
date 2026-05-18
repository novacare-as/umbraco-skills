# Graders | AI in Umbraco

Built-in graders for evaluating AI test outputs.

Shared Configuration

| Option | Type | Default | Description |
|---|---|---|---|
| `Negate` | bool | false | Inverts the result (pass becomes fail) |
| `Severity` | string | Error | `Info` , `Warning` , or `Error` |
| `Weight` | double | 1.0 | Weight for aggregate scoring (0 to 1) |

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-97adefd523b360a114332d01f259f3a619b45fa7%252Fbackoffice-ai-test-grader-settings.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3ccb1472&sv=2)

Code-Based Graders

exact-match

| Config Property | Type | Default | Description |
|---|---|---|---|
| `ExpectedValue` | string | (empty) | The exact value to match |
| `IgnoreCase` | bool | true | Case-insensitive comparison |

contains

| Config Property | Type | Default | Description |
|---|---|---|---|
| `SearchPattern` | string | (empty) | The substring to find |
| `IgnoreCase` | bool | true | Case-insensitive search |

regex

| Config Property | Type | Default | Description |
|---|---|---|---|
| `Pattern` | string | (empty) | The regex pattern to match |
| `IgnoreCase` | bool | true | Case-insensitive matching |
| `Multiline` | bool | false | Enable multiline mode (^ and $ match line boundaries) |

json-schema

| Config Property | Type | Default | Description |
|---|---|---|---|
| `ExpectedKeys` | string | (empty) | Required JSON keys (comma-separated, dot-notation for nested) |
| `RequireAllKeys` | bool | true | All keys must be present |

tool-call

| Config Property | Type | Default | Description |
|---|---|---|---|
| `ExpectedTools` | string | (empty) | Tool names (comma-separated) |
| `ValidationMode` | string | Any | `Any` , `All` , `Exact` , or `None` |
| `ValidateOrder` | bool | false | Whether tool calls must appear in order |

| Mode | Description |
|---|---|
| `Any` | At least one expected tool was called |
| `All` | All expected tools were called (in any order) |
| `Exact` | The expected tools match the actual calls (same set) |
| `None` | None of the expected tools were called |

guardrail

| Config Property | Type | Default | Description |
|---|---|---|---|
| `EvaluatorId` | string | (empty) | The guardrail evaluator to run |
| `EvaluatorConfig` | JSON (optional) | null | Evaluator-specific configuration |

Model-Based Graders

llm-judge

| Config Property | Type | Default | Description |
|---|---|---|---|
| `ProfileId` | guid | null | AI profile for the judge (optional) |
| `EvaluationCriteria` | string | (default) | What aspects to evaluate |
| `PassThreshold` | double | 0.7 | Minimum score to pass (0 to 1) |

Combining Graders

Related

Last updated

Was this helpful?