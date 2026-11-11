---
name: client-follow-ups
description: Go through a creator's or team's clients in Linker's Clients and work out who needs a reply, a nudge or a next step today, then draft the messages and update their stage and follow-up day. Use when someone asks who to follow up with, wants a pipeline or client overview, a weekly client review, or asks what is waiting on a client. Needs Linker's Max or Ultra plan.
---

# Client follow-ups in Linker

The point is a short list of who to contact today and what to say, not a
report on every client.

## Gather

1. `list_clients`: everyone, with stage, follow-up day and whether archived.
   Leave archived clients out.
2. For the clients that need attention (below), `get_client`: their workflow
   (each step, what they were asked, what they answered) and their timeline.

## Who needs attention

In this order:

1. **Answered and waiting on the team**: a step the client approved, accepted,
   replied to or asked changes on, with nothing done since. These are the
   most urgent; the client is waiting.
2. **Follow-up day today or past.**
3. **Waiting on the client** for more than a week: a step sent and not
   answered.
4. **Stalled**: in `talking` or `proposal` with no timeline activity for two
   weeks or more.

Use today's date for "past" and "a week". Say "nothing urgent" when that is
the truth.

## Hand it back

A short list, most urgent first. For each client: one line on where it stands,
then a draft message ready to send (two or three sentences, friendly, one
clear ask). If they already have a client page link, include it so the client
lands on their steps.

## Then update Linker

After the person agrees (or straight away when they asked you to "sort it"):

- Set a new follow-up day: `update_client` with `followUpOn` (YYYY-MM-DD), or
  `null` for none.
- Move the stage when it changed (`proposal` once a quote is sent, `working`
  once accepted, `done` or `lost` at the end).
- Note what was sent with `add_client_note`, so the team sees it on the
  timeline.

`update_client` answers with the client `before`; offer it back if a change
was wrong. Archive finished clients with `archived: true` only when asked.

## On Pro

Client tools refuse below Max. Say that clients reach AI apps on Linker's Max
and Ultra plans (https://linker.cool/docs/ai-connector#plans) and that Clients
is in the dashboard. Don't push an upgrade.
