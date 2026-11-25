# Installing the Keystone MCP server

Keystone is a hosted remote MCP server. Do not clone or build anything.

1. Add a remote MCP server named `keystone` with the URL `https://keystonecloud.ai/mcp` and transport streamable HTTP.
2. Keystone uses OAuth 2.1 with dynamic client registration. When the client connects, it opens a browser sign-in. The user signs in to Keystone (or starts the 14-day free trial at https://keystonecloud.ai/signin) and approves access.
3. If the client cannot run a browser sign-in, ask the user for a personal token from https://keystonecloud.ai/setup and send it as the header `Authorization: Bearer <token>`.
4. Test the connection by calling the `whoami` tool. It returns the account, the active workspace and the connected apps.

Example config for clients that read `mcpServers` JSON:

```json
{ "mcpServers": { "keystone": { "url": "https://keystonecloud.ai/mcp" } } }
```
