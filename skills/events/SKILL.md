---
description: Manage your live ticketed events — see what's on, open the door / guest list for a date, check guests in by confirmation code, put a date on sale, or cancel a date (which notifies every attendee). Use when the operator asks about their actual events, the attendee list, checking someone in, or changing an event date's status. Requires a Fudis account and the event ticketing capability.
---

Use $ARGUMENTS for the event name, a date, an action ("check in", "cancel", "on sale"), or a confirmation code. If nothing is given, start by listing events.

This skill operates on **live event data** via the MCP. It is distinct from `/fudis:event`, which *plans* a new event as content. Use this one when the operator is running events that already exist in Fudis.

### Seeing what's on
1. `list_events` — leads with a summary (total, by status, how many have upcoming dates) and each event's next date + cupos. Optionally filter by `status` (draft / published / archived).
2. To drill into one event: `get_event` for its full definition (type, visibility, recurrence, requires booking/approval).
3. For an event's calendar of dates: `list_event_occurrences` — each date with its status (draft / on_sale / sold_out / cancelled / completed) and sale windows.

### The door / guest list
1. `list_event_attendees` for the event — every issued or checked-in ticket with guest name, phone, ticket class, confirmation code, and check-in state.
2. Lead with the summary line: total · registrados (issued) · ingresados (checked-in).
3. Always show confirmation codes in monospace.

### Checking a guest in (live, at the door)
1. The operator reads the **confirmation code** off the guest's WhatsApp/screen.
2. `check_in_attendee` with the code → transitions the ticket `issued` → `checked_in`.
3. Show the confirm card: guest name + ticket class prominent, event time + code below.
4. Handle clean failures plainly: unknown code, already checked in, or void/cancelled ticket. Door staff (staff role) can always do this — no capability gate.

### Changing a date's status
1. Identify the **occurrence** (date), not the event, via `list_event_occurrences`.
2. `update_occurrence_status` with one of: `draft` · `on_sale` · `sold_out` · `cancelled` · `completed`.
3. Putting a date `on_sale` or `sold_out` is routine — just confirm the change.
4. **Cancelling a date is heavy and irreversible-feeling**: it cancels every confirmed order on that date and fans out a cancellation notification to each attendee. ALWAYS confirm with the operator before cancelling, then report how many attendees were notified ("N asistentes notificados"). Requires manager role.
5. Show the time_change card: before status (strikethrough) → after status.

Never output raw JSON. Quantify in the restaurant's own currency. If a tool reports the plan doesn't include the event capability, say so plainly and point the operator to their Fudis plan — don't retry.
