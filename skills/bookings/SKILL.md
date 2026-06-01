---
description: Show today's bookings, create a reservation, update a booking status, or reschedule. Use when the operator asks about reservations, the floor plan for tonight, wants to book a table, or needs to move a reservation to a different time.
---

Use $ARGUMENTS to accept optional parameters: a date (defaults to today), a guest name to search, or an action like "create", "cancel", or "reschedule".

For listing bookings:
1. `list_bookings` for today (or the date in $ARGUMENTS)
2. Lead with VIP guests (★), then confirmed count, then pending
3. Flag any large parties (6+) and note special requests if present

For creating a booking:
1. Gather: guest name, party size, date, time, phone (optional), notes (optional)
2. `create_booking` in preview mode first — show the preview card
3. Ask for confirmation before finalizing

For updating status (seated, cancelled, no-show):
1. Identify the booking by guest name or confirmation code
2. `update_booking_status` with the new status
3. Confirm the change

For rescheduling:
1. Identify the booking by guest name or confirmation code
2. Confirm the new date and time with the operator
3. `reschedule_booking` with the new datetime
4. Show the time_change card: old time (strikethrough) → new time

Always show confirmation codes in monospace.
