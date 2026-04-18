---
name: md-craft
description: Craft beautiful, professional markdown files — READMEs, PR templates, CONTRIBUTING, CHANGELOG, and general project docs — that match the project's existing tone and aesthetic. Use this skill whenever the user wants to write, generate, update, rewrite, polish, or "make better" any markdown file in a repo, even if they don't say "use md-craft." Trigger on phrases like "write a readme", "draft a PR template", "update the changelog", "fix my contributing guide", "my readme sucks", "generate docs for this project", or any request where the deliverable is a .md file that represents or describes a project. Also trigger when the user pastes an existing markdown file and asks to improve, clean up, or modernize it. The skill always gathers project context first (CLAUDE.md, package manifests, docs/, recent git log), always asks the user for style/tone preferences before writing, and always shows a plan/diff before touching any file.
---

# md-craft

A skill for writing and updating project markdown files (READMEs, PR templates, CONTRIBUTING, CHANGELOG, docs) that actually look like they belong to the project they're in.

## Core philosophy

Most AI-generated markdown reads the same way: a generic badge row, a robotic "Features" bullet list, an "Installation" section written like a textbook, and an "MIT License" footer. It's instantly recognizable and instantly forgettable.

The goal of this skill is the opposite: markdown that reads like the maintainer wrote it on a good day. That means:

1. **The project decides the vibe, not the skill.** A minimal Vercel-style codebase gets a minimal README. A playful side project with a mascot gets personality. A serious enterprise repo gets dense, precise docs. Match the existing tone, don't overwrite it.
2. **Context before keystrokes.** Never write a README without reading what the project actually is. Never update a CHANGELOG without looking at recent commits. Never draft a PR template without understanding what the team actually reviews.
3. **User intent gates everything.** Ask for style/tone before writing. Show a plan before writing. Only write after approval.

## README quality bar

A generated README is only done when all three of these are true. Measure against every draft before showing it to the user.

1. **10-second scan.** A reader skimming the top of the file (hero + first section) should understand what the project is, who it's for, and whether it's alive. This means the hero needs a concrete tagline (not "a revolutionary tool for X"), and the first section has to commit to a point. If someone reads the first screenful and still doesn't know what the project does, the draft fails.

2. **2-minute local run.** From landing on the README to a working dev loop: 2 minutes max. This means the install section is minimal prose around real commands, prerequisites are stated plainly (exact versions when they matter), and the quick-start example is the smallest thing that works. No "then configure your environment variables" without saying which ones.

3. **First-paragraph audience filter.** The first paragraph of prose should make it obvious whether this project is for the reader. A library for internal Anthropic tooling says so. A side project says so. A production-grade tool says so. Readers shouldn't have to dig to find out they're in the wrong place.

If a draft fails any of these, fix it before showing the user. Don't ship a README that looks polished but doesn't pass these tests.

## When this skill runs

Any request that ends with a markdown file as the deliverable and isn't purely a conversational question. Examples:

- "Write a README for this project"
- "This README is messy, clean it up"
- "Set up a PR template for the team"
- "Draft a CONTRIBUTING.md"
- "Add a changelog entry for v1.2.0"
- "The docs folder is a mess, help me restructure"
- "Make this readme look like [project X]'s"

If the user just asks a question about markdown syntax or wants to discuss what should go in a README without actually producing one, skip the skill and answer normally.

## The workflow

Follow these four phases in order. Don't skip phases — each one exists because the phase before it doesn't produce enough signal on its own.

### Phase 1: Gather project context

Before asking the user anything, read what's available. This makes the style question in Phase 2 much more productive because you can say "I see this is a Next.js library with a minimal vibe — should I match that?" instead of asking cold.

Read, in order of priority, whichever exist:

