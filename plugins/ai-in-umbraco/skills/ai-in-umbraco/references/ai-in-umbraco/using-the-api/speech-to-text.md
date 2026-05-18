# Speech-to-Text | AI in Umbraco

Transcribe audio files to text using the Speech-to-Text API.

IAISpeechToTextService

```
public interface IAISpeechToTextService
{
    Task<SpeechToTextResponse> TranscribeAsync(
        Action<AISpeechToTextBuilder> configure,
        Stream audioStream,
        CancellationToken cancellationToken = default);

    IAsyncEnumerable<SpeechToTextResponseUpdate> StreamTranscriptionAsync(
        Action<AISpeechToTextBuilder> configure,
        Stream audioStream,
        CancellationToken cancellationToken = default);

    Task<ISpeechToTextClient> CreateSpeechToTextClientAsync(
        Action<AISpeechToTextBuilder> configure,
        CancellationToken cancellationToken = default);
}
```

Basic Usage

AISpeechToTextBuilder

| Method | Description |
|---|---|
| `.WithAlias(string alias)` | Required. Sets an alias for auditing and telemetry. |
| `.WithProfile(Guid profileId)` | Selects a profile by ID. Uses default if omitted. |
| `.WithProfile(string profileAlias)` | Selects a profile by alias. |
| `.WithSpeechToTextOptions(SpeechToTextOptions options)` | Overrides profile defaults (language, model). |
| `.WithGuardrails(params Guid[] guardrailIds)` | Applies guardrails by ID. |
| `.WithGuardrails(params string[] guardrailAliases)` | Applies guardrails by alias. |
| `.WithContextItems(IEnumerable<AIRequestContextItem> contextItems)` | Attaches context items to the request. |

Streaming Transcription

Management API Endpoint

| Parameter | Type | Required | Description |
|---|---|---|---|
| `file` | file | Yes | Audio file to transcribe |
| `profileIdOrAlias` | string | No | Profile ID or alias (uses default if omitted) |
| `language` | string | No | Language hint (for example, `en` , `fr` , `de` ) |

Example Request

Response

Setting Up Speech-to-Text

1. Install a Provider with Speech-to-Text Support

2. Create a Connection

3. Create a Profile

| Model | Description |
|---|---|
| `whisper-1` | General-purpose transcription |
| `gpt-4o-transcribe` | Higher accuracy transcription |
| `gpt-4o-mini-transcribe` | Cost-effective transcription |

Copilot Voice Input

Related

Last updated

Was this helpful?