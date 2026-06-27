# Fonts & Licenses — `nocturne` theme

The `nocturne` Marp theme uses two typefaces, loaded at runtime from the
[Fontshare](https://www.fontshare.com/) CSS API (see the `@import url(...)` at the
top of `nocturne.css`). The font files are **not redistributed in this repository** —
they are fetched from Fontshare's CDN — so only attribution is required here.

| Font | Role | Foundry / Source | License |
| ---- | ---- | ---------------- | ------- |
| **Cabinet Grotesk** (800) | Headings / display | Indian Type Foundry, via [Fontshare](https://www.fontshare.com/fonts/cabinet-grotesk) | [ITF Free Font License](https://www.fontshare.com/licenses/itf-ffl) |
| **Satoshi** (500) | Body text | Indian Type Foundry, via [Fontshare](https://www.fontshare.com/fonts/satoshi) | [ITF Free Font License](https://www.fontshare.com/licenses/itf-ffl) |

The ITF Free Font License permits free personal and commercial use, including web
embedding. Its terms require that the license travel with the font **files** if you
ever redistribute those files (e.g. if you self-host them).

## Offline / PDF note

Because the fonts are loaded over the network, they require an internet
connection when the slides are first viewed and when exporting to PDF
(`npm run export`). For a fully offline / self-contained deck, download the font
files, self-host or base64-embed them in `nocturne.css`, and include the license
text alongside the files.

## Changing fonts

Edit the `@import url(...)` line and the `font-family` declarations in
`presentation/themes/nocturne.css`. If you switch to other fonts, update this file
with their attribution and license.
