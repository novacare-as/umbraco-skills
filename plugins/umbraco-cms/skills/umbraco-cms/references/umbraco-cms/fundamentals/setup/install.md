# Install

## Contents

- [Local IIS With Umbraco | CMS](#local-iis-with-umbraco-cms)
- [Install using .NET CLI | CMS](#install-using-net-cli-cms)
- [Install using Visual Studio Code | CMS](#install-using-visual-studio-code-cms)
- [Installing Nightly Builds | CMS](#installing-nightly-builds-cms)
- [Running Umbraco in Docker using Docker Compose | CMS](#running-umbraco-in-docker-using-docker-compose-cms)
- [Running Umbraco on Linux/macOS | CMS](#running-umbraco-on-linuxmacos-cms)
- [Unattended Installs | CMS](#unattended-installs-cms)
- [Install using Visual Studio | CMS](#install-using-visual-studio-cms)

---

## Local IIS With Umbraco | CMS

This article describes how to run an Umbraco 9 site on a local IIS server.

Setting up prerequisites

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b139dcb48047cd1ed549481f1ceeaedf98d90330%252Fiis-module.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=40a0ed8a&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-dd07e16fb942be93538355d9e2b4d1ebe0ba2f0b%252Fiis-site.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=260450ae&sv=2)

Add permissions to NuGet cache folder

Add new launch profile

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-7cc99dd19c5cb78633a798fabd904ce854cc76d2%252Flaunchprofiles.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=597ea27c&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-1b094bdb55682f5c8f583419c007fe4b7801ba64%252Fvoila.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=a0ee4ef4&sv=2)

Last updated

Was this helpful?

This article describes how to run an Umbraco 9 site on a local IIS server.

This is a quick guide on getting your Umbraco website running locally on IIS.

The guide will assume you already have IIS configured and know your way around it, as well as having a local website you wish to host.

Setting up prerequisites

First, you need to ensure you have "Development time IIS support installed". To check this, go to the Visual Studio installer, click modify and check on the right side under "ASP.NET and web development":

Once that is installed you should set up a new IIS site - and make sure to add the hostname to your hosts file as well. Here is my setup for an example:

For the path you want to point it at the root of your site - where the `.csproj`

file is.

Add permissions to NuGet cache folder

You might need to change permissions for the NuGet cache folder - `C:\users\<username>\.nuget\packages`

. The user or group (IIS_IUSRS) that the IIS site is running on requires Read permissions on this folder because this is where some of the files for Umbraco and Umbraco packages are being served from during development. If the IIS user or group does not have permission to read from the NuGet cache folder, you could run into a `DirectoryNotFoundException`

while running the site.

When the site is published these files are copied from the NuGet cache folder to `wwwroot/umbraco`

and `wwwroot/App_Plugins`

and these folders will typically have the correct permissions. For more information on setting permissions, see the [File and folder permissions](/umbraco-cms/fundamentals/setup/server-setup/permissions) article.

Add new launch profile

At this point you can go to your Visual Studio solution of the site and in the `Properties`

folder there is a `launchSettings.json`

file, that looks like this:

You can add a new profile called IIS, and point it at your local domain. Here it is with my example domain:

At this point IIS will be added to the launch profiles, and you can run the site from Visual Studio by choosing IIS in the dropdown:

And finally the site is running from your local IIS:

Last updated

Was this helpful?

Was this helpful?

```
{
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iisExpress": {
      "applicationUrl": "http://localhost:40264",
      "sslPort": 44360
    }
  },
  "profiles": {
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "Umbraco.Web.UI.NetCore": {
      "commandName": "Project",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      },
      "applicationUrl": "https://localhost:44360;http://localhost:40264"
    }
  }
}
```

```
{
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iis": {
      "applicationUrl": "https://testsite.local",
      "sslPort": 0
    },
    "iisExpress": {
      "applicationUrl": "http://localhost:40264",
      "sslPort": 44360
    }
  },
  "profiles": {
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "IIS": {
      "commandName": "IIS",
      "launchBrowser": true,
      "launchUrl": "https://testsite.local",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "Umbraco.Web.UI.NetCore": {
      "commandName": "Project",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      },
      "applicationUrl": "https://localhost:44360;http://localhost:40264"
    }
  }
}
```

---

## Install using .NET CLI | CMS

We have made custom Umbraco templates that are available for use with `dotnet new`

. The steps below will demonstrate the minimum amount of actions required to get you going and set up an Umbraco project from the command line using .NET templates.

Install the latest .

Run

`dotnet new install Umbraco.Templates`

to install the project templates.*The solution is packaged up into the NuGet package**and can be installed into the dotnet CLI*.

Once that is complete, you can see that Umbraco was added to the list of available projects types by running

`dotnet new list`:


In some cases the templates may silently fail to install (usually this is an issue with NuGet sources). If this occurs you can try specifying the NuGet source in the command by running `dotnet new install Umbraco.Templates --nuget-source "https://api.nuget.org/v3/index.json"`.


To get **help** on a project template with `dotnet new`

run the following command:

`dotnet new umbraco -h`


From that command's output, you will get a better understanding of what are the default template options, as well as those command-line flags specific to Umbraco that you can use (as seen below):

Create a new empty Umbraco solution:

`dotnet new umbraco -n MyCustomUmbracoProject`


You will now have a new project with the name *MyCustomUmbracoProject*, or the name you chose to use. The new project can be opened and run using your favorite IDE or you can continue using the CLI commands.

If you want to create a solution file as well you can run the commands below.
`dotnet new sln`

`dotnet sln add MyCustomUmbracoProject`


Navigate to the newly created project folder:

`cd MyCustomUmbracoProject`

Build and run the new Umbraco .Net Core project:

`dotnet build`

`dotnet run`


The project is now running on the and has assigned a free available port to run it on. Look in the terminal window after the `dotnet run`

command to see the URLs.

The next step is to run through the Umbraco CMS installation. If you chose to use MS SQL Server/Azure you will need to add your connection string during this setup process to get access to the Umbraco backoffice.

Last updated

Was this helpful?

---

## Install using Visual Studio Code | CMS

Installing and setting up Visual Studio Code

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-29bb1f5f1df922202717dc2131e82e96720f59a1%252FMarketplace.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c8bd6682&sv=2)

Visual Studio Code install extension

Creating your Umbraco project

Configure Visual Studio Code to run the Umbraco project

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f5500b1d5098eefd7742f6f489179af5f9b5354b%252FVS_Code_Explorer.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c5559545&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-880a0e3e594bb921d81f762c70866a2b28745c54%252FConfigureTask.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=75888781&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8c11cb849b12e055c6cb21a8da2a0160c13d8553%252FTaskJsonFromTemplate.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1554bfde&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f8f28bc4d028cdf58a00c12526b185c02aabf275%252FNetcoreTemplate.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=b5c19db9&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0ce06b712d2be3fa123d1af3a0aea23e1780a052%252FCreate_LaunchJson_file.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=fd8a4c32&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e700d4609b94a550b16bb28785fada36c15eaa78%252FPrompt_Menu.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=6ca1bf95&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-8c6c135c273291df447d462f7175982b3677ae68%252FDropdown_option.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3e6cc7fd&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-0178fb8f0f0912f94cce419e51a790ff6d7b669a%252FlaunchJson.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=66af9dc1&sv=2)

Umbraco Web Installer

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b077660c7207e8080d9782f005581f6f02978bcc%252FInstall_Umbraco.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=bbd90a41&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-3694b3ca07f0cd43b85c3ab90c26a450597616cd%252Fv17-Backoffice.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=ec897716&sv=2)

Last updated

Was this helpful?

---

## Installing Nightly Builds | CMS

Instructions on installing nightly builds of Umbraco.

Adding the nightly feed as a NuGet source

Option 1: Using the command line

```
dotnet nuget add source "https://www.myget.org/F/umbraconightly/api/v3/index.json" -n "Umbraco Nightly"
```

Option 2: Using Visual Studio

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-748293bccb7032e3684439db4ec6b87327ec6ae6%252FPackage-Manager-Settings.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=407f627f&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-bd549030ecc80d767d96f962f0a36536b534a628%252FRegister_Nightly_Feed.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=de4f2b4a&sv=2)

Option 3: Using Rider

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-e17dee522b9932f40ef9abddd94ade478a83ab08%252FNuGet_NewFeed.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=96328284&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-5ce96af75da18fc65b23944f4923e34605ae2c9f%252FNewFeed_Details.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=bebe84d6&sv=2)

Finding the latest nightly version

Option 1: Using Visual Studio

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-68138f7e4b6e74fda6274e4b4cf4161e15e79dc3%252FManage_NuGet_Pkgs.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8677fa3e&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9ff2c8538dc2fbcb564282abb93e67b52c270a4c%252FManage_Packages.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=f9294ec1&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-341da76534c9e7a008cb2d0d4a3756c2cc8daab7%252FLatest_nightly_build_version.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=c333c1fa&sv=2)

