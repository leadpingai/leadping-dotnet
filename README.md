[![](https://img.shields.io/nuget/v/Leadping.OpenApiClient.svg?style=for-the-badge)](https://www.nuget.org/packages/Leadping.OpenApiClient/)
[![](https://img.shields.io/github/actions/workflow/status/leadpingai/leadping-dotnet/publish.yml?style=for-the-badge)](https://github.com/leadpingai/leadping-dotnet/actions/workflows/publish.yml)
[![](https://img.shields.io/nuget/dt/Leadping.OpenApiClient.svg?style=for-the-badge)](https://www.nuget.org/packages/Leadping.OpenApiClient/)
[![](https://img.shields.io/github/actions/workflow/status/leadpingai/leadping-dotnet/codeql.yml?label=CodeQL&style=for-the-badge)](https://github.com/leadpingai/leadping-dotnet/actions/workflows/codeql.yml)

# Leadping .NET SDK

Type-safe .NET client for the Leadping API.

## Install

```bash
dotnet add package Leadping.OpenApiClient
```

For GitHub Packages:

```bash
dotnet nuget add source https://nuget.pkg.github.com/leadpingai/index.json \
  --name leadping-github \
  --username USERNAME \
  --password GITHUB_TOKEN

dotnet add package Leadping.OpenApiClient --source leadping-github
```

## Use

```csharp
using Leadping.OpenApiClient;
using Microsoft.Kiota.Abstractions;

IRequestAdapter adapter = CreateLeadpingRequestAdapter();
var client = new LeadpingOpenApiClient(adapter);

var me = await client.Users.Me.GetAsync();
```

`CreateLeadpingRequestAdapter` is application code. Configure it to send one of:

- `Authorization: Bearer <token>`
- `X-Leadping-Api-Key: <key>`

The client defaults to `https://api.leadping.ai` when the adapter does not already have a base URL.

## Links

- [Documentation](https://leadping.ai/docs)
- [API reference](https://leadping.ai/docs/api-reference)
- [License](LICENSE)
