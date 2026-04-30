<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12,20,24&height=200&section=header&text=md-craft&fontSize=80&fontAlignY=38&fontColor=ffffff&animation=fadeIn" alt="md-craft" />

<p><b>A markdown skill for AI agents that writes like the maintainer, not the model.</b></p>

<p>
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&size=22&duration=3500&pause=600&color=8A2BE2&center=true&vCenter=true&width=620&lines=Six+project+archetypes.;Per-repo+taste+memory.;Plans+before+it+writes." alt="typing" />
</p>

<p>
  <a href="#install">Install</a> &nbsp;·&nbsp;
  <a href="#what-it-does">What it does</a> &nbsp;·&nbsp;
  <a href="#archetypes">Archetypes</a> &nbsp;·&nbsp;
  <a href="#how-it-works">How it works</a> &nbsp;·&nbsp;
  <a href="#quality-bar">Quality bar</a>
</p>

<p>
  <a href="https://docs.claude.com/en/docs/claude-code/plugins"><img src="https://img.shields.io/badge/Claude%20Code-plugin-d97757?style=flat-square" alt="Claude Code plugin" /></a>
  <a href=".cursor/INSTALL.md"><img src="https://img.shields.io/badge/Cursor-skill-000000?style=flat-square" alt="Cursor skill" /></a>
  <a href=".codex/INSTALL.md"><img src="https://img.shields.io/badge/Codex%20CLI-skill-444444?style=flat-square" alt="Codex CLI skill" /></a>
  <a href=".claude-plugin/plugin.json"><img src="https://img.shields.io/badge/version-1.1.0-8A2BE2?style=flat-square" alt="version" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/valetivivek/md-craft-skill?style=flat-square&color=blue" alt="license" /></a>
  <a href="https://github.com/valetivivek/md-craft-skill/stargazers"><img src="https://img.shields.io/github/stars/valetivivek/md-craft-skill?style=flat-square&color=yellow" alt="stars" /></a>
</p>

</div>

## What it does

You can spot AI-written markdown from a scroll away: generic badge row, "Features" bullets with three-word entries, install section explaining what `npm` is, "MIT License" footer. md-craft is the opposite default.

It writes and updates project markdown (README, PR template, CONTRIBUTING, CHANGELOG, docs) in the voice your repo already has, not a generic AI-default one. It is for maintainers who already have a tone and don't want it overwritten.

Works in **Claude Code**, **Cursor 2.4+**, and **Codex CLI**. The skill is the same in all three; only the install path differs.

## 📦 Install

### <img src="https://cdn.simpleicons.org/claude/D97757" height="18" alt="" /> &nbsp;Claude Code

```bash
/plugin marketplace add valetivivek/md-craft-skill
/plugin install md-craft@md-craft-marketplace
```

Update later:

```bash
/plugin marketplace update md-craft-marketplace
```

### <img src="https://cdn.simpleicons.org/cursor/000000" height="18" alt="" /> &nbsp;Cursor

Cursor 2.4+ supports the open Agent Skills standard. Three install paths:

**Symlink (recommended for editing):**

```bash
git clone https://github.com/valetivivek/md-craft-skill.git ~/.cursor/md-craft-skill
mkdir -p ~/.cursor/skills
ln -s ~/.cursor/md-craft-skill/skills/md-craft ~/.cursor/skills/md-craft
```

**GitHub Remote Rule (no terminal):** Cursor Settings (Cmd+Shift+J) → Rules → Add Rule → Remote Rule (Github), paste `https://github.com/valetivivek/md-craft-skill`.

