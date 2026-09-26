---
name: daily-crm-review
description: Run a morning Client Keeper review — upcoming birthdays, housiversaries, due and overdue follow-ups, open to-dos — and turn it into a short action plan; use when the user asks what's on deck today, this week, or wants a CRM check-in.
metadata:
  short-description: Morning sweep of follow-ups, birthdays, and to-dos
---

# Daily CRM Review

Give the user a tight, actionable picture of their day in Client Keeper, then help them act on it.

## Quick start

1. `show_today` — the interactive Today card: overdue and due-today to-dos, follow-ups due, and
   upcoming birthdays and housiversaries, with buttons to complete or reschedule. In a client
   without interactive cards, gather the same data with the next three calls instead.
2. `get_upcoming` with `kind: "all"` (or `"birthdays"`, `"housiversaries"`, `"follow_ups"`) and
   `days` for the horizon — birthdays, housiversaries, and follow-ups coming up.
3. `search_crm` with `entity: "follow_ups"`, `status: "overdue"` — anything that slipped.
4. `search_crm` with `entity: "todos"`, `status: "overdue"`, then `status: "current"` with
   `end_date` set to today — open to-dos that are late or due today.
5. Summarize: today's must-dos first, then this week's, then relationship touches (birthdays /
   housiversaries).
6. Offer actions: reschedule slipped follow-ups (`update_followup`), create missing ones
   (`create_followup`), check off what's done (`update_todo`).

## Guardrails

- Read calls work with any connection; creating or editing anything requires write access. If a
  write fails with a scope error, the user's API key or OAuth grant is read-only.
- Keep the summary short (a scannable list, grouped by urgency), and end with the 2–3
  highest-leverage suggested actions.
- Birthdays and housiversaries are relationship touchpoints: when one is imminent, offer to draft
  a note or create a follow-up.
- Mark a follow-up or to-do complete only when the user says it's done.
