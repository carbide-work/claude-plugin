# Carbide Claude community submission


Version `1.53.0` adds an optional phone extension (1 to 10 digits) to contact and company phone numbers. `create_contact`, `update_contact`, `create_company` and `update_company` accept `phone_number_extension`, and `create_contact_phone`, `update_contact_phone`, `create_company_phone` and `update_company_phone` accept `extension`; reads return them. An extension typed after the number (`555-555-0123 x12`) is split off, and changing a number without sending an extension clears the old one. Existing inputs, results and scopes are unchanged.
Version `1.52.1` fixes estimator customer creation with automatic self-assignment while preserving reassignment restrictions. Assignment refusals now retain a useful permission error. Tool names and input/output schemas are unchanged.
Version `1.52.0` adds a configurable initial PaintScout quote status for request creation or appointment booking and makes quote synchronization outbound-only. Pending creation retains captured settings; disabling outbound quote sync cancels unstarted creation. Configuration remains owner/admin-only with `mcp.write`.

Version `1.51.0` adds read and operational job-import tools for text, documents and PaintScout. Imports retain member permissions, Job Scheduling access, signed uploads, reviewed application and stale-state protection. Mutations require `mcp.operate`; existing grants gain no new scopes.

Version `1.50.0` removes `pipeline_crm_deal_sync_error` and `pipeline_crm_deal_sync_error_at` from the fields `list_requests` can filter and sort by. Carbide stopped writing them when the external sync engine became Pipeline CRM's only writer, so they were always empty; Pipeline CRM problems show as sync issues instead. Results, other inputs and authorization are unchanged. The shared server and portable plugin packages remain on the required 1.x major line.

Version `1.49.1` releases unused Google and Outlook connections immediately when their last calendar is disconnected. Connections still used by another active calendar or integration remain connected.

Version `1.49.0` adds optional `producer_slots` to block and block-day writes: ordered generic or named producers with planned hours and daily production value. Existing count/member inputs remain supported. Hours-mode block budget edits balance planned day/producer hours without changing capacity profiles. Block records include effective day slots; staffing changes retain tenant, roster, and availability checks.

Version `1.48.1` marks `create_phone_agent`, `update_phone_agent` and `pause_phone_agent` as open-world and adds specific annotation explanations for external caller interactions. Draft creation still requires separate phone-number purchase and provisioning in web settings; ready-agent updates sync to the telephony provider in the background; pausing stops the agent answering calls. Tool schemas, authorization and phone-agent conversation behavior are unchanged.

Version `1.48.0` updates request workflow results to use `needs_release` for confirmed appointments waiting for office release. This replaces the previous `need_approval` value in `list_requests` and `get_request`; consumers must accept the renamed value. Tool names, inputs and authorization remain unchanged. The shared server and portable plugin packages remain on the required 1.x major line.

Version `1.47.2` classifies appointment and booking reminder create/update/delete tools as open-world because their settings control customer emails. Tool names, inputs and authorization are unchanged. The ChatGPT ZIP now imports five positive and three negative reviewer cases, the existing walkthrough URL and release notes from `extensions.com.openai`; reviewer credentials remain exclusively in the secure portal. Run the scenarios with the dedicated demo reviewer account before submitting.

Version `1.47.1` corrects review hints for overwrites, replacement lists, default-seeding reads and consequential automation; every tool includes explicit booleans and annotation explanations. It removes the MCP credential-entry tools `connect_paintscout_connection`, `reconnect_paintscout_integration` and `connect_pipeline_crm_connection`: configure those providers in Carbide web settings instead. This deliberately restricts the previous tool contract within the required 1.x major line. Plugin guidance excludes regulated personal data and chat credential collection. Publish the revised privacy policy and deploy this server release before rescanning or resubmitting.

Version `1.47.0` adds a contact's flag to the CRM field mapping options of HubSpot, Pipeline CRM and PaintScout: `flagged_at` (`Flagged at`, type `datetime`) and `flagged_reason` (`Flagged reason`, type `string`), in both directions, so `create_crm_field_mapping` accepts them. Mailchimp's options leave them out. A contact is flagged while `flagged_at` is set. Contact records no longer carry `is_contact_flagged`, `quickbooks_contact_id`, `paintscout_id` or `legacy_contact_method_exempt`, so `search_operational_records` and `read_diagnostic_records` stop returning them; none of them was the staff flag. `get_organization_diagnostic_configuration` adds `job_scheduling_notifications_paused`: whether the organization has paused its Job Scheduling notifications from Production settings. While they are paused, no job start email (or any other Job Scheduling notification) reaches customers or team members. Existing tool names and inputs are unchanged.