Option 2: Using Rider

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-68701876301d3cb4f8f0428dbb0283c6db56c773%252FRider_Nightly_Feed.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=7353c2ec&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-9b60bb59f21ecc24d85a7532b421df1f14caba4d%252FRider_Nightly_Feed_version.jpg%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=14cc7d41&sv=2)

Installing the latest nightly version template

Last updated

Was this helpful?

---

## Running Umbraco in Docker using Docker Compose | CMS

Running Umbraco on docker locally using docker compose

This article shows how to run Umbraco locally in Docker using Docker Compose. You can use either SQL Server or SQLite for development.

This setup is intended for local development only. It is not recommended for production environments.

Before you can run Umbraco in Docker, make sure the following are installed:

.NET SDK with Umbraco Templates v16 or higher

Docker Desktop


To install Umbraco using the provided Dockerfile and Docker Compose setup, follow these steps:

Create a folder and navigate into it:


```
mkdir MyDockerProject
cd MyDockerProject
```

Create a new Umbraco project with Docker support:


```
dotnet new umbraco -n MyDockerProject --add-docker
```

Add Docker Compose files:


The `-P`

flag is required to specify the correct paths in the docker-compose file. The project is now ready to run with Docker Compose.

The folder structure should now look like this:

MyDockerProject/

