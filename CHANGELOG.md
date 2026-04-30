# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0](https://github.com/valetivivek/md-craft-skill/releases/tag/v1.1.0) - 2026-04-30

Reshaped around project-type archetypes, added per-repo taste memory, shipped Cursor support, fixed a malformed YAML frontmatter that was preventing reliable auto-triggering.

### Added

- Six README archetypes under `skills/md-craft/references/archetypes/`: **Library**, **CLI**, **App / Product**, **Framework / Heavy tool**, **Side-project / Internal**, and **Showcase**. Each archetype ships its own visual elements toolkit (badges, hero screenshots, terminal GIFs, mermaid diagrams, command grids, features grids, comparison tables) and a mini example skeleton.
- **Showcase** archetype for visually striking READMEs (profile READMEs, portfolios, hackathon submissions). Opt-in only. Covers animated banners (capsule-render), typing SVGs (readme-typing-svg), theme-aware `<picture>` images, stats and streak cards, snake contribution graph, and skillicons.dev rows. Includes restraint guardrails ("pick 2 to 4 elements, not 12") and "creative within structure" notes for hand-rolled SVGs.
- Per-repo preferences file `.md-craft.json` that stores the chosen archetype, tone, visual element overrides, and notes distilled from in-chat corrections and post-write edits. Later runs in the same repo skip the style question.
- `skills/md-craft/references/preferences-file.md` documenting the `.md-craft.json` schema, evolution flow, and edge cases (CI mode, archetype mismatch, multi-writer repos, notes consolidation).
- New **Phase 5: Show, react, and capture taste** in the workflow. Captures user corrections back into `.md-craft.json` so the skill gets sharper at the user's style every run. Always preserves the Phase 3 plan/diff approval gate.
- Cursor IDE support: `.cursor-plugin/plugin.json`, `.cursor-plugin/marketplace.json`, `.cursor/INSTALL.md`, and a Cursor section in the repo README. Three install paths documented: symlink into `~/.cursor/skills/`, GitHub Remote Rule import via Settings, and Cursor Marketplace once approved.
- Tone axis separate from archetype: `modern-clean`, `narrative-personal`, `dry-operational`. Picked per-archetype by default with override.

### Changed

- `skills/md-craft/SKILL.md` description rewritten to be action-led and trigger-keyword dense. New triggers for showcase ("animated readme", "make it look cool", "make my profile readme", "showcase readme").
- `skills/md-craft/references/readme.md` restructured around an archetype router table and a tone axis. The Modern / Narrative two-preset fork has been removed; tone is now a per-archetype default with override. Visual elements matrix added showing which elements each archetype recommends, optional, or skips.
- Phase 1 of the workflow now reads `.md-craft.json` first, before any user message about style. Phase 2 branches on whether the file exists: silent honor of saved settings vs. archetype detection plus preview. Phase 4 honors `notes[]` from the prefs file as additional writing rules.
- Repo `README.md`, `.claude-plugin/plugin.json`, and `.claude-plugin/marketplace.json` updated to reflect six archetypes and version 1.1.0.

### Fixed

- `skills/md-craft/SKILL.md` YAML frontmatter was malformed: missing closing `---`, and `## name:` written as a markdown heading instead of `name:` as a YAML field. Cursor and the Agent Skills loader silently reject skills without valid frontmatter, which was the most likely cause of past auto-triggering misses. Frontmatter now contains the two required fields (`name`, `description`) and is properly closed.
- All em dashes removed from the skill's reference docs. The "no em dashes" rule already existed for output markdown the skill writes for users; the skill's internal prose now follows the same rule.

### Removed

- `.cursor/` blanket entry from `.gitignore`. The `.cursor/INSTALL.md` distribution doc now ships with the repo, mirroring the existing `.codex/` pattern. Per-developer Cursor workspace state can be ignored on an individual basis instead of repo-wide.

## [1.0.0](https://github.com/valetivivek/md-craft-skill/releases/tag/v1.0.0) - 2026-04-18

Initial public release.

### Added

- `md-craft` skill for writing and updating project markdown (README, PR template, CONTRIBUTING, CHANGELOG, docs) in the voice the repo already has.
- Two README presets: **Modern** (clean, scannable) and **Narrative** (story-driven, opinionated).
- Two-preview preview-then-plan workflow: the skill shows two hero-level previews written with your project's real details before writing anything.
- `KEEP / REWRITE / ADD / REMOVE` diff plan for updating existing files, with an explicit approval gate before any write.
- Reference patterns for PR templates sized to team (solo, small 4-15, strict review culture).
- Reference patterns for CONTRIBUTING files matched to audience (drive-by, regular, internal).
- Reference patterns for CHANGELOG files (Keep a Changelog, conventional-commits auto-generated, freeform release notes). Defers to `release-please`, `changesets`, or `semantic-release` when the repo uses one of them.
- Reference patterns for `docs/` folders, ADRs, guides, and API reference pages.
- Quality bar applied to every generated README: 10-second scan, 2-minute local run, first-paragraph audience filter. Drafts that fail are fixed before they reach the user.
- Claude Code plugin install path via the `md-craft-marketplace`.
- Codex CLI install path via `~/.agents/skills/`, documented in `.codex/INSTALL.md`.
- MIT license.