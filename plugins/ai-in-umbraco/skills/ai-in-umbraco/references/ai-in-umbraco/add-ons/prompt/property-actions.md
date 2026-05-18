# Property Actions | AI in Umbraco

Use prompts directly from property editors in the backoffice.

How Property Actions Work

```
┌─────────────────────────────────────────────────────┐
│ Page Title                                    [AI ▼]│
│ ┌─────────────────────────────────────────────────┐ │
│ │ Welcome to Our Website                          │ │
│ └─────────────────────────────────────────────────┘ │
│                                                     │
│ AI Actions:                                         │
│ ├── Improve SEO                                     │
│ ├── Translate to French                             │
│ └── Generate Alternatives                           │
└─────────────────────────────────────────────────────┘
```

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-948ab55847ef7310c3e703f08e430b7a87fa4558%252Fprompt-property-action-dropdown.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=26735738&sv=2)

Compatible Property Editors

| Editor | Support |
|---|---|
| Textstring | Yes |
| Textarea | Yes |
| Rich Text Editor | Yes (with TipTap toolbar integration) |
| Markdown | Yes |
| Block List/Grid | Yes (on text properties within blocks) |

Scoping Property Actions

Allow on Specific Content Types

Allow on Specific Property Editors

Deny Specific Properties

Rich Text Editor Integration

Block Editor Support

Display Modes

| Mode | Value | Description |
|---|---|---|
| Property Action | `0` | Appears as an action button on compatible property editors |
| TipTap Tool | `1` | Appears as a toolbar button in the rich text editor |

Property Action (Default)

TipTap Tool

Context Extraction

| Context | Description |
|---|---|
| `entityId` | The content/media item ID |
| `entityType` | "document" or "media" |
| `propertyAlias` | The property being edited |
| `culture` | Current culture variant |
| `segment` | Current segment (if applicable) |
| `currentValue` | Current property value |

Applying Results

Single Property

Multiple Properties

Creating Prompts for Property Actions

1. Be Context-Aware

2. Provide Clear Output

3. Consider the Editor Experience

Managing Property Actions

Via Backoffice

Visibility

Troubleshooting

Prompt Not Appearing

Wrong Context

Related

Last updated

Was this helpful?