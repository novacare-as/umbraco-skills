---
name: umbraco-management-api
description: >
  Reference for the Umbraco Management API — the v1 REST surface that administers an Umbraco CMS instance (the headless backoffice / management plane, distinct from the Content Delivery API and from `umbraco-ai`). Use whenever the user mentions Umbraco Management API, backoffice REST, `/umbraco/management/api/v1/`, OpenAPI/Swagger for Umbraco admin, scripted provisioning, custom backoffice UIs, or integration tests against the Umbraco backoffice; or any management domain noun: Document, Document Type, Document Blueprint, Document Version, Media, Media Type, Member, Member Type, Member Group, Template, Partial View, Script, Stylesheet, Static File, Language, Dictionary, Data Type, Relation, Relation Type, Tag, Webhook, Redirect Management, Health Check, Indexer, Searcher, Log Viewer, Telemetry, Server, Upgrade, Install, Published Cache, Imaging, Models Builder, oEmbed, Package, Property Type, Preview, User, User Group, Security, Culture, or Dynamic Root.
---

# Umbraco Management Api

The Umbraco Management API is the REST surface used by the v14+ backoffice itself and by anyone scripting administration of an Umbraco CMS instance. Every route is mounted under `/umbraco/management/api/v1/` (a handful of newer operations live at `v1.1`), is authenticated as a backoffice user or client-credentials app, and is described by the same OpenAPI document the backoffice consumes. Endpoints are grouped by domain — one file per domain in `management-api/api/endpoints/` paired with a schema file in `management-api/api/schemas/` — so most questions resolve to *one* endpoint file plus *one* schema file. Within a domain, expect a consistent shape: a paginated list, a single-item `GET/POST/PUT/DELETE` by `id` (UUIDs everywhere), tree/item/collection sub-routes for backoffice navigation, plus domain-specific verbs (e.g. `publish`, `move-to-recycle-bin`, `invite`, `change-password`). This skill is a navigator over that reference — not a tutorial — so use the routing table and read only the file(s) you need.

## How to use this skill

This skill has 2 layers. Read only what you need for the task at hand.

### Layer 1: This file (SKILL.md)
Always in context. Use the routing table below to decide which files to read next.

### Layer 2: Management Api API (management-api/api/)
Structured API specification — endpoints, parameters, request/response schemas.
Start with `management-api/api/index.md` for the table of contents, then drill into specific domain files.

## Shape of the API

**Base path:** `/umbraco/management/api/v1/` (some newer operations are versioned `v1.1`, e.g. `PUT /document/{id}/validate`). The API is the same OpenAPI/Swagger document the Umbraco backoffice ships with — Swagger UI is served at `/umbraco/swagger` on a running instance.

**Identity model:** resources are addressed by `Guid` UUIDs, not integer ids. Hierarchical resources (Document, Media, Document Type, Member Type, …) expose parallel `tree/<domain>/{root,children,ancestors,siblings}`, `item/<domain>` (lightweight item lookup, often by id list), `collection/<domain>/{id}` (paged listing under a parent), and `recycle-bin/<domain>/…` routes — mirroring the backoffice tree, item, and collection UI primitives.

**Auth:** backoffice user session for interactive use; client-credentials apps (created via `POST /user/{id}/client-credentials`) for server-to-server automation.

**Reference layout:** every domain has two files that are intended to be read together:

- `management-api/api/endpoints/<domain>.md` — every route, method, parameters, request body, response models, operation id.
- `management-api/api/schemas/<domain>.md` — the request and response model field definitions referenced from the endpoint file (e.g. `CreateDocumentRequestModel`, `PagedDocumentCollectionResponseModel`).

A few endpoint files reuse `schemas/common/index.md` instead of a domain-specific schema file (Manifest, Preview, Property Type, Segment, Static File).

## Domain map — what's exposed

Cluster the 50+ endpoint files by what a developer is actually trying to do. Each row points at the endpoint file; the matching schema file lives at the same path under `schemas/`.

| Cluster | Domains (file basename under `management-api/api/endpoints/`) |
|---|---|
| Content & structure | `document`, `document-type`, `document-blueprint`, `document-version`, `media`, `media-type`, `member`, `member-type`, `member-group` |
| Authoring assets | `template`, `partial-view`, `script`, `stylesheet`, `static-file` |
| Configuration & schema | `language`, `dictionary`, `data-type`, `property-type`, `relation`, `relation-type`, `tag`, `object-types`, `dynamic-root`, `segment`, `culture` |
| Integration & lifecycle | `webhook`, `redirect-management`, `import`, `package`, `manifest`, `models-builder`, `oembed`, `temporary-file`, `imaging`, `preview`, `published-cache` |
| Operations & diagnostics | `health-check`, `indexer`, `searcher`, `log-viewer`, `profiling`, `telemetry`, `server`, `upgrade`, `install` |
| People & access | `user`, `user-group`, `user-data`, `security` |
| Backoffice surface | `news-dashboard`, `help` |

