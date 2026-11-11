---
name: page-css
description: Write custom CSS for a Linker page (linker.cool link-in-bio), or fix CSS the Linker CSS tab reports problems with. Use when someone asks for CSS for their Linker page, wants a look that Linker's Look settings can't make (custom gradients, unusual button shapes, hand-made hover effects, a whole themed page like "a 90s arcade"), or pastes CSS that Linker dropped or flagged.
---

<!--
  A copy of the CSS tab's guide in the Linker app
  (apps/app/static/skills/linker-page-css/SKILL.md, served at
  app.linker.cool/skills/linker-page-css/SKILL.md). Only this front matter and
  the note below differ; copy the rest again when that file changes.
-->

> **With the Linker connector**, read the page with `get_page` first (the theme
> and any CSS already there), then save with `set_custom_css` instead of
> handing the CSS back to paste. It replaces the whole stylesheet and answers
> with any problems the sanitizer found, so fix them and save again. Its answer
> keeps the CSS `before`: save that to undo. Ask before replacing CSS someone
> already has. Prefer the Look settings (the `page-design` skill) for anything
> they cover, since CSS overrides them.


# Designing CSS for a Linker page

A creator wants their Linker page (a link-in-bio page at `linker.cool/@name`)
to look a certain way. You write CSS; they paste it into the **CSS tab** of the
Linker dashboard, where it is checked, previewed and saved.

That CSS is not a normal stylesheet. Linker stacks it on top of its own design,
scopes it to the page, and runs it through a sanitizer that **silently drops**
anything outside the rules below. CSS written for a generic website will half
work. Write against this file and it works the first time, in the dashboard's
preview and on the live page alike.

## What to hand back

1. **One sentence** naming the design you made ("Lime Rush: a glowing green
   gradient, chunky sticker buttons that bounce on hover").
2. **One complete `css` code block**, ready to paste. It replaces whatever is
   in the CSS tab, so never answer with a fragment to merge, unless they
   asked for a single change to CSS they gave you.
3. **Two to four short notes**, only what they need: what to change to tweak
   it (point at the colour variables at the top), what it overrides from the
   Look tab (see "What your CSS overrides"), and anything that depends on
   their content (a background picture, section titles).

Make bold choices. "Fun, exciting and green" is a whole brief: pick a palette,
a font stack, a button shape and a hover with some personality, and go. Ask a
question only when you truly can't proceed. Keep the CSS readable: a small
block of named colours at the top, then one commented section per part of the
page. Comments are fine; they help the creator find their way.

If the creator pastes back problems from the CSS tab (each is
`line:column` and a message), fix exactly those and hand back the whole block
again.

## The page you are styling

Every element you may style carries a `data-part` attribute. **Select by
`data-part` only.** Never select by tag (`h1`, `a`, `ul`) or by class: the
dashboard's preview draws the same parts with different tags (the name is an
`h1` on the page and a `p` in the preview), and class names change without
notice.

```
[data-part="page"]                    the root; in your CSS also :root (or html, body)
├── [data-part="backdrop"]            the animated background from the Background studio
│   └── [data-part="scene"]           what draws it: a div, a video, or a frame
├── [data-part="scrim"]               dims a background picture so text stays legible
├── [data-part="content"]             the centred column everything sits in
│   ├── [data-part="banner"]          the header's wide picture (an img); only with a Banner or Hero header
│   ├── [data-part="avatar"]          the profile picture (an img), or a div with initials
│   ├── [data-part="identity"]        wraps the name and description
│   │   ├── [data-part="name"]        the display name
│   │   │   └── [data-part="logo"]    an image logo drawn instead of the name's text (alt is the name)
│   │   └── [data-part="description"] the bio; line breaks are kept
│   ├── [data-part="links"]           a list (ul) of buttons; there can be TWO, see below
│   │   ├── li > [data-part="section"] > [data-part="section-title"]   a heading among the buttons
│   │   └── li > [data-part="link"]   a button; data-spotlight="true" when the owner spotlit it
│   │              ├── [data-part="icon"]   the platform icon (an svg, coloured by currentColor)
│   │              └── the link's name, as text
│   ├── [data-part="socials"]         the icon row: small square buttons (ul)
│   │   └── li > [data-part="social"] an icon-only button
│   ├── [data-part="links"]           more buttons, below the icon row
│   ├── [data-part="grid"]            a grid of tiles, four square cells across
│   │   └── [data-part="tiles"] > [data-part="tile"] > [data-part="link"]
│   │              data-w and data-h on the tile: the cells it spans, 1 to 4
│   └── [data-part="carousel"]        a row of cards that scrolls sideways; data-cards: their shape
│       └── [data-part="card"] > [data-part="link"]
```

