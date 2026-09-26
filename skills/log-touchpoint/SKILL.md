---
name: log-touchpoint
description: Capture a call, meeting, or conversation into Client Keeper as notes, follow-ups, to-dos, and calendar events; use when the user says "just got off a call", pastes meeting notes, or wants an interaction logged.
metadata:
  short-description: Log calls and meetings as notes, follow-ups, and events
---

# Log a Touchpoint

Turn a raw account of an interaction into durable CRM records so nothing is lost.

## Quick start

1. Identify the contact: `search_crm` with `entity: "contacts"`. Ambiguous name → list matches and
   ask.
2. Extract from the user's account: what happened, commitments made (theirs and the client's),
   dates mentioned, life events, and property details.
3. Review and save:
   - `show_debrief` with the contact id, the note, the to-dos, the next follow-up and any contact
     updates opens a debrief card; the user edits, toggles and saves the records from the card.
   - Or write the records directly:
     - `create_note` linked to the contact — the substance of the conversation.
     - `create_followup` for each commitment with a date ("call back Friday" → a follow-up on
       Friday).
     - `create_todo` for the user's own action items, with `contact_ids` linking the contact.
     - `manage_event` for any concrete appointment scheduled (showing, listing appointment,
       closing).
     - `add_property` if a specific property's criteria, sale, or listing came up.
     - `update_contact` / `update_lead` if the conversation changed contact facts (new phone,
       new email) or lead status.
4. Confirm back what was logged in one compact list.

## Guardrails

- One conversation usually yields several records — capture them all, and ask before logging
  anything the user only implied.
- Dates: resolve relative dates ("next Tuesday") against today before creating follow-ups or
  events, and state the resolved date in the confirmation.
- All of these are writes — they require write access.
- Touchpoints are append-only: existing notes stay as they are. Corrections to contact fields go
  through `update_contact`, not a note.
