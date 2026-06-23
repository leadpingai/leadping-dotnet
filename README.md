# Leadping .NET SDK

Typed .NET client for the Leadping API, generated from `leadpingai/openapi` with Kiota.

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
adapter.BaseUrl = "https://api.leadping.ai";

var client = new LeadpingOpenApiClient(adapter);
var me = await client.Users.Me.GetAsync();
```

`CreateLeadpingRequestAdapter` should return a Kiota request adapter configured with your Leadping authentication.

## Notes

- Generated code comes from `leadpingai/openapi`; update the OpenAPI spec instead of hand-editing generated files.
- Package ID: `Leadping.OpenApiClient`
- License: see `LICENSE`
