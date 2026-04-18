<div align="center">

# md-craft

**You can spot AI-written markdown from a scroll away. md-craft is the opposite default.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-black.svg)](.claude-plugin/plugin.json)
[![Claude Code plugin](https://img.shields.io/badge/Claude_Code-plugin-8A2BE2.svg)](https://docs.claude.com/en/docs/claude-code/plugins)

</div>

md-craft is a Claude Code skill for writing and updating project markdown (README, PR template, CONTRIBUTING, CHANGELOG, docs) in the voice your repo already has, not a generic AI-default one.

It is for maintainers who already have a tone in their repo and don't want it overwritten by badge rows, "Features" bullets with three-word entries, install sections explaining what npm is, or "Made with heart" footers.

## Install

### Claude Code

```bash
/plugin marketplace add valetivivek/md-craft-skill
/plugin install md-craft@md-craft-marketplace
```

Update later:

```bash
/plugin marketplace update md-craft-marketplace
```

### Codex CLI

Codex discovers skills under `~/.agents/skills/`. Clone the repo and symlink the skill:

```bash
git clone https://github.com/valetivivek/md-craft-skill.git ~/.codex/md-craft-skill
mkdir -p ~/.agents/skills
ln -s ~/.codex/md-craft-skill/skills/md-craft ~/.agents/skills/md-craft
```

Restart Codex so it picks up the new skill. Full steps, Windows instructions, and update/uninstall: [`.codex/INSTALL.md`](.codex/INSTALL.md).

## How it works

1. **Read.** `CLAUDE.md`, `AGENTS.md`, the existing target file, package manifests, `docs/`, config files, recent git log.
2. **Preview.** For READMEs, show two style previews (Modern and Narrative) written with your project's real details, then ask which fits.
3. **Plan.** Section outline for new files, `KEEP / REWRITE / ADD / REMOVE` diff for updates. Approval gate.
4. **Write.** Matched to the preset, your project's tone, and the quality bar below.

Two README presets built in: **Modern** (clean, scannable, shadcn/Vercel vibe) and **Narrative** (story-driven, opinionated, personality-forward).

## What it writes

| File | What it does |
| --- | --- |
| `README.md` | New or existing, Modern or Narrative preset, adapts to project tone |
| `.github/pull_request_template.md` | Sized to team: solo, small (4-15), strict review culture |
| `CONTRIBUTING.md` | Audience-first (drive-by, regular, internal) |
| `CHANGELOG.md` | Keep a Changelog style, or freeform release notes. If the repo uses `release-please`, `changesets`, or `semantic-release`, the skill defers to those tools instead of hand-writing. |
| `docs/**/*.md` | Folder structures, ADRs, guides, API reference pages |

## Use it for

- "Write a README for this project"
- "This README is messy, clean it up"
- "Set up a PR template for the team"
- "Draft a CONTRIBUTING.md"
- "Add a changelog entry for v1.2.0"
- "Fix my docs folder"

Does not trigger for general questions about markdown syntax.

## Quality bar

Every generated README has to pass three checks before you see it:

1. **10-second scan.** Reader understands the project from the hero plus first section.
2. **2-minute local run.** From landing on the README to a working dev loop in two minutes.
3. **First-paragraph audience filter.** Reader knows in the first paragraph whether this project is for them.

Draft fails any check, the skill fixes it before showing you. No polished-but-hollow output.

## Status

v1.0.0. Two README presets, four other markdown file types, one opinionated quality bar. Tested by rewriting this README with itself, twice.

## Contributing

Issues and style-preset suggestions welcome. If you want to propose a new preset (e.g., "data-oriented" or "showcase"), open an issue with a short sample of what it should look like at the hero level.

## License

MIT

---

<sub>Footnote: this README, and the one before it, were written by md-craft using its own presets. The original dogfood line at the bottom was an accidental add by Claude during generation. It stayed because it was funnier than anything on purpose.</sub>
