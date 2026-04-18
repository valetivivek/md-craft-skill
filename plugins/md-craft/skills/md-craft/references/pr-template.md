# PR template patterns

Reference for writing `.github/pull_request_template.md` files. Read this when the user's task involves a PR template.

## The core question

Before writing, figure out what the team actually reviews. PR templates that ask for things nobody fills out are worse than no template. Signals from context:

- **Team size** (from git log author count): solo → minimal template, small team → structured, large org → detailed with required sections.
- **Commit style**: conventional commits → template can match (feat/fix/chore sections). Free-form → template should be prose-friendly.
- **Existing CI**: if tests and linting are enforced in CI, don't put "did you run tests?" in the template. Automation handles it.
- **Issue linking conventions**: if `CLAUDE.md` or contributing docs mention JIRA, Linear, or GitHub issues, surface that in the template.

Ask the user about team size and review culture if it's not obvious.

## Archetypes

### Solo / tiny team (1-3 contributors)

Keep it absolutely minimal. The template exists mostly as a reminder to write a sentence.

```md
## What
<!-- One or two sentences. What does this PR do? -->

## Why
<!-- Why now? Link to issue if relevant. -->
```

### Small team (4-15)

Structured but not bureaucratic. Focus on context for reviewers.

```md
## Summary
<!-- What does this change? -->

## Context
<!-- Why this change? Link to issue, design doc, or Slack thread. -->

## Testing
<!-- How did you verify this works? -->

## Screenshots / recordings
<!-- If UI changes, drop them here. Delete this section otherwise. -->
```

### Larger team / strict review culture

More sections, explicit checklists. Use this when the user confirms the team wants it.

```md
## Summary

## Motivation

## Changes
<!-- Bullet list of notable changes. -->

## Testing
<!-- What did you run? Any manual verification? -->

## Rollout plan
<!-- Feature-flagged? Backwards compatible? Migration needed? -->

## Checklist
- [ ] Linked to issue
- [ ] Added tests
- [ ] Updated docs
- [ ] No breaking changes (or documented in changelog)
```

### Bug-fix-specific template

For repos that make heavy use of `.github/PULL_REQUEST_TEMPLATE/` directory with multiple templates:

```md
## Bug
<!-- What was broken? -->

## Root cause
<!-- Why did it happen? -->

## Fix
<!-- What changed? -->

## Regression test
<!-- Link to the test that catches this. -->
```

## Principles

- **Every section should get filled in most of the time.** If 80% of PRs will leave a section blank, delete it.
- **Prefer prompts over checklists.** "How did you test this?" gets better answers than "- [ ] Tested."
- **Use HTML comments for instructions**, not placeholder text. Placeholder text gets submitted as-is by lazy authors.
- **Don't duplicate CI.** If CI checks lint, tests, types, don't make the author confirm each one.
- **Link templates to the repo culture.** If the team uses Linear, the template should mention Linear. Don't leave generic "link the issue" boilerplate.

## Multiple templates

GitHub supports `.github/PULL_REQUEST_TEMPLATE/` as a directory with multiple templates (feature.md, bugfix.md, chore.md). Suggest this only if the user confirms they want it — most repos are fine with one template.
