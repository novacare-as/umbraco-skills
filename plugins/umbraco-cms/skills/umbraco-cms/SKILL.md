---
name: umbraco-cms
description: >
  Reference for Umbraco CMS — the open source .NET CMS at docs.umbraco.com/umbraco-cms. Use whenever the user mentions Umbraco, Umbraco CMS, the backoffice, document types, data types, property editors, the block list / block grid / rich text editors, members, media, dictionary items, languages and culture variants, Razor templating, `IPublishedContent`, `UmbracoHelper`, `IPublishedContentQuery`, `IContentService`, `IMediaService`, `IMemberService`, `RenderController` route hijacking, `SurfaceController`, `UmbracoApiController`, `IComposer` / `IUserComposer`, `IContentFinder`, `IUrlProvider`, `INotificationHandler` and `ContentSavingNotification` / `ContentPublishedNotification`, the new Lit-based backoffice extension API and `umbraco-package.json` manifests, dashboards, sections, workspaces, contexts, Models Builder, Examine search, Content Delivery API, custom routing, health checks, packages, webhooks, configuration, security, Umbraco upgrades, multisite, and CMS tutorials.
---

# Umbraco Cms

Umbraco CMS is an open source ASP.NET Core content management system. Editors work in the **backoffice** with content modeled by **Document Types** (content types) made of **Data Types** and rendered through **Razor templates**; developers extend Umbraco at three levels — the **C# integration layer** (services, composers, controllers, notifications) for server-side logic, the **Razor / templating layer** for output, and the new **Lit-based backoffice extension API** (manifest-driven web components) for custom UI. Two flavours of "content" are easy to conflate and matter throughout: **persisted** content accessed through `IContentService` (writeable, includes drafts) versus **published** content accessed through `IPublishedContent` / `UmbracoHelper` / `IPublishedContentQuery` (read-only, cached, what the front-end renders). This skill covers the broad CMS surface; see the **Scope** section for sibling skills that cover the Management REST API and Umbraco.AI separately.

## How to use this skill

This skill has 2 layers. Read only what you need for the task at hand.

### Layer 1: This file (SKILL.md)
Always in context. Use the routing table below to decide which files to read next.

### Layer 2: Documentation (references/)
Conceptual documentation — how things work, best practices, guides.
Read these when the user asks "how does X work" or "what's the best way to do Y".

## Mental model — content tree, document types, published vs persisted

Everything in Umbraco hangs off a **content tree** of nodes. Each node has a **Document Type** (sometimes called a content type / doctype) which defines its **properties**; each property is backed by a **Data Type**, which is a configured instance of a **Property Editor** (Textstring, Block List, Block Grid, Rich Text, Markdown, Media Picker, etc.). The same shape applies to **Media** (Media Types, `IMediaService`) and **Members** (Member Types, `IMemberService`).

Two content APIs exist side by side and are not interchangeable:

- **Persisted** content — `IContentService` and `IContent`. Writeable, includes unpublished drafts, used from composers, notification handlers, and admin code. Triggers events / notifications on save & publish.
- **Published** content — `IPublishedContent`, `UmbracoHelper`, `IPublishedContentQuery`. Read-only and cache-backed; this is what Razor views and the front-end render. Strongly-typed access goes through **Models Builder** generated classes.

A third front-end surface is the **Content Delivery API** (the read-only headless JSON layer over published content). Editor-side actions create **drafts** in `IContentService`; **publishing** copies the values into the published cache where `IPublishedContent` exposes them. Multilingual sites use **languages** + **culture variants** on properties; reusable text uses **Dictionary items**. Notification names follow the pattern `<Service><Verb>ingNotification` (cancellable, before) and `<Service><Verb>edNotification` (after) — e.g. `ContentSavingNotification`, `ContentPublishedNotification`.

## C# integration surfaces — which interface for which job

All major surfaces live under `Umbraco.Cms.Core.*` and are resolved via constructor DI. Pick the right one for the job:

