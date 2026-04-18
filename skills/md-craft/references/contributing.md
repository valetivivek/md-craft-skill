# CONTRIBUTING.md patterns

Reference for writing CONTRIBUTING.md files. Read this when the task involves a contributing guide.

## Core question

Who's the audience? CONTRIBUTING.md serves three different groups, and writing for the wrong one makes the file useless:

1. **External drive-by contributors** — they need: how to set up, what to avoid, how PRs work here.
2. **Regular external contributors** — they need: coding conventions, release process, where to ask questions.
3. **Internal team members** — they need: onboarding steps, where the hidden knowledge lives, who to ping.

Most open-source CONTRIBUTING.md files are written for group 1 but accidentally start addressing group 3. Pick one primary audience and make the file good for them. Link or link-mention the others.

## Standard structure

```md
# Contributing to <project>

Thanks for your interest. A few notes before you dig in.

## Getting started
<!-- Clone, install, run tests. The smallest path to a working dev loop. -->

## Development workflow
<!-- How to run the project locally while you work on it. -->

## Project structure
<!-- Top-level folder tour, one line each. Optional. -->

## Making changes
<!-- How to branch, how to commit, how to open a PR. -->

## Testing
<!-- What tests exist, how to run them, what's required for a PR to merge. -->

## Style
<!-- Formatter? Linter? Type checker? Just link to config if it's enforced. -->

## Submitting a PR
<!-- Where to open it, what info to include, what the review cycle looks like. -->

## Getting help
<!-- Discord, Discussions, issue tracker, whatever is real. -->
```

## Principles

- **Every step must actually work.** The fastest way to lose a contributor is a broken "clone and run" on page one. Verify commands before finalizing.
- **Don't explain Git.** If you feel like you need to, the audience is wrong.
- **Be honest about what's rough.** "The frontend tests are flaky, rerun them" is more useful than pretending everything is smooth.
- **Link don't explain.** If there's an architecture doc, link it. Don't recap it here.

## Tone

CONTRIBUTING.md can carry personality when the project already has it. A warm opening paragraph ("thanks for being here, here's how we work") is fine for community-driven projects. Skip it for corporate-owned OSS where the tone is operational.

## What to leave out

- Code of conduct — link to CODE_OF_CONDUCT.md if separate.
- License details — link to LICENSE.
- Long philosophy essays about software quality. Nobody reads these.
- Exhaustive commit message grammars unless the project actually enforces one. If you have commitlint, say "we use conventional commits, see commitlint config" and stop.
