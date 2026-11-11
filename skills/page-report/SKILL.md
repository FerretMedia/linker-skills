---
name: page-report
description: Report how a Linker page (linker.cool link-in-bio) is doing - visits, link clicks, where visitors come from, which TikTok posts sent people, tracked links - and what to change. Use when someone asks how their page or links are doing, wants a weekly or monthly recap, asks which link or post works best, or wonders why clicks dropped. Needs Linker's Max or Ultra plan.
---

# A Linker page report

Numbers are only useful with a "so what". A report is a few numbers, what they
mean, and one to three things to do, not a dump of every figure.

## Gather

Pick the range from the question: 7 days for "this week", 30 for "this month"
(the default), 90 for a quarter. Those are the ranges Linker keeps.

- `get_analytics` with `days`: visits, unique visitors and clicks, by day and
  per link, where visitors came from, their countries and devices, and
  `previous`, the same totals for the range just before, for "up or down".
- `get_post_results` (same range, or `"all"`): their TikTok posts with views,
  likes and the visits each sent to the page. It needs TikTok connected in
  Linker's settings; if it isn't, skip it and mention it once.
- `list_tracked_links`, and `get_tracked_link_stats` for the ones that matter.

For "better than last month?", compare with `previous`. Say when a number is
too small to mean much (a handful of clicks).

## Write it up

1. **The headline**, one sentence: visits and clicks over the range, and the
   direction ("1,240 visits this month, up about a third; 38% tapped a link").
   Click rate is clicks divided by visits.
2. **What works**: the top two or three links by clicks, the top sources, and
   the post that sent the most visits (a post with fewer views that sent more
   visits is the more useful finding).
3. **What doesn't**: links near the top that nobody taps, a source that
   dropped, a tracked link with no opens.
4. **One to three things to do**, each concrete and tied to a number: move a
   link up, rename a vague label, post again where visits came from, retire a
   dead link.

Offer to make the page changes right away with the Linker tools (`move_link`,
`update_link`), and remember the order before so it can be put back.

Keep it short. A table helps for links or posts side by side; no charts unless
asked.

## On Pro

The numbers tools refuse below Max. Say plainly that numbers, posts and tracked
links reach AI apps on Linker's Max and Ultra plans, that they are all in the
Linker dashboard's Analytics, and link https://linker.cool/docs/ai-connector#plans.
Don't push an upgrade, and don't guess at numbers.
