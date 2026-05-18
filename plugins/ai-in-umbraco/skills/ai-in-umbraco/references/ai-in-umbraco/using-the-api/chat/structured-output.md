# Structured Output | AI in Umbraco

Get structured, typed responses from chat completions using output schemas.

AIOutputSchema

From a Type

```
using Umbraco.AI.Core.Chat;

public class ContentSuggestion
{
    public string Title { get; set; } = string.Empty;
    public string Summary { get; set; } = string.Empty;
    public string[] Tags { get; set; } = [];
}

var schema = AIOutputSchema.FromType<ContentSuggestion>();
```

From a JSON Schema

```
using System.Text.Json;
using Umbraco.AI.Core.Chat;

var jsonSchema = """
{
    "type": "object",
    "properties": {
        "title": { "type": "string" },
        "summary": { "type": "string" },
        "tags": {
            "type": "array",
            "items": { "type": "string" }
        }
    },
    "required": ["title", "summary"]
}
""";

var schema = AIOutputSchema.FromJsonSchema(
    JsonDocument.Parse(jsonSchema).RootElement);
```

Getting Structured Chat Responses

Reading Results

Structured Agent Responses

Setting the Schema on the Agent Config

Configuring in the Backoffice

Overriding at Runtime

Reading Agent Results

When to Use Structured Output

| Scenario | Approach |
|---|---|
| Display AI text to users | Standard chat response |
| Parse AI output in code | `.WithOutputSchema()` + `GetResult<T>()` |
| Agent pipelines and automation | Agent `OutputSchema` config or runtime override |
| Basic JSON requests | `ChatResponseFormat.Json` (see
|

Related

Last updated

Was this helpful?