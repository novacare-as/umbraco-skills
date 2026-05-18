# Entity Lifecycle Notifications | AI in Umbraco

Complete reference for all entity lifecycle notifications in Umbraco.AI.

Notification Categories

| Entity | Save/Delete | Rollback | Execution |
|---|---|---|---|
| AIProfile | ✅ | ✅ | - |
| AIConnection | ✅ | ✅ | - |
| AIContext | ✅ | ✅ | - |
| AIGuardrail | ✅ | ✅ | - |
| AITest | ✅ | ✅ | - |
| AISettings | ✅ (Save only) | - | - |
| AIPrompt | ✅ | - | ✅ |
| AIAgent | ✅ | - | ✅ |
| AIChat (Inline) | - | - | ✅ |
| AISpeechToText (Inline) | - | - | ✅ |
| AIEmbedding (Inline) | - | - | ✅ |

AIProfile Notifications

AIProfileSavingNotification (Cancelable)

AIProfileSavedNotification (Non-Cancelable)

Other AIProfile Notifications

| Notification | Cancelable | Properties |
|---|---|---|
| `AIProfileDeletingNotification` | Yes | `EntityId` (Guid), `Messages` , `Cancel` |
| `AIProfileDeletedNotification` | No | `EntityId` (Guid), `Messages` |
| `AIProfileRollingBackNotification` | Yes | `ProfileId` (Guid), `TargetVersion` (int), `Messages` , `Cancel` |
| `AIProfileRolledBackNotification` | No | `Profile` (AIProfile), `TargetVersion` (int), `Messages` |

AIConnection Notifications

| Notification | Cancelable | Key Properties |
|---|---|---|
| `AIConnectionSavingNotification` | Yes | `Entity` (AIConnection), `Messages` , `Cancel` |
| `AIConnectionSavedNotification` | No | `Entity` (AIConnection), `Messages` |
| `AIConnectionDeletingNotification` | Yes | `EntityId` (Guid), `Messages` , `Cancel` |
| `AIConnectionDeletedNotification` | No | `EntityId` (Guid), `Messages` |
| `AIConnectionRollingBackNotification` | Yes | `ConnectionId` (Guid), `TargetVersion` (int), `Messages` , `Cancel` |
| `AIConnectionRolledBackNotification` | No | `Connection` (AIConnection), `TargetVersion` (int), `Messages` |

AIContext Notifications

| Notification | Cancelable | Key Properties |
|---|---|---|
| `AIContextSavingNotification` | Yes | `Entity` (AIContext), `Messages` , `Cancel` |
| `AIContextSavedNotification` | No | `Entity` (AIContext), `Messages` |
| `AIContextDeletingNotification` | Yes | `EntityId` (Guid), `Messages` , `Cancel` |
| `AIContextDeletedNotification` | No | `EntityId` (Guid), `Messages` |
| `AIContextRollingBackNotification` | Yes | `ContextId` (Guid), `TargetVersion` (int), `Messages` , `Cancel` |
| `AIContextRolledBackNotification` | No | `Context` (AIContext), `TargetVersion` (int), `Messages` |

AIPrompt Notifications

| Notification | Cancelable | Key Properties |
|---|---|---|
| `AIPromptSavingNotification` | Yes | `Entity` (AIPrompt), `Messages` , `Cancel` |
| `AIPromptSavedNotification` | No | `Entity` (AIPrompt), `Messages` |
| `AIPromptDeletingNotification` | Yes | `EntityId` (Guid), `Messages` , `Cancel` |
| `AIPromptDeletedNotification` | No | `EntityId` (Guid), `Messages` |
| `AIPromptExecutingNotification` | Yes | `Prompt` (AIPrompt), `Request` (AIPromptExecutionRequest), `Messages` , `Cancel` |
| `AIPromptExecutedNotification` | No | `Prompt` (AIPrompt), `Request` (AIPromptExecutionRequest), `Result` (AIPromptExecutionResult), `Messages` |

AIAgent Notifications

| Notification | Cancelable | Key Properties |
|---|---|---|
| `AIAgentSavingNotification` | Yes | `Entity` (AIAgent), `Messages` , `Cancel` |
| `AIAgentSavedNotification` | No | `Entity` (AIAgent), `Messages` |
| `AIAgentDeletingNotification` | Yes | `EntityId` (Guid), `Messages` , `Cancel` |
| `AIAgentDeletedNotification` | No | `EntityId` (Guid), `Messages` |
| `AIAgentExecutingNotification` | Yes | `Agent` (AIAgent), `ChatMessages` (IReadOnlyList<ChatMessage>), `Messages` , `Cancel` |
| `AIAgentExecutedNotification` | No | `Agent` (AIAgent), `ChatMessages` (IReadOnlyList<ChatMessage>), `Duration` (TimeSpan), `IsSuccess` (bool), `Messages` |

