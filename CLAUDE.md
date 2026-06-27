# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a template for academic papers and presentations at Hochschule der Medien Stuttgart (HdM). It bundles two independent deliverables that share a repo and a single `config.yml` toggle:

- A **Typst paper** (`paper/`) built to a timestamped PDF.
- A **Marp presentation** (`presentation/`) deployed to GitHub Pages.

Either deliverable can be turned off in `config.yml` without removing its files.

## Commands

**Paper (Typst):**
```bash
typst watch paper/paper.typ      # live rebuild while editing
typst compile paper/paper.typ    # one-shot build -> paper/paper.pdf
```

**Presentation (Marp):**
```bash
cd presentation
npm install
npm run dev        # live preview server with watch
npm run build      # build self-contained HTML -> dist/index.html
npm run export     # export to PDF -> dist/slides.pdf (needs Chrome/Chromium)
```

## Architecture

### Feature toggling
`config.yml` holds `features.paper` and `features.presentation` booleans. Both GitHub Actions workflows start with a `check-config` job that greps these values out of `config.yml` and gates the `build` job on them. There is no central config loader — the grep in each workflow *is* the config parser, so the YAML shape (`features:` block with `paper:`/`presentation:` two lines below) must stay stable for the toggle to keep working.

### Paper
- `paper/lib.typ` defines the single `academic-paper(...)` show-rule function: title page, typography, heading styles, abstract, acknowledgments, and IEEE bibliography. This is the reusable template — change layout/styling here.
- `paper/paper.typ` is the actual content; it imports `lib.typ` and calls `#show: academic-paper.with(...)` with metadata (title, author, course, etc.), then writes the body in Typst markup.
- `paper/references.bib` is the BibTeX source, wired in via the `bibliography-file` parameter.
- `typst.toml` declares the Typst package metadata with `entrypoint = "paper/lib.typ"`.

### Presentation
- `presentation/slides.md` is the Marp deck: Markdown with a `marp: true` front-matter block, slides separated by `---`, and a built-in theme set via `theme:` (template defaults to `gaia` + `class: invert`). Per-slide settings and presenter notes are HTML comments (`<!-- _class: lead -->`, `<!-- ... -->`).
- `presentation/marp.config.js` holds Marp CLI settings shared by all scripts (`html: true`, and `themeSet: './themes'` to register custom themes). `package.json` has `"type": "module"` so this config is ESM.
- `presentation/themes/nocturne.css` is the custom default theme (`theme: nocturne`) — a dark design with a blue accent (`/* @theme nocturne */`, extends `@import 'default'`). It sets `color-scheme: dark` so the imported default theme's `light-dark()` variables (tables, code) resolve to dark; lead slides use `<!-- _class: lead -->`. Fonts (Cabinet Grotesk / Satoshi) come from Fontshare at view time — attribution/licenses in `presentation/themes/FONTS.md`.
- Note: Marp Core has no Slidev-style step/click reveals, no presenter/overview routes, and no UnoCSS/Tailwind utility classes — slides are static Markdown styled by the theme.

### CI/CD (`.github/workflows/`)
- `build-paper.yml`: on push to `main` touching `paper/**` (or manual dispatch), builds the PDF, copies it to the repo root as `paper-YYYY-MM-DD-HHMM.pdf`, **commits that PDF back to `main`**, uploads an artifact, and on tag pushes deletes all prior releases and publishes a fresh release with the PDF. Be aware this workflow pushes a commit — pulled history will include bot commits.
- `deploy-slides.yml`: on push to `main` touching `presentation/**` (or manual dispatch), runs `npm ci` + `npm run build` to produce a single self-contained `presentation/dist/index.html`, uploads that dir as the Pages artifact, and deploys it (served at `https://<user>.github.io/<repo>/`). No base-path or SPA-routing handling is needed since Marp emits one static HTML. Pages must be set to "GitHub Actions" source in repo settings. `npm ci` requires `presentation/package-lock.json` to be committed.

## Conventions

- Both workflows trigger only on `main` and only when their own subtree (or `config.yml` / the workflow file) changes; editing the paper does not rebuild slides and vice versa.
- A new release deletes all previous releases by design (single "latest PDF" model), so tag pushes are destructive to release history.

## Academic integrity

This is a template for academic work produced *with* AI assistance, so AI help must stay disclosable and reviewable. See [`ACADEMIC_INTEGRITY.md`](ACADEMIC_INTEGRITY.md) for the full guidance. When assisting on actual paper/presentation content (as opposed to template plumbing):

- Keep the author as the accountable party; AI output is an unverified draft, not a finished claim.
- Record substantive AI contributions so they can flow into the paper's AI-usage declaration (`ai-usage` / `ai-tools` in `paper/paper.typ`) and the presentation's "Acknowledgements & AI Use" slide.
- Never fabricate facts or citations; every reference must be real and verified against its source. Read and test any code before relying on it.
- The paper template renders these disclosures via the `ai-usage`, `ai-tools`, `declaration`, and `declaration-place` parameters in `paper/lib.typ` (sections appear after the bibliography).
- Do not invent specific HdM/Prüfungsordnung policy wording; point users to their official examination regulations for binding rules.