**Marketplace:** if listed at [cursor.com/marketplace](https://cursor.com/marketplace), search for `md-craft` and click Install.

Restart Cursor (or reload the window) after install. Full steps, Windows instructions, update/uninstall, and verification: [`.cursor/INSTALL.md`](.cursor/INSTALL.md).

### <img src="https://www.google.com/s2/favicons?domain=openai.com&sz=64" height="18" alt="" /> &nbsp;Codex CLI

Codex discovers skills under `~/.agents/skills/`. Clone and symlink:

```bash
git clone https://github.com/valetivivek/md-craft-skill.git ~/.codex/md-craft-skill
mkdir -p ~/.agents/skills
ln -s ~/.codex/md-craft-skill/skills/md-craft ~/.agents/skills/md-craft
```

Restart Codex so it picks up the new skill. Full steps, Windows instructions, update/uninstall: [`.codex/INSTALL.md`](.codex/INSTALL.md).

## How it works

1. **Read.** `.md-craft.json` (if present), `CLAUDE.md`, `AGENTS.md`, the existing target file, package manifests, `docs/`, config files, recent git log.
2. **Pick archetype + tone.** First run in a repo: detect the project type, show a short preview, ask once. Later runs: skip the question, use the saved choice.
3. **Plan.** Section outline for new files, `KEEP / REWRITE / ADD / REMOVE` diff for updates. Approval gate.
4. **Write.** Matched to the archetype, your project's tone, and the quality bar.
5. **Capture taste.** Save the choice (and any corrections you make) to `.md-craft.json` so the skill gets sharper at your style every run.

## Archetypes

Six README archetypes. Each ships its own visual elements toolkit (badges, hero screenshots, terminal GIFs, mermaid diagrams, command grids, features grids, comparison tables) and a mini example skeleton. The skill picks the right one for the project.

| Archetype | One-line | When to pick |
| --- | --- | --- |
| **Library** | npm / pip / cargo packages, SDKs | Single import surface, small API, no UI |
| **CLI** | Terminal tools, binaries | `bin` field in `package.json` or `cmd/` Go folder |
| **App / Product** | Web apps, desktop, mobile, browser extensions | Has a UI, deployed for end users, screenshot-worthy |
| **Framework / Heavy tool** | Frameworks, ORMs, design systems | Multiple core concepts, separate docs site, comparison-shopped |
| **Side-project / Internal** | Hobby projects, internal monorepo packages | One author, hobby vibe, or internal-only ownership |
| **Showcase** | Profile READMEs, portfolios, hackathon submissions | Animated banners, typing SVGs, stats cards. Opt-in only. |

Tone is a separate axis: `modern-clean`, `narrative-personal`, `dry-operational`. Picked per-archetype by default, override anytime.

## What it writes

| File | What it does |
| --- | --- |
| `README.md` | New or existing, picks one of six project-type archetypes, adapts tone to the repo |
| `.md-craft.json` | Per-repo memory: archetype, tone, visual choices, evolving notes from your corrections |
| `.github/pull_request_template.md` | Sized to team: solo, small (4-15), strict review culture |
| `CONTRIBUTING.md` | Audience-first (drive-by, regular, internal) |
| `CHANGELOG.md` | Keep a Changelog style, or freeform release notes. Defers to `release-please`, `changesets`, or `semantic-release` if the repo uses them. |
| `docs/**/*.md` | Folder structures, ADRs, guides, API reference pages |

## Use it for

- "Write a README for this project"
- "This README is messy, clean it up"
- "Set up a PR template for the team"
- "Draft a CONTRIBUTING.md"
- "Add a changelog entry for v1.2.0"
- "Make my profile readme look cool"

Does not trigger for general questions about markdown syntax.

## Quality bar

Every generated README has to pass three checks before you see it:

1. **10-second scan.** Reader understands the project from the hero plus first section.
2. **2-minute local run.** From landing on the README to a working dev loop in two minutes.
3. **First-paragraph audience filter.** Reader knows in the first paragraph whether this project is for them.

Draft fails any check, the skill fixes it before showing you. No polished-but-hollow output.

## Status

**v1.1.0.** Six README archetypes (library, cli, app, framework, side-project, showcase), four other markdown file types, per-repo taste memory in `.md-craft.json`, one opinionated quality bar. Tested by rewriting this README with itself, three times now.

## Contributing

Issues and archetype suggestions welcome. To propose a new archetype (e.g., "data-notebook," "research-paper," "game"), open an issue with a short sample of what the hero and one section would look like. See [`CONTRIBUTING.md`](CONTRIBUTING.md).

## License

MIT. See [`LICENSE`](LICENSE).

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12,20,24&height=80&section=footer" alt="footer" />

</div>

---

Footnote: this README, and the two before it, were written by md-craft using its own presets. The original dogfood line at the bottom was an accidental add by Claude during generation. It stayed because it was funnier than anything on purpose.
