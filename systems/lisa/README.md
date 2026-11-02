# Lisa style guide

> Ink does the talking. The rainbow does the shouting.

Live at [billyhunt.com/design-systems/lisa](https://www.billyhunt.com/design-systems/lisa/).

Lisa is a neon, 90s-school-supplies design system with two modes: **Day**
(white paper, ink outlines, hard shadows) and **Dusk** (midnight sky, lavender
outlines, glow). It started from five explorations: Trapper Keeper, Sticker
Sheet, Airbrush Dusk, Holo Foil and Gel Pen. It keeps Trapper Keeper's bones
for Day and Airbrush Dusk's colour for Dusk.

| File | Role |
|---|---|
| `index.html` | Start here. Every token and component, live, in both modes. |
| `README.md` | The rules and why they exist. Read this before you design anything new. |
| `lisa.css` | Drop-in stylesheet: tokens for Day and Dusk, `.lisa-*` components, prose, print. Inert until an element opts in. The source of truth for every value. |
| `tokens.json` | The same tokens in the Design Tokens Community Group (DTCG) format, for design tools. `$value` is Day; Dusk is under `$extensions["com.lisa.mode"].dusk`. |
| `assets/shapes/` | Every shape as a standalone SVG in Day colours, with the 3px ink edge and hard shadow baked in. For decks and documents; in code, use the `<symbol>` sprite in `index.html` so fills follow the tokens. |
| `assets/logos/` | `lisa-icon.svg` (app icon, 64px and up) and `lisa-favicon.svg` (32px and below). |

When a value changes, change `lisa.css` and `tokens.json` together.

---

## 1. Principles

1. **Neon is a fill.** By Day, neon never carries text: lime on white is 1.6:1.
   By Dusk it may, because every fill passes 4.5:1 on Midnight.
2. **Ink does the talking.** One text colour, one muted, and one accent for
   links. That is all the coloured text there is.
3. **Every edge is 3px.** Borders, rules, outlines and shapes. It keeps the
   neon from melting together, and it keeps working in print, greyscale and
   high-contrast modes, where fills drop out.
4. **Shadows by day, glow by night.** `--depth` is the only token that changes
   shape between modes. Everything else only swaps colour.
5. **Tilt one thing per view.** A sticker, a badge or a burst at `--tilt`
   (−6°). Two tilted things and the page looks dropped.
6. **One job per shape.** Shapes never swap jobs (§5).

## 2. Using it

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bungee&family=Nunito:wght@400;700;900&family=Space+Mono:wght@400;700&display=swap">
<link rel="stylesheet" href="lisa.css">

<body class="lisa">
```

- **Mode.** Day by default. Dusk when the OS is in dark mode, unless the root
  element has `data-theme="day"`. Force Dusk with `data-theme="dusk"`.
- **Components** opt in by class: `.lisa-btn`, `.lisa-fat`, `.lisa-chip`,
  `.lisa-alert`, `.lisa-card`, `.lisa-folder`, `.lisa-input`, `.lisa-prose`,
  `.lisa-code`. See `index.html` for markup.
- **Fonts** load from Google Fonts in v0.1. Self-hosting them (as Alethia
  does) is a to-do.

## 3. Colour

Seventeen tokens, same names in both modes. Fills are numbered by job, not by
hue, so a fill can change colour between modes without breaking its meaning.

| Token | Job | Day | Dusk |
|---|---|---|---|
| `--bg` | Page ground | Paper `#FFFFFF` | Midnight `#160B2B` |
| `--surface` | Cards, wells | Lilac `#F6F1FF` | Dusk `#24123F` |
| `--text` | Body text | Ink `#14001F` | Starlight `#F6EEFF` |
| `--text-muted` | Secondary | Smudge `#5B4A66` | Moonlight `#B9A6D6` |
| `--border` | Every edge | Ink `#14001F` | Moonlight `#B9A6D6` |
| `--accent-text` | Links | Berry `#B5006A` | Flamingo `#FF4FD8` |
| `--on-fill` | Text on fills | Ink `#14001F` | Midnight `#160B2B` |
| `--on-fill-6` | Text on violet | White `#FFFFFF` | Midnight `#160B2B` |
| `--ring` | Focus | Violet `#8A2BFF` | Starlight `#F6EEFF` |
| `--fill-1` | Primary action, errors, hearts | Magenta `#FF2DA0` | Flamingo `#FF4FD8` |
| `--fill-2` | Badges, warnings | Tangerine `#FF8A00` | Sunset `#FF9F45` |
| `--fill-3` | Notices, highlights, stars | Lemon `#FFE600` | Lemon `#FFE600` |
| `--fill-4` | Success | Lime `#39E61A` | Lime `#39E61A` |
| `--fill-5` | Selection, info | Cyan `#00D4FF` | Lagoon `#3DE8FF` |
| `--fill-6` | Decoration only | Violet `#8A2BFF` | Ultraviolet `#9B5CFF` |
| `--code-bg` / `--code-text` | Code | Ink / Lemon | Void `#0E061D` / Lemon |

Every text pair passes WCAG AA in both modes; most pass AAA. The one trap is
`--fill-6` by Day: ink on violet is 3.7:1, so it takes white text. Keep words
off it. The full table is in `index.html`.

The `--spectrum` gradient runs fill-1 to fill-6, always in that order. It is
for the slab at the top and bottom of a page and for focus frames. Nowhere
else.

## 4. Type, space, shape

- **Bungee** for display and headings, always capitals, 24px and up.
  **Nunito** 400/700/900 for body and UI. **Space Mono** for labels, tokens
  and code: 12px capitals at +0.08em.
- **Type scale:** 12, 15, 17, 22, 30, 48, 88. Body is 17 on 1.6.
- **Space:** 4, 8, 12, 16, 24, 32, 48, 64. Nothing in between.
- **Shape:** radius 14 (cards), 10 (inputs), pill (buttons, chips). Rules are
  3px; 6px for blockquotes; the spectrum slab is 16px.
- **Depth:** Day is a hard ink offset (`6px 6px 0`, `4px 4px 0` small). Dusk
  is a glow in fill-1. Pressed controls drop depth and shift 3px.

## 5. Shapes

Two kinds.

**Decoration**: star, heart, sparkle, bolt, burst, rainbow, squiggle. For
headers, margins and empty states. Never inside data, never as icons for
actions.

**Fat shapes** do a job. Each has a safe area where text lives, and a limit.

| Shape | Job | Text | Min size |
|---|---|---|---|
| Cloud pill | Button | ≤ 16 characters | 48 tall |
| Fat heart | Toggle (like) | count ≤ 4 | 64 wide |
| Chubby star | Toggle (favourite) | icon only | 56 |
| Soft burst | Badge, never clickable | ≤ 4 characters | 40 |
| Puffy sparkle | Avatar | 2 initials | 48 |
| Puffy tile | Pick one | title + 1 line | 200 × 170 |
| Fat unicorn | Hero button, once per product | ≤ 14 characters | 200 wide |

Rules for fat shapes:

- **Fat, not spiky.** Inner radius stays above about 65% of outer, or labels
  stop fitting.
- **The hit area is the bounding box**, not the bumps.
- **Focus follows the outline.** A 14px stroke behind the shape lights up in
  `--ring` on `:focus-visible`. Never a rectangular outline around a cloud.
- **Not in dense UI.** Forms, tables, toolbars and settings use the plain pill
  (`.lisa-btn`).
- **Cloud pills are fixed sizes in v0.1.** A long or translated label uses the
  plain pill until the cloud can stretch.

Shapes ship as an SVG `<symbol>` sprite at the top of `index.html`. Copy the
sprite into a page and draw a shape with `<use href="#lisa-cloud">`. Its fill
comes from `--shape-fill`.

## 6. Mark and print

The wordmark is "Lisa" in Bungee over the spectrum slab. The app icon is the
unicorn silhouette in ink on Lemon, at 64px and up; below that it turns into a
blob, so the favicon is the sparkle on Magenta.

Lisa always prints in Day. Glows and the sky drop out, fills stay under ink,
and the spectrum slab prints as a solid ink bar. Every shape keeps its 3px
outline, so nothing depends on colour.

## 7. Not done yet

- Self-hosted fonts.
- A cloud pill that stretches to its label.
- Checkbox, radio and switch with shape states; select, menu, dialog, toast,
  tooltip, table.
- A utility icon set (a rounded open-source set, not hand-drawn).
- A Windows high-contrast pass.
