---
name: client-onboarding
description: Bring a new client into Linker's Clients (a simple CRM in the Linker dashboard) - add them, start them on a workflow of steps with links to the team's own documents, and make the link to their client page. Use when someone has a new client, lead, brand deal or booking to set up, wants to send a client a quote, contract or brief to approve, or asks to note something about a client. Needs Linker's Max or Ultra plan.
---

# Onboarding a client in Linker

Linker's Clients keeps the people a creator or team works for. Each client has
details, a stage, a timeline of notes, and a **workflow**: a list of steps,
each a link to something of the team's own (a Google Doc, a quote, a contract,
a Notion page) and what the client is asked to do with it. The client sees
their steps on their own page, with no account, and answers there. Linker
keeps no files, only links.

## Add them

1. `list_clients` first: if they are already there, use that one rather than
   adding a second.
2. `add_client` with the `name` and whatever is known: `company`, `email`,
   `phone`, `website`, `stage` and `followUpOn` (YYYY-MM-DD). Stages: `lead`,
   `contacted`, `talking`, `proposal` (sent), `working`, `done`, `lost`.
   Anything the team should remember goes in `notes`, which the client never
   sees.

## Give them a workflow

1. `list_workflows`: Linker's own workflows first, then the team's. Pick the
   closest, or ask which one if two fit.
2. `start_workflow` with the client's `id` and the workflow's id. Its steps
   arrive without links.
3. For each step there is a link for, `add_client_step` with a `title`, the
   `url`, a `note` the client will read, and the `action`: `read` (have a
   look), `approve` (or ask for changes), `accept` (with their name, for a
   contract or quote) or `reply` (a few words). Steps without links are filled
   in later in the dashboard.

Only link to documents the team has shared for viewing. If a link looks private
(a Google Doc only the team can open), say so before adding it.

## Make their link

`get_client` shows whether they already have a page link. If they do, use it:
making a new one with `make_client_link` ends the old one. Hand the link back
with a short message they can send, for example:

> Hi Mila, here's everything for the Studio Noord campaign in one place:
> the brief to read and the quote to accept. <link>

Then set the stage (`update_client`, `stage: "proposal"`) and a follow-up day
if there isn't one.

## Notes and changes later

- "Note that she wants it by Friday" → `add_client_note`.
- Details, stage or follow-up day → `update_client`; its answer keeps the
  client `before`, to put back on request.
- Archiving: `update_client` with `archived: true` (and `false` to bring them
  back). Deleting a client and their timeline is only in the dashboard.

## On Pro

Client tools refuse below Max. Say that clients reach AI apps on Linker's Max
and Ultra plans (https://linker.cool/docs/ai-connector#plans) and that Clients
is in the dashboard. Don't push an upgrade.
