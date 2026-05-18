# Requirements | CMS

The Umbraco UI works in all modern browsers:

Chrome (Latest)

Edge (Chromium)

Firefox (Latest)

Safari (Latest)


Below you can find the minimum requirements to run Umbraco on your machine:

One of the following .NET Tools or Editors:

2022 version 17.14 or higher.

Optional: version 2025.3.0.1 and higher



and higher


Umbraco can be installed with a SQLite or SQL Server database and configured with a [connection string](/umbraco-cms/reference/configuration/connectionstringssettings). For SQL Server, indicating a minimum supported version of SQL Server 2016.

When using Visual Studio as your primary Integrated Development Environment (IDE) we recommend [finding and downloading the Software Development Kits (SDKs) for Visual Studio arrow-up-right](https://dotnet.microsoft.com/en-us/download/visual-studio-sdks)

Are you using Microsoft SQL as your data?
The Umbraco Data Access Layer (DAL) does not support case-sensitive naming.
When you use Microsoft SQL as your database, ensure that the database is created using a case-insensitive (CI) collation variant. For example, `SQL_Latin1_General_CP1_CI_AS`.

Learn more about in the official Microsoft documentation.

As Umbraco releases are aligned to the .NET release cadence, it's also aligned with Microsoft's Long-term support policy for the underlying framework. For the best experience, we would recommend that you ensure to be on the latest and supported Microsoft versions to run and host Umbraco CMS:

*For more information, see the* *article in the Microsoft documentation.*

You can use to manage the hosting infrastructure. All Umbraco Cloud plans are hosted on Microsoft Azure, which gives your site a proven and solid foundation.

Ability to set file permissions to include create/read/write (or better) for the user that "owns" the Application Pool for your site. This would typically be

**NETWORK SERVICE**.

The database account used in the connection string will need permission to read and write from tables. It will also require permission to create schema during installs and upgrades:

The

`db_owner`

role has full permissions on the database.To use an account with more restricted permissions, the

`db_datareader`

and`db_datawriter`

roles will be needed for normal use to read from and write to the database. The`db_ddladmin`

role, which can modify the database schema, is required for installs and upgrades of the CMS and/or any packages that create database tables.

For more information on the Database-level roles, see the .

For more information on how to create a database user via SQL, you can check the .

Last updated

Was this helpful?