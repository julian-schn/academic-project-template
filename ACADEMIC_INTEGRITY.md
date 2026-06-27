# Academic Integrity & Responsible AI Use

This template is built to be used *with* AI assistance while keeping your work
academically honest and defensible. The guiding idea is simple:

> **AI is an assistant. You are the author.** You remain fully responsible and
> accountable for every claim, citation, figure, and line of code you submit —
> regardless of which tool helped produce it.

> ⚠️ **This document is guidance, not policy.** The binding rules for any
> submission come from your course and the official Hochschule der Medien
> examination regulations (Prüfungsordnung) and your examiner's instructions.
> When this guidance and an official rule disagree, the official rule wins. If
> in doubt, ask your supervisor *before* submitting.

## Acceptable vs. risky uses

| Generally acceptable (with disclosure) | Risky or not acceptable |
| --- | --- |
| Brainstorming and structuring ideas | Presenting AI-generated text as your own without disclosure |
| Rephrasing **your own** drafts for clarity | Inventing facts, data, or results |
| Grammar, spelling, and style fixes | Citing sources you have not read and verified |
| Scaffolding example code you then read and test | Trusting AI-produced citations or quotes verbatim |
| Summarizing sources you have already read | Submitting reasoning/proofs you cannot explain yourself |
| Explaining unfamiliar concepts as a starting point | Pasting confidential, personal, or unpublished third-party data into a tool |

The line that matters: AI may help you *express* and *organize* understanding
you have and can defend — it must not *replace* that understanding.

## What to disclose, and how

Disclose AI tools that made a substantive contribution to the content. This
template gives you two dedicated places:

- **Paper** — fill in the declaration parameters in `paper/paper.typ`:
  - `ai-usage` — a short statement of how AI was used overall.
  - `ai-tools` — a per-tool list of `(tool, purpose, verification)` rendered as
    a table in a *Declaration on the Use of AI Tools* section.
  - `declaration` + `declaration-place` — the formal *Declaration of Authorship*.
- **Presentation** — the "Acknowledgements & AI Use" slide in
  `presentation/slides.md`.

Keep notes as you go (which tool, what for) so the declaration reflects what you
actually did rather than a guess at the end.

## How to verify AI output

Treat anything an AI produces as an unverified draft from a confident but
fallible source:

- **Facts & numbers** — check against primary sources, not the model's memory.
- **Citations** — confirm every reference exists, is real, and actually says
  what you claim. AI tools routinely fabricate plausible-looking citations.
- **Quotes** — verify wording against the original document.
- **Code** — read it, understand it, and run/test it before relying on it.
- **Reasoning** — if you cannot explain a step in your own words, do not include
  it.

## AI assistance on this repository

This repo is itself maintained with AI assistance (Claude Code). See
[`CLAUDE.md`](CLAUDE.md) for how that assistance is expected to stay disclosable
and reviewable, so contributions can flow into the declarations above.