Grids and carousels sit among the lists, in the owner's order, and there can
be any number of them. A tile or a card is a `[data-part="link"]` inside, with
`[data-part="thumb"]` (its picture, if any), `[data-part="icon"]` and
`[data-part="caption"]` (the name). Select `[data-part="tile"] > [data-part="link"]`
to style tiles only; a one-cell tile hides its caption from sight.

A button with a picture is `[data-part="link"]` holding
`[data-part="thumb"]` (the picture, 16:9, across the top) and
`[data-part="caption"]` (the icon and the name, underneath).

What Linker already gives each part, so you only add what's different:

| Part                     | Linker's design                                                                                   |
| ------------------------ | ------------------------------------------------------------------------------------------------- |
| `page`                   | Background colour and picture, text colour, the system font. Position relative, overflow hidden.  |
| `content`                | Flex column, centred, `gap: 0.75rem`, `padding: 2rem 1.5rem`, centred text                        |
| `banner` | Only with a Banner or Hero header: edge to edge across the top, `object-fit: cover` |
| `avatar`                 | `4rem` circle, `object-fit: cover`, a shadow. Initials: centred on the button colour. The Look tab may change its size, shape and ring |
| `name`                   | `1rem`, weight 600                                                                                |
| `description`            | `0.875rem`, 85% opacity, at most `28ch` wide                                                      |
| `links`, `socials`       | No bullets, full width up to `20rem`, `gap: 0.5rem`. `socials` is a wrapping, centred row         |
| `section-title`          | `0.8125rem`, weight 600                                                                           |
| `link`, `social`         | `display: block`, a `2px` border, `border-radius: var(--linker-radius)`, padding with room for the icon on the left; `position: relative`; transitions on transform, shadow and colours |
| `icon`                   | Absolutely placed at the button's left edge, vertically centred, 85% opacity                      |
| `social`                 | A `2.75rem` square, icon centred                                                                  |
| `grid`, `tiles`, `tile`  | Up to `20rem` wide, four square cells, `gap: 0.5rem`; a tile's `link` fills its cells              |
| `carousel`, `card`       | A sideways-scrolling row, snapping to each card; a card is `9rem` wide (`7.5` portrait, `15` landscape) |

Things that trip people up:

- **There can be two `[data-part="links"]` lists**, above and below the icon
  row. Your rules hit both, which is almost always what you want.
- **Buttons are `link` and `social`.** Style both together with
  `:is([data-part="link"], [data-part="social"])`, or the icon row won't match.
- **The avatar may be initials.** `[data-part="avatar"]:not(img)` is the
  initials; `img[data-part="avatar"]` is a real picture. Give both a look.
- **A hover needs three states**, or it won't show in the dashboard's preview
  or for keyboard users:
  `:is([data-part="link"], [data-part="social"]):is(:hover, :focus-visible, [data-demo])`.
- **The root's attributes go on `:root`**, written without a space:
  `:root[data-style="outline"] [data-part="link"]`. Written as
  `[data-style="outline"] [data-part="link"]` it never matches.
- **You don't know their content.** Write for any number of links, with or
  without a picture, description, section titles or icon row. Never style by
  position (`li:nth-child(3)` meaning "my shop link"), except for decoration
  like staggered animations.

## Never change the layout

**The page's layout is Linker's, not yours.** Everything sits in one centred
column, in the order the creator chose, and it must stay exactly there. You
change how the parts _look_, never where they _are_. A design that pushes the
column to one side, lines the text up on the left, or reorders the parts is
broken, however good it looks otherwise.

So never set any of these, on any part or on `:root`:

- `display`, `flex-direction`, `flex-wrap`, `align-items`, `align-content`,
  `align-self`, `justify-content`, `justify-items`, `justify-self`,
  `place-items`, `place-content`, `place-self`, `order`, `float`
- `text-align`
- `margin` in any form, `position`, `inset`, `top`, `right`, `bottom`, `left`
- `width`, `max-width` or `min-width` on `page`, `content`, `identity`,
  `links`, `socials`, `grid`, `tiles`, `tile`, `carousel` or `card`
