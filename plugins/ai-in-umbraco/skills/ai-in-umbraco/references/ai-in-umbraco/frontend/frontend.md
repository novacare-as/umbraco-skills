# Overview | AI in Umbraco

Integrate AI capabilities into custom backoffice elements.

Package

```
import { UaiChatController, UaiChatMessage, UaiChatResult } from "@umbraco-ai/core";
```

Quick Start

```
import { LitElement, html } from "lit";
import { customElement, state } from "lit/decorators.js";
import { UaiChatController, UaiChatMessage, UaiChatResult } from "@umbraco-ai/core";

@customElement("my-ai-element")
export class MyAIElement extends LitElement {
    #chatController = new UaiChatController(this);

    @state()
    private _response?: string;

    @state()
    private _loading = false;

    async #handleSubmit() {
        this._loading = true;

        const messages: UaiChatMessage[] = [{ role: "user", content: "Hello, can you help me?" }];

        const { data, error } = await this.#chatController.complete(messages);

        if (data) {
            this._response = data.message.content;
        } else {
            console.error("Chat error:", error);
        }

        this._loading = false;
    }

    render() {
        return html`
            <button @click=${this.#handleSubmit} ?disabled=${this._loading}>
                ${this._loading ? "Loading..." : "Ask AI"}
            </button>
            ${this._response ? html`<p>${this._response}</p>` : ""}
        `;
    }
}
```

Key Concepts

Controller Pattern

Profile Selection

Cancellation

In This Section

[Embeddings Controller chevron-right](/ai-in-umbraco/frontend/embeddings-controller)

Last updated

Was this helpful?