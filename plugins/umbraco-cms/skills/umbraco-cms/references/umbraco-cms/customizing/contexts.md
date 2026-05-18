# Contexts | CMS

Contexts are APIs that are made available via the Context API. This section describes how some of the most commonly used Contexts work and how they can be utilized.

Common Contexts

Current User Context

Section Context

Workspace Context

Property Context

Modal Context

Notification Context

Entity Context

App Language Context

Workspace Split View Context

Block Entry Context

Parent Entity Context

Ancestors Entity Context

Last updated

Was this helpful?

## Property Dataset Context | CMS

The owner of the values for properties, enabling you to communicate with other properties.

```
this.consumeContext(UMB_PROPERTY_DATASET_CONTEXT, async (context) => {...
});
```

Observe the value of another Property

```
this.consumeContext(UMB_PROPERTY_DATASET_CONTEXT, async (context) => {
    this.observe(
        await context?.propertyValueByAlias("alias-of-other-property"),
        (value) => {
            console.log("the value of the other property", value)
        }
    );
});
```

Set the value of another Property

Dataset Context in relation to Property Editors and Workspaces

Last updated

Was this helpful?
