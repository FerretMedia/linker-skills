---
name: media-kit
description: Write a creator's media kit or brand pitch from their real Linker numbers (linker.cool link-in-bio page and tracked links). Use when someone asks for a media kit, a rate card intro, a pitch email to a brand or sponsor, or a recap of how a sponsored link performed. Needs Linker's Max or Ultra plan for the numbers.
---

# A media kit from Linker numbers

Brands want three things: who the audience is, proof that the creator moves
people to act, and what a deal looks like. Linker has the proof: visits,
clicks, where people come from, and what tracked links did.

## Gather

- `get_page` for the name, description and links (which platforms they are on).
- `get_analytics` with `days: 90` for the steady picture: visits, click rate,
  top sources, countries and devices.
- `get_post_results` with `"all"` if TikTok is connected: the posts that sent
  the most visits.
- For a sponsor recap: `list_tracked_links` and `get_tracked_link_stats` for
  the sponsor's link (opens by day, source, country, device).

Ask for what Linker can't know, in one message: follower counts per platform,
past brand partners, rates or "rates on request", and contact email.

## Write it

**Media kit**, one page, in this order:

1. Who they are, in two sentences, in their voice.
2. Audience: platforms and follower counts (from them), countries and devices
   (from Linker).
3. Proof: monthly page visits, click rate, the best-performing post or tracked
   link with its number ("one TikTok sent 2,300 people to the shop link").
4. What they offer: formats (a dedicated video, a story, a link on the page for
   a month, a tracked link with a report afterwards).
5. Contact.

**Pitch email**: under 150 words. One line on why this brand fits, one proof
number, one concrete offer, one question to close.

**Sponsor recap**: the tracked link's opens over the campaign, by source and
country, compared with the page's usual traffic, and one sentence on what to
repeat next time. Linker's dashboard also makes a shareable sponsor report with
a PDF.

## Honesty rules

- Use Linker's numbers exactly; round only as "about 2,300", never upward.
- Say the range ("last 90 days").
- Never invent follower counts, demographics Linker doesn't have (age, gender),
  or past deals. Leave a clear `[fill in]` instead.

## On Pro

The numbers tools refuse below Max. Say that numbers reach AI apps on Linker's
Max and Ultra plans (https://linker.cool/docs/ai-connector#plans), and offer to
write the kit with numbers they copy from the dashboard's Analytics.
