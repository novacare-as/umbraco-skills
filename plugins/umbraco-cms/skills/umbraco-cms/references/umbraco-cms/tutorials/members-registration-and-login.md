# Member Registration and Login | CMS

In this article you can learn about how to create Member registration and login functionality for the frontend of your application.

Prerequisites

Create Partial Views for Registration and Login

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-67a27313078a0a6f78a43c038bd6e041b4fbc258%252Fcreate-partial-view-from-snippet.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fdb36786&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-264a966a96867a730f1c9ca6d9dbbf37b4dfea4b%252Fcreate-partial-view-from-login-snippet.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f2303d68&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1d4b056d86be88eccbadb8914c879c0d64cb209d%252Flist-of-partial-views.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=4bf39a85&sv=2)

Create a new Document Type for Registration and Login

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8a719670c04c0711d24d90483c596c5ece398204%252Fcomposition-view.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9649055f&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-200946bef084a4bfb1784ea5e80b7ba1cc991a0d%252Fstructure-setting.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=d5bf57b1&sv=2)

Render the partial views in the template

Create the Register/Login page

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d6ce01db6b10ef16717badae356fa4e708e8e26f%252Fv14-create-register-login-page.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=53f4c878&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-46a30c3f6266eac485132a75a5778d42bc8e8198%252Fregister-login-page-rendered.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=e2aba1b9&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-19d78f48d28f002358203bfa12cc900529e288cf%252Fmembers-overview.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ff42af2f&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-666eb0ebb08214f7eb3b01cbed9679e213d74eda%252Fv14-login-status.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=83b2e84f&sv=2)

Member-only pages/Restricted access

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e05cbb8be20b0a2d87c4b4663d6981ff3c8cfafb%252Fcreate-member-group.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=79cfddb2&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-d9760888528558dc6730c44c61c662b404e9fb5b%252Fv14-create-member-group-step-2.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fafe3c25&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-53618dcae48a32130f6c2c7c63e5ccede1d32463%252Fv14-assign-member-group.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9f914bc1&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-ee09e6e888f78bd5732fe9e1aef602f306a1eea0%252Fv16-restrict-content-access.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3e1293a7&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-56edc0cd0691c420cd8aaed138478933d67a728f%252Fv14-configure-public-access.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8ff11db4&sv=2)

Assigning new members to groups automatically

Last updated

Was this helpful?