Version `1.46.0` enforces the optional initial appointment approval gate for estimator request access. Pending requests and related records remain unavailable to estimator-only members until office approval or estimator self-booking. Existing tool inputs are unchanged.

Version `1.45.0` adds Pipeline CRM's owner and deal stage to `list_pipeline_crm_field_mapping_options` as Carbide fields with a `remote_property` (`user_id` for a person's and a deal's owner, `owner_id` for a company's, `deal_stage_id` for the stage), and gives the contact's and request's lead source one too (`lead_source_id`, `source_id`): each maps only to that Pipeline CRM field, and no other field may map it. New Pipeline CRM integrations get default mappings for them, a deal's address and source, and a contact's lead source, which take effect once the external sync engine runs for Pipeline CRM. The options no longer offer Carbide's own id and link custom fields, and `create_crm_field_mapping` and `configure_crm_field_mapping` refuse those fields and a deal's name for Pipeline CRM. Existing tool names and payloads are unchanged.

Version `1.44.0` enforces request permissions from the signed-in member's current work profiles. Owners, admins and active CSRs manage all organization requests; estimator-only members manage requests for customers assigned to them; members without either profile have no request access. Only owners, admins and CSRs change assignments. These rules also cover related records, search, counts and live or delayed notifications. This intentionally tightens the previous member-wide authorization contract within the required 1.x version line. Tool names and input shapes are unchanged.

Version `1.43.0` adds HubSpot's owner and deal stage to `list_hubspot_field_mapping_options` as Carbide fields with a new `remote_property`: each maps only to that HubSpot property, and no other field may map it. They are default mappings `list_crm_field_mappings` lists, and `remove_crm_field_mapping` stops one syncing. `create_crm_field_mapping` and `configure_crm_field_mapping` now accept those fields onto their own properties, and still refuse them for any other field. Carbide's id and link properties and the deal name stay outside the mappings: Carbide always writes them, and every mapping tool still refuses them. Existing tool names and payloads are unchanged.

Version `1.42.0` adds the estimator wrap-up time (`wrap_up_minutes`) to the organization and estimator scheduling settings tools, a `wrap_up` option for `set_estimator_setting_default`, and an optional `include_wrap_up` switch when booking; changing an existing appointment's wrap-up while rescheduling requires an owner, an admin or the assigned estimator; `save_estimator_availability` keeps an estimator's wrap-up when `wrap_up_minutes` is left out. Existing tool names and payloads are unchanged.

Version `1.41.0` adds `open_sync_issues` to `get_integration_diagnostic_evidence`: the contact's open HubSpot external sync issues by kind, each with a count and whether one keeps its field out of the sync, never their fields, details or values. `create_contact` and `update_contact` with `commercial_customer: false` (or without it) no longer unlink the contact's companies; saving a contact as commercial still requires a company and still replaces its other companies. Clients that relied on `commercial_customer: false` to unlink companies must stop expecting it. Every HubSpot connection now runs the external sync engine, so `get_integration_diagnostic_evidence` no longer returns `sync_error_present` or `sync_error_at` (HubSpot sync problems are no longer saved on the contact; `open_sync_issues` reports them), and `get_background_job_evidence` for a contact lists the engine's HubSpot sync jobs that name the contact instead of the retired contact push jobs. Tool names, inputs and other outputs are unchanged.

Version `1.40.1` corrects the `get_google_analytics_connection` description: when the Google authorization needs renewing, changes that need the customer's Google account (choosing a stream, Tag Manager setup) stop, but events keep being sent with the stream's API secret. The tool's inputs and outputs are unchanged.

Version `1.40.0` adds `add_crew_trades` and `add_job_producer` production-plan changes, plus optional `project_trade_ids` on changes. Missing-trade suggestions can repair a grouped crew conflict by declaring its missing trades (owners/admins) or assigning qualified, available job producers (members). Every option is simulated and rechecked on apply. Existing change kinds remain available.

