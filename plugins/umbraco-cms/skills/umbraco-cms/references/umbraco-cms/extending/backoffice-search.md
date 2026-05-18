# Backoffice Search | CMS

A guide to customization of Backoffice Search

| Node Type | Propagated Fields |
|---|---|
| All Nodes | Id, NodeId and Key |
| Media Nodes | UmbracoFileFieldName |
| Member Nodes | email, loginName |

Adding custom properties to backoffice search

```
builder.CreateUmbracoBuilder()
    .AddBackOffice()
    .AddWebsite()
    .AddDeliveryApi()
    .AddComposers()
    .Build();

builder.Services.AddUnique<IUmbracoTreeSearcherFields, CustomUmbracoTreeSearcherFields>();
```

```
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.DependencyInjection;
using Umbraco.Cms.Infrastructure.Examine;
using Umbraco.Extensions;

namespace Umbraco.Docs.Samples.Web.BackofficeSearch;

public class BackofficeSearchComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.Services.AddUnique<IUmbracoTreeSearcherFields, CustomUmbracoTreeSearcherFields>();
    }
}
```

Last updated

Was this helpful?