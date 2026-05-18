# Utilities

## Contents

- [Modals | CMS](#modals-cms)
- [UI Sorting | CMS](#ui-sorting-cms)

---

## Modals | CMS

In this section you can find information about different modal utilities that can be used in your extension when customizing the Backoffice.

Last updated

Was this helpful?

In this section you can find information about different modal utilities that can be used in your extension when customizing the Backoffice.

Present a dialog to ask the user for confirmation.

Last updated

Was this helpful?

Was this helpful?

### Confirm Dialog | CMS

Present a dialog to ask the user for confirmation.

Last updated

Was this helpful?

Present a dialog to ask the user for confirmation.

Confirmation dialogs are used to ask the user for confirmation to complete some action and are presented as a center-aligned modal in the backoffice.

Extension authors do not need to register the dialog in their extension's manifest, instead these dialogs are opened by importing and calling the `umbOpenModal`

function.

Extension authors can customize the dialog with configuration options such as headline, body content, colors, and button labels.

`headline`

- The headline of the modal.`content`

- The content of the modal, which can be a TemplateResult or a string.`color`

- (Optional) The color of the modal, can be`positive`

or`danger`

. Defaults to`positive`

.`confirmLabel`

- (Optional) The label of the confirmation button.`cancelLabel`

- (Optional) The label of the cancel button.

To see all properties of the `UMB_CONFIRM_MODAL`

token, see the .

The `onSubmit`

method returns a promise that resolves when the user confirms the dialog, and rejects when the user cancels the dialog.

Opening a Confirmation Dialog

my-element.ts

```
import {
    html,
    LitElement,
    customElement,
} from "@umbraco-cms/backoffice/external/lit";
import { UmbElementMixin } from "@umbraco-cms/backoffice/element-api";
import { umbOpenModal, UMB_CONFIRM_MODAL } from "@umbraco-cms/backoffice/modal";

@customElement("my-confirmation-modal")
export class MyConfirmationModal extends UmbElementMixin(LitElement) {
    #onRequestDisable() {
        umbOpenModal(this, UMB_CONFIRM_MODAL, {
            data: {
                headline: this.localize.term("actions_disable"),
                content: this.localize.term("defaultdialogs_confirmdisable"),
                color: "danger",
                confirmLabel: this.localize.term("actions_disable"),
            },
        })
            .then(() => {
                console.log("User has approved");
            })
            .catch(() => {
                console.log("User has rejected");
            });
    }

    render() {
        return html`<uui-button
            look="primary"
            color="danger"
            @click=${this.#onRequestDisable}
            label=${this.localize.term("actions_disable")}
        ></uui-button>`;
    }
}
```

Convenience Method

Confirmation dialogs can be opened using the `umbConfirmModal`

method, which offers a slightly simplified API.

Last updated

Was this helpful?

Was this helpful?

my-element.ts

```
import {
    html,
    LitElement,
    customElement,
} from "@umbraco-cms/backoffice/external/lit";
import { UmbElementMixin } from "@umbraco-cms/backoffice/element-api";
import { umbConfirmModal } from "@umbraco-cms/backoffice/modal";

@customElement("restart-services-modal")
export class RestartServicesModal extends UmbElementMixin(LitElement) {
    #onRequestDisable() {
        umbConfirmModal(this, {
            headline: this.localize.term("actions_disable"),
            content: this.localize.term("defaultdialogs_confirmdisable"),
            color: "danger",
            confirmLabel: this.localize.term("actions_disable"),
        })
            .then(() => {
                console.log("User has approved");
            })
            .catch(() => {
                console.log("User has rejected");
            });
    }

    render() {
        return html`<uui-button
            look="primary"
            color="positive"
            @click=${this.#onRequestDisable}
            label=${this.localize.term("actions_disable")}
        ></uui-button>`;
    }
}
```

---

## UI Sorting | CMS

Enable sorting elements via drag and drop

This page is a work in progress and may undergo further revisions, updates, or amendments. The information contained herein is subject to change without notice.

The Umbraco Sorter enables you to make a list of elements sortable via drag-and-drop interaction. You have to set up the sorter once on the Element that renders the items to be sorted. As part of the configuration, you shall provide an `onChange`

callback method, which will be executed every time the sorter makes a difference to the data.

The following example shows a basic setup of the Sorter.

```

type ModelEntryType = {
    id: string;
    name: string;
}

this.#sorter = new UmbSorterController(this, {
    itemSelector: '.sorter-item',
    containerSelector: '.sorter-container',
    getUniqueOfElement: (element) => {
        return element.getAttribute('data-sorter-id');
    },
    getUniqueOfModel: (modelEntry) => {
        return modelEntry.id;
    },
    onChange: ({ model }) => {
        const oldValue = this._items;
        this._items = model;
        this.requestUpdate('_items', oldValue);
    },
});
```

The properties provided are the following:

`itemSelector`

: A query selector that matches the items that should be draggable.`containerSelector`

: A query elector that matches the parent element of the items.`getUniqueOfElement`

: A method that returns the unique element`getUniqueOfModel`

: Provide a method that returns the unique of a given model entry`onChange`

: Provide a method to retrieve the changed model. This is called every time the model is changed, including when the user is dragging around.

The model given to the Sorter must be an Array. The following example extends the example from above:

The Sorter does not move elements, instead, it updates the model as the user drags an item around. This puts higher pressure on the rendering of the sortable Elements. This means we need to make sure that the rendering re-uses the same element despite sorting the data differently.

Lit does provide a render helper method called `repeat`

that does this for us. The following example shows a render method that continues the work of the examples above:

Last updated

Was this helpful?

---