| Interface / base class | Namespace (typical) | Use for |
|---|---|---|
| `IContentService` | `Umbraco.Cms.Core.Services` | CRUD on persisted content, including drafts; publish/unpublish; admin scripts. |
| `IMediaService` | `Umbraco.Cms.Core.Services` | CRUD on media items and folders. |
| `IMemberService` / `IMemberGroupService` / `IMemberTypeService` | `Umbraco.Cms.Core.Services` | Members and member groups (front-end auth audience). |
| `IContentTypeService` / `IDataTypeService` | `Umbraco.Cms.Core.Services` | Programmatically read/manage Document Types and Data Types. |
| `ILocalizationService` | `Umbraco.Cms.Core.Services` | Languages and dictionary items. |
| `IPublishedContent` | `Umbraco.Cms.Core.Models.PublishedContent` | The published-cache view of a node — what views render. |
| `UmbracoHelper` / `IPublishedContentQuery` | `Umbraco.Cms.Web.Common` | Convenience query API over the published cache (`Content(id)`, `ContentAtRoot()`, `Search()`). |
| `RenderController` | `Umbraco.Cms.Web.Common.Controllers` | Inherit + name `[DocumentTypeAlias]Controller` to hijack the front-end route for a doctype. |
| `SurfaceController` | `Umbraco.Cms.Web.Website.Controllers` | Front-end form posts and child actions inside an Umbraco-rendered page. |
| `UmbracoApiController` | `Umbraco.Cms.Web.Common.Controllers` | Custom JSON endpoints under `/umbraco/api/` (front-end) or `/umbraco/backoffice/api/` (backoffice-auth). |
| `IComposer` / `IUserComposer` / `ComponentComposer` | `Umbraco.Cms.Core.Composing` | Compose at startup — register services, notification handlers, and collections via `IUmbracoBuilder`. `IUserComposer` runs after core composers so it can override. |
| `INotificationHandler<T>` / `INotificationAsyncHandler<T>` | `Umbraco.Cms.Core.Events` | Hook before/after notifications (`ContentSavingNotification`, `ContentPublishedNotification`, `MediaSavedNotification`, …). Cancel inside the *-ing notifications via `CancelOperation`. |
| `IContentFinder` | `Umbraco.Cms.Core.Routing` | Custom logic for resolving an inbound URL to an `IPublishedContent`. |
| `IUrlProvider` | `Umbraco.Cms.Core.Routing` | Custom outbound URL generation (the inverse of `IContentFinder`). |
| `IExamineManager` / `ISearcher` | `Umbraco.Cms.Infrastructure.Examine` | Lucene-based search over the External / Internal / Members indexes. |
| `AppCaches` / `ICacheRefresher` | `Umbraco.Cms.Core.Cache` | Application caches and distributed cache invalidation. |

Typical pattern: an `IComposer` runs at startup and calls `builder.AddNotificationHandler<ContentSavingNotification, MyHandler>()` to wire up an `INotificationHandler`. Constructor injection then provides whatever services that handler needs.

## Backoffice extensibility — the Lit-based extension API

The current Umbraco backoffice is a **TypeScript + Lit web-component** SPA driven by JSON manifests, not the older AngularJS extension model. If a question references AngularJS controllers, `package.manifest`, or `editorState.current` — that is the **legacy** model and applies only to Umbraco 10/below; on current Umbraco the extension story is entirely different.

Key concepts in the new model:

- **`umbraco-package.json` manifest** at the package root declares the package and its extensions. Entry points (`backofficeEntryPoint`) load JS modules at boot.
- **Extensions are typed registrations.** Each extension declares a `type` (see table below), an `alias`, optional `conditions` (when to show it), and a JS `element` (a Lit web component) or controller class.
- **Contexts** (`umb-context`) are the dependency-injection / pub-sub system between extensions — workspace context, entity context, modal context, etc. Extensions consume contexts via `consumeContext` mixins.

Most-used extension types (non-exhaustive — see `customizing/extending-overview/extension-types/`):

| Type | Adds | Read |
|---|---|---|
| `section` | A top-level section in the backoffice nav (like Content / Media). | `customizing/extending-overview/extension-types/sections/` |
| `dashboard` | A landing tab inside a section. | `customizing/extending-overview/extension-types/dashboard.md` |
| `workspace` / `workspaceView` / `workspaceAction` | The editor and its tabs / action buttons for an entity type. | `customizing/extending-overview/extension-types/workspaces/` |
| `propertyEditorUi` / `propertyEditorSchema` | A backoffice editor (UI + the data-side schema). | `customizing/property-editors/` |
| `headerApp`, `menu`, `entityAction`, `modal` | Header buttons, tree menus, entity-level actions, modal dialogs. | `customizing/extending-overview/extension-types/` |
| `globalContext`, `entryPoint`, `condition` | Cross-cutting contexts, JS bootstrap, show/hide rules. | `customizing/extending-overview/extension-types/` |
| `repository`, `store` | Data access plumbing for custom entity types. | `customizing/foundation/` |

