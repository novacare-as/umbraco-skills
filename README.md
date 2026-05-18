# Umbraco Skills

A [Claude Code plugin marketplace](https://docs.claude.com/en/docs/claude-code/plugin-marketplaces) by [Novacare AS](https://novacare.no) that bundles agent skills covering the Umbraco CMS ecosystem. Install the marketplace once and the three skills become available as routing references whenever you work on Umbraco code.

## Plugins

| Plugin | What it covers |
|---|---|
| [`umbraco-cms`](./plugins/umbraco-cms) | Umbraco CMS itself — backoffice, document/data types, property editors, Razor templating, `IPublishedContent` / `IContentService`, composers, notifications, controllers, custom routing, the Lit-based backoffice extension API, Examine, Content Delivery API. Mirrors `docs.umbraco.com/umbraco-cms`. |
| [`umbraco-management-api`](./plugins/umbraco-management-api) | The v1 REST surface under `/umbraco/management/api/v1/` — every endpoint and schema for the backoffice management plane (documents, media, members, users, webhooks, health checks, …). |
| [`ai-in-umbraco`](./plugins/ai-in-umbraco) | Umbraco.AI — the provider-agnostic AI integration layer built on `Microsoft.Extensions.AI`. Providers, connections, profiles and aliases, `IAIChatService` / `IAIEmbeddingService`, guardrails, contexts, the AI backoffice section and add-ons. |

Each plugin contains a single skill with a routing table in `SKILL.md` and the underlying reference content under `references/` (or `management-api/api/` for the REST surface). The skills are designed to be read by Claude on demand — `SKILL.md` is always loaded, and deeper files are pulled in only when the question warrants it.

## Installation

Add the marketplace inside Claude Code:

```
/plugin marketplace add novacare-as/umbraco-skills
```

Then install the plugins you want:

```
/plugin install umbraco-cms@umbraco-skills
/plugin install umbraco-management-api@umbraco-skills
/plugin install ai-in-umbraco@umbraco-skills
```

Skills activate automatically when the conversation matches their description — there is no slash command to invoke.

## Repository layout

```
.claude-plugin/
  marketplace.json          # Marketplace manifest listing the three plugins
plugins/
  umbraco-cms/
    .claude-plugin/plugin.json
    skills/umbraco-cms/
      SKILL.md
      references/…          # Umbraco CMS docs, mirroring docs.umbraco.com
  umbraco-management-api/
    .claude-plugin/plugin.json
    skills/umbraco-management-api/
      SKILL.md
      management-api/api/   # Endpoint + schema reference per domain
  ai-in-umbraco/
    .claude-plugin/plugin.json
    skills/ai-in-umbraco/
      SKILL.md
      references/…          # Umbraco.AI docs
```

## License

See individual plugins for upstream documentation attribution. Skill content is derived from the official Umbraco documentation.
