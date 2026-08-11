[![](https://img.shields.io/nuget/v/Leadping.OpenApiClient.svg?style=for-the-badge)](https://www.nuget.org/packages/Leadping.OpenApiClient/)
[![](https://img.shields.io/github/actions/workflow/status/leadpingai/leadping-dotnet/publish.yml?style=for-the-badge)](https://github.com/leadpingai/leadping-dotnet/actions/workflows/publish.yml)
[![](https://img.shields.io/nuget/dt/Leadping.OpenApiClient.svg?style=for-the-badge)](https://www.nuget.org/packages/Leadping.OpenApiClient/)
[![](https://img.shields.io/github/actions/workflow/status/leadpingai/leadping-dotnet/codeql.yml?label=CodeQL&style=for-the-badge)](https://github.com/leadpingai/leadping-dotnet/actions/workflows/codeql.yml)

# ![Leadping](https://leadping.ai/favicon.ico) Leadping .NET SDK

The official, type-safe .NET SDK for the Leadping API. Use it to integrate lead management, conversations, SMS and calling, automations, reporting, billing, and business settings into .NET applications.

The package is generated from the [Leadping OpenAPI specification](https://leadping.ai/docs/openapi.json) with Microsoft Kiota. It contains request builders and models; your application supplies the HTTP request adapter, credentials, retry policy, and credential storage.

## Installation

Install the SDK and Kiota's `HttpClient` transport:

```bash
dotnet add package Leadping.OpenApiClient
dotnet add package Microsoft.Kiota.Http.HttpClientLibrary
```

## Authentication

Set `LEADPING_API_KEY` to a WorkOS organization API key (`sk_...`). The SDK sends it as `Authorization: Bearer <credential>`. User access tokens are also supported when acting for a signed-in user; `lp_src_...` keys are only for lead-ingestion endpoints. See [API authentication](https://leadping.ai/docs/api-authentication).

## Create a client

Kiota includes an API-key authentication provider that can place the complete Bearer value in the `Authorization` header:

```csharp
using Leadping.OpenApiClient;
using Microsoft.Kiota.Abstractions.Authentication;
using Microsoft.Kiota.Http.HttpClientLibrary;

var credential = Environment.GetEnvironmentVariable("LEADPING_API_KEY")
    ?? throw new InvalidOperationException("LEADPING_API_KEY is not set.");

var authProvider = new ApiKeyAuthenticationProvider(
    $"Bearer {credential}",
    "Authorization",
    ApiKeyAuthenticationProvider.KeyLocation.Header,
    ["api.leadping.ai"]);

var adapter = new HttpClientRequestAdapter(authProvider);
var client = new LeadpingOpenApiClient(adapter);
```

The client defaults to `https://api.leadping.ai`.

## Common operations

Request builders mirror the API path. Indexers select a resource ID; terminal methods send the request.

```csharp
// Requires a user access token.
var currentUser = await client.Users.Me.GetAsync(cancellationToken: cancellationToken);

// Retrieve organization resources by ID.
var source = await client.Sources["source-id"]
    .GetAsync(cancellationToken: cancellationToken);

var lead = await client.Leads["lead-id"]
    .GetAsync(cancellationToken: cancellationToken);
```

Create and update operations accept models from `Leadping.OpenApiClient.Models`. Generated methods also accept request configuration and a `CancellationToken`.

## Resources

- [Leadping introduction](https://leadping.ai/docs/introduction)
- [API authentication](https://leadping.ai/docs/api-authentication)
- [API reference](https://leadping.ai/docs/api-reference)
- [OpenAPI specification](https://leadping.ai/docs/openapi.json)
- [NuGet package](https://www.nuget.org/packages/Leadping.OpenApiClient/)
- [License](LICENSE)
