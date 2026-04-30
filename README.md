# md-craft

**You can spot AI-written markdown from a scroll away. md-craft is the opposite default.**

[License: MIT](LICENSE)
[Version](.claude-plugin/plugin.json)
[Claude Code plugin](https://docs.claude.com/en/docs/claude-code/plugins)

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

### Cursor

Cursor 2.4+ supports the open Agent Skills standard. Three install paths:

**Symlink (recommended for editing):**

```bash
git clone https://github.com/valetivivek/md-craft-skill.git ~/.cursor/md-craft-skill
mkdir -p ~/.cursor/skills
ln -s ~/.cursor/md-craft-skill/skills/md-craft ~/.cursor/skills/md-craft
```

**GitHub Remote Rule (no terminal):** Cursor Settings (Cmd+Shift+J) -> Rules -> Add Rule -> Remote Rule (Github), paste `https://github.com/valetivivek/md-craft-skill`.

**Marketplace:** if listed at [cursor.com/marketplace](https://cursor.com/marketplace), search for `md-craft` and click Install.

Restart Cursor (or reload the window) after install. Full steps, Windows instructions, update/uninstall, and verification: `[.cursor/INSTALL.md](.cursor/INSTALL.md)`.

### Codex CLI

Codex discovers skills under `~/.agents/skills/`. Clone the repo and symlink the skill:

```bash
git clone https://github.com/valetivivek/md-craft-skill.git ~/.codex/md-craft-skill
mkdir -p ~/.agents/skills
ln -s ~/.codex/md-craft-skill/skills/md-craft ~/.agents/skills/md-craft
```

Restart Codex so it picks up the new skill. Full steps, Windows instructions, and update/uninstall: `[.codex/INSTALL.md](.codex/INSTALL.md)`.

## How it works

1. **Read.** `.md-craft.json` (if present), `CLAUDE.md`, `AGENTS.md`, the existing target file, package manifests, `docs/`, config files, recent git log.
2. **Pick archetype + tone.** First run in a repo: detect the project type, show a short preview, ask once. Later runs in the same repo: skip the question, use the saved choice.
3. **Plan.** Section outline for new files, `KEEP / REWRITE / ADD / REMOVE` diff for updates. Approval gate.
4. **Write.** Matched to the archetype, your project's tone, and the quality bar below.
5. **Capture taste.** Save the choice (and any corrections you make) to `.md-craft.json` so the skill gets sharper at your style every run.

Six README archetypes built in:

- **Library** (npm/pip/cargo packages, SDKs)
- **CLI** (terminal tools, binaries)
- **App / Product** (web apps, desktop, mobile, browser extensions)
- **Framework / Heavy tool** (frameworks, ORMs, design systems)
- **Side-project / Internal** (hobby projects, internal monorepo packages)
- **Showcase** (profile READMEs, portfolios, hackathon submissions; opt-in, animated banners and stats cards)

Each archetype has its own visual element toolkit: badge rows, hero screenshots, terminal GIFs, mermaid diagrams, comparison tables, command grids, features grids, animated banners, typing SVGs, stats cards, skill icons. The skill picks the right ones for the project type.

## What it writes


| File                               | What it does                                                                                                                                                                        |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `README.md`                        | New or existing, picks one of five project-type archetypes, adapts tone to the repo                                                                                                 |
| `.md-craft.json`                   | Per-repo memory: archetype, tone, visual choices, evolving notes from your corrections                                                                                              |
| `.github/pull_request_template.md` | Sized to team: solo, small (4-15), strict review culture                                                                                                                            |
| `CONTRIBUTING.md`                  | Audience-first (drive-by, regular, internal)                                                                                                                                        |
| `CHANGELOG.md`                     | Keep a Changelog style, or freeform release notes. If the repo uses `release-please`, `changesets`, or `semantic-release`, the skill defers to those tools instead of hand-writing. |
| `docs/**/*.md`                     | Folder structures, ADRs, guides, API reference pages                                                                                                                                |


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

v1.1.0. Six README archetypes (library, cli, app, framework, side-project, showcase), four other markdown file types, per-repo taste memory in `.md-craft.json`, one opinionated quality bar. Tested by rewriting this README with itself, twice.

## Contributing

Issues and archetype suggestions welcome. If you want to propose a new archetype (e.g., "data-notebook" or "showcase"), open an issue with a short sample of what the hero and one section would look like.

## License

MIT

---

Footnote: this README, and the one before it, were written by md-craft using its own presets. The original dogfood line at the bottom was an accidental add by Claude during generation. It stayed because it was funnier than anything on purpose.