Version `1.36.1` makes a linked scheduling member use the connected user's first name, last name and email. Account changes synchronize those details; member profile writes cannot override them while linked. Existing tool names and input/output fields remain available. Conflicting scheduling-member emails refuse the change without merging records. Shared scheduling conflict review groups excess-producer blocks by job, with evidence-checked crew-target and roster repairs. Existing MCP tool shapes remain compatible.

Version `1.36.0` lets `simulate_production_plan` and `apply_plan_scenario` take a `set_block_days` change, which sets or clears the crew size of some of a work block's days, and optionally names their people (each with `day_index`, `crew_size` and optional `member_ids`). The MCP server and both portable plugins share this minor version; existing tool names, other inputs, outputs and authorization are unchanged.

Version `1.35.0` removes production skills throughout Carbide. This is an intentional breaking contract change within the required 1.x version line: skill catalog, member-skill and crew-skill tools are removed, along with skill fields in crew/member/job data, crew routing rules, scheduling results and PaintScout proposals. Integrations must omit those fields and stop calling the removed tools. Trades, roles, equipment and coordination remain supported.


Release policy: keep this package on 1.x; a major version change requires explicit user consent. Version `1.28.0` supersedes the unapproved 2.x and 3.0.0 version labels; the contract changes recorded in those earlier notes still apply.

Version `1.34.0` adds `cancellation_source` to appointment diagnostic records. It names the Google Calendar or Outlook calendar an estimator removed an appointment from when the organization uses bidirectional calendar sync, and is empty otherwise. Existing tool names, inputs and fields are unchanged.

Version `1.33.0` extends request-link presets to shared-builder project, timeline, lead-source, intake-channel and custom-field answers. Public questions receive editable defaults; fields absent from Public are saved server-side. Contact, company, address and consent fields are excluded. New presets validate against tenant-scoped definitions and choices; unchanged legacy values remain stored, and unavailable values are skipped at submission. Estimator-managed links keep their names and owner assignments. Existing tool names and map conventions remain compatible.

Version `1.32.1` retires Public Page choice, A/B testing, unit visibility and commercial-bookings controls. Public choices and Customer type follow the published builder; Location always includes an optional unit. Legacy fields and inputs remain compatible and cannot reactivate retired behavior.

