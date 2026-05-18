# Create Connection | AI in Umbraco

Create a new AI provider connection.

Endpoint

```
POST /umbraco/ai/management/api/v1/connections
```

Request

Headers

| Header | Value |
|---|---|
| Content-Type | `application/json` |

Body

```
{
    "alias": "openai-prod",
    "name": "OpenAI Production",
    "providerId": "openai",
    "isActive": true,
    "settings": {
        "apiKey": "sk-your-api-key",
        "organization": null
    }
}
```

Required Fields

| Field | Type | Description |
|---|---|---|
| `alias` | string | Unique alias (lowercase, hyphens allowed) |
| `name` | string | Display name |
| `providerId` | string | ID of the provider to use |

Optional Fields

| Field | Type | Default | Description |
|---|---|---|---|
| `isActive` | boolean | true | Whether connection is enabled |
| `settings` | object | null | Provider-specific settings |

Settings with Configuration References

Response

Success (201 Created)

400 Bad Request

Missing Required Field

Duplicate Alias

Invalid Provider

Examples

cURL

JavaScript

Last updated

Was this helpful?