# Test Connection | AI in Umbraco

Test a connection to verify credentials are valid.

Endpoint

```
POST /umbraco/ai/management/api/v1/connections/{idOrAlias}/test
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `idOrAlias` | string | Connection GUID or alias |

Request

Response

Success (200 OK)

```
{
    "success": true,
    "errorMessage": null
}
```

Test Failed (200 OK)

404 Not Found

How Testing Works

Examples

cURL

JavaScript

Test After Creation

Last updated

Was this helpful?