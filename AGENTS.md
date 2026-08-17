# AGENTS.md

This file is the operating guide for coding agents working in the public Leadping .NET SDK repository. Follow it together with `CONTRIBUTING.md`, `SECURITY.md`, and the repository’s existing style.

## Repository purpose

This repository contains the official .NET client for the Leadping API. Microsoft Kiota generates the client from Leadping’s OpenAPI contract. Applications provide the request adapter, authentication provider, credential storage, retry policy, and logging policy.

Authoritative public resources:

- API contract: <https://leadping.ai/docs/openapi.json>
- API documentation: <https://leadping.ai/docs/api-reference>
- Authentication discovery: <https://leadping.ai/auth.md>
- Security reporting: `SECURITY.md`

## Understand the change before editing

Classify the request first:

1. **API shape or behavior:** endpoint paths, request or response fields, required parameters, status codes, and schemas belong in the upstream Leadping API/OpenAPI contract. Do not conceal a contract problem with a local generated-code patch.
2. **Generated client output:** request builders, models, serializers, parsers, and `LeadpingOpenApiClient.cs` are generated. Regenerate them from the corrected contract and review the complete diff.
3. **Repository-owned content:** documentation, examples, package metadata, workflows, and contributor files may be edited directly.
4. **Generator defect:** if correct OpenAPI produces invalid C#, fix or report the generator problem and document any narrowly scoped temporary workaround.

Do not run broad regeneration for an unrelated documentation or packaging change. Do not hand-format generated trees or mix unrelated generated churn into a pull request.

## .NET conventions

- Preserve nullable-reference-type annotations and the project’s target frameworks.
- Follow existing Kiota abstractions for authentication, request adapters, backing stores, serialization, and error mappings.
- Keep async APIs asynchronous and accept or propagate `CancellationToken` where the generated surface provides it.
- Do not introduce a competing HTTP stack or expose transport-specific behavior through the public SDK API.
- Treat public type, namespace, member, and package changes as compatibility-sensitive. A breaking change requires explicit approval and a corresponding release plan.

## Authentication and examples

Leadping credentials are sent as `Authorization: Bearer <credential>`. Supported credentials and their scopes are described by the authentication guide. Never commit or print real user tokens, WorkOS agent assertions or refresh tokens, organization API keys, or source keys.

Examples must use nonfunctional example values, show secure credential injection, dispose transports appropriately, and avoid implying that the SDK persists or refreshes credentials automatically.

## Validation

Choose checks proportional to the change. For code, generated output, dependencies, or package metadata, run:

```bash
dotnet restore Leadping.OpenApiClient.csproj
dotnet build Leadping.OpenApiClient.csproj --configuration Release --no-restore
```

If tests are added later, run the relevant tests as well. Documentation-only changes normally need link, spelling, and example review rather than a package build.

Before handing off:

- inspect `git diff` for accidental generated churn;
- confirm examples compile conceptually against the current public API;
- update README or examples when usage changes;
- state whether the OpenAPI contract or Kiota version changed;
- report commands run and any validation not performed.

## Releases and security

Do not change package versions, tags, signing settings, release workflows, or publish artifacts unless the task explicitly authorizes a release. Do not disclose suspected vulnerabilities in public issues or pull requests; follow `SECURITY.md`.
