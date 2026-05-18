# Speech-to-Text Controller | AI in Umbraco

Controller and recorder for speech-to-text transcription in custom elements.

Import

```
import {
    UaiSpeechToTextController,
    UaiAudioRecorder,
    UaiSpeechToTextOptions,
    UaiSpeechToTextResult,
    UaiAudioRecorderState
} from "@umbraco-ai/core";
```

UaiAudioRecorder

Constructor

```
new UaiAudioRecorder(host: UmbControllerHost)
```

| Parameter | Type | Description |
|---|---|---|
| `host` | `UmbControllerHost` | The controller host (usually `this` in a Lit element) |

Properties

| Property | Type | Description |
|---|---|---|
| `state` | `UaiAudioRecorderState` | Current state: `"idle"` or `"recording"` |
| `state$` | `Observable<UaiAudioRecorderState>` | RxJS observable of state changes |

Methods

start

stop

cancel

Example

UaiSpeechToTextController

Constructor

| Parameter | Type | Description |
|---|---|---|
| `host` | `UmbControllerHost` | The controller host (usually `this` in a Lit element) |

Methods

transcribe

| Parameter | Type | Description |
|---|---|---|
| `audioFile` | `Blob` | The recorded audio blob |
| `options` | `UaiSpeechToTextOptions` | Optional transcription config |

Options

Result

Complete Example

Related

Last updated

Was this helpful?