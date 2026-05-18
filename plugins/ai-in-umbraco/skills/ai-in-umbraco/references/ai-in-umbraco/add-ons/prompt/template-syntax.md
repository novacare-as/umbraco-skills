# Template Syntax | AI in Umbraco

Variable interpolation syntax for prompt templates.

Basic Variables

```
Translate the following text to {{language}}:

{{text}}
```

Nested Paths

```
User: {{user.name}}
Email: {{user.email}}
Company: {{user.company.name}}
```

Dictionary and Array Access

Image Variables

Executing Prompts

From Property Actions

From Code

| Property | Type | Required | Description |
|---|---|---|---|
| `EntityId` | `Guid` | Yes | Entity (document, media, etc.) key |
| `EntityType` | `string` | Yes | Entity type, for example `document` or `media` |
| `PropertyAlias` | `string` | Yes | Property alias being edited |
| `ContentTypeAlias` | `string` | Yes | Content type alias (or element type alias for blocks) |
| `ElementId` | `Guid?` | No | Block content key when executing inside a block element |
| `ElementType` | `string?` | No | Element type when executing inside a block element |
| `Culture` | `string?` | No | Culture/language variant |
| `Segment` | `string?` | No | Segment variant |
| `Context` | `IReadOnlyList<AIRequestContextItem>?` | No | Frontend context items processed by runtime context contributors |

Passing Custom Context

Combining Variables

Best Practices

Be Explicit

Document Variables

Structure Complex Templates

Related

Last updated

Was this helpful?