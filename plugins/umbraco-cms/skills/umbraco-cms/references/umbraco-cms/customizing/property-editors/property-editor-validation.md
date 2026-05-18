# Property Editor Validation | CMS

Looking to add Validation rules for your own Property Editor? This article describes how to append validation rules to your Property Editor.

```
import { customElement } from '@umbraco-cms/backoffice/external/lit';
import { UmbLitElement } from '@umbraco-cms/backoffice/lit-element';
import { UmbFormControlMixin } from '@umbraco-cms/backoffice/validation';

@customElement('my-property-editor')
export class MyPropertyEditorElement
	extends UmbFormControlMixin<string | undefined, typeof UmbLitElement, undefined>(UmbLitElement)
	implements UmbPropertyEditorUiElement {
	
	/**
	Notice 'value'-property is already defined via the FormControlMixin, based on the first generic type given to it
	*/...
	

}

export default MyPropertyEditorElement;

declare global {
	interface HTMLElementTagNameMap {
		'my-property-editor': MyPropertyEditorElement;
	}
}
```

Add Validation rules

Integrate the validation of an inner element

Last updated

Was this helpful?