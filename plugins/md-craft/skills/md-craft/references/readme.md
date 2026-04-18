# README patterns

Reference for writing README.md files. Read this when the user's task involves a README.

## The two presets

md-craft offers two README style presets. Pick one as the center of gravity, then adapt.

### Modern

Clean structure, clear visual hierarchy, skimmable. Readers can scan the file in 10 seconds and know what's going on. Good for libraries, tools, products, SDKs.

Reference shape:

```md
# <project>

<one-line tagline, 8-14 words, concrete>

```bash
<install command>
```

## <Why / What it is>
<2 short paragraphs explaining the problem and approach>

## Quick start
<smallest working example in a code block>

## <API or Usage or Features>
<table, short list, or a few labeled examples>

## <Stack / Configuration / Examples>
<as needed>

## Status
<one short paragraph: what works, what doesn't, who it's for>

## License
<one line>
```

Tone: factual, slightly warm. Earned word choices, no marketing verbs.

### Narrative

Story-driven prose with personality. The "why" matters as much as the "what." Good for opinionated tools, side projects, and projects that exist because the author had a specific beef with the status quo.

Reference shape:

```md
# <project>

<one-line tagline or opening line, can be a sentence fragment>

<2-4 paragraph opener telling the reader why this exists and what it does, in plain prose>

## How it works
<prose + one or two code blocks, written conversationally>

## Running it
<install + quick start, can share a section>

## <Design notes / Tradeoffs / Things it won't do>
<the honest stuff>

## Status
<real talk about where it is>

## License
```

Tone: conversational, specific, willing to name what the project isn't. Short sentences. First person is fine.

## The hero is 80% of the README

Most READMEs fail at the top. A reader decides within 5 seconds whether to keep reading. The hero (name, tagline, optional install block) needs to do three jobs at once:

1. Say what the project is concretely
2. Hint at who it's for
3. Let them start trying it

### Good hero examples

**Modern, library:**
```md
# drift

Typed environment variable loader for Node, 0 dependencies.

```bash
npm install drift
```
```

**Modern, tool:**
```md
# vercel-cli

Deploy to Vercel from your terminal. Previews, production, rollbacks, logs.

```bash
npm i -g vercel
```
```

**Narrative, opinionated library:**
```md
# drift

I got tired of writing `process.env.PORT ? parseInt(process.env.PORT) : 3000`. So I wrote drift. It's a 400-line TypeScript file that gives you typed env vars with defaults and fails loud at boot if something required is missing.
```

**Narrative, side project:**
```md
# comite

A reading-first manga platform. I wanted a place to read that wasn't trying to sell me NFTs, push notifications, or an algorithmic feed. This is that.
```

### Bad hero patterns (reject these)

- **Marketing fluff:** "The next-generation platform for X" → reader learned nothing
- **Feature dump in the tagline:** "Fast, reliable, scalable, enterprise-ready logging library" → reader learned nothing
- **Decorative emoji banners:** `# 🚀📚✨ My Project ✨📚🚀` → noise
- **Vague tagline:** "A tool for developers" → obvious, reader leaves
- **Corporate vertical-speak:** "Streamline your workflow with comprehensive tooling" → reader flees

### The concrete-tagline test

Write the tagline, then ask: could this tagline apply to 100 other projects? If yes, rewrite it.

- ❌ "A modern build tool" (could be anything)
- ✅ "Next-gen frontend tooling, built on esbuild and written in Go" (concrete, names the thing)
- ❌ "A powerful data library"
- ✅ "Read, transform, and write CSV files without loading them into memory"

## Section library (use as needed)

Not every README needs every section. Pick based on project type and style preset.

### Hero

See above. Always required.

### Why / What it is / Motivation

Required for Narrative. Strongly recommended for Modern (helps the 10-second scan). Two paragraphs max. Describe the problem, then how this solves it.

### Install

Single code block, one command per package manager if it ships to multiple. Don't wrap with explanation prose unless there's a non-obvious prerequisite.

### Quick start / Usage

Smallest possible working example. If it fits in 10 lines, put it in 10 lines. Show the import, the main call, and the result as a comment. This is where you earn the "2-minute local run" bar.

### API

Libraries only. Table format works well for small APIs (<=10 exports). For deep APIs, link out.

| Export | Description |
| --- | --- |
| `load(schema)` | Loads and validates env vars against a schema |
| `loadSafe(schema)` | Same, but returns `{ ok, data, error }` instead of throwing |

### Configuration

Tools and apps. Show a minimal example. Link to a full reference.

### Stack

Useful when the reader wants to know what they'd be pulling in. Compact, ideally one line or a short list.

### Examples

If there's an `examples/` folder, point to it. Optionally a one-line summary of what each example does.

### Status

Almost always include this. One paragraph. Name:
- What works
- What doesn't yet
- Who this is for right now

This section is what passes the "first-paragraph audience filter." Don't hide it at the bottom if the project is early.

### License

One line at the bottom. `MIT (c) Author Name` or similar.

## Anti-patterns to strip

When updating an existing messy README, actively remove:

- Generic "Features" bullet lists with 3-word entries ("Fast", "Beautiful"). Either write a paragraph or drop the section.
- Fake badges (stars, forks, version 0.1.0 with "stable" badge).
- "Installation" sections that explain what npm is.
- "Contributors" ASCII portraits on projects with 1 contributor.
- "Made with heart" footers unless the rest of the file has matching personality.
- "Acknowledgments" sections thanking coffee, open source, the sun.
- Long AI-written "About" paragraphs with "seamlessly", "comprehensive", "next-generation", "revolutionary", "empower", "unlock", "leverage".
- Prerequisites lists that don't actually list the prerequisites. ("Node.js installed" is useless. "Node 20+, pnpm 9+, Postgres 16 running on :5432" is useful.)

## Tone calibration examples

Before writing a hero paragraph, pick a tone that matches the project. Three archetypes:

**Dry / systems** (infra, protocols, runtime code):
> A content-addressable append-only log. Durable, single-writer, no dependencies.

**Modern / SaaS-adjacent** (developer tools, libraries):
> The typed env var loader you meant to write. 0 deps, works anywhere Node runs.

**Narrative / opinionated** (side projects, specific tools):
> Every env var loader I tried either did too much or too little. This one does exactly what I want, which may or may not be what you want. Read on.

If the CLAUDE.md or repo suggests one of these, match it. If nothing suggests anything, ask.

## Deciding between Modern and Narrative

Not sure which preset fits? Ask these:

- **Does the project have a clear "I built this because..." story?** Narrative.
- **Is it a library or tool where readers mostly want to install and use?** Modern.
- **Will most readers be strangers finding it via Google?** Modern (scannable wins).
- **Will most readers be people who already heard about it from a blog post or tweet?** Narrative (they're already curious).
- **Is there a strong author voice in CLAUDE.md or existing docs?** Narrative.
- **Is the author anonymous or a team?** Modern.

When in genuine doubt, Modern is the safer default.
