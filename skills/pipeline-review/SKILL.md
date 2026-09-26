---
name: pipeline-review
description: Review and work the Client Keeper transaction pipeline — deals by stage, stalled transactions, stage moves, and CRM health stats; use for "how's my pipeline", deal reviews, or moving transactions between stages.
metadata:
  short-description: Review deals by stage and update the pipeline
---

# Pipeline Review

Show the user where every deal stands and help them move the stuck ones.

## Quick start

1. `show_pipeline` — the interactive pipeline board: every column with its deals, deal count and
   total price, and a "Move to" control on each card.
2. `get_crm_stats` — the topline: contacts, leads, follow-ups, to-dos and transactions.
3. `search_crm` with `entity: "transactions"` — the deal list with pipeline column names and
   linked contacts (up to 100 per call; page with `offset`).
4. Group by pipeline stage; flag deals that look stalled — cross-check a specific deal with
   `get_transaction`, which returns linked contacts, tags and the available columns.
5. Report: deals per stage, the stalled list with how long since movement, and anything closing
   soon (`show_closing_timeline` shows one deal's countdown to close).
6. Act on request:
   - Move a deal: `manage_transaction` (stage/column update).
   - Link a missing party: `manage_transaction` (link contacts).
   - Rename/recolor/create pipeline columns: `manage_transaction`.
   - Create follow-ups on stalled deals: `create_followup` on the linked contact.

## Guardrails

- Stage moves change the user's deal board — restate the deal and the from → to stage before
  calling `manage_transaction`, and move only deals the user named.
- Column restructuring (create/rename/recolor) affects every deal in the pipeline; confirm before
  doing it.
- For a report, summarize from the data already fetched. `export_data` is the CSV-by-email export:
  use it only when the user asks for that, and tell them it emails a download link to their
  account address.
- Writes require write access.