AIGuardrail Notifications

| Notification | Cancelable | Key Properties |
|---|---|---|
| `AIGuardrailSavingNotification` | Yes | `Entity` (AIGuardrail), `Messages` , `Cancel` |
| `AIGuardrailSavedNotification` | No | `Entity` (AIGuardrail), `Messages` |
| `AIGuardrailDeletingNotification` | Yes | `EntityId` (Guid), `Messages` , `Cancel` |
| `AIGuardrailDeletedNotification` | No | `EntityId` (Guid), `Messages` |
| `AIGuardrailRollingBackNotification` | Yes | `GuardrailId` (Guid), `TargetVersion` (int), `Messages` , `Cancel` |
| `AIGuardrailRolledBackNotification` | No | `Guardrail` (AIGuardrail), `TargetVersion` (int), `Messages` |

AITest Notifications

| Notification | Cancelable | Key Properties |
|---|---|---|
| `AITestSavingNotification` | Yes | `Entity` (AITest), `Messages` , `Cancel` |
| `AITestSavedNotification` | No | `Entity` (AITest), `Messages` |
| `AITestDeletingNotification` | Yes | `EntityId` (Guid), `Messages` , `Cancel` |
| `AITestDeletedNotification` | No | `EntityId` (Guid), `Messages` |
| `AITestRollingBackNotification` | Yes | `TestId` (Guid), `TargetVersion` (int), `Messages` , `Cancel` |
| `AITestRolledBackNotification` | No | `TestId` (Guid), `TargetVersion` (int), `Messages` |

AISettings Notifications

| Notification | Cancelable | Key Properties |
|---|---|---|
| `AISettingsSavingNotification` | Yes | `Entity` (AISettings), `Messages` , `Cancel` |
| `AISettingsSavedNotification` | No | `Entity` (AISettings), `Messages` |

Inline Chat Notifications

| Notification | Cancelable | Key Properties |
|---|---|---|
| `AIChatExecutingNotification` | Yes | `ChatId` (Guid), `Alias` (string), `Name` (string), `ProfileId` (Guid?), `Messages` , `Cancel` |
| `AIChatExecutedNotification` | No | `ChatId` (Guid), `Alias` (string), `Name` (string), `ProfileId` (Guid?), `Duration` (TimeSpan), `IsSuccess` (bool), `Messages` |

Inline Speech-to-Text Notifications

| Notification | Cancelable | Key Properties |
|---|---|---|
| `AISpeechToTextExecutingNotification` | Yes | `TranscriptionId` (Guid), `Alias` (string), `Name` (string), `ProfileId` (Guid?), `Messages` , `Cancel` |
| `AISpeechToTextExecutedNotification` | No | `TranscriptionId` (Guid), `Alias` (string), `Name` (string), `ProfileId` (Guid?), `Duration` (TimeSpan), `IsSuccess` (bool), `Messages` |

Inline Embedding Notifications

| Notification | Cancelable | Key Properties |
|---|---|---|
| `AIEmbeddingExecutingNotification` | Yes | `EmbeddingId` (Guid), `Alias` (string), `Name` (string), `ProfileId` (Guid?), `Messages` , `Cancel` |
| `AIEmbeddingExecutedNotification` | No | `EmbeddingId` (Guid), `Alias` (string), `Name` (string), `ProfileId` (Guid?), `Duration` (TimeSpan), `IsSuccess` (bool), `Messages` |

Base Notification Classes

| Base Class | Kind | Key Properties |
|---|---|---|
| `AIEntitySavingNotification<T>` | Cancelable | `Entity` (T), `Messages` , `Cancel` |
| `AIEntitySavedNotification<T>` | Stateful | `Entity` (T), `Messages` |
| `AIEntityDeletingNotification<T>` | Cancelable | `EntityId` (Guid), `Messages` , `Cancel` |
| `AIEntityDeletedNotification<T>` | Stateful | `EntityId` (Guid), `Messages` |

Registration

Best Practices

Last updated

Was this helpful?