Database/

Dockerfile

healthcheck.sh

setup.sql

startup.sh


MyDockerProject/

Your project files

Dockerfile

.dockerignore


.env

docker-compose.yml



The project now includes docker files for both Umbraco and the SQL server database.

It also includes additional scripts to launch and configure the database and a `.env`

file with the database password.

Run the following command from the root folder (where

`docker-compose.yml`

is located):

Access the site at

`http://localhost:44372`.


Create a new folder and navigate into it:


Create a new Umbraco project:


Add a Dockerfile


To speed up the build process, add a `.dockerignore`

file to exclude unnecessary folders like `.git`

, `bin`

, and `obj`.


Build the container:


Run the container:


Access the site at

`http://localhost:8080`.


There are some useful commands you can use to manage the docker containers:

`docker compose down --volumes`

: Deletes containers and the volumes they use. This is useful if you want to start from scratch.

Be careful with this command, as it deletes your database and all data in it.

`docker compose up --build`

: Rebuild the images and start the containers. This is useful if you have made changes to the project and want to see them reflected on the running site.`docker compose watch`

: Start the containers and watch the default models folder. This means that if the project uses a source-code models builder the images are automatically rebuilt and restarts when you change the models.

The docker compose file uses bind mounts for the following folders:

`/wwwroot/media`

`/wwwroot/scripts`

`/wwwroot/css`

`/Views`

`/models`


This is not meant to be used in production.

For local development, however, this means that the files necessary for development are available from outside the container in your IDE. This allows development even though the project is running in docker.

The `umbraco-compose`

template supports:

`-P`

or`--project-name`

: The name of the project. This is required and used to set the correct paths in the docker-compose file.`-dbpw`

or`--DatabasePassword`

: Used to specify the database password. This is stored in the`.env`

file and defaults to:`Password1234`

.`-p`

or`--Port`

: Used to specify the port the site will run on. Defaults to`44372`.


Last updated

Was this helpful?

---

## Running Umbraco on Linux/macOS | CMS

Since Umbraco 9 it has been possible to run Umbraco CMS natively on Linux or macOS High Sierra 10.13 and newer.

Last updated

Was this helpful?

Since Umbraco 9 it has been possible to run Umbraco CMS natively on Linux or macOS High Sierra 10.13 and newer.

With Umbraco CMS on .NET Core, Linux and macOS is natively supported with SQLite as the database.

In the below section, we describe how to get started with running Umbraco CMS on Linux or macOS.

How to get started running Umbraco CMS on Linux or macOS

