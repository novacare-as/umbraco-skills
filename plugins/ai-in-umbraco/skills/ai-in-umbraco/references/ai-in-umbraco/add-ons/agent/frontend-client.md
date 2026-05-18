# Frontend Client | AI in Umbraco

Build custom agent-driven UIs using the UaiAgentClient base client.

Overview

Installation

```
Install-Package Umbraco.AI.Agent
```

```
dotnet add package Umbraco.AI.Agent
```

Import

Quick Start

API Reference

Factory Method

`UaiAgentClient.create(config, callbacks?)`

| Parameter | Type | Required | Description |
|---|---|---|---|
| `config` | `UaiAgentClientConfig` | Yes | Client configuration |
| `callbacks` | `AgentClientCallbacks` | No | Event callbacks |

Constructor

`new UaiAgentClient(transport, callbacks?)`

| Parameter | Type | Required | Description |
|---|---|---|---|
| `transport` | `AgentTransport` | Yes | Custom transport implementation |
| `callbacks` | `AgentClientCallbacks` | No | Event callbacks |

Instance Methods

`sendMessage(messages, tools?, context?)`

| Parameter | Type | Required | Description |
|---|---|---|---|
| `messages` | `UaiChatMessage[]` | Yes | Conversation messages |
| `tools` | `UaiFrontendTool[]` | No | Available frontend tools (extends AG-UI `Tool` with `scope` /`isDestructive` ) |
| `context` | `Array<{description: string, value: string}>` | No | Context items for LLM awareness |

`setCallbacks(callbacks)`

| Parameter | Type | Required | Description |
|---|---|---|---|
| `callbacks` | `AgentClientCallbacks` | Yes | New callbacks |

`reset()`

Callbacks

Text Streaming

| Callback | Parameters | Description |
|---|---|---|
| `onTextStart` | `(messageId: string) => void` | Called when a new text message starts |
| `onTextDelta` | `(delta: string) => void` | Called when a text chunk is received |
| `onTextEnd` | `() => void` | Called when text message is complete |

Tool Calls

| Callback | Parameters | Description |
|---|---|---|
| `onToolCallStart` | `(info: UaiToolCallInfo) => void` | Called when a tool call starts |
| `onToolCallArgsEnd` | `(id: string, args: string) => void` | Called when tool arguments are complete |
| `onToolCallEnd` | `(id: string) => void` | Called when tool call completes (args streamed) |
| `onToolCallResult` | `(id: string, result: string) => void` | Called when tool result is received (backend execution) |

Run Lifecycle

| Callback | Parameters | Description |
|---|---|---|
| `onRunFinished` | `(event: RunFinishedEvent) => void` | Called when the run finishes (success, interrupt, or error) |
| `onError` | `(error: Error) => void` | Called on error |

State Updates

| Callback | Parameters | Description |
|---|---|---|
| `onStateSnapshot` | `(state: UaiAgentState) => void` | Called when a state snapshot is received |
| `onStateDelta` | `(delta: Partial<UaiAgentState>) => void` | Called when a state delta is received |
| `onMessagesSnapshot` | `(messages: UaiChatMessage[]) => void` | Called when messages snapshot is received |

Custom Events

| Callback | Parameters | Description |
|---|---|---|
| `onCustomEvent` | `(name: string, value: unknown) => void` | Called when the agent emits an AG-UI `CUSTOM` event (application-specific streaming events). |

Message Format

Related

Last updated

Was this helpful?