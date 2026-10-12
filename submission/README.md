# Carbide Claude community submission

This package is prepared for Anthropic's reviewed `claude-community` marketplace. The official `claude-plugins-official` marketplace is curated separately by Anthropic and has no application process.

Version `1.17.1` lets `cancel_appointment` cancel a booked appointment that has already ended or has no calendar event; cancelling an appointment that has already ended sends no customer or estimator messages. Tool names and payloads are unchanged. Version `1.17.0` adds `record_lead_source` to the Phone Agent tools that `create_phone_agent` and `update_phone_agent` accept in `allowed_tools`: an agent that creates requests asks a new caller how they heard about the company once the appointment step is over and records it on the request. Existing tool names and payloads are unchanged. Version `1.16.2` shares the estimator ranking and month availability that `find_appointment_options` and `get_booking_evidence` read with the app's new staff scheduler; the results are unchanged. Tool names and payloads are unchanged. Version `1.16.1` clarifies that HubSpot journal polling runs by default for every eligible integration and follows its automatic-update and inbound-sync settings. Tool names and payloads are unchanged. Version `1.16.0` adds per-day overrides of production blocks: `update_block_day`, `assign_block_day_members` and `reset_block_day` change one productive day's crew size, trades, named people or notes, and block records from `search_operational_records` list every day with its effective values. A day with more or fewer people changes how many days a block takes. Existing tool names and payloads are unchanged. Version `1.15.0` adds HubSpot deal-stage-to-request-status configuration tools. Version `1.14.3` links a verified address given to `create_contact` or `update_contact` as a saved property of the contact, as `create_company` and `update_company` already did for companies; an address without coordinates no longer becomes a property through either until it is confirmed, and the deprecated `materialize_address_property` input of `create_contact` is ignored. Tool names and payloads are unchanged. Version `1.14.2` requires an active organization member for the `create_block` and `update_block` tools, as it already did for `assign_block_members`; tool names and payloads are unchanged. Version `1.14.1` refuses a request address change through `update_request` or `update_request_intake` once a booked appointment for the request has started, refuses assigning an estimator whose membership is not active in the organization, and requires an active organization member for the request write tools; tool names and payloads are unchanged. Version `1.14.0` lets request listings filter and sort by when a request was received, its customer type, and the start, status and cancellation initiator of its relevant appointment. Version `1.13.0` adds effective trade IDs to crew-member read results while keeping direct trade proficiencies separate. Version `1.12.0` lets request listings filter and sort by whether the customer asked for a callback that is still open. Version `1.11.0` adds Google Tag Manager container selection and independent Google Analytics and Tag Manager controls to the MCP configuration tools and packaged integration guidance. Version `1.10.0` was the first marketplace submission. It rebases the unpublished internal `2.0.0`–`5.0.0` labels onto the `1.x` line that began at `1.0.0`. Ten additive capability milestones account for the minor version: Meta Pixel and job blocks; Dialpad SMS and templates; PaintScout quote controls; Canadian territories; scheduling roles and Members; commercial booking; declared crew capacity; estimator and CSR routing controls; production units and planning; and public booking and Request Link customer-type options. That release also folded in compatible fixes, including removal of guidance for the retired in-app assistant; its tool names and payloads were unchanged. The current production-plan contract omits the obsolete `unlock_block` change kind.

## Submission values

- Plugin name: Carbide
- Plugin ID: `carbide`
- Publisher: Carbide
- Category: Productivity
- Version: `1.17.1`
- Public source repository: `https://github.com/carbide-work/claude-plugin`
- Homepage: `https://www.carbide.work`
- Support: `https://www.carbide.work/support`
- Privacy policy: `https://www.carbide.work/privacy`
- Terms of service: `https://www.carbide.work/terms`
- MCP server URL: `https://app.carbide.work/mcp`
- Authentication: OAuth 2.0 authorization code with PKCE and dynamic client registration
- License: MIT

Suggested short description:

> Run and configure your contracting operations from Claude Code.

Suggested long description:

> Connect Claude Code to your Carbide organization to find and manage customers, requests, appointments, production jobs, teams, intake, communications, integrations, and diagnostics. Carbide enforces the signed-in user's organization role, product access, OAuth scopes, and tenant boundary for every action.

## Publish the public mirror

Keep `apps/claude` canonical in the private Carbide repository. From a clean, committed release checkout, publish only this subtree to the public mirror:

```sh
git subtree split --prefix=apps/claude --branch claude-plugin-release
git push git@github.com:carbide-work/claude-plugin.git claude-plugin-release:main
git push git@github.com:carbide-work/claude-plugin.git claude-plugin-release:refs/tags/v1.17.1
git branch -D claude-plugin-release
```

Create the public repository before the first push. Do not force-push an existing mirror or reuse a release tag. Clone the public mirror into a temporary directory and run the same validation against that clone before submitting.

## Reviewer account

Create a dedicated reviewer user without MFA in a fully seeded demo organization. Give the user an active administrator membership so reviewers can exercise read, operational, and configuration scopes. Use the existing demo reseed workflow to keep customers, requests, appointments, jobs, crews, and diagnostics populated. Store credentials only in Anthropic's submission form, never in this repository.

## Positive review cases

1. **Weekly operations summary:** “Summarize this week's new requests and upcoming appointments.” Expected: uses reporting tools and changes no data.
2. **Customer and request creation:** “Create a residential customer and estimate request at 123 Main Street, Austin, Texas.” Expected: verifies the address before creating records and uses the automatic single complete match.
3. **Ambiguous address:** “Create an estimate request at 100 Broadway.” Expected: presents exactly two returned candidates in text, waits for the reviewer to choose, resolves that candidate, and creates no request before selection.
4. **Appointment scheduling:** “Show me the best appointment times for request 123.” Expected: presents at most three verified slots in text and calls `book_appointment` only after the reviewer selects one.
5. **Setup audit and remediation:** “Audit my Carbide setup and fix the safe missing settings.” Expected: reports health issues and uses configuration tools only with the granted configuration scope.
6. **Production planning:** “Move this job to next week and keep the assigned crew.” Expected: simulates the change, explains conflicts, and applies only a valid requested scenario.

## Negative review cases

1. A member asks to change organization settings. Configuration tools are absent or return the underlying authorization error.
2. “Delete the old one.” Claude asks for the exact record and explains the irreversible effect before calling a destructive tool.
3. A user supplies a record ID from another organization. Tenant policies return no record or forbid the action, and Claude does not retry against another tenant.

## Final checks

1. Run the repository package and MCP tests.
2. Run `claude plugin validate apps/claude` locally.
3. With a current Claude Code release, run `claude plugin validate apps/claude --strict` and repeat it against a clean clone of the public mirror.
4. Start `claude --plugin-dir apps/claude`, run `/mcp`, and complete OAuth from a clean browser.
5. Verify all nine skills appear and exercise the positive and negative review cases with the dedicated reviewer account.
6. Confirm MCP initialization and both portable plugin manifests advertise version `1.17.1` after deploying the server change.
7. Submit through `https://platform.claude.com/plugins/submit` or, for a Team or Enterprise organization owner, `https://claude.ai/admin-settings/directory/submissions/plugins/new`.
8. After approval and the nightly catalog sync, verify `claude plugin install carbide@claude-community` succeeds.
