# docs/ patterns

Reference for writing and organizing general project documentation in a `docs/` folder. Read this when the task involves docs beyond the standard README/PR/CHANGELOG/CONTRIBUTING files.

## Common docs/ structures

Pick based on project type.

### Library with an API surface

```
docs/
├── getting-started.md
├── api/
│   ├── core.md
│   ├── helpers.md
│   └── types.md
├── guides/
│   ├── migration-from-v1.md
│   └── using-with-next.md
└── internals/
    └── architecture.md
```

### Application

```
docs/
├── setup.md
├── architecture.md
├── deployment.md
├── operations/
│   ├── monitoring.md
│   ├── backups.md
│   └── incident-response.md
└── decisions/
    ├── 001-why-postgres.md
    └── 002-auth-stack.md
```

The `decisions/` folder is an ADR (Architecture Decision Records) pattern. Useful for non-obvious choices.

### Internal tool

```
docs/
├── README.md           — landing page, who owns this, where to get help
├── runbooks/
│   ├── deploy.md
│   └── rollback.md
└── design/
    └── system-overview.md
```

## Writing individual doc pages

### Getting started pages

- Smallest working example first.
- Use headings as a TOC (readers scan, they don't read linearly).
- Link to deeper docs instead of inlining everything.

### API reference pages

- Alphabetical or logical grouping, not random.
- Each entry: signature, description, parameters table, return value, example.
- Don't duplicate JSDoc/docstrings if they're auto-generated elsewhere. Link instead.

### Guide pages

- One task per guide. "How to add a new provider" not "Everything about providers."
- Numbered steps if the order matters. Prose if it doesn't.

### Architecture pages

- Diagram early if you can. ASCII, Mermaid, or a linked image.
- Describe the top-level components in 2-3 sentences each before going deep.
- Label the tradeoffs, not just the choices. "We chose X because Y, at the cost of Z."

### ADR pages

Follow a light template:

```md
# 001: Why we chose Postgres

**Status:** Accepted
**Date:** 2026-02-14

## Context
<!-- What problem are we solving? -->

## Decision
<!-- What did we pick? -->

## Consequences
<!-- What are we trading off? What does this make easier/harder? -->
```

## Principles

- **Docs rot faster than code.** Write the minimum necessary. Every page is a page someone has to maintain.
- **Link out to code for examples.** Don't paste 80 lines of implementation. Link to the file and line.
- **Don't nest headings past `###`.** If you need to, split into another page.
- **Each page has one job.** If a page has four unrelated sections, it's four pages pretending to be one.

## When the user asks to "restructure the docs folder"

Do not start moving files. The existing structure probably has reasons behind it (links from blog posts, CI paths, embedded in error messages). Propose a plan first. Ask what can change and what must stay.