Within a cluster the verbs are predictable. For example, `document` exposes the full lifecycle (`POST /document`, `PUT /document/{id}`, `PUT /document/{id}/publish`, `…/unpublish`, `…/move`, `…/move-to-recycle-bin`, `…/copy`, `…/public-access`, `…/notifications`, `…/audit-log`, `…/preview-url`, `…/referenced-by`, `…/validate`, plus `tree/document/*`, `item/document/*`, `collection/document/{id}`, `recycle-bin/document/*`). `user` exposes the corresponding identity lifecycle (invite, enable/disable, unlock, change-password, reset-password, 2FA, client-credentials, set-user-groups, avatar). Webhooks have logs (`/webhook/{id}/logs`, `/webhook/logs`) and a discoverable event catalogue (`/webhook/events`).

## How to navigate the bundled reference

Workflow for any Management API question:

1. Identify the **domain** from the user's wording (e.g. "create a content node" → Document; "add a webhook subscriber" → Webhook; "invite a backoffice user" → User).
2. Open `management-api/api/endpoints/<domain>.md`. The file starts with a flat list of every route in that domain — scan it first to confirm the operation exists, then jump to the section for the specific verb.
3. Open `management-api/api/schemas/<domain>.md` (or `schemas/common/index.md` for the few domains that share it) to resolve any `→ ModelName` references in the request body or response.
4. If a route references a model from another domain (e.g. a Document handler returns a `DocumentTypeReferenceModel`), follow the reference into the matching `schemas/<other>.md`.

Avoid scanning every endpoint file — the routing table in `SKILL.md` is the index, the per-domain endpoint+schema pair is the leaf. For "what operations exist for X?" questions, the **Contents** list at the top of each endpoint file is the fastest answer.

When you need a quick capability check rather than a deep read, the operation id (e.g. `GetDocumentById`, `PostWebhook`, `PutUserById`) follows a `<Verb><Resource>[By<Param>]` pattern, which makes grep across the endpoint files reliable.

## Scope — what's in this skill, and what isn't

**In scope** — the v1 (and v1.1) Umbraco Management REST surface as exposed by a stock Umbraco CMS install: every domain in the routing table above, including legacy/back-compat routes that ship in the same OpenAPI document.

**Not in scope:**

- The **Umbraco Content Delivery API** (`/umbraco/delivery/api/v*/…`) — the public read API for *published* content consumed by headless front-ends. Different audience, different auth, different routes; it is not documented here.
- The **Umbraco AI Management API** and everything under `Umbraco.AI.*` — covered by the separate `umbraco-ai` skill. Routes like `/umbraco/management/api/v1/ai/…` belong there, not here.
- The **C# service layer** of the Umbraco CMS itself — `IContentService`, `IPublishedContent`, `UmbracoApiController`, notification handlers, content events, etc. These are the in-process API used by site code and belong to the Umbraco CMS skill, not the management REST reference.
- Provisioning patterns, deployment pipelines, and Umbraco Cloud / Deploy specifics. Some endpoints touch these areas (e.g. `install`, `upgrade`, `package`), but the broader workflow is out of scope.

When a question mixes layers — e.g. "create a document from a scheduled job" — prefer the C# service layer for in-process work, and reach for this skill only when the integration genuinely lives over HTTP (external automation, custom backoffice UI, cross-environment scripting).

## Routing table

Use this table to determine which file(s) to read based on the user's question.

### Management Api API → management-api/api/

#### Top-level files in management-api/api/endpoints/

