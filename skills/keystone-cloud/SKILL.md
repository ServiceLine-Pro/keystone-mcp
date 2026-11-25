---
name: keystone-cloud
description: Do real work in a business's apps through the Keystone MCP server, including calls, Google Maps rankings, ads, reviews, CRM, websites and any web app.
version: 1.0.0
author: Keystone
license: MIT-0
homepage: https://keystonecloud.ai/connect-your-ai
metadata:
  openclaw:
    homepage: https://keystonecloud.ai/connect-your-ai
  hermes:
    tags: [business, marketing, agency, crm, ads, phone, seo]
---

# Keystone Cloud

Keystone is a hosted MCP server at `https://keystonecloud.ai/mcp`. Once it is connected, the agent can work in the apps a business already uses: its phone line and call recordings, Google Business Profile, Google and Meta ads, analytics, reviews, calendar, CRM, accounting, email and hosted websites. Web apps with no API work through API Anything, which runs the task in a cloud browser. Agencies keep one workspace per client.

## When to Use

- The user asks about their business apps: calls, leads, ad spend, rankings, reviews, appointments, invoices, website pages.
- The user wants a job done inside one of those apps: pause a campaign, answer a review, confirm a booking, buy a tracking number, publish a page.
- An agency user names a client. Switch to that client's workspace first.

## Prerequisites

Add the MCP server once, then sign in to Keystone in the browser window that opens. A Keystone account is required (14-day free trial at https://keystonecloud.ai/signin).

OpenClaw:

```bash
openclaw mcp add keystone --url https://keystonecloud.ai/mcp --transport streamable-http --auth oauth
openclaw mcp login keystone
```

With the Gateway running, add `--no-probe` to the first command. The saved config is `mcp.servers.keystone` with `"url": "https://keystonecloud.ai/mcp"`, `"transport": "streamable-http"` and `"auth": "oauth"`.

Hermes Agent: `hermes mcp add keystone --url https://keystonecloud.ai/mcp`, then `hermes mcp login keystone`. Or in `~/.hermes/config.yaml`:

```yaml
mcp_servers:
  keystone:
    url: "https://keystonecloud.ai/mcp"
    auth: oauth
```

Claude Code: `claude mcp add --transport http keystone https://keystonecloud.ai/mcp`, then `/mcp` to sign in.

Codex: `codex mcp add keystone --url https://keystonecloud.ai/mcp`, then `codex mcp login keystone`.

Cursor, VS Code and other clients: add a remote server with the URL `https://keystonecloud.ai/mcp`. Keystone uses OAuth with dynamic client registration, so no client id or secret is needed. Headless setups can send a personal token from https://keystonecloud.ai/setup as `Authorization: Bearer <token>`.

## How to Run

1. Call `whoami` to see the account, the active workspace, what is connected and what to connect next.
2. For an agency, call `workspaces_list` and `workspace_use` to pick the client.
3. Use the named tool for the job (table below). For any other app, call `apps_search`, read the action with `apps_schema`, then run it with `apps_run`.
4. If an app is not connected yet, call `connect` and give the user the link it returns.

## Quick Reference

| Job | Tools |
|---|---|
| Account and workspaces | `whoami`, `workspaces_list`, `workspace_use`, `connections_list`, `connect` |
| Any connected app (1,800 in the catalog) | `apps_search`, `apps_schema`, `apps_run` |
| Calls and recordings | `calls_list`, `call_get`, `call_place` |
| Google Maps rank grid | `grid_results` |
| Appointments | `appointment_get`, `appointment_confirm` |
| Phone numbers and domains | `phone_search`, `phone_buy`, `domain_search` |
| Web apps with no API | `anything_apps`, `anything_run`, `computer_view` |
| Agency playbooks | `playbook_list`, `playbook_get` |

## Procedure

1. Confirm which business the request is for. Never guess between client workspaces.
2. Read before you change anything: pull the current campaign, listing or record first.
3. Make the change with one tool call per step and report what changed in plain words.
4. Purchases (numbers, domains, postcards, calls) are paid from the Keystone wallet. When Keystone asks for the owner's approval, tell the user where to approve and wait.

## Pitfalls

- Tools act on the active workspace only. Switch with `workspace_use` before working on another client.
- A tool that returns a `connect` link means the app is not connected in this workspace yet.
- A call limit of 300 tool calls a minute stops runaway loops. Batch reads where the tool allows it.

## Verification

`whoami` returns the signed-in account and the active workspace name. `connections_list` lists the connected apps for that workspace.
