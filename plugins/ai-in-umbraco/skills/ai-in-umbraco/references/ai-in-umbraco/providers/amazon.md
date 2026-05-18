# Amazon Bedrock | AI in Umbraco

Configure Amazon Bedrock as an AI provider for chat and embedding capabilities.

Installation

```
Install-Package Umbraco.AI.Amazon
```

```
dotnet add package Umbraco.AI.Amazon
```

Connection Settings

| Setting | Required | Description |
|---|---|---|
| Region | Yes | AWS region (e.g., `us-east-1` ) |
| Access Key ID | Yes | Your AWS access key ID |
| Secret Access Key | Yes | Your AWS secret access key |
| Endpoint | No | Custom endpoint URL (for VPC endpoints) |

Getting AWS Credentials

Required IAM Policy

Enabling Models

![](https://docs.umbraco.com/~gitbook/image?url=https%3A%2F%2F675241704-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FeAvcb24lmqdKvNUvRquG%252Fuploads%252Fgit-blob-273d32ea6916cd9a661b15e086e2f705b25296ef%252Famazon-bedrock-create-connection.png%3Falt%3Dmedia&width=768&dpr=3&quality=100&sign=3c350316&sv=2)

Related

Last updated

Was this helpful?