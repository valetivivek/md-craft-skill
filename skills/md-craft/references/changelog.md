# CHANGELOG patterns

Reference for writing and updating CHANGELOG.md files. Read this when the task involves a changelog.

## First: pick a convention

Three conventions dominate. Look at the existing file (if any) and commit style to pick.

### Keep a Changelog

Most common. Human-readable, opinionated, works for any project. https://keepachangelog.com

```md
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- New `--watch` flag on the CLI

### Fixed
- Memory leak when parsing large files

## [1.2.0] - 2026-04-15

### Added
- Support for YAML config files
- New `load()` overload accepting a Buffer

### Changed
- Default timeout increased from 5s to 30s

### Deprecated
- `legacyParse()` — use `parse()` instead, will be removed in 2.0.0

### Removed
### Fixed
### Security
```

Standard headings: **Added, Changed, Deprecated, Removed, Fixed, Security**. Only include the headings with entries.

### Conventional commits auto-generated

If the project uses conventional commits and a tool like `release-please`, `changesets`, or `semantic-release`, the CHANGELOG is generated. Don't hand-write it. Suggest the user run their release tool instead.

Signals this is the setup: `.changeset/` folder, `release-please` workflow file, `semantic-release` in package.json.

### Git-style / release notes

Freeform per-version notes, usually paired with GitHub Releases. Common for small projects.

```md
# Changelog

## v1.2.0

Adds YAML config support and bumps the default timeout to 30s.
Also fixes a memory leak in the large-file parser.
```

Fine for projects that value brevity over structure.

## Adding an entry

When the user asks to "add a changelog entry for X", the default action:

1. Read the existing CHANGELOG.md.
2. Identify the convention (Keep a Changelog / conventional / freeform).
3. Look at recent commits since the last version tag: `git log <last-tag>..HEAD --oneline`.
4. Categorize the change (Added / Fixed / Changed / etc.).
5. Write a user-facing description, not a commit message.
6. Place it under `## [Unreleased]` if that section exists, otherwise at the top under a new version heading.

**User-facing description vs commit message:**

- Commit: `fix: handle null response in loadConfig`
- Changelog: `Fixed a crash when the config file was empty.`

The changelog is for users who don't read code. Write like it.

## Writing for a new version release

When cutting a version (e.g., "add a 1.3.0 entry for today's release"):

1. Move everything under `## [Unreleased]` into a new `## [1.3.0] - YYYY-MM-DD` section.
2. Keep `## [Unreleased]` at the top, empty.
3. Update version links at the bottom if the project uses them.

Don't invent entries that aren't in the commit log. If the user says "release v1.3.0" and the commits since the last tag are thin, the changelog entry is thin. That's correct.

## Anti-patterns

- Copying commit messages verbatim. They're written for reviewers, not users.
- Marketing language. Changelogs are operational documents.
- Entries without dates on released versions.
- Silent breaking changes. Always flag breaking changes explicitly, usually under **Changed** with a `**BREAKING**:` prefix, or with a separate note.
