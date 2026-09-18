---
name: carbide-production-management
description: Manage Carbide production jobs, scope, teams, blocks, crews, constraints, colors, checklists, and project check-ins. Use for job planning and execution after a request reaches production.
---

# Carbide production management

1. Resolve the job, blocks, crews, crew members, constraints, and requirements with `search_operational_records` and the production list tools.
2. For schedule changes, call `simulate_production_plan` with the proposed changes and locks. Explain conflicts, shortages, and non-applicable scenarios.
3. Call `apply_plan_scenario` only for a valid scenario that matches the user's requested change. Never use it to acknowledge unresolved conflicts.
4. Use the typed job, block, team, color, constraint, checklist, and check-in tools for the smallest change. Re-read the affected records afterward.
5. Treat job archival, completion, final check-in submission, and removals as consequential; identify the exact record and effect before acting.

These tools appear only for organizations with production scheduling enabled. Job execution mutations require `mcp.operate`; archiving a job, changing its team, extending an appointment, and requesting a project check-in are shown only to owners and administrators. Production catalogue and crew roster or capability setup requires `mcp.write` and an administrator role. The user's ordinary Carbide authorization remains authoritative.
