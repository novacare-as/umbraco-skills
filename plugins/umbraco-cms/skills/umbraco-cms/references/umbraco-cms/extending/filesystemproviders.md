# Custom File Systems (IFileSystem) | CMS

A guide to creating custom file systems in Umbraco

Before considering a custom media file system, be sure to first read about the configuration options for `UmbracoMediaPath`

and `UmbracoMediaPhysicalRootPath`

in the [configuration reference docs](/umbraco-cms/reference/configuration/globalsettings). These configurations may save you from creating your own media file system entirely.

By default, Umbraco uses an instance of `PhysicalFileSystem`

to handle the storage location of the media archive (wwwroot/media).

This can be configured by composition:

```
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Logging;
using Umbraco.Cms.Core.Composing;
using Umbraco.Cms.Core.DependencyInjection;
using Umbraco.Cms.Core.Hosting;
using Umbraco.Cms.Core.IO;
using Umbraco.Cms.Infrastructure.DependencyInjection;

namespace UmbracoExamples.Composition;

public class SetMediaFileSystemComposer : IComposer
{
    public void Compose(IUmbracoBuilder builder)
    {
        builder.SetMediaFileSystem((factory) =>
        {
            IHostingEnvironment hostingEnvironment = factory.GetRequiredService<IHostingEnvironment>();
            var folderLocation = "~/CustomMediaFolder";
            var rootPath = hostingEnvironment.MapPathWebRoot(folderLocation);
            var rootUrl = hostingEnvironment.ToAbsolute(folderLocation);

            return new PhysicalFileSystem(
                factory.GetRequiredService<IIOHelper>(),
                hostingEnvironment,
                factory.GetRequiredService<ILogger<PhysicalFileSystem>>(),
                rootPath,
                rootUrl);
        });
    }
}
```

When creating a `PhysicalFileSystem`

it takes some dependencies like `IIOHelper`

, but the last two parameters are what we're interested in.

The `rootPath`

is where your media will be stored on the disk. Since netcore by default stores files in the `wwwroot`

, we must put our desired folder somewhere within `wwwroot`

to ensure that we use `hostingEnvironment.MapPathWebRoot(~/CustomMediaFolder)`

. The `~`

will be mapped to your `wwwroot`

folder, so the final `rootPath`

will be `your/project/path/wwwroot/CustomMediaFolder`

. The `~`

is therefore important.

The `rootUrl`

is the base URL that your media files will be served from. In this case, your image URL could look something like `mysite.com/CustomMediaFolder/MyAwesomePicture.png`

. Again the `~`

is important.

In the code sample above, the `rootUrl`

must map to the the same physical location as `rootPath`

, which again must be placed under `wwwroot`

. If you want to store the media files outside of `wwwroot`

there is an extra step involved; you need to instruct netcore to include static files from a different physical location.

The `rootUrl`

is the base URL that your media files will be served from. In this case, your image URL could look something like `mysite.com/CustomMediaFolder/MyAwesomePicture.png`

. Again the `~`

is important. With the code sample above, the `rootUrl`

must map to the same physical location as `rootPath`

, otherwise, you will get 404's for your images.

If you want to store the media files outside of `wwwroot`

there is an extra step involved; you need to instruct netcore to include static files from a different physical location.

In the `Program.cs`

file, register a new static file location like so:

The PhysicalFileProvider takes a single parameter, the

. This is the rooted filesystem path using directory separator chars and not ending with a directory separator, eg: **RootPath**`c:\storage\umbracoMedia`

or `\\server\path`

. The safest way to achieve this is using `Path.Combine`.


You also have to specify the

. This is the relative URL where the media will be served using URL separator chars and not ending with a separator, eg: **RequestPath**`/CustomPath`

or `/Media`.


Now you can use your newly registered static file location as if it was `wwwroot`

. Notice how you no longer need to use `hostingEnvironment.MapPathWebRoot(folderLocation)`

, since you're no longer trying to map the location to somewhere within `wwwroot`

, but instead use your newly registered static file location.

