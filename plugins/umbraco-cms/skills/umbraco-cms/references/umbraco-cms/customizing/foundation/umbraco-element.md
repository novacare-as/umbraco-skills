# Umbraco Element | CMS

Ease the integration with Backoffice by using a Umbraco Element

Last updated

Was this helpful?

Ease the integration with Backoffice by using a Umbraco Element

This provides a few methods to ease the connection with Backoffice, giving you the ability to:

Consume a Context —

[Learn more about Consuming Contexts](/umbraco-cms/customizing/foundation/context-api/consume-a-context)Provide Context —

[Learn more about Providing Contexts](/umbraco-cms/customizing/foundation/context-api/provide-a-context)Observe a State —

[Learn more about States](/umbraco-cms/customizing/foundation/states#observe-a-state-via-umbraco-element-or-umbraco-controller)Use localization —

[Learn more about Localization](/umbraco-cms/extending/language-files)Host Controllers —

[Learn more about Controllers](/umbraco-cms/customizing/foundation/umbraco-controller)

Create an Umbraco Element

You can turn any Web Component into an Umbraco Element by using the Umbraco Element Mixin, as done in the following example:

```
import { UmbElementMixin } from '@umbraco-cms/backoffice/element-api'

@customElement('my-extension-element')
class MyExtensionElement extends UmbElementMixin(HTMLElement) {...
}
```

This means you can use any base class, whether it’s a Web Component or a base class from your framework of choice. As long as it’s compatible with Web Components, it can be enhanced to become an Umbraco Element:

```
import { UmbElementMixin } from '@umbraco-cms/backoffice/element-api'
import { UUIButtonElement } from '@umbraco-cms/backoffice/external/uui'

@customElement('my-extension-element')
class MyExtensionElement extends UmbElementMixin(UUIButtonElement) {...
}
```

The Backoffice is generally built with Lit. To simplify things for those who prefer using the Lit version provided by the Backoffice, you can create your Web Components as Umbraco Elements like this:

Notice that it is identical to this:

Learn more about how to write Web Components with Lit in the [Lit Element article](/umbraco-cms/customizing/foundation/lit-element).

Last updated

Was this helpful?

Was this helpful?

```
import { UmbLitElement } from '@umbraco-cms/backoffice/lit-element'

@customElement('my-extension-element')
export class MyExtensionElement extends UmbLitElement {...
}
```

```
import { UmbElementMixin } from '@umbraco-cms/backoffice/element-api'
import { LitElement } from '@umbraco-cms/backoffice/external/lit'

@customElement('my-extension-element')
class MyExtensionElement extends UmbElementMixin(LitElement) {...
}
```