Version `1.32.0` adds Schedule Job for organizations with Job Scheduling. `auto_schedule_job` moves an unscheduled production job to `analyzing` and, in the background, places it on the best crew (crew routing rules, ranked by each qualified crew's earliest opening) with a tentative start date; `get_job` shows the result. The crew routing rules returned by `get_crew_routing_rules` now drive that placement. Existing tool names and inputs are unchanged.

Version `1.31.0` adds crew routing rules for organizations with Job Scheduling. `get_crew_routing_rules` reads the ordered rules (seeding the defaults on first read) and `replace_crew_routing_rules` replaces them; rules select, exclude, prioritize or deprioritize crews by customer history, territory, trades, skills or first availability, with conditions on the job's type, territory, category and company. Existing tool names and inputs are unchanged.

Version `1.30.0` gives crews a territory. `update_crew_territory` replaces a crew's postal codes (five-digit US ZIPs and three-character Canadian FSAs) and rebuilds its map outline in the background; `list_crews` returns each crew's `zip_codes`. Existing tool names and inputs are unchanged.

Version `1.29.0` makes routing rules the only estimator and CSR routing. `get_estimator_routing_rules`, `replace_estimator_routing_rules`, `simulate_estimator_routing`, `get_csr_routing_rules`, `replace_csr_routing_rules`, `simulate_csr_routing` and `update_estimator_profile_performance_rate` are listed without a feature flag. `get_estimator_assignment_configuration`, `replace_estimator_assignment_configuration` and `get_estimator_routing_rules_source` are removed. Estimator routing rules no longer accept or return `options` or the `prefer` action, and every rule needs a `qualifier`. This is a breaking contract change; clients must use the routing rules tools.

Version `1.28.0` replaces project-requirement tools and job selections with Coordination and Equipment. Equipment adds owned inventory, reservations per work block, date availability, and extra shared stock (default 0). Every job-selected Coordination item appears in its checklist at every status and completes without required notes or a date. Job-wide crew notes are also retired from current job contracts. This is a breaking contract change; clients must use the new coordination names and equipment tools.

Version `2.3.0` makes Request Intake available to every organization with Estimate Scheduling: `get_request_intake_definition` and `evaluate_request_intake` are listed without a separate feature flag, and phone definitions require only Phone Agents. Custom field tool descriptions now describe `public_visible` as controlling whether customers see their own saved answers. Tool names and payloads are unchanged.

Version `2.2.0` keeps request intake choices in Settings order and adds an optional `selectable` flag to Project type options in internal intake definitions: `get_request_intake_definition` marks inactive project types `selectable: false`, which staff keep on requests that already have them but are not offered for new selections. Public intake definitions may now require a question that the internal form leaves optional, or the reverse, when the organization sets that on its public form. Tool names and inputs are unchanged.

Version `2.1.0` adds two customer email templates for organizations with Job Scheduling, `job_start_tentative` and `job_start_confirmed`, which tell a job's customer its tentative or confirmed start date. `list_email_templates` returns them and `preview_email_template` and `update_email_template` accept them only for those organizations; other organizations never see them. Their placeholders include `{job.start_date}`, `{job.start_day_of_week}` and `{job.number}`. Existing tool names and payloads are unchanged.

Version `2.0.1` makes request intake discovery agree with the app: requests without a recorded form submission follow the latest published Internal Form across all creation channels. Actual submissions retain their immutable version. Tool names and input/output schemas are unchanged.

Version `2.0.0` replaces the prelaunch job-color tool contract with one assignment per job, area and substrate. `create_job_color` and `update_job_color` take organization-owned area, substrate, color, product and finish option IDs instead of free-text catalog snapshots. `search_paint_options` and `find_or_create_paint_option` discover and create those reusable choices. Duplicate area/substrate pairs are refused; color records expose their five option IDs and display labels.

Version `1.27.0` adds nullable `matching_crew_ids` to crew-skill violation details in production-plan results. The list identifies other active, non-archived crews covering all missing skills; an empty list means none. Skill coverage alone does not guarantee a verified schedule repair. Existing tool names, inputs and apply confirmation remain unchanged.

Version `1.26.0` adds an optional `typed_location_kind` to request creation for ZIP/postal-code locations. Approximate locations retain coordinates for distance estimates, create no property or Zillow lookup, and require a full street address before booking. Existing street-address searches and property workflows remain available.

This package is prepared for Anthropic's reviewed `claude-community` marketplace. The official `claude-plugins-official` marketplace is curated separately by Anthropic and has no application process.

Version `1.25.0` adds an optional `display` flag to note results from `create_note`, `update_note` and `search_operational_records`; it is true when staff marked a request note to appear in staff calendar events and emails. Tool names and inputs are unchanged.

Version `1.24.1` documents Production settings live updates, draft preservation, and directory pagination in the hosted operating manual. Existing tool names, inputs, and result schemas are unchanged.

Version `1.24.0` adds `embed_allowed_origins`, the websites allowed to embed the booking page, to the public page record that `update_public_page_profile` returns. The tool does not change it: owners and admins manage the list in the web app. Existing tool names and input payloads are unchanged.

Version `1.23.0` adds contact-owner IDs and relationships to contact-method and company-contact result schemas while preserving existing tool names and inputs. Staff customer and appointment workflows now use the private GraphQL API; behavioral resources document their pagination and live-refresh rules.

Version `1.22.0` adds the `browser_tracking_enabled` connection field to existing Google Analytics mutation results. The web app can disable direct GA4 browser tracking while retaining server Measurement Protocol events, so a GTM container can own browser tracking. Existing connections keep direct browser tracking enabled by default.

Version `1.21.0` adds `get_request_intake_definition` and `evaluate_request_intake` for published or pinned questions, and clarifies collection visibility versus explicit template/CRM mappings. Phone definitions add voice-agent guidance prompts and linear question ordering with inherited field names. Fixed contact/property fields are marked managed_by=default_script and excluded from configurable Phone questions. Public choices now follow the published builder; legacy field and lead-source flags are compatibility defaults.

Version `1.20.0` retires job block mode. `update_job_scope` no longer accepts `use_blocks` or `crew_size`, and job records the MCP tools return no longer include `use_blocks`. Every job plans with its blocks: a job's `labor_hours` and `value_cents` are its estimate and no longer change its single block, so set a block's hours, crew size and duration with the block tools. `promote_request_to_production` still creates one default block unless `blocks` is given. Other tool names and payloads are unchanged.

Version `1.19.1` lets `cancel_appointment` cancel a booked appointment that has already ended or has no calendar event; cancelling an appointment that has already ended sends no customer or estimator messages. Tool names and payloads are unchanged.

Version `1.19.0` adds `job_id` to the job color and job constraint records that the color and constraint tools and `search_operational_records` return. The `create_job_color`, `update_job_color`, `remove_job_color`, `check_job_item` and `uncheck_job_item` tools, and reads of a job's colors and constraints and of the paint color catalog, now require an active organization member, as the other job tools already did. Existing tool names and input payloads are unchanged.

Version `1.18.0` adds optional machine-name input to custom-field creation and updates, and generated/publication lock status to field listings. Generated names follow reusable-label edits until manually edited; any published appearance permanently locks and reserves the ID. Unpublished renames retain answers and update saved template and CRM references. Existing tool names and native request attributes remain unchanged. Version `1.17.0` adds `record_lead_source` to the Phone Agent tools that `create_phone_agent` and `update_phone_agent` accept in `allowed_tools`: an agent that creates requests asks a new caller how they heard about the company once the appointment step is over and records it on the request. Existing tool names and payloads are unchanged. Version `1.16.2` shares the estimator ranking and month availability that `find_appointment_options` and `get_booking_evidence` read with the app's new staff scheduler; the results are unchanged. Tool names and payloads are unchanged. Version `1.16.1` clarifies that HubSpot journal polling runs by default for every eligible integration and follows its automatic-update and inbound-sync settings. Tool names and payloads are unchanged. Version `1.16.0` adds per-day overrides of production blocks: `update_block_day`, `assign_block_day_members` and `reset_block_day` change one productive day's crew size, trades, named people or notes, and block records from `search_operational_records` list every day with its effective values. A day with more or fewer people changes how many days a block takes. Existing tool names and payloads are unchanged. Version `1.15.0` adds HubSpot deal-stage-to-request-status configuration tools. Version `1.14.3` links a verified address given to `create_contact` or `update_contact` as a saved property of the contact, as `create_company` and `update_company` already did for companies; an address without coordinates no longer becomes a property through either until it is confirmed, and the deprecated `materialize_address_property` input of `create_contact` is ignored. Tool names and payloads are unchanged. Version `1.14.2` requires an active organization member for the `create_block` and `update_block` tools, as it already did for `assign_block_members`; tool names and payloads are unchanged. Version `1.14.1` refuses a request address change through `update_request` or `update_request_intake` once a booked appointment for the request has started, refuses assigning an estimator whose membership is not active in the organization, and requires an active organization member for the request write tools; tool names and payloads are unchanged. Version `1.14.0` lets request listings filter and sort by when a request was received, its customer type, and the start, status and cancellation initiator of its relevant appointment. Version `1.13.0` adds effective trade IDs to crew-member read results while keeping direct trade proficiencies separate. Version `1.12.0` lets request listings filter and sort by whether the customer asked for a callback that is still open. Version `1.11.0` adds Google Tag Manager container selection and independent Google Analytics and Tag Manager controls to the MCP configuration tools and packaged integration guidance. Version `1.10.0` was the first marketplace submission. It rebases the unpublished internal `2.0.0`–`5.0.0` labels onto the `1.x` line that began at `1.0.0`. Ten additive capability milestones account for the minor version: Meta Pixel and job blocks; Dialpad SMS and templates; PaintScout quote controls; Canadian territories; scheduling roles and Members; commercial booking; declared crew capacity; estimator and CSR routing controls; production units and planning; and public booking and Request Link customer-type options. That release also folded in compatible fixes, including removal of guidance for the retired in-app assistant; its tool names and payloads were unchanged. The current production-plan contract omits the obsolete `unlock_block` change kind.

## Submission values

- Plugin name: Carbide
- Plugin ID: `carbide`
- Publisher: Carbide
- Category: Productivity
- Version: `1.41.0`
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
git push git@github.com:carbide-work/claude-plugin.git claude-plugin-release:refs/tags/v1.33.0
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
6. Confirm MCP initialization and both portable plugin manifests advertise version `2.0.0` after deploying the server change.
7. Submit through `https://platform.claude.com/plugins/submit` or, for a Team or Enterprise organization owner, `https://claude.ai/admin-settings/directory/submissions/plugins/new`.
8. After approval and the nightly catalog sync, verify `claude plugin install carbide@claude-community` succeeds.