To get started with Umbraco CMS first have a look at the [requirements for running Umbraco CMS](/umbraco-cms/fundamentals/setup/requirements#local-development).

Once you've made sure you meet the requirements it is time to install the Umbraco Templates on your system.

To do this follow the [Install using .NET CLI](/umbraco-cms/fundamentals/setup/install/install-umbraco-with-templates#install-the-template) guide.

With the templates installed on your system, it is now possible to create Umbraco projects.

To create a project, there are two options:

Continue creating projects using the .NET CLI.

Create new projects using Visual Studio (only macOS).


To create new projects using Visual Studio, you can use the [Install using Visual Studio](/umbraco-cms/fundamentals/setup/install/visual-studio) guide.

Once you create a new project it will use SQLite by default on Linux/macOS.

If you prefer using SQL Server as your database, you can either install it locally or run it via .

Last updated

Was this helpful?

Was this helpful?

---

## Unattended Installs | CMS

In some cases, you might need to install Umbraco instances automatically without having to run through the installation wizard to configure the instance.

You can use the **Unattended installs** feature to allow for quick installation and set up of Umbraco instances on something like Azure Web Apps.

This article will give you the details you need to install Umbraco unattended.

In order to get a clean instance of Umbraco, follow our installation guide for how to [Install an Umbraco project template](/umbraco-cms/fundamentals/setup/install/install-umbraco-with-templates#install-using-net-cli).

As you will not be running through the installation wizard when using this feature, you need to manually tell Umbraco which database to use.

Set up and configure a new database - see

[Requirements](/umbraco-cms/fundamentals/setup/requirements#hosting)for details.Add the connection string using configuration.


Umbraco can create an SQL Server database for you during the unattended install process. The user specified by the credentials in your connection string needs to have the `CREATE DATABASE`

permission granted and the global setting [InstallMissingDatabase](/umbraco-cms/reference/configuration/globalsettings#install-missing-database) is set to `true`.


If your connection string is for SQLite or SQL Server Express LocalDB it is assumed that a database should be created when missing. This is regardless of the value of the `InstallMissingDatabase`

setting.

```
{
  "ConnectionStrings": {
    "umbracoDbDSN": "server=localhost;database=UmbracoUnicore;user id=sa;password='P@ssw0rd'",
    "umbracoDbDSN_ProviderName": "System.Data.SqlClient"
  }
}
```

The 'umbracoDbDSN_ProviderName' attribute sets the .NET Framework data provider name for the DataSource control's connection. For more information on the data providers included in the .Net Framework, see the .

A value is configured for the key`umbracoDbDSN_ProviderName`

to ensure usage of the `Microsoft.Data.SQLite`

ADO.NET provider.

It is recommended that you make use of the values shown below for the `Cache`

, `Foreign Keys`

and `Pooling`

keywords on your connection string.

The unattended installs feature is disabled by default. In order to enable it, you need to add the following JSON object to a JSON configuration source.

Remember to set the value of `InstallUnattended`

to `true`.


The `UnattendedTelemetryLevel`

can be set to `Minimal`

, `Basic`

, or `Detailed`

. If omitted, `Detailed`

is the default.

Alternatively you may set your configuration with Environment Variables or other means. Learn more about this in the .

The keys for this would then be as follows:

After completing the steps above you can now initialize the installation by booting up the Umbraco instance.

Once it has completed, you should see the following when visiting the frontend of the site.

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-f20cd2a606e4c184fb43434412ab07e2e99c2c99%252Ffinal-screen.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=8dbf6050&sv=2)

Depending on your preferences, you can use any type of configuration to specify the connection string and login information, as well as enable unattended install. With the extending configuration functionality, it is possible to read from all kinds of sources. One example can be using a JSON file or environment variables.

**Program.cs** has a condition, which if met, an *appsettings.Local.json* file will be added and configured as a configuration source.

Having intellisense will help you to add your connection string and information needed for the unattended install.

We have added support for unattended installs with Name, Email and Password, and Connection String as CLI params, which are also available in Visual Studio. There you can fill in your information as follows:

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-fa3d0b02ce1518d967f1b1f399ac24825814f4e5%252FAddtional_Info_17.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=1c14c7fb&sv=2)

For running Umbraco in Docker containers, see [Running Umbraco in Docker using Docker Compose](/umbraco-cms/fundamentals/setup/install/running-umbraco-on-docker-locally) article.

Last updated

Was this helpful?

---

## Install using Visual Studio | CMS

A guide to install Umbraco CMS using Visual Studio.

Prerequisites

Install the template

Create the Visual Studio project

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-b8e78fb2df0e7ab690a0edb407696b8f86e0ca6b%252Fcreate-project.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=9c42bf8&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-88c719c7b96eec7835f4aeb5594c88a5cf8d8b28%252FNew_Project.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=cbb7467d&sv=2)

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F2050077833-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252Fb0WSXUuM7Qx5BfREagAI%252Fuploads%252Fgit-blob-254eb8d89be44d42e123c997fb4fd7483e39cdd9%252FSolution_Explorer.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=148f22d4&sv=2)

Running the site

Next steps

Last updated

Was this helpful?

A guide to install Umbraco CMS using Visual Studio.

Prerequisites

Check the

[Requirements](/umbraco-cms/fundamentals/setup/requirements)article to ensure you have everything you need to start your Umbraco project.

Install the template

Install the latest .

Run

`dotnet new install Umbraco.Templates`

to install the project templates.

Create the Visual Studio project

Go to

**File > New > Project/Solution**.Search for

`Umbraco`

in the*Search for templates*field.

Select

**Umbraco Project (Umbraco HQ)**.Click

**Next**.Enter a

**Project name**.

Refrain from changing the Solution name, as this will cause a namespace conflict with the CMS itself.

Select

**.Net 10.0 Long-Term Support (LTS)**from the**Framework**dropdown. The rest of the fields are optional.Click

**Create**.

The Umbraco Project is ready for you.

Running the site

You can now run the site through Visual Studio using **F5** or the **Debug** button.

Follow the installation wizard and after a few steps, you will get a message saying the installation was a success.

Next steps

You are now ready to start building your Umbraco project. Have a look below for different resources on the next steps.

Last updated

Was this helpful?

Was this helpful?

---
