# AIPrompt | AI in Umbraco

Model representing a prompt template.

Namespace

```
using Umbraco.AI.Prompt.Core.Prompts;
```

Definition

```
public sealed class AIPrompt : IAIVersionableEntity
{
    public Guid Id { get; internal set; }
    public required string Alias { get; set; }
    public required string Name { get; set; }
    public string? Description { get; set; }
    public required string Instructions { get; set; }
    public Guid? ProfileId { get; set; }
    public IReadOnlyList<Guid> ContextIds { get; set; } = [];
    public IReadOnlyList<Guid> GuardrailIds { get; set; } = [];
    public IReadOnlyList<string> Tags { get; set; } = [];
    public bool IsActive { get; set; } = true;
    public bool IncludeEntityContext { get; set; } = true;
    public int OptionCount { get; set; } = 1;
    public AIPromptDisplayMode DisplayMode { get; set; } = AIPromptDisplayMode.PropertyAction;
    public AIPromptScope? Scope { get; set; }

    // Audit properties
    public DateTime DateCreated { get; init; }
    public DateTime DateModified { get; set; }
    public Guid? CreatedByUserId { get; set; }
    public Guid? ModifiedByUserId { get; set; }

    // Versioning
    public int Version { get; internal set; } = 1;
}
```

Properties

| Property | Type | Description |
|---|---|---|
| `Id` | `Guid` | Unique identifier |
| `Alias` | `string` | Unique alias for code references (required) |
| `Name` | `string` | Display name (required) |
| `Description` | `string?` | Optional description |
| `Instructions` | `string` | Prompt template text (required) |
| `ProfileId` | `Guid?` | Associated AI profile |
| `ContextIds` | `IReadOnlyList<Guid>` | AI Contexts to inject |
| `GuardrailIds` | `IReadOnlyList<Guid>` | Guardrails to evaluate during prompt execution |
| `Tags` | `IReadOnlyList<string>` | Organization tags |
| `IsActive` | `bool` | Whether prompt is available |
| `IncludeEntityContext` | `bool` | Include entity in system message |
| `OptionCount` | `int` | Number of result options to generate (0 = informational, 1 = single, 2+ = options) |
| `DisplayMode` | `AIPromptDisplayMode` | Where the prompt is shown (`PropertyAction` or `TipTapTool` ) |
| `Scope` | `AIPromptScope?` | Allow/deny rules defining where the prompt runs |
| `DateCreated` | `DateTime` | When created |
| `DateModified` | `DateTime` | When last modified |
| `CreatedByUserId` | `Guid?` | Key of the user who created the prompt |
| `ModifiedByUserId` | `Guid?` | Key of the user who last modified the prompt |
| `Version` | `int` | Current version number |

AIPromptDisplayMode

Example

AIPromptScope

Properties

| Property | Type | Description |
|---|---|---|
| `AllowRules` | `IReadOnlyList<AIPromptScopeRule>` | Whitelist of places the prompt is allowed to run |
| `DenyRules` | `IReadOnlyList<AIPromptScopeRule>` | Blacklist of places the prompt is not allowed to run |

AIPromptScopeRule

Properties

| Property | Type | Description |
|---|---|---|
| `PropertyEditorUiAliases` | `IReadOnlyList<string>?` | Property Editor UI aliases to match (e.g., `Umb.PropertyEditorUi.TextBox` ). Null or empty means any. |
| `PropertyAliases` | `IReadOnlyList<string>?` | Property aliases to match (e.g., `pageTitle` ). Null or empty means any. |
| `ContentTypeAliases` | `IReadOnlyList<string>?` | Content type aliases to match (e.g., `blogPost` ). Null or empty means any. |

Related

Last updated

Was this helpful?