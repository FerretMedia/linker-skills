---
name: page-setup
description: Set up or tidy up a Linker page (linker.cool link-in-bio): its name, description and links. Use when someone is starting their Linker page, asks what to put on it, wants it reviewed ("is my page any good?", "clean up my links"), or wants their links reordered, grouped under section titles, hidden for now or marked 18+.
---

# Setting up a Linker page

A Linker page has a name, a short description and a column of links, often
with section titles between them. Visitors arrive from a bio on Bluesky,
TikTok or Instagram, on a phone, and decide within seconds. A good page answers
"who is this, and what should I tap?" before they scroll.

## Read, then interview briefly

Call `get_page`. If the page is new or nearly empty, ask at most three things
in one message:

1. What do you do, in a sentence?
2. What is the one thing you most want visitors to do (watch, buy, book,
   subscribe, follow)?
3. Which links do you have? (Paste them; Linker recognises social profiles and
   gives them their network's icon by itself.)

If the page already has content, skip the interview and review it.

## What good looks like

- **The main action first.** The top link is the one thing they most want
  visitors to do. Put it in the spotlight (`spotlight: true`) only if it is
  time-limited or the main reason the page exists; one spotlight at a time.
- **Five to nine links.** More than that, group them under section titles
  ("Watch", "Shop", "Work with me"), added with `add_link` and `section: true`,
  or hide what is out of date (`hidden: true`) rather than deleting.
- **Labels that say what happens.** "Watch the new video" over "YouTube";
  "Book a call (15 min)" over "Calendly". Under 30 characters, no emoji soup:
  one emoji at the start at most, and only if the rest of the page uses them.
- **A description that does a job.** One or two lines: what they make and for
  whom, or what is new. No list of hashtags. Under 160 characters reads well on
  a phone.
- **The name.** Their creator name, as people search for it. Empty shows their
  Bluesky display name.

## Making the changes

- Name and description: `update_profile`. Leaving `description` out keeps it;
  `useBlueskyDescription: true` goes back to the Bluesky one.
- New links: `add_link` (`to: "top"` or `before`/`after` another link's id).
- Changing one: `update_link`. Reordering: `move_link`.
- **18+ links**: `adult: true` asks visitors their age before the link opens.
  Mark adult platforms and adult content; Linker marks well-known adult sites
  by itself.
- **Always the newest video**: a link to a YouTube channel with `latest: true`
  points at its newest upload, with its thumbnail, so the page never shows an
  old video.
- **Removing** a link: ask first, then `remove_link`. Its answer is the link as
  it was, so it can be added back.

Show the plan before a big rework ("I'll move Shop to the top, group the
socials under Follow, and hide the 2024 tour link. Go?"), then make it in one
go and list what changed. For a small, clear request, just do it.

## Then

Offer the `page-design` skill if the page looks plain, and on Max the
`page-report` skill once it has had visitors for a week.

Without the connector, write the plan as a list they can follow in the
dashboard's Links tab (app.linker.cool).
