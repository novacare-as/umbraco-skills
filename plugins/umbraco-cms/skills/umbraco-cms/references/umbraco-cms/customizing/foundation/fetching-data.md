# Fetching Data

## Contents

- [Custom Generated Client | CMS](#custom-generated-client-cms)
- [Fetch API | CMS](#fetch-api-cms)
- [Umbraco HTTP Client | CMS](#umbraco-http-client-cms)
- [Executing Requests | CMS](#executing-requests-cms)

---

## Custom Generated Client | CMS

Learn how to create a custom-generated client with TypeScript types for your OpenAPI specification.

Umbraco uses to generate its HTTP client for the OpenAPI specification of the Management API. It is available through the `@umbraco-cms/backoffice/http-client`

package.

[Umbraco HTTP Client chevron-right](/umbraco-cms/customizing/foundation/fetching-data/http-client)

The following examples show how to generate a client from an OpenAPI specification and how to use it in the project. Below, the `@hey-api/openapi-ts`

library is used, but the same principles apply to any other library that generates a TypeScript client.

The generated client provides a convenient way to make requests to the specified API with type-safety without having to manually write the requests yourself. Consider generating a client to save time and reduce effort when working with custom API controllers.

To get started, install the generator using the following command:

```
npm install @hey-api/openapi-ts
```

Then, use the `openapi-ts`

command to generate a client from your OpenAPI specification:

```
npx openapi-ts --input https://example.com/openapi.json --output ./my-client
```

This will generate a TypeScript client in the `./my-client`

folder. Import the generated client into your project to make requests to the Management API.

To learn more about OpenAPI and how to define your API specification, visit the .

Your generated client needs the correct base URL, credentials, and authentication to talk to the Management API. The recommended approach uses hey-api's `runtimeConfigPath`

to inherit these settings automatically from the built-in backoffice HTTP client (`umbHttpClient`

).

The [Umbraco Extension Template](/umbraco-cms/customizing/development-flow/umbraco-extension-template) already includes this setup. If you scaffolded your extension with `dotnet new umbraco-extension`

, authentication works out of the box — no additional configuration needed.

`runtimeConfigPath`

(Recommended)To pass plugin options like `runtimeConfigPath`

, create a config file instead of using CLI flags.

Create

`openapi-ts.config.ts`

in your project root:

Run the generator, which will pick up the config file automatically:


Create a

`src/hey-api.ts`

file and add the following:

This copies `baseUrl`

, `credentials`

, `auth`

, and `headers`

from the backoffice HTTP client into your generated client at initialization time. Extensions load after the backoffice is fully configured, so all values are available.

When the generator runs, the generated `client.gen.ts`

will automatically import `createClientConfig`

and apply it during client creation. Your SDK functions will be authenticated without any entrypoint setup.

`umbHttpClient`

directlyIf you only have a few requests, you can skip client configuration entirely and pass `umbHttpClient`

as the `client`

parameter on each call:

The example above uses the backoffice HTTP client directly instead of the generated client. The `umbHttpClient`

already has authentication and the correct base URL configured.

The `auth`

callback on `umbHttpClient`

only fires when a request carries `security`

metadata. Here is how that metadata flows from your API to the generated client:

Each operation in your OpenAPI spec has an optional

`security`

field listing the security schemes it requires. Example:`[{ "Backoffice-User": [] }]`

.Those scheme names are defined in

`components.securitySchemes`

, where their type (OAuth2, HTTP Bearer, and so on) is declared.When hey-api generates your client, it reads both and resolves them into its own runtime shape -

`security: [{ type: 'http', scheme: 'bearer' }]`

- emitted directly into each generated SDK function.

The resolved shape is what `umbHttpClient`

checks before invoking the `auth`

callback.

If your controllers are part of the Umbraco Management API — tagged with `[MapToApi("management")]`

— Umbraco writes the `operation.security`

requirement into the OpenAPI spec automatically. This is done by `BackOfficeSecurityRequirementsOperationFilter`

, a Swashbuckle operation filter registered as part of the Management API configuration. It inspects each operation at startup. If neither the controller class nor the action method carries `[AllowAnonymous]`

, it adds a security requirement referencing the globally registered `"Backoffice-User"`

scheme.

When hey-api generates your client from that spec, it resolves the scheme and emits the runtime security metadata into each SDK function. No extra setup needed.

If you expose a separate API with its own Swagger document, security requirements are not added automatically. You must apply them to each operation in your OpenAPI specification, for example via an operation filter. Umbraco provides `BackOfficeSecurityRequirementsOperationFilterBase`

as a public base class you can subclass:

Register it in your SwaggerGen configuration:

No `AddSecurityDefinition`

call is needed — Umbraco already registers the required Bearer security scheme globally, and the base filter references it automatically. Once in place, hey-api will generate SDK functions with the correct `security`

metadata.

For a full walkthrough of setting up a custom API, see [Creating a Backoffice API](/umbraco-cms/tutorials/creating-a-backoffice-api).

When calling `umbHttpClient`

directly — without a generated SDK function — there is no spec to derive security metadata from. Pass it explicitly on each call:

See [Umbraco HTTP Client](/umbraco-cms/customizing/foundation/fetching-data/http-client) for more details.

If you only have a few requests, you can also use the `fetch`

function directly. Read more about that here:

Last updated

Was this helpful?

---

## Fetch API | CMS

The Fetch API is a modern way to make network requests in JavaScript. It provides a more powerful and flexible feature set than the older XMLHttpRequest.

The is a Promise-based API that allows you to make network requests similar to XMLHttpRequest. It is a modern way to make network requests in JavaScript and provides a more powerful and flexible feature set than the older XMLHttpRequest. It is available in all modern browsers and is the recommended way to make network requests in JavaScript.

The Fetch API can also be used in Umbraco to make network requests to the server. Since it is built into the browser, you do not need to install any additional libraries or packages to use it. The Fetch API is available in the global scope and can be used directly in your JavaScript code. The Fetch API is a great way to make network requests in Umbraco because it provides a lot of flexibility. You can use it to make GET, POST, PUT, DELETE, and other types of requests to the server. You can also use it to handle responses in a variety of formats, including JSON, text, and binary data.

For this example, we are using the Fetch API to make a GET request to the `/umbraco/MyApiController/GetData`

endpoint. The response is then parsed as JSON and logged to the console.

The example assumes that you have a controller set up at the `/umbraco/MyApiController/GetData`

endpoint that returns JSON data. You can replace this with your own endpoint as needed. Read more about creating a controller in the [Controllers](/umbraco-cms/implementation/controllers) article.

If there is an error with the request, it is caught and logged to the console:

```
const data = await fetch('/umbraco/MyApiController/GetData')
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .catch(error => {
    console.error('There was a problem with the fetch operation:', error);
  });

if (data) {
  console.log(data); // Do something with the data
}
```

When using the Fetch API, you need to manually handle errors and authentication. For most scenarios, we recommend using the Umbraco HTTP Client, which provides built-in error handling and authentication.

When making requests to the Umbraco API controllers, you may need to include an authorization token in the request headers. This is especially important when making requests to endpoints that require authentication.

The Fetch API does not automatically include authentication tokens in requests. Add the authentication token to the request headers manually. The recommended approach in the Backoffice is to use the **UMB_AUTH_CONTEXT**. This context provides tools to manage authentication tokens and ensures that your requests are properly authenticated.

`UMB_AUTH_CONTEXT`

for AuthenticationThe following example demonstrates how to use `UMB_AUTH_CONTEXT`

to retrieve the latest token and make an authenticated request:

When using the Fetch API with `UMB_AUTH_CONTEXT`

, you need to handle token expiration errors manually. If the token is expired, the request will return a 401 error. You will need to refresh the token or prompt the user to log in again.

Why Use **UMB_AUTH_CONTEXT**?

Simplifies Token Management: Automatically retrieves and refreshes tokens when needed.

Aligns with Best Practices: Ensures your requests are authenticated in a way that integrates seamlessly with the Backoffice.

Reduces Errors: Avoids common pitfalls like expired tokens or incorrect headers.


The **UMB_AUTH_CONTEXT** is only available in the Backoffice. For external applications, you will need to manage tokens manually or use an API user. Read more about API users in the [API Users](/umbraco-cms/fundamentals/data/users/api-users) article.

The Fetch API can also be used to make requests to the Management API controllers. The Management API is a set of RESTful APIs that allow you to interact with Umbraco programmatically. You can use the Fetch API to make requests to the Management API controllers like you would with any other API. The Management API controllers are located in the `/umbraco/api/management`

namespace. You can use the Fetch API to make requests to these controllers like you would with any other API.

You can create an API user in Umbraco to authenticate requests to the Management API. This is useful for making requests from external applications or services. You can create an API user in the Umbraco backoffice by going to the Users section and creating a new user with the "API" role. Once you have created the API user, you can make requests to the Management API using the API user's credentials. You can find these in the Umbraco backoffice.

You can read more about this concept in the [API Users](/umbraco-cms/fundamentals/data/users/api-users) article.

The Fetch API can also be used to make requests to the Management API using a Backoffice token. This is useful for making requests from custom components that are running in the Backoffice. The concept is similar to the API Users, but the Backoffice token represents the current user in the Backoffice. You will share the access policies of the current user, so you can use the token to make requests on behalf of the current user.

To use the Backoffice access token, you will have to consume the **UMB_AUTH_CONTEXT** context. You can use the `getLatestToken()`

method to get the current access token.

It is rather tiresome to manually add the token to each request. Therefore, you can wrap the Fetch API in a custom function that automatically adds the token to the request headers:

The above example illustrates the process of making a request to the Management API. The function does not handle errors or responses, so you will need to add that logic yourself. If the token has expired, you will get a 401 error back.

Regardless of method, you can execute the fetch requests through Umbraco's function. This function will handle any errors that occur during the request and will automatically refresh the token if it is expired. If the session is expired, the function will also make sure the user logs in again.

**Example:**

You can read more about the `tryExecute`

function in this article:

[Executing Requests chevron-right](/umbraco-cms/customizing/foundation/fetching-data/try-execute)

The Fetch API is a powerful and flexible way to make network requests in JavaScript. It is available in all modern browsers and is the recommended way to make network requests in JavaScript. The Fetch API can be used in Umbraco to make network requests to the server. It can also be used to make requests to the Management API controllers. You can use the Fetch API to make requests to any endpoint in the Management API. You can also use it to handle responses in a variety of formats. This is useful if you only need to make a few requests.

However, if you have a lot of requests to make, you might want to consider an alternative approach. You could use a library like to generate a TypeScript client. The library requires an OpenAPI definition and allows you to make requests to the Management API without having to manually write the requests yourself. The generated client will only need the token once. This can save you a lot of time and effort when working with the Management API. The Umbraco Backoffice itself is running with this library and even exports its internal HTTP client. You can read more about this in the [HTTP Client](/umbraco-cms/customizing/foundation/fetching-data/http-client) article.

Last updated

Was this helpful?

---

## Umbraco HTTP Client | CMS

Learn more about working with the Umbraco HTTP Client.

The Umbraco Backoffice includes a built-in HTTP client commonly referred to as the Umbraco HTTP Client for making network requests. It is generated using `@hey-api/openapi-ts`

around the OpenAPI specification and is available through the `@umbraco-cms/backoffice/http-client`

package.

**Example:**

```
import { umbHttpClient } from '@umbraco-cms/backoffice/http-client';

const { data } = await umbHttpClient.get({
	url: '/umbraco/myextension/api/v1/endpoint',
	security: [{ scheme: 'bearer', type: 'http' }],
});

if (data) {
	console.log('Data:', data);
}
```

The above example shows how to use the Umbraco HTTP client to make a GET request. The `umbHttpClient`

object provides methods for making requests, including `get`

, `post`

, `put`

, and `delete`

. Each method accepts an options object with the URL, headers, and body of the request.

The `security`

array tells the client to invoke the `auth`

callback, which provides the Bearer token for the request. Generated SDK functions include this metadata automatically from the OpenAPI specification — but when calling endpoints directly with `.get()`

or `.post()`

, you must pass it yourself.

You can also pass `umbHttpClient`

as the `client`

parameter to any generated SDK function. This lets the generated function use the backoffice's HTTP client (with its authentication) instead of its own. See [Custom Generated Client](/umbraco-cms/customizing/foundation/fetching-data/custom-generated-client) for details.

The Umbraco HTTP client is a wrapper around the Fetch API that provides a more convenient way to make network requests. It handles request and response parsing, error handling, and retries. The Umbraco HTTP client is available through the `@umbraco-cms/backoffice/http-client`

package, which is included in the Umbraco Backoffice. You can use it to make requests to any endpoint in the Management API or to any other API.

The recommended way to use the Umbraco HTTP Client is with the `tryExecute`

function. This function handles any errors that occur during the request and automatically refreshes the token if it has expired. If the session has expired, it prompts the user to log in again.

You can read more about the `tryExecute`

function in this article:

[Executing Requests chevron-right](/umbraco-cms/customizing/foundation/fetching-data/try-execute)

You can also generate your own client using the `@hey-api/openapi-ts`

library. This library allows you to generate a TypeScript client from an OpenAPI specification. The generated client will handle authentication and error handling for you, so you don't have to worry about those details.

Read more about generating your own client here:

[Custom Generated Client chevron-right](/umbraco-cms/customizing/foundation/fetching-data/custom-generated-client)

Last updated

Was this helpful?

---

## Executing Requests | CMS

Requests can be made using the Fetch API or the Umbraco HTTP client. The Backoffice also provides a `tryExecute`

function that you can use to execute requests. This function handles any errors that occur during the request and automatically refreshes the token if it has expired. If the session has expired, it prompts the user to log in again.

You can read the technical documentation for the `tryExecute`

function in the class.

Here is an example of how to use the `tryExecute`

function with the Umbraco HTTP client:

```
import { tryExecute } from '@umbraco-cms/backoffice/resources';
import { umbHttpClient } from '@umbraco-cms/backoffice/http-client';

const { data, error } = await tryExecute(this, umbHttpClient.get({
    url: '/umbraco/management/api/v1/server/status'
}));

if (error) {
    console.error('There was a problem with the fetch operation:', error);
} else {
    console.log(data); // Do something with the data
}
```

The `tryExecute`

function takes the context of the current class or element as the first argument and the request as the second argument. Therefore, the above example can be used in any class or element that extends from either the or classes.

The above example requires a host element illustrated by the use of `this`

. This is typically a custom element that extends the `UmbLitElement`

class.

It is recommended to always use the `tryExecute`

function to wrap HTTP requests. It simplifies error handling, manages token expiration, and ensures a consistent user experience in the Backoffice.

The `tryExecute`

function will automatically show error bubbles if a request fails. There may be valid cases where you want to handle errors yourself. This could, for instance, be if you want to show a custom error message. You can disable the notifications by passing the `disableNotifications`

option to the `tryExecute`

function:

The `tryExecute`

function also supports cancelling requests. This is useful in scenarios where a request is taking too long, or the user navigates away from the page before the request completes. You can cancel a request by using the . The `AbortController`

API is a built-in API in modern browsers that allows you to cancel requests. You can use it directly with tryExecute:

Last updated

Was this helpful?

---
