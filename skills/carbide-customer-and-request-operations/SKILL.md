---
name: carbide-customer-and-request-operations
description: Find, create, and update Carbide contacts, companies, properties, requests, contact methods, notes, assignments, and outcomes. Use for CRM and intake operations, not organization-wide configuration.
---

# Carbide customer and request operations

1. Search before creating. Use `search_operational_records` to resolve contacts, companies, requests, properties, and notes and avoid duplicates.
2. For a new or changed address, call `find_address_options`. When it returns `selected`, use `selected_address` immediately and do not ask the user to confirm it. When it returns `needs_selection`, present exactly the two returned candidates in text and wait for the user to choose. Call `resolve_address` with the chosen candidate's `place_id` and the returned `session_token`, then use the canonical street, city, state, zipcode, and resolved map as `selected_place`. Never invent coordinates or choose between ambiguous candidates.
3. Create or reuse the customer, then call `create_request` with the verified address fields, including `selected_place`. Commercial requests require a company associated with the contact; residential requests must not include a company.
4. Use the contact-method tools to add or update email and phone records, then set a primary method explicitly when requested.
5. Explain irreversible or externally visible effects before actions such as setting a final request outcome or sending a referral email. Ask for the exact target if “old,” “latest,” or similar wording could identify multiple records.

Respect the connected user's Carbide role and the granted `mcp.operate` scope. Never work around a forbidden or cross-organization result.