This is almost the same as when registering a location within the `wwwroot`

folder. The only difference is that `rootPath`

is now set to the path we gave the `PhysicalFileProvider`

and the `rootUrl`

is the same as we set as the `RequestPath`

in the `StaticFileOption`.


Our media is now stored in `C:\storage\umbracoMedia`

, and is served from the base URL `/CustomPath`

, so an image URL will look something like `mysite.com/CustomPath/MyAwesomePicture.png`.


You can replace `PhysicalFileSystem`

with a custom file system implementation - eg. if you want your media files stored on Amazon S3 or elsewhere outside your site.

To achieve this, you must first create your own file system by implementing the interfaces `IFileSystem`

and `IFileProviderFactory`

(the interfaces that are implemented by `PhysicalFileSystem`

).

You then replace the media filesystem by composition using `IUmbracoBuilder.SetMediaFileSystem(...)`

(as is demonstrated in the paragraphs above), but instead of returning a `PhysicalFileSystem`

, you return your own file system implementation.

For inspiration on building a custom file system, have a look at the [Azure Blob Storage file system implementation arrow-up-right](https://github.com/umbraco/Umbraco.StorageProviders#umbracostorageprovidersazureblob)

`UmbracoAuthorizedApiController`

has been removed from Umbraco 14. Use`ManagementApiControllerBase`

class instead.

Read the [Creating a Backoffice API article](/umbraco-cms/tutorials/creating-a-backoffice-api) for a comprehensive guide to writing APIs for the Management API.

Since the default media file system can be swapped with custom implementations, you should never access the implementation directly. Umbraco uses a manager class called `MediaFileManager`

. You can get a reference to this manager class via dependency injection in the constructor for your custom class or controller:

You can then access the configured file system provider through `_mediaFileManager.FileSystem`

, which is the same way Umbraco will access the file system provider.

The MediaPath Scheme defines the current set of rules that decide the format of the Media Path when it is saved into the media archive wherever it is located.

By default the MediaPath scheme used by Umbraco is the `UniqueMediaPathScheme`

this generates a 'folder' to place the uploaded image in, for example:

`/media/dozdrg2f/mylovelyimage.jpg`


`/media`

is defined by the PhysicalFileSystem and `dozdrg2f`

is generated by the `UniqueMediaPathScheme`.


The folder generated by `UniqueMediaPathScheme`

is not strictly unique, as it's based on the first eight characters of the GUID for the media item. In practice, with randomly generated GUIDs, a collision is unlikely.

There is an increased possibility of generating colliding paths if creating media programmatically and setting keys using version 7 "ordered" GUIDs via `Guid.CreateVersion7()`

. As such these should be avoided. `UniqueMediaPathScheme`

will throw an exception if it detects they have been used. Any manually created keys should use `Guid.NewGuid()`.


You can create your own logic for the path by implementing `IMediaPathScheme`

and setting it during composition with:

Umbraco also registers instances of `PhysicalFileSystem`

for the following parts of Umbraco that persist to 'files':

`PartialViewsFileSystem`

`StylesheetsFileSystem`

`ScriptsFileSystem`

`MvcViewsFileSystem`


These are accessible via dependency injection.

`IFileSystem`

, `MediaFileManager`

, and `FileSystems`

are located in the `Umbraco.Cms.Core.IO`

namespace.

Like with the media file system it is also possible to replace the stylesheet filesystem with your own implementation of `IFileSystem`

in a composer. It's important to note here that, unlike media file system, you cannot replace the filesystem with a `PhysicalFileSystem`

using a different root path or root URL, this will not work, and will cause issues since the root path is coupled to the virtual path, given by the frontend, e.g. `/css/MyBeautifulStyle.css`.


When replacing the stylesheet filesystem, you don't need to register it, since it's only available through Filesystems, what you need to do instead is configure the `FileSystems`

to use your implementation for the `StylesheetsFileSystem`.


The IUmbracoBuilder has an extension method for configuring the `FileSystems`

, you need to invoke this method with an action that accepts an `IServiceProvider`

and the `FileSystems`

you will configure, configuring the `FileSystems`

can look like this:

Where `YourFileSystemImplementation`

is a class that implements `IFileSystem`

. This should always be done in a composer, since we do not recommend trying to change filesystems on the fly.

After the `SetStylesheetFileSystem`

method has run, `FileSystems.StylesheetsFileSystem`

will return the instance that was created in the `ConfigureFileSystems`

extension method.

There is an Azure Blob Storage provider:

[Previous Embedded Media Providers chevron-left](/umbraco-cms/extending/embedded-media-providers)

[Next Using Azure Blob Storage for Media and ImageSharp Cache chevron-right](/umbraco-cms/extending/filesystemproviders/azure-blob-storage)

Last updated

Was this helpful?

## Using Azure Blob Storage for Media and ImageSharp Cache | CMS

Setup your site to use Azure Blob storage for media and ImageSharp cache

There are some scenarios where you may want or need to consider leveraging Azure Blob Storage. An example would be for media in Umbraco sites with substantial media libraries.

Having your site's media in Azure Blob Storage can help your deployments complete more quickly. This has the potential to positively affect site performance, as the ImageSharp cache is moved to Azure Blob Storage.

The setup consists of adding a package to your site, setting the correct configuration, and adding the services and middleware. Before you begin you’ll need to create an Azure Storage Account and a container for your media and ImageSharp cache. In this example, we assume your container name is "mysitestorage" and has already been created.

See the for a quickstart guide on how to create a blob storage container.

Before you begin, you need to install the `Umbraco.StorageProviders.AzureBlob`

and the `Umbraco.StorageProviders.AzureBlob.ImageSharp`

NuGet packages. There are two approaches to installing the packages:

Use your favorite Integrated Development Environment (IDE) and open up the NuGet Package Manager to search and install the packages

Use the command line to install the packages


Navigate to your project folder, which is the folder that contains your `.csproj`

file. Now use the following `dotnet add package`

commands to install the packages:

```
dotnet add package Umbraco.StorageProviders.AzureBlob
dotnet add package Umbraco.StorageProviders.AzureBlob.ImageSharp
```

The correct packages will have been installed in your project.

The next step is to configure your blob storage. There are multiple approaches for this, but in this document, we're going to do it through `appsettings.json`

. For more configuration options, see the on the GitHub repository.

Open up your `appsettings.json`

file and add the connection string and container name under `Umbraco:Storage:AzureBlob:Media`

. Your Umbraco section of appsettings will look something like this:

In this example, the container name is `mysitestorage`.


You can get your connection string from your Azure Portal under "Access Keys".

You are almost there. The last step is to set up the required services and middleware. This can be done using extension methods.

Invoke the `.AddAzureBlobMediaFileSystem()`

and the `.AddAzureBlobImageSharpCache()`

extension methods using the `CreateUmbracoBuilder()`

builder chain in the `Program.cs`

file like shown below.

Learn more about invoking and registering extension methods in the [Dependency Injection](/umbraco-cms/reference/using-ioc) article.

**Upgrading from Umbraco 9/10**:

As of of `Umbraco.StorageProviders`

, the ImageSharp dependency has been separated into its own package.

Therefore, if you're planning on upgrading your site from Umbraco 9/10 to 11+, don't forget to install and setup the new `Umbraco.StorageProviders.AzureBlob.ImageSharp`

package. This will ensure that your ImageSharp cache continues to be stored in your blob storage container.

Now when you launch your site again, the blob storage will be used to store media items as well as the ImageSharp cache. Do note though that the `/media`

and `/cache`

folders do not get created until a piece of media is uploaded.

Any media files you already have on your site will not automatically be added to the blob storage container. You will need to copy the contents on the `/wwwroot/media`

folder and upload them to a new folder called `/media`

in your blob storage container. Once you've done that, you can safely delete the `wwwroot/media`

folder locally, as it is no longer needed.

Any new media files you upload to the site will automatically be added to the Blob Storage.

Last updated

Was this helpful?