- `grid-template-*`, `grid-column`, `grid-row`, `grid-area`

What you may do: colours, backgrounds, fonts and text sizes, borders, corner
radius, shadows, the avatar's size, padding inside a button, `padding-block`
on `content` (more room above and below), and `transform` for hover effects
and animations (they move a part for a moment, then it comes back). Decoration
on `::before` and `::after` may be placed absolutely, inside its own part.

If the creator asks for a different layout (links side by side, the picture on
the left), say plainly that Linker's layout is fixed and the CSS tab is for the
look, and design the look they want inside the centred column.

## Colours and the Look tab

The creator also has a **Look tab**: colours, button style, corner roundness,
shadow, hover effect, background picture, and the page's font (any Google
Font), text size, bold and italic. Those reach the page as CSS
variables on the root, and Linker's own design is built from them.

**Set the colours through the variables, on `:root`.** The four colour
variables below are inputs that Linker mixes into everything else (the button
fill, the name panel, the glow), and that mixing happens on the root. So
setting `--linker-button` on `:root` recolours every button, frame and glow at
once; setting it on `[data-part="link"]` only half works.

| Variable                   | What it is                                                                                |
| -------------------------- | ----------------------------------------------------------------------------------------- |
| `--linker-bg`              | Background colour (under any picture); also the colour of the scrim                       |
| `--linker-text`            | All page text, and the keyboard focus ring                                                |
| `--linker-button`          | Button colour: a solid button's fill, an outline's frame and label, glows                 |
| `--linker-button-text`     | The label on a solid button, and the initials                                             |
| `--linker-font`            | The page's font: the Google Font picked in the Look tab, or the system font               |
| `--linker-text-scale`      | The Look tab's text size as a factor, `0.75` to `1.5`; `1` by default                     |
| `--linker-radius`          | Every button's corners, e.g. `0.75rem` or `9999px`                                        |
| `--linker-blur`            | `none` or `blur(12px)`: frosted glass behind buttons                                      |
| `--linker-shadow`          | The avatar's shadow                                                                       |
| `--linker-button-shadow`   | A resting button's shadow (only solid buttons have one)                                   |
| `--linker-hover-transform` | What the Look tab's hover does to a button, e.g. `translateY(-3px)`                       |
| `--linker-hover-shadow`    | The shadow under a hovered button                                                         |
| `--linker-bg-image`        | The creator's background picture, wide screens (`none` if they have none)                 |
| `--linker-bg-image-mobile` | The same picture, cropped for phones (the page uses it at `40rem` wide and narrower)      |
| `--linker-bg-dim`          | How strongly the scrim dims the picture, `0` to `1`; `0` without a picture                |
| `--linker-avatar-size`     | The picture's size from the Look tab: `3rem`, `4rem`, `6rem` or `8rem`                    |
| `--linker-avatar-radius`   | The picture's shape from the Look tab, as a `border-radius` (`9999px` is the circle)      |
| `--linker-avatar-ring`     | The colour of the ring or glow around the picture; the text colour unless one is picked   |
| `--linker-name-font`       | The name's own typeface from the Look tab; `var(--linker-font)` when it has none           |
| `--linker-name-size`       | The name's size from the Look tab: `1rem`, `1.5rem` or `2.25rem`, before the text scale   |
| `--linker-logo-height`     | How tall a logo drawn instead of the name is: `2.5rem`, `4rem` or `6rem`                  |

