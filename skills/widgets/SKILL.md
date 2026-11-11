---
name: widgets
description: Write, fix and publish widgets for Linker (linker.cool): small cards (a rating, a menu, opening hours, an event, a product) that a business makes once and offers to creators’ link-in-bio pages. Use whenever someone asks for a Linker widget, wants one changed or restyled, or has problems the widget checker reported.
---

<!--
  Built from the widget guide in the Linker app (packages/widgets/src/skill.ts,
  served at app.linker.cool/skills/linker-widgets/SKILL.md). Only this front
  matter and comment differ; copy the rest again when that file changes.
-->

# Making a Linker widget

A business wants a widget: a small card that shows on the Linker pages of the
creators it works with. You write its three files. Linker checks every file
against the rules below and won't publish a widget with any problem, so write
against them and check your work.

## If you are connected to Linker

With the Linker AI connector you have tools that work on the business's own
widgets. Use them instead of handing files back:

1. `list_widgets` to find the widget they mean, or `create_widget` to start
   one, empty or from a starter (rating, menu, hours, event, product).
2. `get_widget` for its files as they are now and the checker's problems.
3. `save_widget` with all three files, complete. It answers with what the
   checker found: fix every problem and save again until there are none.
4. Tell them what you made, and that the builder in the Linker dashboard
   (Widgets, then the widget) shows it on a sample page in every look.
5. `publish_widget` only when they ask. Publishing changes the widget on
   every page that shows it.

Keep what they already have unless they ask to change it: field names, the
layout, the look. Renaming or removing a field makes the next version one
every page has to accept.

## If you are not connected

Hand back the three files, complete, each in its own code block named
widget.json, widget.html and widget.css. They paste them into the builder's
tabs in the Linker dashboard, where the checker runs as they type.

# Writing a Linker widget

A widget is a small card on someone's Linker page (a link-in-bio page). It is
three files: widget.json (its name and fields), widget.html (the markup, with
slots) and widget.css (its look). It is drawn as plain HTML inside the page,
as a block among the links or as a tile in a grid (see "Block or tile").

## widget.json

{
  "name": "Rating badge",
  "description": "One line on what it shows.",
  "fields": {
    "score": { "type": "rating", "max": 10, "label": "Score", "required": true },
    "quote": { "type": "text", "label": "Quote" },
    "review": { "type": "link", "label": "Full review" },
    "accent": { "type": "colour", "label": "Colour", "filledBy": "owner", "default": "#e4572e" }
  }
}

- Field names: a lowercase letter, then letters and digits (camelCase).
- Types: text, longtext, number, rating, image, link, date, colour, choice, list.
  - rating has "max" (default 5); number may have "min" and "max".
  - choice has "options" (2 to 12, lowercase-with-dashes) and may have "default".
  - colour may have "default" (a hex colour).
  - list has "columns" (fields without filledBy; types text, longtext, number,
    rating, image, link, date) and "maxRows" (at most 20).
- "filledBy": "maker" (default) is filled in by the business for each page
  that shows the widget, and the page's owner can't change it. "owner" is
  filled in by the page's owner. Pictures (image) are always the maker's.
  Anything the same on every page is just written into the HTML.
- "required": true means the widget isn't shown until it has a value.
- "assets" names the widget's own pictures: { "logo": "pictures/logo.png" },
  by their path in the widget's folder (PNG, JPEG, WebP or GIF), or uploaded
  in the builder. Use them as {{asset:logo}} and url(asset:logo).
- At most 15 fields. Text is at most 120 characters, longtext 600.

## widget.html

Plain HTML with slots. No <html>, <head>, <body>, <style> or <script>.

- {{name}} puts a field's value in as text. A date reads like "24 Nov 2026".
- {{#if name}} … {{else}} … {{/if}} shows a part only when a field has a value.
- {{#each list}} … {{/each}} repeats for each row; inside, {{column}} is that row's value.
- <a href="{{link}}"> for a link field, or a fixed https:// address.
- <img src="{{image}}" alt="…"> for an image field, or src="{{asset:logo}}" for
  one of the widget's own pictures. Every <img> needs alt.
- class="card {{choice}}" puts a choice field's option in as a class.
- style="--score: {{score}}" sets CSS variables from number, rating and colour
  fields (and only variables). Use them in CSS: width: calc(var(--score) * 10%).
- Allowed elements: div, span, p, h2 to h6, strong, em, b, i, u, s, small, mark,
  sub, sup, abbr, code, pre, del, ins, q, cite, br, hr, ul, ol, li, dl, dt, dd,
  figure, figcaption, blockquote, section, article, header, footer, aside,
  details, summary, time, a, img, and SVG shapes (svg, g, path, circle, ellipse,
  rect, line, polyline, polygon, text, tspan, defs, linearGradient,
  radialGradient, stop, clipPath, mask). Use <h2> or smaller: <h1> is the page's name.
- Attributes: class, title, aria-label, aria-hidden, lang, dir, style (variables
  only), plus href on a, src/alt/width/height on img, datetime on time, open on
  details, and SVG's own (viewBox, d, fill, …). An SVG gradient may have an id;
  point at it with fill="url(#id)".
- Not allowed, because widgets can't run code, collect information or load
  anything from elsewhere: <script>, on… attributes, javascript: links, forms,
  inputs and buttons, iframes, <video>, <audio>, <use>, <foreignObject>.
- Each field and column also becomes a CSS variable on the widget: colour,
  number, rating and choice fields as --name.
- At most 400 elements and 20 KB.

## widget.css

Any CSS: layout, grid, flex, gradients, shadows, keyframe animations, :hover,
:focus, transitions, @media and @container. It only styles the widget: ":root",
"html" and "body" mean the widget's own box.

- Round the widget's outer box with var(--linker-widget-radius): the page's
  corners, so the widget matches the links around it (square on a square page).
  Inner pieces round no more than that: min(12px, var(--linker-widget-radius)).
- The page's look is there to borrow: var(--linker-text), var(--linker-bg),
  var(--linker-button), var(--linker-button-text), var(--linker-radius) (its
  buttons' corners), and the page's font is inherited. A widget may also
  ignore them and wear its own.
- No url() except the widget's own pictures: url(asset:logo). No @import, no
  @font-face: use the page's font or a system font stack.
- Style with classes. A visitor who asked for less motion gets no animation.
- At most 30 KB.

## Block or tile

A page shows the widget in one of two ways, and it should look right in both:

- As a block among the links: up to 320px wide, as tall as its content, and
  cut off past 600px.
- As a tile in a grid: a box of a fixed size that the content doesn't change.
  The smallest is 2 × 2, about 156 × 156px; a wide tile is about 320 × 156px,
  and a tall one up to 320 × 330px. Anything past the box is cut off.

The widget's own box is what @container measures. Only a tile has a fixed
height, so @container (max-height: 220px) means a small tile: there, give the
outer element height: 100% and box-sizing: border-box, and keep what fits
(the score and the link; the first few rows of a list).

## Good widgets

- Readable on a phone (320px wide) and on light and dark pages: set your own
  background and text colour together, or borrow both from the page.
- Look right with a field left empty and with a long name.
- Use {{#if}} around anything optional, so an empty field leaves no gap.
