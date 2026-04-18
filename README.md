# md-craft

A Claude skill for writing and updating project markdown (README, PR templates, CONTRIBUTING, CHANGELOG, docs) that actually looks like it belongs to the project it's in.

## Why

Most AI-generated markdown reads the same way: a generic badge row, a robotic "Features" list, an install section explaining what npm is, and a "Made with ❤️" footer. You can spot it from a scroll away.

md-craft is the opposite default. It reads your project first (CLAUDE.md, package manifests, docs, recent commits), asks you which of two style presets you want with short previews, shows a plan before it writes anything, and holds every draft to three checks: a reader understands the project in 10 seconds, can run it locally in 2 minutes, and knows if it's for them in the first paragraph.

## How it works

Four-phase workflow on every markdown task:

1. **Gather context.** Reads `CLAUDE.md`, `AGENTS.md`, the existing target file, package manifests, `docs/`, config files, and recent git log.
2. **Style preview + ask.** Shows 2-3 short previews written with the project's actual details, then asks you to pick. No cold "what vibe do you want" questions.
3. **Plan.** Section outline for new files, `KEEP / REWRITE / ADD / REMOVE` diff plan for updates. Approval required before writing.
4. **Write.** Matched to the preset, the project's tone, and the quality bar.

Two README presets built in: **Modern** (clean, scannable, shadcn/Vercel vibe) and **Narrative** (story-driven, opinionated, personality-forward).

## Install

md-craft ships as a Claude Code plugin via this marketplace.

```bash
# Add the marketplace
/plugin marketplace add valetivivek/md-craft-skill

# Install the plugin
/plugin install md-craft@md-craft-marketplace
```

To update later:

```bash
/plugin marketplace update md-craft-marketplace
```

Once installed, the skill triggers automatically on markdown requests. It does nothing until you confirm the style and plan, so you stay in control.

## What triggers it

Any request where the deliverable is a markdown file. Examples:

- "Write a README for this project"
- "This README is messy, clean it up"
- "Set up a PR template for the team"
- "Draft a CONTRIBUTING.md"
- "Add a changelog entry for v1.2.0"
- "Fix my docs folder"

It does not trigger for general questions about markdown syntax.

## Supported file types

| File | What it does |
| --- | --- |
| `README.md` | New or existing, Modern or Narrative preset, adaptive to project tone |
| `.github/pull_request_template.md` | Sized to team: solo, small (4-15), strict review culture |
| `CONTRIBUTING.md` | Audience-first (drive-by, regular, internal) |
| `CHANGELOG.md` | Keep a Changelog, conventional-commits auto-gen, freeform release notes |
| `docs/**/*.md` | Folder structures, ADRs, guides, API reference pages |

## Contributing

Issues and style-preset suggestions welcome. If you want to propose a new preset (e.g., "data-oriented" or "showcase"), open an issue with a short sample of what it should look like at the hero level.

## License

MIT

---

<sub>This README was written by md-craft, using its own Modern preset. Dogfooded all the way down.</sub>