Made from those, on the root; read them, rarely set them:
`--linker-button-surface` (the button colour at the Look tab's button opacity:
a solid button's real fill), `--linker-label-surface`, `--linker-label-border`
and `--linker-label-text` (the name panel), `--linker-fill` and
`--linker-fill-text` (what the Fill hover floods a button with).

**Define your own palette as variables too**, at the top of `:root`, named
`--fun-*` or similar (never `--linker-*`), and build everything from them, so
the creator can recolour your whole design by changing three or four lines.

### What your CSS overrides

Your CSS always wins over the Look tab, whatever the selector. So tell the
creator plainly what stops responding while your CSS is in:

- Setting the colour variables (or colours on parts) overrides the Look tab's
  colours.
- Setting `background` or `background-image` on `:root` replaces their
  background picture. To keep the picture under your design, see "Layering
  over their picture".
- Styling the buttons' background, border and colour yourself makes the Look
  tab's button style (Solid, Outline, Ghost) stop mattering. That is usually
  right for a strong design: it then looks as you meant whatever they picked.
- Setting `transform` or `box-shadow` on the hover states replaces the Look
  tab's hover effect.

The root carries the Look tab's settings as attributes, if you'd rather adapt
than override:

| Attribute            | Values                                                                            |
| -------------------- | --------------------------------------------------------------------------------- |
| `data-style`         | `solid`, `outline`, `ghost` (the button style)                                    |
| `data-hover`         | `none`, `lift`, `grow`, `press`, `slide`, `tilt`, `glow`, `ring`, `fill`, `shine` |
| `data-text-backdrop` | `true`, `false` (the text background: a panel behind the name and description, and behind each section title) |
| `data-layout`        | `stack`, `grid`, `compact` (always `stack`; ignore it, grids are their own part)  |
| `data-scene`         | `none`, `noise`, `aurora`, `scatter`, `liquid`, `waves`, `stars`, `video`, `shader` (the Background studio's style) |
| `data-header`        | `classic`, `banner`, `hero`, `side` (the header layout; only `banner` and `hero` draw the banner) |
| `data-icons`         | `flow`, `left`, `right` (the icon row among the buttons, or pinned to that side)  |

```css
/* Dashed frames, only while the button style is Outline. */
:root[data-style="outline"] [data-part="link"] {
  border-style: dashed;
}
```

Two of the hover effects draw with pseudo-elements: **Shine** uses each
button's `::after`. Use `::before` for your own decoration on buttons.

## The rules your CSS must follow

The CSS tab runs every rule through a sanitizer. What breaks a rule is left
out, one declaration at a time, and the rest still applies: a mistake shows up
as part of your design quietly missing. So:

- **No `url()`, anywhere.** Not in `background`, not in a variable, not in
  `content`. No background images from the web, no web fonts, no cursors.
  Draw with gradients, shadows, borders, shapes and emoji instead.
- **The creator's own images are the exception, as variables.** Each image
  they add under "My images" on the Look tab (a paid feature) is
  `var(--linker-asset-<name>)`, the name shown under it there, for example
  `background-image: var(--linker-asset-paper)` or
  `content: var(--linker-asset-star)` on a `::before`. Ask the creator which
  names they have; one that doesn't exist draws nothing.
- **Web fonts come from the Look tab only.** `@font-face` is refused, but the
  creator can pick any Google Font there, and the page loads it. If your
  design wants a particular font, tell them which one to pick (say, "Pick
  Fredoka in the Look tab's Font section") and write
  `font-family: var(--linker-font)`, or leave `font-family` alone, which the
  Look tab's font already sets. Otherwise write font stacks from the visitor's
  own fonts, which fall back well:
  - rounded and friendly: `ui-rounded, "SF Pro Rounded", "Arial Rounded MT Bold", "Nunito", system-ui, sans-serif`
  - bold and loud: `"Arial Black", "Helvetica Neue", Impact, system-ui, sans-serif`
  - elegant: `ui-serif, "Iowan Old Style", Georgia, "Times New Roman", serif`
  - techy: `ui-monospace, "SF Mono", "Cascadia Code", Menlo, Consolas, monospace`
  - handwritten: `"Segoe Print", "Bradley Hand", "Comic Sans MS", cursive`
- **At-rules:** only `@media`, `@supports`, `@container`, `@starting-style`,
  and `@keyframes` at the top level (never inside another rule). `@import`,
  `@font-face`, `@layer`, `@scope`, `@property` and every other at-rule are
  refused. Don't wrap your CSS in anything: Linker scopes it to the page itself.
- **Functions** must be standard CSS ones: `var()`, maths (`calc`, `min`,
  `max`, `clamp`, `round`, trig), colours (`rgb`, `hsl`, `hwb`, `lab`, `lch`,
  `oklab`, `oklch`, `color`, `color-mix`, `light-dark`), every gradient
  (`linear`, `radial`, `conic` and their `repeating-` forms), transforms,
  filters (`blur`, `drop-shadow`, `hue-rotate`, …), `cubic-bezier`, `steps`,
  `linear()`, shapes (`circle`, `ellipse`, `polygon`, `inset`, `path`),
  `minmax`, `repeat`, `fit-content`, `anchor()`, `scroll()`, `view()`, `attr()`,
  `counter()`, `env()`. Nothing else, so no `image-set()` or `url()`.
- **Real properties with valid values only.** A typo or a made-up property is
  dropped. Values built with `var()` are always accepted.
- **Keyframe names are yours.** Linker renames them so they can't clash; just
  use the same name in `animation`.
- **At most 32 KB**, 1,000 rules, nesting 8 levels deep. Over 32 KB, none of
  it is used. A great page needs far less: aim for under 6 KB.

Two things are always true, whatever you write, `!important` included:

- **Nothing draws outside the page.** The root is `position: relative` with
  `contain: layout paint`, so even `position: fixed` stays inside it.
  Decorate within the page.
- **Visitors who ask for less motion get none.** With
  `prefers-reduced-motion: reduce`, every animation and transition is
  switched off for them. Design so the page still looks finished standing
  still, and animate freely for everyone else.

## Making it look great

- **Phones first.** Most visitors are on a phone, and the dashboard's preview
  is phone-sized. For wider screens, use a container query, not `@media` (a
  media query in the preview reads the dashboard's window, not the preview):

  ```css
  :root { container-type: inline-size; }

  @container (min-width: 40rem) {
    [data-part="content"] { padding-block: 4rem; }
  }
  ```

- **Readable first, then fun.** Text and button labels need strong contrast
  against what they sit on (aim for 4.5:1). Keep the focus ring: never
  `outline: none` on buttons without a visible replacement.
- **Tints from your palette:** `color-mix(in oklab, var(--fun-lime) 35%, transparent)`.
- **Gradients for depth:** layer a few `radial-gradient`s over a
  `linear-gradient` on `:root` for a glowing background; give it a
  `background-size` larger than the page and animate `background-position`
  for slow drift.
- **Personality in the buttons:** a chunky offset shadow
  (`box-shadow: 0 4px 0 <dark>`) that deepens on hover reads as a pressable
  sticker; `transition` with `cubic-bezier(0.34, 1.56, 0.64, 1)` gives a
  bounce; `:active` can push it back down.
- **Entrances:** animate each `[data-part="links"] > li` in with a short
  keyframe and stagger them with `animation-delay` on `:nth-child()`.
  `@starting-style` works too.
- **Decoration:** emoji or symbols in `content` on `::before` of `content`,
  `name` or the buttons; gradient text with `background-clip: text` plus
  `color: transparent`; `text-shadow` for sticker-style lettering; `filter`
  and `mix-blend-mode` are allowed.
- **The avatar is the hero.** A bigger size (`6rem`), a thick ring
  (`border` plus a spread `box-shadow`), a gentle float animation.

### Layering over their picture

Setting `background-image` on `:root` replaces the picture. To keep it under
your design, list the picture last, for both crops, and keep the gradients on
top translucent:

```css
:root {
  background-image: linear-gradient(transparent 40%, color-mix(in oklab, var(--linker-bg) 80%, transparent)), var(--linker-bg-image);
}

@media (max-width: 40rem) {
  :root {
    background-image: linear-gradient(transparent 40%, color-mix(in oklab, var(--linker-bg) 80%, transparent)), var(--linker-bg-image-mobile);
  }
}
```

When you replace the picture instead, also set `--linker-bg-dim: 0` on
`:root`, or the scrim will dim your design wherever they had a picture. If
`data-scene` isn't `none`, the owner chose an animated background: it is
drawn in `[data-part="backdrop"]`, over the colour and picture, so a design of
your own should hide that part (`visibility: hidden`) or leave the
background alone.

## Before you answer, check

- The layout is untouched: nothing from "Never change the layout", so the
  column is still centred and every part is where it was.
- Every selector uses `data-part` (or `:root` and its attributes), with no
  tags or classes.
- No `url()`, `@import`, `@font-face`, `@layer` or `@scope`; `@keyframes`
  only at the top level.
- Buttons styled as `:is([data-part="link"], [data-part="social"])`, and every
  hover written for `:hover`, `:focus-visible` and `[data-demo]`.
- Colours set as variables on `:root`; a palette of your own at the top.
- Text readable on its background; focus ring intact.
- It still looks finished with no animation.
- One complete block, then the short notes, including what it overrides.

## Example: "fun, exciting and green"

```css
/* Lime Rush: change these four colours to recolour the whole page. */
:root {
  --fun-deep: #052e16;
  --fun-mid: #15803d;
  --fun-lime: #a3e635;
  --fun-sun: #facc15;

  /* Linker's colour inputs, so every built-in piece follows the palette. */
  --linker-bg: var(--fun-deep);
  --linker-text: #f0fdf4;
  --linker-button: var(--fun-lime);
  --linker-button-text: var(--fun-deep);
  --linker-radius: 1rem;
  --linker-bg-dim: 0;

  container-type: inline-size;
  font-family: ui-rounded, "SF Pro Rounded", "Arial Rounded MT Bold", "Nunito", system-ui, sans-serif;
  background-color: var(--fun-deep);
  background-image:
    radial-gradient(circle at 15% 10%, color-mix(in oklab, var(--fun-lime) 45%, transparent), transparent 40%),
    radial-gradient(circle at 85% 85%, color-mix(in oklab, var(--fun-sun) 30%, transparent), transparent 45%),
    linear-gradient(160deg, var(--fun-mid), var(--fun-deep) 70%);
  background-size: 180% 180%;
  background-position: 0% 0%;
  animation: drift 14s ease-in-out infinite alternate;
}

/* The picture: bigger, ringed in lime, floating. */
[data-part="avatar"] {
  width: 6rem;
  height: 6rem;
  border: 4px solid var(--fun-lime);
  box-shadow:
    0 0 0 6px color-mix(in oklab, var(--fun-lime) 30%, transparent),
    0 12px 30px rgb(0 0 0 / 0.35);
  animation: float 4s ease-in-out infinite;
}

/* The name: big sticker lettering. */
[data-part="name"] {
  font-size: 2rem;
  font-weight: 800;
  letter-spacing: -0.02em;
  line-height: 1.1;
  color: var(--linker-text);
  text-shadow:
    0 3px 0 var(--fun-mid),
    0 0 24px color-mix(in oklab, var(--fun-lime) 60%, transparent);
}

[data-part="description"] {
  font-size: 1rem;
  opacity: 0.9;
}

[data-part="section-title"] {
  color: var(--fun-sun);
  text-transform: uppercase;
  letter-spacing: 0.12em;
}

/* Buttons: chunky lime stickers that bounce. */
:is([data-part="link"], [data-part="social"]) {
  background: var(--fun-lime);
  border-color: var(--fun-deep);
  color: var(--fun-deep);
  font-weight: 700;
  box-shadow: 0 4px 0 var(--fun-deep);
  transition:
    transform 160ms cubic-bezier(0.34, 1.56, 0.64, 1),
    box-shadow 160ms ease,
    background-color 160ms ease;
}

:is([data-part="link"], [data-part="social"]):is(:hover, :focus-visible, [data-demo]) {
  background: var(--fun-sun);
  transform: translateY(-3px) rotate(-1deg);
  box-shadow: 0 7px 0 var(--fun-deep);
}

:is([data-part="link"], [data-part="social"]):active {
  transform: translateY(2px);
  box-shadow: 0 1px 0 var(--fun-deep);
}

/* The buttons pop in, one after another. */
[data-part="links"] > li {
  animation: pop-in 480ms cubic-bezier(0.34, 1.56, 0.64, 1) both;
}

[data-part="links"] > li:nth-child(2) { animation-delay: 60ms; }
[data-part="links"] > li:nth-child(3) { animation-delay: 120ms; }
[data-part="links"] > li:nth-child(4) { animation-delay: 180ms; }
[data-part="links"] > li:nth-child(n + 5) { animation-delay: 240ms; }

/* More room on a wide screen. */
@container (min-width: 40rem) {
  [data-part="content"] {
    padding-block: 4rem;
  }
}

@keyframes drift {
  to { background-position: 100% 100%; }
}

@keyframes float {
  50% { transform: translateY(-6px) rotate(2deg); }
}

@keyframes pop-in {
  from { opacity: 0; transform: translateY(12px) scale(0.96); }
}
```

Notes that would go with it:

- Change the four `--fun-*` colours at the top to recolour everything.
- It sets its own colours, background and buttons, so the Look tab's colours,
  background picture, button style and hover effect won't change the page
  while this CSS is in. Corner roundness still works if you delete the
  `--linker-radius` line.
