# Carbide for Claude Code

Use Claude Code to read and manage the contracting operations in your Carbide organization. The plugin connects to Carbide's production MCP server and includes skills for reporting, customer and request work, appointment scheduling, organization setup, communications, production, integrations, phone agents, and diagnostics.

## Install

Until the plugin is approved for the Claude community marketplace, load this directory directly from a Carbide checkout:

```sh
claude --plugin-dir apps/claude
```

Once approved, install it from the public community marketplace:

```sh
claude plugin marketplace add anthropics/claude-plugins-community
claude plugin install carbide@claude-community
```

Start Claude Code, run `/mcp`, and authenticate the `carbide` server. Sign into Carbide, choose the organization, select the access level, and allow access.

## Access levels

- **Read only** grants `mcp.read` for reports, searches, availability, simulations, and diagnostics.
- **Read and operate** also grants `mcp.operate` for day-to-day customer, request, appointment, job, schedule, and check-in changes.
- **Read, operate, and configure** also grants `mcp.write` for owners and administrators configuring organization settings, integrations, production catalogues, and teams.

Carbide still applies the signed-in user's membership role, product access, feature flags, tenant boundary, and action policies. The plugin never bypasses ordinary Carbide authorization.

## Skills

Claude automatically loads the relevant skill, or you can invoke one directly using its namespaced name:

- `/carbide:carbide-operational-reporting`
- `/carbide:carbide-customer-and-request-operations`
- `/carbide:carbide-appointment-scheduling`
- `/carbide:carbide-organization-team-and-routing`
- `/carbide:carbide-intake-public-page-and-communications`
- `/carbide:carbide-production-management`
- `/carbide:carbide-integrations-webhooks-and-api-keys`
- `/carbide:carbide-phone-agents`
- `/carbide:carbide-diagnostics-and-health`

The address and appointment skills present choices in text. Claude waits for an explicit selection and then uses the exact verified address candidate or appointment slot returned by Carbide.

## Security and privacy

- Authentication uses Carbide OAuth discovery and authorization-code flow with PKCE.
- Do not paste Carbide passwords, API keys, OAuth tokens, or provider secrets into chat.
- Confirm exact targets before destructive or externally visible actions.
- Review Carbide's [privacy policy](https://www.carbide.work/privacy) and [terms of service](https://www.carbide.work/terms).

Support is available at [carbide.work/support](https://www.carbide.work/support).
