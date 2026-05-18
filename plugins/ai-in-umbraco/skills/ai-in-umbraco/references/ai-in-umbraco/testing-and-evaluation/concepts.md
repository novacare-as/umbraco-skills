# Concepts | AI in Umbraco

Core concepts of the AI Testing and Evaluation framework.

What is a Test?

Test Properties

| Property | Description |
|---|---|
| `Alias` | Unique identifier for code and API references |
| `Name` | Display name in the backoffice |
| `Description` | Optional description of what the test validates |
| `TestFeatureId` | The test feature (harness) to use: `prompt` , `agent` |
| `TestTargetId` | The ID of the prompt or agent to test |
| `ProfileId` | Optional default profile for execution |
| `ContextIds` | Optional default contexts for execution |
| `TestFeatureConfig` | Feature-specific configuration (JSON) |
| `Graders` | Success criteria that evaluate the output |
| `Variations` | A/B testing configuration overrides |
| `RunCount` | Number of times to run per execution (1 to N) |
| `Tags` | Organization tags for filtering and batch execution |
| `BaselineRunId` | Baseline run for regression detection |

Test Feature (Harness)

Built-in Test Features

| ID | Name | Description |
|---|---|---|
| `prompt` | Prompt | Executes a prompt and captures the response text |
| `agent` | Agent | Runs an agent and captures the full conversation |

Graders

Grader Types

| Type | Description |
|---|---|
| CodeBased | Deterministic, fast. Exact match, regex, JSON validation, tool call checks. |
| ModelBased | Flexible, uses an LLM. Semantic evaluation with custom criteria. |

Grader Configuration Options

| Option | Type | Default | Description |
|---|---|---|---|
| `Negate` | bool | false | Inverts the result (pass becomes fail) |
| `Severity` | string | Error | `Info` , `Warning` , or `Error` |
| `Weight` | double | 1.0 | Weight for aggregate scoring (0 to 1) |

Variations

Baseline

Execution

Execution Modes

| Mode | Description |
|---|---|
| Single | Run one test via `POST /tests/{idOrAlias}/run` |
| Batch | Run multiple tests via `POST /tests/run-batch` |
| By Tags | Run all tests with specific tags via `POST /tests/run-by-tags` |

Execution Flow

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-3d53efcd240f46ae5f964b33fcd2bf1481466d67%252Fbackoffice-ai-test-run-details.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3b8c7044&sv=2)

Metrics

| Metric | Formula | Description |
|---|---|---|
| pass@k | `PassedRuns / TotalRuns` | Probability that at least one run succeeds |
| pass^k | `AllPassed ? 1.0 : 0.0` | Whether all runs succeeded |

Transcript

| Field | Description |
|---|---|
| `Messages` | Chat messages exchanged (system, user, assistant) |
| `ToolCalls` | Tool calls made during execution (agent tests) |
| `Reasoning` | Reasoning or thinking steps (if captured) |
| `Timing` | Step-by-step timing information |
| `FinalOutput` | The final output produced by the execution |

Related

Last updated

Was this helpful?