1. **CLAUDE.md** (or `.claude/CLAUDE.md`, `AGENTS.md`) — the single highest-signal file. Often contains project description, architecture, conventions, and tone hints.
2. **Existing target file** — if updating a README, read the current README. Same for CHANGELOG, CONTRIBUTING, PR templates. The existing voice is the voice to match.
3. **Package manifests** — `package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`. Pull name, description, version, dependencies, scripts.
4. **Docs folder** — skim `docs/`, `ARCHITECTURE.md`, `DESIGN.md` if they exist. Don't read everything; look for structure and tone.
5. **Config files** — `tsconfig.json`, `next.config.js`, `Dockerfile`, CI configs. Tells you the actual stack, not just the claimed stack.
6. **Recent git log** — run `git log --oneline -30` (or `-50` for a CHANGELOG task). Pulls commit message style, recent features, and whether the team uses conventional commits.
7. **Top-level file tree** — `ls` or equivalent. Tells you if it's a monorepo, what the entry points are, whether there's a `public/`, `examples/`, etc.

Keep this phase fast. Don't read every file in `src/`. You're gathering signal, not auditing the codebase.

Produce an internal context summary (don't show it to the user verbatim unless they ask) covering:

- What the project is (one sentence)
- Stack / language / framework
- Apparent tone (minimal / playful / formal / technical-dense / startup-marketing / etc.)
- Existing markdown conventions (emoji usage, heading depth, badge style, example density)
- Anything unusual (monorepo, custom CLI, unusual license, branded naming)

### Phase 2: Show style options with previews, then ask

Always ask. But don't ask cold. Based on Phase 1, pick 2-3 style directions that would actually work for this project and show a tiny preview of each so the user can feel the difference before committing. Asking without previews is the difference between "pick a color" and "pick from these swatches."

For READMEs, there are two primary style presets. See `references/readme.md` for full specs and section templates.

**Modern** — clean structure, clear visual hierarchy, good for libraries, tools, and products where readers want to scan and get working fast. Think shadcn/ui, Radix, Drizzle, tRPC. Sections have earned purpose. Slight polish without decoration.

**Narrative** — story-driven prose, personality-forward, good for opinionated tools, side projects with a point of view, and projects where the "why" matters as much as the "what." Think Pieter Levels' projects, sindresorhus essays-in-READMEs, tools that exist because the author had a specific complaint with the status quo.

These are starting points, not cages. A Modern README can have a narrative opener; a Narrative README can have a clean stack table. Use the preset to set the center of gravity, then adapt.

**How to present options:**

Show a short preview (roughly 6-10 lines each) of what the hero + first section would look like in each style, for this specific project. Previews must be written using the project's actual details, not generic placeholders. Follow with a one-line question.

Example presentation:

> Based on what I see in CLAUDE.md, either of these would work. Short previews below so you can feel the difference:
>
> **Option A — Modern**
> ```md
> # drift
>
> Typed environment variable loader for Node, 0 dependencies.
>
> ```bash
> npm install drift
> ```
>
> ## Why
> Most env loaders either do too much (secrets, rotation, multi-source merging) or too little (process.env as-is). Drift does one thing: typed vars with defaults, validated at load.
> ```
>
> **Option B — Narrative**
> ```md
> # drift
>
> I got tired of writing `process.env.PORT ? parseInt(process.env.PORT) : 3000` on every project. So I wrote drift.
>
> It's 400 lines of TypeScript and it has one job: give you typed environment variables with sensible defaults, and fail loud at startup if something required is missing.
> ```
>
> Which one lands closer? Or mix and match?

Wait for the answer. If the user says "just do it, you decide," proceed with whichever preset the project most suggests, and say which one you picked and why.

For non-README files (PR template, CONTRIBUTING, CHANGELOG, docs), skip the preview-based picker. Those files don't have the same style fork — see their reference files for the archetypes that matter.

### Phase 3: Show the plan before writing

Never go from "gathered context" straight to "wrote the file." Show a plan that the user can correct cheaply.

**For new files**, show the section outline plus a one-line note for each section saying what it will contain. Example:

```
Plan for README.md:

1. Hero        — project name, one-line tagline, install command
2. Why         — two short paragraphs on what problem this solves
3. Quick start — 3-step code block (install, configure, run)
4. API         — table of the 4 main exports with link to docs/
5. Examples    — link to examples/ folder, one inline snippet
6. Contributing — link to CONTRIBUTING.md
7. License     — MIT, one line

Roughly matching the current file's structure but adding Quick start and tightening the API section. Sound right?
```

**For updates to existing files**, show a diff-style plan: what you'll keep, what you'll change, what you'll remove. Example:

```
Plan for updating README.md:

KEEP:
  - Hero section (works well)
  - Install instructions
  - License footer

REWRITE:
  - "Features" bullet list → replace with a short paragraph + code example (the bullets are generic)
  - API reference → move to docs/ and link, README is 300 lines today

ADD:
  - Quick start section after Install
  - Badges row (build, npm version, license) — you mentioned wanting these

REMOVE:
  - "Motivation" section (redundant with Why)
  - Contributor avatars block (stale, 3 of 5 links are 404)

Want me to proceed, or adjust anything?
```

Wait for confirmation. Accept corrections. Don't skip this step even for small files — small files are where over-eager changes hurt most.

### Phase 4: Write the file

Once the plan is approved, write the file. Follow these principles:

**Structure**

- Use the sections you agreed to. Don't sneak in extras.
- Lead with whatever the reader needs most. For a library, that's usually an install command and a 5-line usage example. For a CLI, that's a GIF or a command example. For a CONTRIBUTING guide, that's the dev setup.
- If the project is small, the file should be small. A 200-line README for a 300-line utility is noise.

**Voice**

- Match the tone you identified in Phase 1 and confirmed in Phase 2.
- Don't invent marketing copy. If the project is described as "a small JSON diff tool" in CLAUDE.md, don't call it "the next generation of data transformation infrastructure."
- Don't use em dashes (`—` or `--`). Use commas, periods, or parentheses instead. This is a hard rule for this skill.
- Avoid AI-slop phrasing: "seamlessly", "in the ever-evolving landscape", "revolutionize", "unlock", "leverage", "robust", "comprehensive solution". Write like a tired engineer describing their own project.

**Formatting**

- Use fenced code blocks with language tags (```ts, ```bash, ```py).
- Keep headings shallow. `##` for top-level sections, `###` for subsections, avoid `####` unless the section is genuinely deep.
- Tables are good for API references, feature comparisons, and config options. Don't force a table where a bullet list is clearer.
- Badges are optional. If the project has no existing badges and isn't open-source-facing, skip them. If you use them, use shields.io and keep them to one row.
- Emojis: use what the project already uses. If the existing file has no emojis, don't add them. If it uses a few as section anchors, match the pattern.

**File-type specifics**

See `references/` for per-file guidance:

- `references/readme.md` — README structure patterns, common sections, examples
- `references/pr-template.md` — PR template patterns for different team sizes and workflows
- `references/contributing.md` — CONTRIBUTING.md patterns
- `references/changelog.md` — CHANGELOG conventions (Keep a Changelog, conventional commits, release-drift)
- `references/docs.md` — docs/ folder structure and tone

Read the relevant reference file before writing. Don't try to remember patterns from memory — the references have concrete examples.

## After writing

- Show the file to the user. Don't write it and disappear.
- If the file is long (>150 lines), offer to walk through specific sections.
- Ask: "Anything you want to change?" Then iterate. Don't treat the first draft as final.

## What this skill does not do

- Generate fake content. If you don't know the install command, ask — don't make one up.
- Add sections the user didn't approve. No sneaking in a "Star History" badge because it "looks good."
- Restructure docs/ without explicit permission. You can suggest it; don't do it.
- Write the full CHANGELOG from scratch by reading every commit in history. For CHANGELOG work, scope to a version range and ask.

## Quick escape hatches

- User says "just write it, don't ask me": skip Phase 2 and Phase 3, but still do Phase 1. Tell them which direction you picked.
- User pastes an existing file with "improve this": Phase 1 is just reading the file and its context. Phase 2 becomes "what specifically bothers you about it?" Phase 3 is a diff plan.
- User asks for something tiny ("add a license section"): compress all four phases into one message. Still ask once before writing if there's any ambiguity.
