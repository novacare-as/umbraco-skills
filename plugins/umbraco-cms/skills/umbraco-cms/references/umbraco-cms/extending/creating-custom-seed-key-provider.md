# Creating a Custom Seed Key Provider | CMS

A guide to creating a custom seed key provider for Umbraco

Implementation

```
using Umbraco.Cms.Infrastructure.HybridCache;

namespace MySite.SeedKeyProviders;

public class BlogSeedKeyProvider : IDocumentSeedKeyProvider
{
    public ISet<Guid> GetSeedKeys()
    {
    }
}
```

```
using Umbraco.Cms.Core.Services.Navigation;
using Umbraco.Cms.Infrastructure.HybridCache;

namespace MySite.SeedKeyProviders;

public class BlogSeedKeyProvider : IDocumentSeedKeyProvider
{
    private readonly IDocumentNavigationQueryService _documentNavigationQueryService;

    public BlogSeedKeyProvider(IDocumentNavigationQueryService documentNavigationQueryService)
        => _documentNavigationQueryService = documentNavigationQueryService;

{...}
```

Registering the Seed Key Provider

Last updated

Was this helpful?

A guide to creating a custom seed key provider for Umbraco

Umbraco uses a lazy loaded cache, which means that content is loaded into the cache on an as-needed basis. However, you may need specific content to always be in the cache. To achieve this you can implement your own custom seed key providers.

There are two types of seed key providers: `IDocumentSeedKeyProvider`

for documents and `IMediaSeedKeyProvider`

for media. As these interfaces are identical only `IDocumentSeedKeyProvider`

is demonstrated in this article.

Seed keys are cached and calculated once. Any documents created after the site has started will not be included in the seed keys until after a server restart.

Implementation

This example implements a `IDocumentSeedKeyProvider`

which seeds all the children of a node, in this case blog posts.

Create a new class called

`BlogSeedKeyProvider`

that implements`IDocumentSeedKeyProvider`.


```
using Umbraco.Cms.Infrastructure.HybridCache;

namespace MySite.SeedKeyProviders;

public class BlogSeedKeyProvider : IDocumentSeedKeyProvider
{
    public ISet<Guid> GetSeedKeys()
    {
    }
}
```

Inject the

`IDocumentNavigationQueryService`

to get the children of the blog node.

```
using Umbraco.Cms.Core.Services.Navigation;
using Umbraco.Cms.Infrastructure.HybridCache;

namespace MySite.SeedKeyProviders;

public class BlogSeedKeyProvider : IDocumentSeedKeyProvider
{
    private readonly IDocumentNavigationQueryService _documentNavigationQueryService;

    public BlogSeedKeyProvider(IDocumentNavigationQueryService documentNavigationQueryService)
        => _documentNavigationQueryService = documentNavigationQueryService;

{...}
```

Parse a hardcoded string to a GUID.

Use the

`IDocumentNavigationQueryService`

to get the children of the blog node.Return their keys as a

`HashSet`.


Since this returns it as a set, and all the sets get unioned, we do not have to worry about duplicates.

The final class looks like this:

Registering the Seed Key Provider

Now that the `BlogSeedKeyProvider`

is implemented, it must be registered in the `Startup`

class.

All blogpost will now be seeded into the cache on startup, and will always be present in the cache.

Last updated

Was this helpful?

Was this helpful?

```
public ISet<Guid> GetSeedKeys()
{
    var blogRoot = Guid.Parse("a5fdb22d-b7f2-4a59-8c4e-46ed86bde56c");

    if (_documentNavigationQueryService.TryGetChildrenKeys(blogRoot, out IEnumerable<Guid> blogPostKeys))
    {
        return new HashSet<Guid>(blogPostKeys);
    }

    return new HashSet<Guid>();
}
```

```
using Umbraco.Cms.Core.Services.Navigation;
using Umbraco.Cms.Infrastructure.HybridCache;

namespace MySite.SeedKeyProviders;

public class BlogSeedKeyProvider : IDocumentSeedKeyProvider
{
    private readonly IDocumentNavigationQueryService _documentNavigationQueryService;

    public BlogSeedKeyProvider(IDocumentNavigationQueryService documentNavigationQueryService)
        => _documentNavigationQueryService = documentNavigationQueryService;

    public ISet<Guid> GetSeedKeys()
    {
        var blogRoot = Guid.Parse("a5fdb22d-b7f2-4a59-8c4e-46ed86bde56c");

        if (_documentNavigationQueryService.TryGetChildrenKeys(blogRoot, out IEnumerable<Guid> blogPostKeys))
        {
            return new HashSet<Guid>(blogPostKeys);
        }

        return new HashSet<Guid>();
    }
}
```

```
using MySite.SeedKeyProviders;
using Umbraco.Cms.Infrastructure.DependencyInjection;
using Umbraco.Cms.Infrastructure.HybridCache;

WebApplicationBuilder builder = WebApplication.CreateBuilder(args);

builder.Services.AddSingleton<IDocumentSeedKeyProvider, BlogSeedKeyProvider>();
{...}
```