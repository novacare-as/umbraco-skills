# Authentication | AI in Umbraco

Authentication requirements for the Umbraco.AI Management API.

Authentication Method

Required Permissions

Making Authenticated Requests

From Backoffice JavaScript

```
import { umbHttpClient } from "@umbraco-cms/backoffice/http-client";

const response = await fetch("/umbraco/ai/management/api/v1/connections", {
    method: "GET",
    headers: {
        "Authorization": `Bearer ${await umbHttpClient.getToken()}`,
        "Content-Type": "application/json",
    },
});
```

From Server-Side Code

Authorization Errors

401 Unauthorized

403 Forbidden

Example Error Response

Best Practices

Creating a Public API

Last updated

Was this helpful?