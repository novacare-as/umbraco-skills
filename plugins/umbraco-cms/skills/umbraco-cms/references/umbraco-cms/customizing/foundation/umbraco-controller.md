# Umbraco Controller | CMS

Contain or reuse logic across Elements. A Controller enables you to separate logic while still being connected with the life cycle of an element.

Last updated

Was this helpful?

Contain or reuse logic across Elements. A Controller enables you to separate logic while still being connected with the life cycle of an element.

An Umbraco controller provides all the features of an Umbraco element within a separate class. Do this for architectural reasons or to reuse a feature across elements.

Host Element

A Controller is assigned to a Host Element. This assignment may be indirect, since Controllers can host other Controllers.

The host element is a web component enhanced to host controllers. All [Umbraco Elements](/umbraco-cms/customizing/foundation/umbraco-element) are controller hosts, as are all Umbraco controllers, allowing controllers to host other controllers.

To retrieve the controller’s host element, use the `getHostElement()`

method.

Element Life Cycle

Controllers can declare the following methods, which are triggered depending on the host element’s life cycle:

`hostConnected()`

— Called when the host element connects to the DOM.`hostDisconnected()`

— Called when the host element disconnects from the DOM.`destroy()`

— Called when the controller is taken out of commission.

Additionally, Umbraco Controllers implement a `getHostElement()`

method, which enables any Controller to receive the Element that hosts the Controllers.

Registration

A Controller should register itself with a given host. This is handled automatically when extending the `UmbControllerBase`

class. The following example demonstrates a controller implementation:

```
import { UmbControllerBase } from '@umbraco-cms/backoffice/class-api';
import type { UmbControllerHost } from '@umbraco-cms/backoffice/controller-api';

export class MyOwnControllerImplementation extends UmbControllerBase {

    #secondsAlive = 0;

    constructor(host: UmbControllerHost) {
        // Parse the host to the base class, this will trigger the registration.
        super(host);
    }
    
    hostConnected() {
        // It's important to call the super method when overriding a method of the base class.
        super.hostConnected();
        this.#timer = setInterval(this.#onInterval, 1000)
    }
    
    hostDisconnected() {
        // It's important to call the super method when overriding a method of the base class.
        super.hostDisconnected();
        clearInterval(this.#timer);
    }
    
    #onInterval = () => {
        this.#secondsAlive++;
        console.log(`My own controller have been connected in ${this.#secondsAlive} seconds.`);
    }

    override destroy(): void {
        // It's important to call the super method when overriding a method of the base class.
        super.destroy();
        // We do not need to stop the timer in the Destroy method, because the hostDisconnected method is also called if connected and destroyed.
    }
}
```

If you don't like to extend the `UmbControllerBase`

, then you can register a class as a controller as shown in the following example. Note that manual deregistration is required in this case.

Last updated

Was this helpful?

Was this helpful?

```
export class MyOwnControllerImplementation {

    #host: UmbControllerHost;

    constructor(host: UmbControllerHost) {
        this.#host = host;
        this.#host.addUmbController(this);
    }
    
    override destroy(): void {
        this.#host.removeUmbController(this);
    }
}
```

## Write your own controller | CMS

Reuse functionality across components by writing it as a Controller.

```
import { UmbControllerBase } from '@umbraco-cms/backoffice/class-api';

class MyController extends UmbControllerBase {
	
	override hostConnected() {
		super.hostConnected();
		// Your code for when the controller is connected.
		console.log('Your controller's Host element has been connected.')
	}
	override hostDisconnected() {
		super.hostDisconnected();
		// Your code for when the controller is disconnected.
		console.log('Your controller's Host element got disconnected.')
	}
	override destroy() {
		super.destroy();
		// Your code for when this controller gets destroyed.
		console.log('Your controller's are getting destroyed, it will never be reconnected. Use this callback to end all the opperations of this controller')
	}
}
```

Last updated

Was this helpful?

Reuse functionality across components by writing it as a Controller.

To create a custom controller, implement the `UmbController`

interface.

To ease the implementation, you can base your class on the `UmbControllerBase`:


```
import { UmbControllerBase } from '@umbraco-cms/backoffice/class-api';

class MyController extends UmbControllerBase {
	
	override hostConnected() {
		super.hostConnected();
		// Your code for when the controller is connected.
		console.log('Your controller's Host element has been connected.')
	}
	override hostDisconnected() {
		super.hostDisconnected();
		// Your code for when the controller is disconnected.
		console.log('Your controller's Host element got disconnected.')
	}
	override destroy() {
		super.destroy();
		// Your code for when this controller gets destroyed.
		console.log('Your controller's are getting destroyed, it will never be reconnected. Use this callback to end all the opperations of this controller')
	}
}
```

Once this is done, your Controller can host other Controllers. You can also override the available lifecycle methods when needed. Overriding these methods is optional and should only be done if the controller must perform logic during those callbacks.

Last updated

Was this helpful?

Was this helpful?
