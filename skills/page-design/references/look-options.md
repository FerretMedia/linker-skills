# Look options

Every value the Linker tools take for a page's look. Anything left out stays as
it is.

## `update_theme`

| Field | Values |
| --- | --- |
| `textColor`, `buttonColor`, `buttonTextColor`, `backgroundColor` | `#rrggbb` |
| `removeBackgroundImage` | `true` takes an uploaded background picture off, leaving the colour |
| `font` | A Google Fonts family, or `null` for the system font |
| `textSize` | 75 to 150, percent of normal |
| `bold`, `italic` | `true` or `false`, for all text |
| `radius` | `none`, `small`, `medium`, `large`, `full` (pill buttons) |
| `shadow` | `none`, `soft`, `strong` |
| `buttonStyle` | `solid`, `outline`, `ghost` |
| `buttonOpacity` | 0 to 100; below 100 the background shows through |
| `buttonBlur` | 0 to 24 px of blur behind see-through buttons (glass) |
| `buttonHover` | `none`, `lift`, `grow`, `press`, `slide`, `tilt`, `glow`, `ring`, `fill`, `shine` |
| `textBackdrop` | `true` puts the name and description on the buttons' surface |
| `layout` | `stack` (one column), `grid` (two across), `compact` (tight list) |
| `iconRow` | `top`, `bottom`, `left`, `right`: where the social icons sit |
| `header` | `classic` (picture over name), `banner` (wide picture behind), `hero` (big picture), `side` (picture beside name) |
| `pictureShape` | `circle`, `rounded`, `square`, `arch`, `blob`, `leaf` |
| `pictureSize` | `small`, `medium`, `large`, `huge` |
| `pictureRing` | `none`, `solid`, `gradient`, `glow` |
| `pictureRingColor` | `#rrggbb`, or `null` to follow the text colour |
| `nameFont` | A Google Fonts family for the name only, or `null` |
| `nameSize` | `regular`, `large`, `huge` |
| `nameEffect` | `none`, `outline`, `shadow`, `gradient`, `glow` |
| `align` | `center`, `left` |
| `entrance` | `none`, `fade`, `rise`, `cascade` (one piece at a time) |
| `logo` | The name of one of the person's images, shown instead of the name, or `null` |
| `logoSize` | `small`, `medium`, `large` |

A `banner` header and a background picture use pictures uploaded in the
dashboard; the tools can't upload.

## `set_background`

The animated background, drawn over the page colour.

| Field | Values |
| --- | --- |
| `preset` | `noise` (soft blobs of light drifting), `aurora` (drifting colour), `scatter` (shapes, icons or images strewn about), `liquid` (marbled ink), `waves` (rolling bands), `stars` (flying through stars), `shader` (your own GLSL) |
| `on` | `false` switches it off; picking a preset switches it on |
| `colors` | One to four `#rrggbb`; the first is the base |
| `speed` | 0 (still) to 100 |
| `scale` | 0 to 100: blob size, glow size, item size, detail, wave size or star density, by preset |
| `knobs` | A preset's own sliders, 0 to 100. Noise: `light`, `softness`, `swirl`, `rim`. Scatter: `amount`, `variety`, `tilt`, `depth` |
| `items` | Scatter only: up to six of `heart`, `star`, `sparkle`, `circle`, `bolt`, `note`, `moon`, `smile`, `plus`, a network's icon (`youtube`, `tiktok`, `instagram`, `twitch`…), or `image:<name>` for one of the person's images |
| `motion` | Scatter only: `still`, `float`, `twinkle`, `rise`, `fall` |
| `code` | Shader only: a GLSL fragment shader, run in a sandboxed frame |
| `reshuffle` | `true` scatters it differently |
| `dim` | 0 to 100: lays the page colour over it to calm it down |
| `grain`, `grainSize`, `grainMotion` | Film grain over any background: amount, coarseness, movement |
| `vignette` | 0 to 100: darker edges |
| `scroll` | `none`, `hue` (colour shifts), `drift` |
| `hover` | `none`, `glow`, `zoom` |

A video background is uploaded in the dashboard.

## Starting points

| Brief | Try |
| --- | --- |
| Calm, minimal | Off-white background, near-black text, `ghost` or `outline` buttons, `radius: small`, `entrance: fade`, no animated background |
| Bold, loud | Saturated `buttonColor`, `shadow: strong`, `buttonHover: press`, `nameEffect: shadow`, `nameSize: huge` |
| Dreamy | `noise` with two or three soft colours, `speed` about 15, `buttonOpacity` 70 and `buttonBlur` 12, `pictureRing: glow` |
| Retro | A display `nameFont` ("Press Start 2P", "Bungee"), `radius: none`, `shadow: strong`, `scatter` with `star` and `sparkle` twinkling |
| Editorial | A serif `nameFont` ("DM Serif Display", "Fraunces"), `align: left`, `header: side`, `layout: compact` |
| Music | `waves` or `liquid` in the cover's colours, `scatter` with `note` rising |
