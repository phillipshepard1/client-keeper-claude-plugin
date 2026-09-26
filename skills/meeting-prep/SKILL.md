---
name: meeting-prep
description: Build a pre-meeting brief from Client Keeper — contact details, relationship history, notes, properties, open follow-ups, and active transactions; use before a call, showing, listing appointment, or client meeting.
metadata:
  short-description: Pull full contact context before a meeting
---

# Meeting Prep

Assemble everything the user needs to walk into a meeting knowing the client cold.

## Quick start

1. Find the contact: `search_crm` with `entity: "contacts"` and `query` set to the name, phone or
   email the user gave. If several match, list them and ask which one.
2. `get_contact` with the id and `include_activity: true` — profile, relationships, notes,
   property records, follow-ups, groups and open to-dos. `show_contact` shows the same contact as
   an interactive card when the user wants to see it.
3. Transactions: `search_crm` with `entity: "transactions"` returns deals with the names of their
   linked contacts (`query` filters by address; page with `limit` and `offset`). Pick the deals
   whose `contacts` include this client, then `get_transaction` with that id for the pipeline
   stage, every linked party and the tags.
4. Produce the brief:
   - **Who**: name, role (buyer/seller/lead), family/relationship notes.
   - **Where things stand**: lead status, active transaction + stage, last touchpoint.
   - **Open loops**: incomplete follow-ups, promised actions from notes.
   - **Personal**: upcoming birthday/housiversary, preferences captured in notes.
   - **Suggested talking points**: 2–3, grounded in the open loops.
5. Offer to log prep output: a `create_note` with the brief, or a `create_followup` for the
   commitments that come out of the meeting.

## Guardrails

- The brief contains only what is actually in the CRM. If the record is thin, say so and suggest
  what to capture.
- One `get_contact` with activity covers most of the brief; extra searches are for transactions.
- If the meeting is about a specific property, include the property records from the contact and
  offer `add_property` for anything new discussed.
