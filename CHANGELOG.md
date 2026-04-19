# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-04-18

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

[1.0.0]: https://github.com/valetivivek/md-craft-skill/releases/tag/v1.0.0
