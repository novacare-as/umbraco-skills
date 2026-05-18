# Custom Guardrail Evaluators | AI in Umbraco

Create custom guardrail evaluators to enforce domain-specific safety and compliance rules.

Overview

Creating a Code-Based Evaluator

Step 1: Define Configuration

```
using Umbraco.AI.Core.EditableModels;

public class ProfanityFilterConfig
{
    [AIField(
        Label = "Word List",
        Description = "Comma-separated list of words to flag",
        EditorUiAlias = "Umb.PropertyEditorUi.TextArea",
        SortOrder = 1)]
    public string WordList { get; set; } = string.Empty;

    [AIField(
        Label = "Ignore Case",
        Description = "Case-insensitive matching",
        EditorUiAlias = "Umb.PropertyEditorUi.Toggle",
        SortOrder = 2)]
    public bool IgnoreCase { get; set; } = true;
}
```

Step 2: Implement the Evaluator

Creating a Model-Based Evaluator

Evaluator Registration

AIGuardrailResult

| Property | Type | Description |
|---|---|---|
| `EvaluatorId` | `string` | ID of the evaluator that produced this result |
| `Flagged` | `bool` | Whether the content was flagged |
| `Score` | `double?` | Confidence score (0-1). Code-based evaluators typically return 0 or 1 |
| `Reason` | `string?` | Human-readable explanation |
| `Metadata` | `JsonElement?` | Evaluator-specific metadata (matched patterns, LLM reasoning, etc.) |

Built-in Evaluators

| ID | Name | Type | Description |
|---|---|---|---|
| `contains` | Contains | Code-based | Flags content containing a specific substring |
| `regex` | Regex Match | Code-based | Flags content matching a regular expression pattern |
| `llm-judge` | LLM Safety Judge | Model-based | Uses an AI model to evaluate content for safety and compliance |

Related

Last updated

Was this helpful?