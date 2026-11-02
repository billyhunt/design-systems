# Design systems

Open-source design systems by Billy Hunt, in one place. Each system is a
folder under `systems/` with its own rules, tokens, stylesheet, specimen page
and license, so you can take one without the others.

Live specimens: <https://www.billyhunt.com/design-systems/>

| System | What it is | Specimen | License |
|---|---|---|---|
| [Lisa](systems/lisa/) | A neon, 90s-school-supplies system with two modes: Day (white paper, ink outlines, hard shadows) and Dusk (midnight sky, lavender outlines, glow). "Ink does the talking. The rainbow does the shouting." | [Lisa](https://www.billyhunt.com/design-systems/lisa/) | MIT |
| [Alethia](systems/alethia/) | The visual language of Alethia, a markdown editor for macOS: paper ground, hard black rules, one hot orange. | [Alethia](https://www.billyhunt.com/design-systems/alethia/) | MIT |

## What each system contains

Every system ships the same pieces, so tools can treat them alike:

| File | Role |
|---|---|
| `README.md` | The rules and why they exist. Read it before designing anything new. |
| `<name>.css` | A drop-in Cascading Style Sheet (CSS) with tokens as custom properties and the components. The source of truth for every value. |
| `tokens.json` | The same tokens in the Design Tokens Community Group (DTCG) format, for design tools. |
| `index.html` | The live specimen: every token and component, rendered. |
| `assets/` | Scalable Vector Graphics (SVG) shapes and logos. |
| `LICENSE` | That system's license. |

## Using a system

Copy the folder, or link the stylesheet. For Lisa:

```html
<link rel="stylesheet" href="lisa.css">
<body class="lisa">
```

To view a specimen locally, serve its folder (browsers block web fonts on
`file://`):

```sh
cd systems/lisa && python3 -m http.server 8000
```

## Adapters

Adapters carry a system into another tool and live in their own repositories:

- [herdr-lisa](https://github.com/billyhunt/herdr-lisa): Lisa for the Herdr
  desktop app and oh-my-pi (themes, layouts, mods, fonts).

## Where each system is maintained

- **Lisa** is maintained here.
- **Alethia**: the values come from the app's own stylesheets in the
  [Alethia repository](https://github.com/billyhunt/alethia-markdown-editor).
  Where the guide and the app disagree, the app wins and the guide is wrong.
  The history of the original
  [alethia-style-guide](https://github.com/billyhunt/alethia-style-guide)
  repository is kept in this one.

## Licenses

Each system is MIT-licensed; see `systems/<name>/LICENSE`. The files at the
root (this README, the site landing page and the publish workflow) are MIT too
(`LICENSE`). Fonts keep their own licenses: the SIL Open Font License (OFL)
texts ship beside the fonts where a system bundles them.
