# Provider Settings | AI in Umbraco

Define provider settings with automatic UI generation.

AIFieldAttribute

```
[AIField(
    Label = "Display Label",           // Shown in the UI
    Description = "Help text",         // Description below the field
    EditorUiAlias = "Umb.PropertyEditorUi.TextBox",  // Umbraco editor
    SortOrder = 1                       // Display order
)]
public string? MyProperty { get; set; } = "default";  // Set defaults on the property itself
```

Properties

| Property | Type | Description |
|---|---|---|
| `Label` | `string` | Display label in the UI |
| `Description` | `string` | Help text shown below the field |
| `EditorUiAlias` | `string` | Umbraco property editor UI alias |
| `EditorConfig` | `string` | Configuration for the editor UI |
| `SortOrder` | `int` | Order in which settings are displayed |
| `IsSensitive` | `bool` | Marks the field as sensitive (value masked in UI) |
| `Group` | `string` | Groups settings under a collapsible heading |

Automatic Type Inference

| C# Type | Inferred Editor |
|---|---|
| `string` | `Umb.PropertyEditorUi.TextBox` |
| `int` | `Umb.PropertyEditorUi.Integer` |
| `bool` | `Umb.PropertyEditorUi.Toggle` |
| `decimal` , `float` , `double` | `Umb.PropertyEditorUi.Decimal` |

Example Settings Class

Validation Attributes

Configuration References

Sensitive Settings

Custom Editors

Accessing Settings in Capabilities

Last updated

Was this helpful?