| Topic | Read file | Schemas file |
|---|---|---|
| Culture | `management-api/api/endpoints/culture.md` | `management-api/api/schemas/culture.md` |
| Data Type | `management-api/api/endpoints/data-type.md` | `management-api/api/schemas/data-type.md` |
| Dictionary | `management-api/api/endpoints/dictionary.md` | `management-api/api/schemas/dictionary.md` |
| Document Blueprint | `management-api/api/endpoints/document-blueprint.md` | `management-api/api/schemas/document-blueprint.md` |
| Document Type | `management-api/api/endpoints/document-type.md` | `management-api/api/schemas/document-type.md` |
| Document Version | `management-api/api/endpoints/document-version.md` | `management-api/api/schemas/document-version.md` |
| Document | `management-api/api/endpoints/document.md` | `management-api/api/schemas/document.md` |
| Dynamic Root | `management-api/api/endpoints/dynamic-root.md` | `management-api/api/schemas/dynamic-root.md` |
| Health Check | `management-api/api/endpoints/health-check.md` | `management-api/api/schemas/health-check.md` |
| Help | `management-api/api/endpoints/help.md` | `management-api/api/schemas/help.md` |
| Imaging | `management-api/api/endpoints/imaging.md` | `management-api/api/schemas/imaging.md` |
| Import | `management-api/api/endpoints/import.md` | `management-api/api/schemas/import.md` |
| Indexer | `management-api/api/endpoints/indexer.md` | `management-api/api/schemas/indexer.md` |
| Install | `management-api/api/endpoints/install.md` | `management-api/api/schemas/install.md` |
| Language | `management-api/api/endpoints/language.md` | `management-api/api/schemas/language.md` |
| Log Viewer | `management-api/api/endpoints/log-viewer.md` | `management-api/api/schemas/log-viewer.md` |
| Manifest | `management-api/api/endpoints/manifest.md` | `management-api/api/schemas/common/index.md` |
| Media Type | `management-api/api/endpoints/media-type.md` | `management-api/api/schemas/media-type.md` |
| Media | `management-api/api/endpoints/media.md` | `management-api/api/schemas/media.md` |
| Member Group | `management-api/api/endpoints/member-group.md` | `management-api/api/schemas/member-group.md` |
| Member Type | `management-api/api/endpoints/member-type.md` | `management-api/api/schemas/member-type.md` |
| Member | `management-api/api/endpoints/member.md` | `management-api/api/schemas/member.md` |
| Models Builder | `management-api/api/endpoints/models-builder.md` | `management-api/api/schemas/models-builder.md` |
| News Dashboard | `management-api/api/endpoints/news-dashboard.md` | `management-api/api/schemas/news-dashboard.md` |
| Object Types | `management-api/api/endpoints/object-types.md` | `management-api/api/schemas/object-types.md` |
| oEmbed | `management-api/api/endpoints/oembed.md` | `management-api/api/schemas/oembed.md` |
| Package | `management-api/api/endpoints/package.md` | `management-api/api/schemas/package.md` |
| Partial View | `management-api/api/endpoints/partial-view.md` | `management-api/api/schemas/partial-view.md` |
| Preview | `management-api/api/endpoints/preview.md` | `management-api/api/schemas/common/index.md` |
| Profiling | `management-api/api/endpoints/profiling.md` | `management-api/api/schemas/profiling.md` |
| Property Type | `management-api/api/endpoints/property-type.md` | `management-api/api/schemas/common/index.md` |
| Published Cache | `management-api/api/endpoints/published-cache.md` | `management-api/api/schemas/published-cache.md` |
| Redirect Management | `management-api/api/endpoints/redirect-management.md` | `management-api/api/schemas/redirect-management.md` |
| Relation Type | `management-api/api/endpoints/relation-type.md` | `management-api/api/schemas/relation-type.md` |
| Relation | `management-api/api/endpoints/relation.md` | `management-api/api/schemas/relation.md` |
| Script | `management-api/api/endpoints/script.md` | `management-api/api/schemas/script.md` |
| Searcher | `management-api/api/endpoints/searcher.md` | `management-api/api/schemas/searcher.md` |
| Security | `management-api/api/endpoints/security.md` | `management-api/api/schemas/security.md` |
| Segment | `management-api/api/endpoints/segment.md` | `management-api/api/schemas/common/index.md` |
| Server | `management-api/api/endpoints/server.md` | `management-api/api/schemas/server.md` |
| Static File | `management-api/api/endpoints/static-file.md` | `management-api/api/schemas/common/index.md` |
| Stylesheet | `management-api/api/endpoints/stylesheet.md` | `management-api/api/schemas/stylesheet.md` |
| Tag | `management-api/api/endpoints/tag.md` | `management-api/api/schemas/tag.md` |
| Telemetry | `management-api/api/endpoints/telemetry.md` | `management-api/api/schemas/telemetry.md` |
| Template | `management-api/api/endpoints/template.md` | `management-api/api/schemas/template.md` |
| Temporary File | `management-api/api/endpoints/temporary-file.md` | `management-api/api/schemas/temporary-file.md` |
| Upgrade | `management-api/api/endpoints/upgrade.md` | `management-api/api/schemas/upgrade.md` |
| User Data | `management-api/api/endpoints/user-data.md` | `management-api/api/schemas/user-data.md` |
| User Group | `management-api/api/endpoints/user-group.md` | `management-api/api/schemas/user-group.md` |
| User | `management-api/api/endpoints/user.md` | `management-api/api/schemas/user.md` |
| Webhook | `management-api/api/endpoints/webhook.md` | `management-api/api/schemas/webhook.md` |
