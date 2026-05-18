# Server Setup

## Contents

- [Running Umbraco On Azure Web Apps | CMS](#running-umbraco-on-azure-web-apps-cms)
- [Health Probes | CMS](#health-probes-cms)
- [Hosting Umbraco in IIS | CMS](#hosting-umbraco-in-iis-cms)
- [Load Balancing](#load-balancing)
- [File And Folder Permissions | CMS](#file-and-folder-permissions-cms)
- [Running Umbraco in Docker | CMS](#running-umbraco-in-docker-cms)
- [Runtime Modes | CMS](#runtime-modes-cms)

---

## Running Umbraco On Azure Web Apps | CMS

This section describes best practices with running Umbraco on Azure Web Apps

They have been called a few names in the past, many people still know Azure Web Apps as Azure Web Sites.

App Service is a fully Managed Platform for professional developers that brings a rich set of capabilities to web, mobile and integration scenarios. Quickly create and deploy mission critical web Apps that scale with your business by using Azure App Service.


Umbraco will run on Azure Web Apps but there are some configuration options and specific Azure Web Apps environment limitations to be aware of.

You need to add these configuration values. E.g in a json configuration source like `appSettings.json`:


```
{
    "Umbraco": {
        "CMS": {
            "Global": {
                "MainDomLock" : "FileSystemMainDomLock"
            },
            "Hosting": {
                "LocalTempStorageLocation": "EnvironmentTemp"
            },
            "Examine": {
                "LuceneDirectoryFactory": "SyncedTempFileSystemDirectoryFactory"
            }
        }
    }
}
```

You can also copy the following JSON directly into your Azure Web App configuration via the Advanced Edit feature.

Remember to add an `ASPNETCORE_ENVIRONMENT`

variable with values `Development`

, `Staging`

, or `Production`.


The minimum recommended Azure SQL Tier is "S2", however noticeable performance improvements are seen in higher Tiers

If you are load balancing or require the scaling ("scale out") ability of Azure Web Apps then you need to consult the [Load Balancing documentation](/umbraco-cms/fundamentals/setup/server-setup/load-balancing). This is due to the fact that a lot more needs to be configured to support scaling/auto-scaling.

It is important to know that Azure Web Apps uses a remote file share to host the files to run your website. This is due to the files running your website do not exist on the machine running your website. In many cases this isn't an issue. It can become one if you have a large amount of IO operations running over remote file-share.

Although Umbraco can be configured to use environmental storage it still requires its working-directory to be writable. If Umbraco is deployed to a read-only file system it will .

For example, Azure's is not supported by Umbraco. To check if your web app is using this feature you can check the `WEBSITE_RUN_FROM_PACKAGE`

environment variable.

If you require the scaling ("scale out") ability of Azure Web Apps you need to consult the [Load Balancing documentation](/umbraco-cms/fundamentals/setup/server-setup/load-balancing). This is due to the fact that a lot more needs to be configured to support scaling/auto-scaling.

It's important to know that Azure Web Apps may move your website between their 'workers' at any given time. This is normally a transparent operation. In some cases you may be affected by it if any of your code or libraries use the following variables:

`Environment.MachineName`

(or equivalent)

When your site is migrated to another worker, these variables will change. You cannot rely on these variables remaining static for the lifetime of your website.

The quickest way to get to your logs is using the following URL template and replacing `{app}`

with your Web App name:

`https://{app}.scm.azurewebsites.net/api/logstream`


You can also find this in the KUDU console by clicking **Advanced Tools** > **Log Stream** on the Web App in the Azure Portal.

Consult the [Azure Key Vault documentation](/umbraco-cms/extending/key-vault) if you would like to directly reference Azure Key Vault Secrets to your Azure Web App.

Last updated

Was this helpful?

---

## Health Probes | CMS

Use .NET health probe endpoints to monitor whether your Umbraco application is alive and ready to serve requests.

Overview

Endpoints

| Endpoint | Behavior |
|---|---|
| `GET /umbraco/api/health/live` | Returns HTTP 200 if the process is responding. No checks run. |
| `GET /umbraco/api/health/ready` | Returns HTTP 200 when the site is running normally. Returns HTTP 503 when the site is not ready, for example, during startup or an unattended upgrade. |

Configuring health probes

```
/umbraco/api/health/ready
```

```
livenessProbe:
  httpGet:
    path: /umbraco/api/health/live
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 10
readinessProbe:
  httpGet:
    path: /umbraco/api/health/ready
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 10
```

```
services:
  umbraco:
    image: my-umbraco-app
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8080/umbraco/api/health/ready"]
      interval: 10s
      timeout: 5s
      retries: 3
      start_period: 30s
```

Related

Last updated

Was this helpful?

---

## Hosting Umbraco in IIS | CMS

Information on hosting Umbraco on IIS

Install .NET Core Runtime

Install the Hosting Bundle

Restart IIS

```
net stop was /y
net start w3svc
```

Create the Site in IIS

Set Application Pool

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-3be0fd98be84ed3e99c9466f667a34e4892bba70%252Fiis-app-pool-core-v15.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=977ad25e&sv=2)

Create a Site

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1a2d0659547ad4e73a41f6136d1665aa32beca4c%252Fcreate-site-in-iis.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=47c4fe30&sv=2)

Publish the Website

Option 1: Use dotnet CLI for Manual Deployment

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-45619a693f8526e574278312e97e89b2708b92a8%252Fdotnet-cli-command.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=eb417e3f&sv=2)

Option 2: Use Visual Studio to Deploy

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e920000213d0f924cd13f6de8ca29141acd469e6%252Fvisual-studio-deploy.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b5312cd2&sv=2)

Configure Environment Variables

Configure Environment Variables in IIS

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9af7c7413ae00a07907e383749456c45224946c0%252Fiis-core-website-config-v15.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fd67fcab&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d53383954f844f3a21553e6afc1adda1b70ca215%252Fiis-environment-variables-v15.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=57024d07&sv=2)

IIS Hosting Models

In-process Hosting (Default)

Default Configuration

Out-of-process Hosting

Configuration

Troubleshooting: Handling WebDAV Module Interference

Last updated

Was this helpful?

---

## Load Balancing

### Contents

- [Load Balancing Azure Web Apps | CMS](#load-balancing-azure-web-apps-cms)
- [Standalone File System | CMS](#standalone-file-system-cms)
- [Advanced Techniques With Flexible Load Balancing | CMS](#advanced-techniques-with-flexible-load-balancing-cms)
- [Load Balancing the Backoffice | CMS](#load-balancing-the-backoffice-cms)
- [Logging With Load Balancing | CMS](#logging-with-load-balancing-cms)
- [SignalR In Load Balanced Environments | CMS](#signalr-in-load-balanced-environments-cms)

---

### Load Balancing Azure Web Apps | CMS

Ensure you read the [Load Balancing overview](/umbraco-cms/fundamentals/setup/server-setup/load-balancing) and general [Azure Web Apps](/umbraco-cms/fundamentals/setup/server-setup/azure-web-apps) documentation before you begin - you will need to ensure that your ASP.NET Core & logging configurations are correct.

2 x App service plans with 1 x web app in each:

One for the backoffice (Administrative) environment

One for your scalable public-facing environment (Public)


1 x SQL server that is shared with these 2 web apps


The setup above will allow for the proper scaling of the Administrative and Public web apps.

The App Service plan with the Administrative web app should only be scaled up. The reason for this is that the web app needs to stay as a single instance.

The App Service plan with the Public web app can be scaled both out and up.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-89f00adff7bc1ee548d00ef2cfe83b15bf99e532%252Floadbalanced-infrastructure.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3a57f6b0&sv=2)

The single instance Backoffice Administrative Web App should be set to use [SyncedTempFileSystemDirectoryFactory](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/file-system-replication#examine-directory-factory-options).

The multi-instance Scalable Public Web App should be set to use [TempFileSystemDirectoryFactory](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/file-system-replication#examine-directory-factory-options).

When an instance of Umbraco starts up it generates some 'temporary' files on disk. In a normal IIS environment, these would be created within the folders of the Web Application. In an Azure Web App, we want these to be created in the local storage of the actual server that Azure happens to be used for the Web App. So we set this configuration setting to 'true' and the temporary files will be located in the environment temporary folder. This is required for both the performance of the website as well as to prevent file locks from occurring due to the nature of Azure Web Apps shared files system.

Umbraco runs within a .

When a host restarts, the current host 'winds down' while another host is started. This means there can be more than one live host during a restart. Restarts can occur in many scenarios including when an Azure Web App auto-transitions between hosts, you scale the instances or you utilize slot swapping.

Some file system based services in Umbraco such as the Published Cache and Lucene files can only be accessed by a single host at once. Umbraco manages this synchronization by an object called `IMainDom`.


By default **Umbraco v9.4 & 9.5** uses a system-wide semaphore locking mechanism. This mechanism only works on Windows systems and doesn't work with multi-instance Azure Web Apps. We need to swap it out for an alternative file system based locking mechanism by using the following appSetting. With **Umbraco v10+** `FileSystemMainDomLock`

is the default setting.

Apply this setting to both the **SCHEDULINGPUBLISHER** Administrative server and the **SUBSCRIBER** scalable public-facing servers.

You can also copy the following JSON directly into your Azure Web App configuration via the Advanced Edit feature.

Create an Azure SQL database

Install Umbraco on your backoffice administrative environment and ensure to use your Azure SQL Database

Install Umbraco on your scalable public-facing environment and ensure to use your Azure SQL Database

Test: Perform some content updates on the administrative environment, ensure they work successfully in that environment, then verify that those changes appear on the scalable public-facing environment

Fix the backoffice environment to be the SCHEDULINGPUBLISHER scheduling server and the scalable public-facing environment to be SUBSCRIBERs - see

[Setting Explicit Server Roles](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/flexible-advanced#explicit-schedulingpublisher-server)

Ensure all Azure resources are in the same region to avoid connection lag.

**Do not scale your backoffice administrative environment** this is not supported and can cause issues.

The public-facing subscriber Azure Web Apps can be manually or automatically scaled up or down and is supported by Umbraco's load balancing.

Since you have 2 x web apps, when you deploy you will need to deploy to both places - There are various automation techniques you can use to simplify the process. That is outside the scope of this article.

This also means that you should not be editing templates or views on a live server as SchedulingPublisher and Subscriber environments do not share the same file system. Changes should be made in a development environment and then pushed to each live environment.

Last updated

Was this helpful?

---

### Standalone File System | CMS

No file replication is configured, deployment handles updating files on the different servers.

If the file system on your servers isn't performing any file replication then no *Umbraco* configuration file changes are necessary. However Media will need to be configured to use a shared location such as Blob storage or S3.

Depending on the configuration and performance of the environment's local storage you might need to consider [Examine Directory Factory Options](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/file-system-replication#examine-directory-factory-options) and the .

The servers are performing file replication, updates to a file on one server, updates the corresponding file on any other servers.

If the file system on your servers is performing file replication then the Umbraco temporary folder (`~/umbraco/Data/TEMP`

) must be excluded from replication.

If the file system on your servers is located on shared storage you will need to configure Umbraco to locate the Umbraco temporary folder outside of the shared storage.

A common way to replicate files on Windows Server is to use [DFS](https://msdn.microsoft.com/en-us/library/windows/desktop/bb540031(v=vs.85), which is included with Windows Server.

Additional DFS resources:

There are other alternatives for file replication out there, some free and some licensed. You'll need to decide which solution is best for your environment.

When deploying Umbraco in a load balanced scenario using file replication, it is important to ensure that not all files are replicated - otherwise you will experience file locking issues. Here are the folders and files that should not be replicated:

`~/umbraco/Data/TEMP/*`


Alternatively store the Umbraco temporary files in the local server's 'temp' folder and set Examine to use a [Directory Factory](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/file-system-replication#examine-directory-factory-options).

Achieve this by changing the value of the `LuceneDirectoryFactory`

setting to 'TempFileSystemDirectoryFactory' in the `appsettings.json`

. The downside is that if you need to view temporary files you'll have to find it in the temp files. Locating the file this way isn't always clear.

Below is shown how to do this in a Json configuration source.

`~/umbraco/Logs/*`

This is

**optional**and depends on how you want your logs configured (see below)


If for some reason your file replication solution doesn't allow you to not replicate specific files folders (which it should!!) then you can use an alternative approach by using virtual directories.

The following is not the recommended setup but it is a viable alternative:

Copy the

`~/umbraco/Data/TEMP`

directory to each server, outside of any replication areas or to a unique folder for each server.Create a virtual directory (not a virtual application) in the

`~/umbraco/Data/`

folder, and name it`TEMP`

. Point the virtual directory to the folder you created in step 2.You may delete the

`~/umbraco/Data/TEMP`

folder from the file system - not IIS as this may delete the virtual directory - if you wish.

IIS configuration is pretty straightforward with file replication. IIS is only reading files from its own file system like a normal IIS website.

In some scenarios you have a mixture of standalone and synchronised file systems. An example of this is Azure Web Apps where the file system isn't replicated between backoffice and front end servers but is replicated between all front end servers, in this configuration you should follow the steps for synchronised file systems.

There is a specific documentation for load balancing with [Azure Web Apps](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/azure-web-apps)

The

`TempFileSystemDirectoryFactory`

allows Examine to store indexes directly in the environment temporary storage directory, and should be used instead of`SyncTempEnvDirectoryFactory`

mentioned above.

The

`SyncedTempFileSystemDirectoryFactory`

enables Examine to sync indexes between the remote file system and the local environment temporary storage directory, the indexes will be accessed from the temporary storage directory. This setting is needed because Lucene has issues when working from a remote file share so the files need to be read/accessed locally. Any time the index is updated, this setting will ensure that both the locally created indexes and the normal indexes are written to. This will ensure that when the app is restarted or the local environment temp files are cleared out that the index files can be restored from the centrally stored index files.

If you are load balancing with [Azure Web Apps](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/azure-web-apps) make sure to check out the article we have for that specific set-up.

Once you are familiar with how flexible load balancing works, you might be interested in some [advanced techniques](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/flexible-advanced).

[Previous SignalR In Load Balanced Environments chevron-left](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/signalr-in-backoffice-load-balanced-environment)

[Next Advanced Techniques With Flexible Load Balancing chevron-right](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/flexible-advanced)

Last updated

Was this helpful?

---

### Advanced Techniques With Flexible Load Balancing | CMS

*This describes some more advanced techniques that you could achieve with flexible load balancing*

The election process that runs during the startup of an Umbraco instance determines the server role that instance will undertake.

There are two server roles to be aware of for flexible load balancing:

`SchedulingPublisher`

- The Umbraco instance usually used for backoffice access, responsible for running scheduled tasks.`Subscriber`

- A scalable instance that subscribes to content updates from the SchedulingPublisher server, not recommended to be used for backoffice access.

These new terms replace 'Master and Replica', in Umbraco versions 7 and 8.

It is recommended to configure an explicit SchedulingPublisher server since this reduces the amount of complexity that the election process performs.

The first thing to do is create a couple of small classes that implement `IServerRoleAccessor`

one for each of the different server roles:

```
public class SchedulingPublisherServerRoleAccessor : IServerRoleAccessor
{
    public ServerRole CurrentServerRole => ServerRole.SchedulingPublisher;
}

public class SubscriberServerRoleAccessor : IServerRoleAccessor
{
    public ServerRole CurrentServerRole => ServerRole.Subscriber;
}
```

then you'll need to replace the default `IServerRoleAccessor`

for the your custom registrars. You'll can do this by using the `SetServerRegistrar()`

extension method on `IUmbracoBuilder`

from a [Composer](/umbraco-cms/implementation/composing).

Now that your subscriber servers are using your custom `SubscriberServerRoleAccessor`

class, they will always be deemed 'Subscriber' servers and will not attempt to run the automatic server role election process or task scheduling.

By setting your SchedulingPublisher server to use your custom `SchedulingPublisherServerRoleAccessor`

class, it will always be deemed the 'SchedulingPublisher' and will always be the one that executes all task scheduling.

This description pertains only to Umbraco database tables

In some cases infrastructure admins will not want their front-end servers to have write access to the database. By default front-end servers will require write full access to the following tables:

`umbracoServer`

`umbracoNode`


This is because by default each server will inform the database that they are active and more importantly it is used for task scheduling. Only a single server can execute task scheduling and these tables are used for servers to use a server role election process without the need for any configuration. So in the case that a subscriber server becomes the SchedulingPublisher task scheduler, **it will require write access to all of the Umbraco tables**.

In order to have read-only database access configured for your front-end servers, you need to implement the [Explicit SchedulingPublisher server](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/flexible-advanced#explicit-schedulingpublisher-server) configuration mentioned above.

Now that your subscriber servers are using your custom `SubscriberServerRoleAccessor`

class, they will always be deemed 'Subscriber' servers and will not attempt to run the automatic server role election process or task scheduling. Because you are no longer using the default `ElectedServerRoleAccessor`

they will not try to ping the umbracoServer table.

When configuring a server as a read-only subscriber, Umbraco automatically detects the state and disables specific background database write operations, such as DistributedBackgroundJobs. A notable exception is the LastSynced process. To ensure the subscriber server tracks synchronization without database write access, Umbraco redirects these updates to a local file instead of the database.

If using [SqlMainDomLock](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/azure-web-apps#appdomain-synchronization) on Azure WebApps then write-permissions are required for the following tables for all server roles including 'Subscriber'.

`umbracoLock`

`umbracoKeyValue`


SQL Server Replica databases cannot be used as they are read-only without replacing the default MainDomLock with a custom provider.

The configurations can be adjusted to control how often the load balancing instructions from the database are processed and pruned.

Below is shown how to do this from a JSON configuration source.

Options:

`TimeToRetainInstructions`

- The timespan to keep instructions in the database; records older than this number will be pruned.`MaxProcessingInstructionCount`

- The maximum number of instructions that can be processed at startup; otherwise the server cold-boots (rebuilds its caches)`TimeBetweenSyncOperations`

- The timespan to wait between each sync operations`TimeBetweenPruneOperations`

- The timespan to wait between each prune operation

These setting would normally be applied to all environments as they are added to the global app settings. If you need these settings to be environment specific, we recommend using [environment specific appSetting files](/umbraco-cms/reference/configuration).

Last updated

Was this helpful?

---

### Load Balancing the Backoffice | CMS

This article contains specific information about load balancing the Umbraco backoffice. Ensure you read the [Load Balancing Overview](/umbraco-cms/fundamentals/setup/server-setup/load-balancing) and relevant articles about general load balancing principles before you begin.

By default, the Umbraco load balancing setup assumes there is a single backoffice server and multiple front-end servers. From version 17, it's possible to load balance the backoffice. This means there's no need to differentiate between backoffice servers and front-end servers. However, this requires some additional configuration steps.

Before configuring backoffice load balancing, you need to decide between two approaches:

Configure your load balancer to use sticky sessions (session affinity). This ensures all requests from a client are routed to the same server.

**Requirements:**

Sticky sessions are enabled on your load balancer.

Any SignalR backplane (SQL Server, Redis, or Azure SignalR Service).


This approach works well for most scenarios.

If you want true horizontal scaling without server affinity, you need additional configuration:

**Requirements:**

[Azure SignalR Service](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/signalr-in-backoffice-load-balanced-environment)for SignalR connection management.for session state management.


Umbraco's cache is built on Microsoft's HybridCache, which automatically uses IDistributedCache as a second-level cache when configured. This means that setting up IDistributedCache for session management also enables distributed caching of Umbraco content across all servers. See [Cache Settings](/umbraco-cms/reference/configuration/cache-settings) for more information.

Traditional SignalR backplanes (SQL Server, Redis) only distribute messages between servers. The WebSocket connection remains tied to a specific server. Without sticky sessions, you will encounter intermittent "No connection with that ID" errors. Only Azure SignalR Service supports stateless operation because it centralizes connection management.

Umbraco uses server roles to differentiate between backoffice servers and front-end servers. Since all servers will be backoffice servers, you need to add a custom `IServerRoleAccessor`

to specify this.

Start by implementing a custom `IServerRoleAccessor`

that pins the role as `SchedulingPublisher`:


You can now register this accessor either in `Program.cs`

or via a Composer:

This will ensure that all servers are treated as backoffice servers.

When load balancing the backoffice, all servers have their own repository caches. Changes made on one server are not reflected on other servers until their cache expires.

To solve this issue, a cache versioning mechanism is used. This is similar to optimistic concurrency control. Each server has a version number for its cache. When a server makes a change, it updates the version identifier. The other servers can then check the version identifier before accessing the cache. If the cache is out of date, they invalidate it.

This means the server needs to check the version identifier before a cache lookup. By default, this behavior is disabled. It's only required when load balancing the backoffice.

You can enable this on the Umbraco builder, either in `Program.cs`

or via a Composer:

The Umbraco backoffice uses SignalR for real-time updates and notifications. When load balancing the backoffice, ensure SignalR is configured correctly based on your chosen approach (sticky sessions or stateless). See [SignalR in a Backoffice Load Balanced Environment](/umbraco-cms/fundamentals/setup/server-setup/load-balancing/signalr-in-backoffice-load-balanced-environment) for configuration details.

If you have custom recurring background jobs that should only run on a single server, you'll need to implement `IDistributedBackgroundJob`

. See [Scheduling documentation](/umbraco-cms/reference/scheduling#background-jobs-when-load-balancing-the-backoffice) for more information.

When load balancing the backoffice, temporary files uploaded through `/umbraco/management/api/v1/temporary-file`

, for instance, media uploads, must be accessible across all server instances.

Temporary files are saved to `umbraco/Data/TEMP/TemporaryFile/`

by default.

**Azure deployments using scale out:** No additional configuration is required, as the `umbraco`

folder is shared between instances.

**Other Environments:** Configure a shared storage location using [the Umbraco:CMS:Hosting:TemporaryFileUploadLocation setting.](/umbraco-cms/reference/configuration/hostingsettings#temporary-file-upload-location)

Ensure this path points to a location accessible by all server instances, such as a shared drive or volume.

**Advanced Scenarios:** You can implement a custom `ITemporaryFileRepository`

for external storage solutions such as Azure Blob Storage.

Last updated

Was this helpful?

---

### Logging With Load Balancing | CMS

Last updated

Was this helpful?

Umbraco v8+ uses Serilog for logging. When load balancing Umbraco consideration should be given as to how the log files from each server will be accessed.

There are many Serilog Sinks available and one of these may be appropriate to store logs for all servers in a central repository such as Azure Application Insights or Elmah.io.

For more information, see .

Last updated

Was this helpful?

Was this helpful?

---

### SignalR In Load Balanced Environments | CMS

When load balancing the backoffice, we also need to take care of the client-to-server communication outside of web requests. Umbraco uses SignalR to abstract away these types of communication. This also allows us to support load balancing by replacing how the communication is done by introducing a backplane.

A traditional SignalR backplane (such as SQL Server or Redis) distributes *messages* between servers. Any server can broadcast messages to clients connected to other servers. However, the WebSocket connection remains tied to the server the client initially connected to.

Using a traditional backplane, routing HTTP requests to a server without the active WebSocket connection causes "No connection with that ID" errors.

**Azure SignalR Service** works differently. Instead of clients connecting directly to your servers, they connect to the Azure SignalR Service. This centralizes connection management, allowing requests to be handled by any server without sticky sessions.

When load balancing the backoffice, you need to decide between two approaches:

Configure your load balancer to use sticky sessions (session affinity). This ensures that once a client connects to a server, all subsequent requests from that client go to the same server.

With sticky sessions enabled, any SignalR backplane works:

SQL Server backplane

Redis backplane

Other third-party backplanes


This approach works if your load balancer supports sticky sessions.

If you want fully stateless servers without sticky sessions, you need:

**Azure SignalR Service**for SignalR connection management.**IDistributedCache**for session state management (see ).

This approach requires additional setup but allows for true horizontal scaling without server affinity.

Umbraco's cache is built on Microsoft's HybridCache, which automatically uses IDistributedCache as a second-level cache when configured. This means that setting up IDistributedCache for session management also enables distributed caching of Umbraco content across all servers. See [Cache Settings](/umbraco-cms/reference/configuration/cache-settings) for more information.

Choosing the right backplane comes down to a few factors:

Whether you can use sticky sessions

Message throughput requirements

Cost

The infrastructure you already have in place


Microsoft has a good list of available backplanes in its , including a list of well-known .

The following code examples show how you can activate SignalR load balancing using an Umbraco composer.

Both Umbraco and these composers use `.AddSignalR()`

. This duplication isn't a concern as the underlying code registers the required services as singletons.

It is possible to use your existing database as a backplane. If this database is hosted in Azure it is not possible to enable Service Broker which will have an impact on message throughput. Nevertheless, it might be sufficient to cover your needs. For more information, check out the .

Add a reference to the

`IntelliTect.AspNetCore.SignalR.SqlServer`

NuGet package.Add the following composer to your project:


Set up a resource as described in the .

Make sure the

`connectionstring`

is set up under the following key:`Azure:SignalR:ConnectionString`

.Add a reference to

`Microsoft.Azure.SignalR`

NuGet package.Add the following composer to your project:


Last updated

Was this helpful?

---

---

## File And Folder Permissions | CMS

Information on file and folder permissions required for Umbraco sites

| File / folder | Permission | Comment |
|---|---|---|
| `/appSettings*.json` | Modify / Full control | Only needed for setting database and a global identifier during installation. So can be set to read-only afterwards for enhanced security. |
| `/App_Plugins` | Modify / Full control | Should always have modify rights as the folder and its files are used by packages. Not part of your project by default. |
| `/umbraco` | Modify / Full control | Should always have modify rights as the folder and its files are used for cache and storage. |
| `/Views` | Modify / Full control | Should always have modify rights as the folder and its files are used for Templates and Partial views |
| `/wwwroot/css` | Modify / Full control | Should always have modify rights as the folder and its files are used for css files. |
| `/wwwroot/media` | Modify / Full control | Should always have modify rights as the folder and its files are used for Media files uploaded via the Umbraco CMS backoffice. |
| `/wwwroot/umbraco` | Modify / Full control | Should always have modify rights as the folder and its files are used by packages. Not part of your project by default. |
| `/wwwroot/scripts` | Modify / Full control | Should always have modify rights as the folder and its files are used for script files. |

Last updated

Was this helpful?

---

## Running Umbraco in Docker | CMS

Exactly how you choose to compose your Dockerfile will depend on your project specific needs. This section is not intended as a comprehensive guide, rather as an overview of topics to be aware of when hosting in Docker.

Docker is a platform for developing, shipping, and running applications in containers. Multiple services exist for hosting these containers. For more information, refer to the

By default, files created inside a container are written to an ephemeral, writable container layer. This means that the files don't persist when the container is removed, and it's challenging to get files out of the container. Additionally, this writable layer is not suitable for performance-critical data processing.

This has implications when running Umbraco in Docker.

For more information, refer to the .

In general, when working with files and Docker you work in a "push" fashion with read-only layers. When you build, you take all your files and "push" them into this read-only layer.

This means that you should avoid making files on the fly, and instead rely on building your image.

In an Umbraco context, this means you should not create or edit template, script or stylesheet files via the backoffice. These should be deployed as part of your web application and not managed via Umbraco.

Similarly, you shouldn't use InMemory modelsbuilder, since that also relies on creating files on the disk. While this is not a hard requirement, it doesn't provide any value unless you are live editing your site.

Instead, configure models builder to use "source code" mode in development, and "none" in production, as .

Umbraco writes logs to the `/umbraco/Logs/`

directory. Due to the performance implications of writing to a writable layer, and the limited size, it is recommended to mount a volume to this directory.

You may prefer to avoid writing to disk for logs when hosting in containers. If so, you can disable this default behavior and register a custom Serilog sink to alternative storage, such as Azure Table storage.

You can also provide an alternative implementation of a common abstraction for the log viewer. In this way you can read logs from the location where you have configured them to be written.

For more details, read the article on Umbraco's [log viewer](/umbraco-cms/fundamentals/backoffice/logviewer).

The `/umbraco/Data/`

directory is used to store temporary files, such as file uploads. Considering the limitations of the writable layer, you should also mount a volume to this directory.

It's recommended to not store media in the writable layer. This is for similar performance reasons as logs, but also for practical hosting reasons. You likely want to persist media files between containers.

One solution is to use bind mounts. The ideal setup, though, is to store the media and ImageSharp cache externally. For more information, refer to the .

Your solution may require some specific files to run, such as license files. You will need to pass these files into the container at build time, or mount them externally.

When running websites in Docker, it's common to do so behind a reverse proxy or load balancer. In these scenarios you will likely handle SSL termination at the reverse proxy. This means that Umbraco will not be aware of the SSL termination, and will complain about not using HTTPS.

Umbraco checks for HTTPS in two locations:

The

`HstsCheck`

health check - This will result in a failed healthcheck.The

`UseHttpsValidator`

- This will result in a build error, if Production runtime mode is used.

To avoid these checks failing, you can remove them in your project.

The health check must be removed via configuration, through the `appsettings.json`

file, environment variables, or similar. For more information see the [Health Check documentation](/umbraco-cms/reference/configuration/healthchecks).

The `HstsCheck`

key is `E2048C48-21C5-4BE1-A80B-8062162DF124`

so the appsettings will look something like:

The `UseHttpsValidator`

must be removed through code For more information see the [Runtime mode documentation](/umbraco-cms/fundamentals/setup/server-setup/runtime-modes).

The code to remove the validator can look something like:

Last updated

Was this helpful?

---

## Runtime Modes | CMS

This section describes how to use the runtime mode setting to optimize Umbraco for the best development experience or optimal production environment.

You can configure the runtime mode to optimize Umbraco for different development experiences and environments by setting `Umbraco:CMS:Runtime:Mode`

to one of the available modes:

`BackofficeDevelopment`

(default)`Development`

`Production`


This can be done via the `appsettings.json`

file, environment variables, or any other .NET configuration provider (like Azure Key Vault/App Configuration). Although this setting affects how Umbraco behaves at runtime, some modes have prerequisites on how the project is built/published. Make sure to read the descriptions of each mode before changing this setting from the default `BackofficeDevelopment`

mode, as incorrect configuration can result in your application not starting (by throwing a `BootFailedException`

).

The `BackofficeDevelopment`

mode is the default behavior for Umbraco: it does not optimize Umbraco for any specific environment and does not have any prerequisites. This mode allows for rapid development (without having to recompile/rebuild your project), including all development from within the backoffice.

The `Development`

mode can be used when you're developing from an IDE (like Visual Studio, VS Code, or Rider) or the dotnet CLI (e.g. using `dotnet watch`

). It is a recommended prerequisite if you want to use the `Production`

mode in your production environment.

This mode disables in-memory ModelsBuilder generation and validates the following setting:

`Umbraco:CMS:ModelsBuilder:ModelsMode`

is**not set**to`InMemoryAuto`.


If you want to use the generated models, use `SourceCodeAuto`

or `SourceCodeManual`

. These require manually recompiling the project after the models have changed (for example after updating Document Types, Media Types, Member Types, or Data Types). Razor views (`cshtml`

files) will still be automatically compiled at runtime. They allow you to quickly iterate on the rendered output from templates, partial views, and view components.

The recommended approach to enable `Development`

mode is to update the `appsettings.json`

file with the following settings:

Ensure your models are generated by running Umbraco and navigating to **Settings** > **Models Builder** > **Generate models**. You can remove the following properties from your `csproj`

project file to enable the compilation of Razor views (which also ensures your views do not contain compilation errors and is a prerequisite for enabling `Production`

mode):

Fix any compilation errors you might get after this, e.g. if you accidentally referenced deleted models or properties. Running the application will still show the rendered content and you're now ready to optionally enable `Production`

mode on your production environment.

Ensure you have the `<CopyRazorGenerateFilesToPublishDirectory>true</CopyRazorGenerateFilesToPublishDirectory>`

property set in your `csproj`

project file, so Razor views are always copied to the publish directory. This is required by the CMS to display the contents in the backoffice, for Forms to lookup custom theme views and for Deploy to be able to compare schemas (otherwise you'll get schema mismatches).

Use `Production`

mode to ensure your production environment is running optimally by disabling development features and validating whether specific settings are configured to their recommended production values.

This mode disables both in-memory ModelsBuilder generation (see [Development mode](/umbraco-cms/fundamentals/setup/server-setup/runtime-modes#development-mode)) and Razor (cshtml) runtime compilation. Production mode requires you to compile your views at build/publish time and enforces the following settings for optimal performance/security:

The application is built/published in Release mode (with JIT optimization enabled), e.g. using

`dotnet publish --configuration Release`

;`Umbraco:CMS:WebRouting:UmbracoApplicationUrl`

is set to a valid URL;`Umbraco:CMS:Global:UseHttps`

is enabled;`Umbraco:CMS:ModelsBuilder:ModelsMode`

is set to`Nothing`.


To compile your views at build/publish time, remove the `<RazorCompileOnBuild>`

and `<RazorCompileOnPublish>`

properties from your project file (see the [Development mode](/umbraco-cms/fundamentals/setup/server-setup/runtime-modes#development-mode) section). If you don't, Umbraco can't find the templates and will return 404 (Page Not Found) errors.

The recommended approach to enable `Production`

mode is to update the `appsettings.Production.json`

file (or create one) with the following settings:

Although you can still edit document types and views (if not running from the published output), changes won't be picked up until you've rebuilt your project or republished the application.

Models won't be generated by ModelsBuilder (because the mode is set to `Nothing`

), requiring you to do all your changes while in `Development`

mode.
As Models Builder is set to `Nothing`

, the Models Builder dashboard is disabled in the backoffice of live environment.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-14492e61ab306748d331dee09c90a8fa1be221ed%252FModelsBuilderDisabledOnProduction.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=ecd609c9&sv=2)


Also, templates cannot be edited on live environment as runtime compilation is not enabled and is set to Production.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f6379dc05f643810c68d60b58a9530dbfeb5626b%252FTemplatedCannotBeEditedWhenRuntimeIsProduction.png%3Falt%3Dmedia&width=300&dpr=3&quality=100&sign=1b0cfd4a&sv=2)


Also ensure the `UmbracoApplicationUrl`

is updated to the primary URL of your production environment, as this is used when sending emails (password reset, notifications, health check results, etc.).

Static web assets are disabled when using Production mode, following . If you are running a non-Development environment using the Production runtime mode from source (non-published output), you will need to explicitly enable this. You can add the following line of code to your `Program.cs`

file:

This should not be used in a more typical production environment where you are hosting your application from published output.

Validation of the above-mentioned settings is done when determining the runtime level during startup using the new `IRuntimeModeValidationService`

and when it fails, causes a `BootFailedException`

to be thrown. The default implementation gets all registered `IRuntimeModeValidators`

to do the validation, making it possible to remove default checks and/or add your own (inherit from `RuntimeModeProductionValidatorBase`

, if you only want to validate against the production runtime mode). The following validators are added by default:

`JITOptimizerValidator`

- Ensure the application is built/published in Release mode (with JIT optimization enabled) when in production runtime mode, e.g. using`dotnet publish --configuration Release`

;`UmbracoApplicationUrlValidator`

- ensure`Umbraco:CMS:WebRouting:UmbracoApplicationUrl`

is configured when in production runtime mode;`UseHttpsValidator`

- ensure`Umbraco:CMS:Global:UseHttps`

is enabled when in production runtime mode;`ModelsBuilderModeValidator`

- ensure`Umbraco:CMS:ModelsBuilder:ModelsMode`

is not set to`InMemoryAuto`

when in development runtime mode and set to`Nothing`

when in production runtime mode.

The following example removes the default `UmbracoApplicationUrlValidator`

and adds a new custom `DisableElectionForSingleServerValidator`:


Last updated

Was this helpful?

---
