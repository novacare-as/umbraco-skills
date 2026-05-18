# UaiAgentRepository | AI in Umbraco

Read-only repository for fetching active agents in frontend components.

Overview

Installation

Import

Quick Start

API Reference

Constructor

`new UaiAgentRepository(host)`

| Parameter | Type | Required | Description |
|---|---|---|---|
| `host` | `UmbControllerHost` | Yes | Umbraco controller host (typically `this` in a Lit element) |

Methods

`fetchActiveAgents(options?)`

| Parameter | Type | Required | Description |
|---|---|---|---|
| `options` | `UaiAgentRepositoryOptions` | No | Filtering and pagination options |

`initialize()`

Observable

`agentItems$`

Options

UaiAgentRepositoryOptions

Response Model

UaiAgentItemModel

Complete Examples

Agent Dropdown Picker

Agent List with Filtering

Reactive Agent Count

Error Handling

When to Use This Repository

Related Repositories

| Repository | Purpose | Use Case |
|---|---|---|
| `UaiAgentRepository` | Read-only active agents | Pickers, dropdowns, lists |
| `UaiAgentDetailRepository` | Full CRUD operations | Agent editor, management dashboard |
| `UaiAgentCollectionRepository` | Collection view patterns | Agent list view with sorting/filtering |

Related

Last updated

Was this helpful?