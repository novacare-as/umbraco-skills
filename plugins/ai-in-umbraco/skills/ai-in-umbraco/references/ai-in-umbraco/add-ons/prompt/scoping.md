# Scoping | AI in Umbraco

Control where a prompt is allowed to run using allow and deny rules.

How Scoping Works

| Property | Description |
|---|---|
| `ContentTypeAliases` | Document, media, member, or element type aliases to match |
| `PropertyAliases` | Property aliases to match (for example `pageTitle` , `summary` ) |
| `PropertyEditorUiAliases` | Property Editor UI aliases (for example `Umb.PropertyEditorUi.TextBox` ) |

Configuring Scope

Via Backoffice

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-8c3465138261b7c2bbbbfb9938d1222f8742759a%252Fprompt-availability-scopes.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3e57fa2a&sv=2)

Via Code

Via API

Scope Model

Examples

Allow on specific content types

Allow on specific property editors

Combine constraints within a rule

Allow and deny combined

Enforcement

Related

Last updated

Was this helpful?