# Multisite Setup | CMS

A guide to setting up a multisite solution in Umbraco

Structuring your website

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-aa391f1a24c89cf030d6048135b14d17387e9e70%252F1-addinghostnames.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e5e4fc1b&sv=2)

Mapping the hostnames to individual websites/root nodes

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-df46387ba42886f98650af7af70c0cdf15d24805%252Fculturehostnames-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d304b1f3&sv=2)

Culture and hostnames ![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ec9d4ea9e01f0433ac3ad6faf052701755bd9215%252Finherit-domain.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8649d243&sv=2)

Domain

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-98fd5b021c9e0b33f77396a6201b921403ee43a0%252F6-dolphins.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=93162f0a&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-6243bd5c891475b2c2fd6196a915da7e37a39d83%252F7-swato.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9b4f46b0&sv=2)

Best practices

Last updated

Was this helpful?

A guide to setting up a multisite solution in Umbraco

This tutorial explains how to host multiple sites from one project or installation of Umbraco. For practical reasons, it is recommended to use on Umbraco Cloud projects.

When using Baselines on Umbraco Cloud for a multisite solution, you don’t need to worry about limits. You may also see better performance compared to hosting multiple websites in one project.

To create a multi-language site, see the [Creating a Multilingual Site](/umbraco-cms/tutorials/multilanguage-setup) tutorial.

Structuring your website

The best way to handle a multisite solution is to create multiple root nodes in the Content section. Each root node acts as a separate website.

All websites in the solution use the same schema. In most cases, content pages on website A use the same properties as on website B.

On Umbraco Cloud, hostnames must be mapped to the project. Before mapping hostnames to individual websites, add them to the **Hostnames** page in the Cloud portal. This ensures they are secure with TLS.

Keep in mind that [hostnames must be configured in a specific way arrow-up-right](/umbraco-cloud/set-up/project-settings/manage-hostnames)

Mapping the hostnames to individual websites/root nodes

At this point, multiple root nodes exist, each acting as a separate website. To map hostnames to root nodes:

Go to the

**Content**section.Click

**...**next to the root node to assign the hostname.Select

**Culture and Hostnames**.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-df46387ba42886f98650af7af70c0cdf15d24805%252Fculturehostnames-v14.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d304b1f3&sv=2)

Culture and hostnames Click

**Add new Domain**in the**Domains**section.Enter the domain in the

**Domain**field.Select the language from the

**Language**drop-down list. For multilanguage setups, different hostnames can map to specific languages.![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ec9d4ea9e01f0433ac3ad6faf052701755bd9215%252Finherit-domain.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8649d243&sv=2)

Domain Click

**Save**.Repeat steps 2-7 for each root node in the Content tree.


The sites are now available under the assigned domains.

Best practices

This setup can be useful, but it also has drawbacks. Keep in mind that having multiple sites in one Umbraco project:

Might increase resource usage.

Could interfere with editors' workflows, especially if multiple people are working on both websites at once. This is because the solution still uses one shared database for both websites.

Limits options for developing new features and making schema changes.


On Umbraco Cloud, it is recommended to use . Baselines provide added benefits and greater stability compared to hosting multiple sites in one project.

Last updated

Was this helpful?

Was this helpful?