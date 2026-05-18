# States | CMS

Enable reactivity with Umbraco States, allowing you to provide a value that others can observe and update when the value changes.

Umbraco States are not related to Web Components reactivity. For more information, see the [Lit Element](/umbraco-cms/customizing/foundation/lit-element) article.

An Umbraco State is a container for a value. You create [Observables](/umbraco-cms/customizing/foundation/states#observe), which are hooks into the State's value. An Observable can then be observed to access the current value. If the State changes, all Observables are updated accordingly.

A typical use case is to bring reactivity across class instances. For example, a Context may provide a value that an Element needs to utilize.

In this case, the Context would implement a State and an Observable of it. The Element would then observe the Observable of the Context.

You can see an example of this pattern in the [Extension Type Workspace Context](/umbraco-cms/customizing/extending-overview/extension-types/workspaces/workspace-context) article.

The example below demonstrates the basics of working with a State and observing its changes:

```
const myState = UmbStringState('the initial value');
const myObservable = myState.asObservable();

this.observe(myObservable, (value) => {
    console.log(value);
});

myState.setValue('updated value');
```

This example will result in the following logs:

```
> 'the initial value'
> 'updated value'
```

Umbraco provides built-in state types for common data structures:

Array State

Boolean State

Class State

Number State

Object State

String State


Use the one fitting for your value type.

Observations are the act of reading the value of a State and reacting to future changes in the value.

The Umbraco Element or Controllers provides the ability to observe an Observable. This example shows how you can observe the value of a State with these.

The example below creates a State and exposes the entire value via an Observable, which can then be observed.

This will result in the following log:

The value of a state can be changed via the `setValue`

method. This replaces the current data with new data and notifies the relevant observers.

The following example shows how to change the value of the state to hold `item2`

and `item3`

. As this builds on the previous example, it means that `item1`

is no longer part of the value of this state:

This will result in the following log, in addition to the one above:

The `asObservablePart`

method creates an Observable that provides a scoped or transformed outcome based on the State.

The following example provides an observable for the first selected item in the selection:

In the above example, the `asObservablePart`

mapping function will be executed whenever the State changes. If the method's result differs from before, it will trigger an update to its observers.

The following example computes the length

As in the previous example, the mapper will be triggered whenever the State values change. But observers of this Observable will only be notified if the outcome value differs.

The example below revisits the earlier scenario to see how an Observable Part is triggered in relation to the value of the state.

This example will result in the following logs:

The `length`

observation was triggered when the length differed.

Last updated

Was this helpful?