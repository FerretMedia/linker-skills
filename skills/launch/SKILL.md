---
name: launch
description: Plan and run a launch on a Linker page (linker.cool link-in-bio) - a new video, single, drop, product, event or sale. Use when someone says they have something coming out or going live, wants to promote it from their link in bio, wants to know which platform sends the most people to it, or wants their page put back after a launch.
---

# Running a launch from a Linker page

A launch is when a link-in-bio page earns its keep: every bio, story and video
says "link in bio", and the page decides whether people find the thing.

## Before: put it first

1. `get_page`, and ask what is launching, the address, and when it ends (a sale,
   a pre-save window, a one-night event) if it does.
2. Add the link at the top with `add_link` (`to: "top"`), labelled with the
   action and the thing ("Pre-save NIGHT DRIVE", "Shop the drop: 48 hours
   only"), and `spotlight: true`. Turn the spotlight off on any other link, so
   there is one.
3. Optional: a matching touch with the `page-design` skill, such as a button
   colour from the cover art. Keep the theme's `before` to put back later.
4. Update the description to point at it ("New single out Friday ↓") with
   `update_profile`. Keep the old description to put back.

## Tracked links (Max and Ultra)

To learn which platform works, make one tracked link per place it will be
posted, all pointing at the same address:

- `create_tracked_link` with `url` and a `name` such as "Night Drive - TikTok",
  "Night Drive - Instagram story", "Night Drive - newsletter".
- Each answers with a code; the address to post is `linker.cool/go/<code>`.
  Hand them back as a short table: where to post it, and the address.

On Pro, tracked links refuse: say they come with Max and Ultra
(https://linker.cool/docs/ai-connector#plans) and carry on without them.

## During: check in

`get_tracked_link_stats` per code (7 days) shows opens by day, source, country
and device; `get_analytics` shows visits and clicks on the page's own links.
Report it plainly: which place sent the most people, and one thing to do about
it (post there again, pin that video).

## After: put the page back

When it ends, offer to:

- Move the launch link down or hide it (`update_link` with `hidden: true`),
  and switch its spotlight off.
- Put the description back with `update_profile`.
- Put the theme back with `restore_theme` and the `before` you kept.
- Point a tracked link somewhere new with `update_tracked_link`: the address
  people saved keeps working. Switch it off (`active: false`) only if nothing
  should be there; its numbers stay either way.
