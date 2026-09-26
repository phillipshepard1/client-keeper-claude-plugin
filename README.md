# Client Keeper - Real Estate CRM, for Claude

[Client Keeper](https://clientkeepercrm.com) is a CRM built for real-estate agents: contacts and
leads, follow-ups, to-dos, notes, birthdays and housiversaries, and a transaction pipeline from
first showing to closing. This plugin brings your Client Keeper account into Claude.

## What the plugin adds

- **The Client Keeper connector** — a connection to Client Keeper's hosted MCP server at
  `https://mcp.clientkeepercrm.com/api/mcp`. It lets Claude search and read your CRM, create and
  update records you ask for, and show interactive cards such as your day, a contact, the pipeline
  and a meeting debrief.
- **Four skills** — step-by-step workflows Claude can follow with the connector:
  - `daily-crm-review` — a morning sweep of follow-ups, to-dos, birthdays and housiversaries.
  - `meeting-prep` — a brief on a client before a call, showing or appointment.
  - `log-touchpoint` — turn a call or meeting into a note, follow-ups, to-dos and events.
  - `pipeline-review` — deals by stage, what is closing soon and what has stalled.

## Requirements

- A Client Keeper account.
- The first time Claude uses the connector, you sign in to Client Keeper and approve access
  (OAuth). The approval screen lists what Claude will be able to do before you allow it, and you
  can disconnect at any time from Claude's connector settings.

## Install

Install **Client Keeper** from the Claude plugin directory, or add this repository as a plugin
marketplace in Claude Code and install `client-keeper` from it:

```
/plugin marketplace add phillipshepard1/client-keeper-claude-plugin
```

## Your data

- The skills are instructions only. They contain no code and send nothing anywhere.
- The connector talks only to Client Keeper's own API at `mcp.clientkeepercrm.com`, using the
  OAuth token from your sign-in. Every request runs as your account and can reach only your own
  records and the ones other Client Keeper users have shared with you.
- Deleting a record always takes two steps: Claude first gets a preview naming the record, and
  the delete runs only when it is confirmed.

Privacy policy: https://clientkeepercrm.com/privacy-policy

## Support

Questions or problems: support@clientkeepercrm.com

## License

MIT — see [LICENSE](LICENSE).
