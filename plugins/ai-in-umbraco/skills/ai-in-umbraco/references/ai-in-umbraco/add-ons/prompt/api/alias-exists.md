# Check Alias Exists | AI in Umbraco

Check whether a prompt alias is in use.

Request

```
GET /umbraco/ai/management/api/v1/prompts/{alias}/exists
```

Path Parameters

| Parameter | Type | Description |
|---|---|---|
| `alias` | string | The alias to check |

Query Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `excludeId` | guid | No | Optional prompt ID to exclude from the check (useful during updates to allow the prompt to keep its own alias). |

Response

Success

```
true
```

Examples

```
curl -X GET "https://your-site.com/umbraco/ai/management/api/v1/prompts/meta-description/exists" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

Last updated

Was this helpful?