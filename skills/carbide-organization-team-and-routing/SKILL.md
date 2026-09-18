---
name: carbide-organization-team-and-routing
description: Audit and configure Carbide organization profile, members, staff roles, estimator routing, availability, territories, crews, trades, skills, and requirements. Use for administrative setup and team routing.
---

# Carbide organization, team, and routing

Start by reading the current state with `get_organization`, member and profile lists, estimator assignment configuration, project areas, trades, skills, requirements, crew members, and crews.

- Use `list_health_check_issues` to prioritize missing setup.
- Make the smallest requested configuration change and re-read it afterward.
- Add staff profiles before assigning their availability, territory, crew membership, trades, or skills.
- For production teams, create crew members before crews, then attach members and capabilities with exact IDs.
- Treat member deactivation, role changes, removals, and assignment replacement as consequential. State the target and effect before calling the tool.

Organization and production-team setup requires `mcp.write` and an owner or administrator role. This includes verified addresses, trades, skills, requirements, crew members, crews, memberships, leads, and capabilities. Day-to-day job scheduling and job-team changes use `mcp.operate`; underlying Carbide policies remain authoritative.