The `customizing/utilities/` area documents the helper functions / mixins available to extension authors. The `customizing/foundation/` area covers cross-cutting infrastructure (localization, repositories, modals, observables). For runnable end-to-end examples, the tutorials at `tutorials/creating-a-property-editor/` and `tutorials/creating-a-custom-dashboard/` are the most direct path in.

## Where to look for what

Skill content mirrors the upstream `docs.umbraco.com/umbraco-cms/` tree. Use this map before grepping:

| When the question is about… | Look in… |
|---|---|
| Installing, hosting, requirements, upgrading | `fundamentals/setup/` |
| Backoffice features (sections, login, sidebar, variants, document blueprints) | `fundamentals/backoffice/` |
| Content modeling (document types, data types, media, members, dictionary, relations, languages, scheduled publishing) | `fundamentals/data/` |
| Razor / RenderMVC / partial views / layouts | `fundamentals/design/` |
| Writing C# code against Umbraco (services, debugging, notifications, source control, forms) | `fundamentals/code/` |
| Composers, runtime levels, `IUmbracoBuilder`, collections | `implementation/composing.md` |
| `RenderController`, `SurfaceController`, `UmbracoApiController`, custom routes | `implementation/controllers.md`, `implementation/custom-routing/`, `reference/routing/` |
| Service-injection patterns, custom `IContentFinder` / `IUrlProvider` | `implementation/services/`, `reference/management/using-services/` |
| Examine indexes and searching | `reference/searching/examine/` |
| Application cache, `ICacheRefresher`, `IServerMessenger` | `reference/cache/` |
| Built-in property editors (Block List, Block Grid, Rich Text, Markdown, Media Picker, …) | `fundamentals/backoffice/property-editors/` |
| Building a property editor UI (Lit) | `customizing/property-editors/`, `tutorials/creating-a-property-editor/` |
| Backoffice extension types (sections, dashboards, workspaces, menus, entity actions, modals) | `customizing/extending-overview/extension-types/` |
| Notifications catalogue (which notification fires when) | `reference/notifications/` |
| Webhooks | `reference/webhooks/` |
| Health checks, packages, file-system providers, server events | `extending/` |
| Security, auth, two-factor, external login providers, password reset | `reference/security/` |
| Configuration (`appsettings.json` Umbraco section) | `reference/configuration/` |
| Content Delivery API (headless read API) | `reference/content-delivery-api/` |
| Pointers to the Management API (admin REST surface) | `reference/management-api/` (then defer to the `umbraco-management-api` skill) |
| End-to-end walkthroughs | `tutorials/` |

## Scope and sibling skills

**In scope** — the entire `docs.umbraco.com/umbraco-cms/` documentation set: backoffice, content modeling, Razor templating, C# integration (services, composers, controllers, notifications, custom routing, content finders, URL providers), the new Lit-based backoffice extension API, Examine search, application cache, configuration, security, webhooks, packages and extending APIs, the Content Delivery API at a conceptual level, and the bundled tutorials.

**Deferred to sibling skills** — do **not** duplicate; route the user to them:

- `umbraco-management-api` — the Backoffice Management REST API (endpoints under `/umbraco/management/api/v1/...`), schemas, and OpenAPI spec. Use that skill for any question about admin REST endpoints, Postman flows, or generating clients against the Management API.
- `ai-in-umbraco` — Umbraco.AI: the provider-agnostic AI layer (`Umbraco.AI.Core` + provider packages, profiles / aliases, `IAIChatService`, guardrails, contexts, the AI backoffice section, AI add-ons).

**Out of scope** (separate Umbraco products with their own docs / skills if any):

- Umbraco Forms
- Umbraco Commerce
- Umbraco Workflow
- Umbraco Heartcore (the SaaS headless product — distinct from the open source CMS)
- Umbraco Cloud (the hosting product) and Umbraco Deploy beyond what the CMS docs reference
- Umbraco UI Library / Bellissima as standalone design-system topics (covered only where the CMS docs reference them under `customizing/ui-library.md`)

If a user question straddles boundaries (e.g. "How do I publish a document via REST?"), use this skill for the conceptual model — Documents, Document Types, publish vs. save semantics — and hand off to `umbraco-management-api` for the exact endpoint and payload.

## Routing table

Use this table to determine which file(s) to read based on the user's question.

### Documentation → references/

Routing is split by area — read the index for the area you need (every area has the full topic list for that subdirectory):

- **Umbraco Cms** → `references/umbraco-cms/index.md` (540 topics)
