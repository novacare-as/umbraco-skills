# Delete | AI in Umbraco

Delete an agent.

Request

```
DELETE /umbraco/ai/management/api/v1/agents/{agentIdOrAlias}
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `agentIdOrAlias` | string | Agent GUID or alias |

Response

Success

```
(empty response body)
```

Not Found

```
{
    "type": "https://tools.ietf.org/html/rfc7231#section-6.5.4",
    "title": "AIAgent not found",
    "status": 404,
    "detail": "The specified agent could not be found."
}
```

Examples

Last updated

Was this helpful?