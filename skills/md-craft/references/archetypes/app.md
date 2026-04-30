# App / Product archetype

For web apps, desktop apps, mobile apps, and end-user products. The reader is somebody who wants to see what the product looks like, decide if it's for them, and either try the hosted version or run it locally.

## When to pick this archetype

- The main user surface is a UI: web app, desktop app, mobile app, browser extension.
- The repo is primarily a deployable product, not a published library.
- A picture or screenshot will tell more than three paragraphs of prose.

If the repo is an open-source app *and* a package other developers consume programmatically, this is still the right archetype as long as the UI is the primary surface.

## Default tone

Modern-clean with mild product polish. Friendly first paragraph, then dense and practical. Sentence-case headings. Don't write marketing copy; describe what the app does and who built it.

Allow narrative tone if the project is a personal app with a strong "I built this because..." story. Otherwise stay neutral.

## Visual elements toolkit

This is the most visually rich archetype. Use generously, but earn each one.

- **Centered hero block**: HTML-wrapped (`<div align="center">`) with logo or wordmark, tagline, and 1 to 3 CTA links (Live demo, Docs, Discord, App Store).
- **Hero screenshot**: one image right under the hero, full width. Light or dark theme, whichever matches the app's identity. Compress aggressively. Alt text required.
- **Optional second screenshot**: only if the app has two distinct surfaces worth showing (e.g. mobile + desktop).
- **Features grid**: 3 columns, 6 rows max. Each cell is a bold title + 1 sentence. Use a markdown table or HTML grid. No 3-word bullet lists.
- **Tech stack badges or list**: short, factual. "Built with: Next.js, Postgres, Tailwind, Stripe."
- **Run-locally section**: stays compact. Most readers won't run it locally; the section is for the few who will.
- **Optional video / animated GIF**: if the product has motion that matters (canvas, drag-and-drop, real-time), one short embedded clip.
- **Sponsors / built-with-love footer**: only if the project actually has sponsors or a community already.

## Section structure

```md
<centered hero: logo, tagline, CTAs>

<hero screenshot>

## What it is
<one to two paragraphs: what the app does, who it's for, where it runs>

## Features
<grid or short list>

## Try it
<live demo link, app store, etc.>

## Run locally
<install, env, run, in 4 to 6 commands max>

## Tech stack
<one short line or list>

## Roadmap or Status
<optional: what's done, what's next>

## License
<one line>
```

## Mini example skeleton

```md
<div align="center">

<img src="docs/logo.svg" width="120" alt="Tilde logo" />

# Tilde

A lightweight, local-first note app for Markdown.

[Live demo](https://tilde.app)  ·  [Docs](https://docs.tilde.app)  ·  [Discord](https://discord.gg/tilde)

</div>

![Tilde screenshot](docs/hero.png)

## What it is

Tilde is a Markdown notes app that stores everything in plain `.md` files on your machine. No accounts, no cloud, no lock-in. Sync is opt-in via Git or iCloud.

It's for writers, engineers, and researchers who want a fast editor without surrendering their notes to a vendor.

## Features

| | |
| --- | --- |
| **Local-first** Plain `.md` files in a folder you choose. | **Fast** Opens 50k notes in under 200ms. |
| **Git sync** Optional, encrypted, your-own-remote. | **Vim mode** Real Vim, not "Vim-like." |
| **Plugin API** TypeScript, hot-reload in dev. | **Cross-platform** macOS, Windows, Linux. |

## Try it

Hosted demo at [tilde.app/demo](https://tilde.app/demo). Or download the desktop app from [tilde.app/download](https://tilde.app/download).

## Run locally

```bash
git clone https://github.com/acme/tilde
cd tilde
pnpm install
pnpm dev
```

Requires Node 20+ and pnpm 9+.

## Tech stack

Tauri, React, Tiptap, SQLite (FTS5), Tailwind.

## Status

Public beta. Stable on macOS, mostly stable on Windows, Linux is community-maintained. See [Roadmap](https://github.com/acme/tilde/projects/1).

## License

AGPL-3.0

```

## Anti-patterns specific to apps

- **No screenshot**. An app README without a visual is missing its single best 3-second sales pitch.
- **A screenshot of the login page**. Show what the app actually does, not its empty state.
- **Stale screenshots** that don't match the current UI. Date them or regenerate when shipping a redesign.
- **A 30-feature feature grid**. Pick 6. The rest go in the docs.
- **Pretending it's open source** when it isn't (source-available, BUSL, "non-commercial only"). Be explicit in the License section.
- **"Coming soon" sections** with empty checklists. Either ship it or omit the section.
```

