---
name: carbide-appointment-scheduling
description: Find real Carbide appointment availability and book, extend, relocate, or cancel appointments. Use when scheduling must account for estimators, routing, calendars, travel, and conflicts.
---

# Carbide appointment scheduling

1. Resolve the request with `get_request`, `list_requests`, or `search_operational_records` and verify it has the required customer and verified address.
2. Call `find_appointment_options` for the desired inclusive local date window and optional time or estimator constraints. Never infer availability from `list_appointments`. Present up to the three returned verified slots in text, including the estimator, local date and time, relevant routing evidence, and request URL.
3. Let the user choose when several options satisfy the request. After the user selects an exact option, pass its unchanged estimator and times to `book_appointment` (its `estimator_id`, `start` and `end` as `estimator_user_id`, `start_at` and `end_at`, with `mode: "first"` for a request's first appointment); do not substitute or reconstruct a slot.
4. Use `extend_appointment`, `update_appointment_location`, or `cancel_appointment` only for the exact appointment the user identified.
5. Re-read the appointment after a mutation when confirmation matters. If availability changed, return to step 2 rather than forcing stale data.

Booking and cancellation require `mcp.operate`; read-only connections can still analyze options.
