# Notifications | AI in Umbraco

Subscribe to entity lifecycle events in Umbraco.AI to add custom validation, audit logging, and automation.

Notification Types

| Notification Type | When Published | Cancelable | Use Cases |
|---|---|---|---|
| Saving | Before entity is saved | ✅ Yes | Validation, business rules, pre-save modifications |
| Saved | After entity is saved | ❌ No | Audit logging, cache invalidation, webhooks |
| Deleting | Before entity is deleted | ✅ Yes | Dependency checks, confirmation prompts |
| Deleted | After entity is deleted | ❌ No | Cleanup, cascade deletes, audit logs |
| Rolling Back | Before version rollback | ✅ Yes | Permission checks, validation |
| Rolled Back | After version rollback | ❌ No | Audit logging, notifications |
| Executing | Before execution starts | ✅ Yes | Rate limiting, authorization, resource checks |
| Executed | After execution completes | ❌ No | Usage tracking, performance metrics, billing |

Entities with Notifications

Core Entities (Umbraco.AI)

Prompt Add-on (Umbraco.AI.Prompt)

Agent Add-on (Umbraco.AI.Agent)

Quick Example

Cancelable vs Stateful Notifications

Cancelable Notifications (Before Operations)

Stateful Notifications (After Operations)

State Propagation

Architecture

In This Section

Last updated

Was this helpful?

## Sub-topics

- [Entity Lifecycle Notifications | AI in Umbraco](notifications/entity-notifications.md)
