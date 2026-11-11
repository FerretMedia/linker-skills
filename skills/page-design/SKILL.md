---
name: page-design
description: Restyle a Linker page (linker.cool link-in-bio) from a description. Use when someone wants their Linker page to look a certain way ("make it feel like a 90s arcade", "calm and minimal", "match my new album cover"), asks for new colours, fonts, buttons, a header layout, an animated background or a ready-made look, or wants an earlier look back.
---

# Designing a Linker page

A Linker page is a creator's link-in-bio page at `linker.cool/@name`: a picture,
a name, a short description and a column of links, seen mostly on phones. The
Linker connector's tools change it directly, and every change is public at once.

Most looks need no CSS. Linker's **Look** settings cover colours, fonts, button
shapes and hovers, the header, the picture's frame, the name's style, an
animated background and how the page comes in. Reach for custom CSS (the
`page-css` skill) only for what those settings can't do.

## The order of work

1. **Read first.** Call `get_page`. Note the current theme, whether there is
   custom CSS (it overrides the Look settings it touches), the person's own
   images (`theme.assets`) and how many links there are.
2. **Turn the brief into a direction.** Pick one idea and commit to it: a
   palette of two or three colours plus a neutral, one display font for the
   name and one readable font for everything else, and one button treatment.
   "Fun, exciting and green" is a whole brief; don't ask five questions back.
   Ask one question only when the brief truly forks (for example "dark or
   light?" when nothing hints either way).
3. **Try the gallery when it fits.** `list_looks` returns ready-made looks with
   their kinds (bold, soft, minimal, retro, playful, editorial, dark, light,
   animated) and colours. If one matches the brief, `apply_look` it, then adjust
   with `update_theme`. A look keeps the person's pictures, links, text and text
   size.
4. **Otherwise build it.** One `update_theme` call with every field the
   direction needs, then `set_background` if it wants motion. The options and
   their values are in `references/look-options.md`.
5. **Say what changed** in two to four lines: the idea, the main colours and
   fonts, and what to ask for to push it further. Keep the `before` theme from
   the first change of the session: that is the way back.

## Taste rules that keep pages working

- **Contrast.** Text on the background and labels on buttons need at least
  4.5:1. Pale text on a busy animated background fails: raise the background's
  `dim`, or set `textBackdrop: true` so the name and description sit on the
  buttons' surface.
- **Phones first.** The column is about 375px wide. `huge` name sizes with long
  names wrap badly; prefer `large` for names over 14 characters. A `hero`
  header pushes the links below the fold on a small phone; use it when the
  picture is the point.
- **Fonts.** Google Fonts family names, spelled exactly as Google does
  ("Space Grotesk", "DM Serif Display"). Use a display face for `nameFont` only,
  and a readable one for `font`. Two families at most.
- **Motion with restraint.** One moving thing at a time: an animated background
  or a lively button hover or an entrance, rarely all three. Keep background
  `speed` under 40 unless the brief is loud. Linker already turns motion off for
  visitors who ask their device for less.
- **Keep what's theirs.** Never remove a background picture, logo or custom CSS
  unless asked. If custom CSS overrides what you just changed, say so and offer
  to adjust the CSS.

## Undo

Every change answers with the theme `before` it. To put a look back, call
`restore_theme` with that `before`, unchanged. After several changes, the
first `before` of the session is the page as it was when you started; offer it
when someone says "go back to how it was".

## When things refuse

- **Not connected.** Without the Linker tools, describe the settings to set by
  hand in the dashboard's Look tab (app.linker.cool), or write CSS with the
  `page-css` skill for them to paste.
- **Plan.** The tools refuse on Linker's free plan. Say plainly that the AI
  connector comes with Linker's paid plans and point to
  https://linker.cool/docs/ai-connector#plans; don't push an upgrade.
- **An image name that isn't there.** Logos and Scatter images must already be
  uploaded under My images in the dashboard; the tool lists the names that
  exist.
