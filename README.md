# Freshsales MCP server

Inspect an existing CRM contact before explicitly adding another contact.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `FRESHSALES_API_KEY`
- `FRESHSALES_SUBDOMAIN`



Credential help: https://developers.freshworks.com/crm/api/

## Provider setup

Use a Freshsales Suite account on myfreshworks.com and its own API key; FRESHSALES_SUBDOMAIN is only the account label. This connector targets the documented /crm/sales API, not legacy freshsales.io tenants.

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call freshsales_get_contact '{"id":1001}'
```

## Use with an MCP client

Launch `node /absolute/path/freshsales-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| freshsales_get_contact | Read | Read one contact by its authorized numeric ID. |
| freshsales_create_contact | Explicit approval required | Create a CRM contact, subject to account-specific required fields. |

## Concrete workflow

Inspect an existing CRM contact before explicitly adding another contact.

1. freshsales_get_contact
2. freshsales_create_contact

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Import with PipMCP](https://pipmcp.com/github/start?integration=openapi-to-mcp&utm_source=github&utm_campaign=github-freshsales-mcp&utm_content=readme) when you want the hosted service. This provider is not currently listed as a managed template. Import selected-openapi.json (REST) or the official GraphQL schema linked in provenance, configure authentication, and review the tools before execution. Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/freshsales/).

## Provenance and maintenance

- https://developers.freshworks.com/crm/api/

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
