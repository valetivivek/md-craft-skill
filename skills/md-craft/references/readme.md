# README patterns

Reference for writing README.md files. Read this when the user's task involves a README. After this, read the archetype-specific file under `references/archetypes/` for the chosen project type.

## Two axes: archetype and tone

A README has two design choices, picked independently:

1. **Archetype**: what *kind* of project this is. Sets structure and visual elements.
2. **Tone**: how the prose *sounds*. Sets voice and word choice.

### Archetypes (pick one)

| Archetype | When | Reference |
| --- | --- | --- |
| **Library** | npm/pip/cargo packages, SDKs, importable code | `archetypes/library.md` |
| **CLI** | Command-line tools, terminal binaries | `archetypes/cli.md` |
| **App / Product** | Web apps, desktop apps, browser extensions, products | `archetypes/app.md` |
| **Framework / Heavy tool** | Frameworks, ORMs, build tools, design systems | `archetypes/framework.md` |
| **Side-project / Internal** | Hobby projects, internal monorepo packages | `archetypes/side-project.md` |
| **Showcase** | GitHub profile READMEs, hackathon submissions, portfolios, opt-in visually striking READMEs | `archetypes/showcase.md` |

Each archetype has a default tone and a recommended visual elements toolkit. Read its file before writing.

**Showcase is opt-in only.** Don't pick it for libraries, CLIs, frameworks, apps, or internal repos, even if the user says "make it nice." Pick it only when the project genuinely is a profile README, a portfolio, a hackathon submission, or the user explicitly asks for "animated," "visually stunning," "showcase," or similar.

### Tone (pick one, or use the archetype default)

- **Modern-clean**: factual, slightly warm, no marketing verbs. Default for Library, CLI, App, Framework.
- **Narrative-personal**: story-driven, first person, willing to name what the project isn't. Default for Side-project (side-project flavor).
- **Dry-operational**: factual, brief, ownership-first. Default for Side-project (internal flavor).

Override the default tone only when the project's existing voice (in `CLAUDE.md`, the existing README, or recent commit messages) clearly points elsewhere.

## The hero is 80% of the README

Most READMEs fail at the top. A reader decides within 5 seconds whether to keep reading. The hero (name, tagline, optional install or screenshot) needs to do three jobs at once:

1. Say what the project is concretely.
2. Hint at who it's for.
3. Let them start trying it.

### Good hero examples

**Library, modern-clean:**
```md
# drift

Typed environment variable loader for Node, zero dependencies.

```bash
npm install drift
```
```

**CLI, modern-clean:**
```md
# tunl

Open a public HTTPS tunnel to anything running on localhost. One command, no signup.

![demo](docs/demo.gif)
```

**Side-project, narrative-personal:**
```md
# comite

A reading-first manga platform. I wanted a place to read that wasn't trying to sell me NFTs, push notifications, or an algorithmic feed. This is that.
```

**Internal, dry-operational:**
```md
# pricing-svc

Calculates per-tenant pricing for invoices. Consumed by `billing-svc` and the admin dashboard.

**Owner:** Billing team  ·  **Slack:** `#billing-eng`  ·  **On-call:** [PagerDuty](https://acme.pagerduty.com/services/PRC)
```

### Bad hero patterns (reject these)

- **Marketing fluff:** "The next-generation platform for X" (reader learned nothing).
- **Feature dump in the tagline:** "Fast, reliable, scalable, enterprise-ready logging library" (reader learned nothing).
- **Decorative emoji banners:** `# 🚀📚✨ My Project ✨📚🚀` (noise).
- **Vague tagline:** "A tool for developers" (obvious, reader leaves).
- **Corporate vertical-speak:** "Streamline your workflow with comprehensive tooling" (reader flees).

### The concrete-tagline test

Write the tagline, then ask: could this tagline apply to 100 other projects? If yes, rewrite it.

- Bad: "A modern build tool" (could be anything).
- Good: "Next-gen frontend tooling, built on esbuild and written in Go" (concrete, names the thing).
- Bad: "A powerful data library."
- Good: "Read, transform, and write CSV files without loading them into memory."

## Section library (use as needed)

Not every README needs every section. The archetype file tells you which sections that archetype uses. Below is the shared definition of each section.

### Hero

See above. Always required.

### Why / What it is / Motivation

Required for narrative tone. Strongly recommended for modern-clean (helps the 10-second scan). Two paragraphs max. Describe the problem, then how this solves it.

### Install

Single code block, one command per package manager if it ships to multiple. Don't wrap with explanation prose unless there's a non-obvious prerequisite.

### Quick start / Usage

Smallest possible working example. If it fits in 10 lines, put it in 10 lines. Show the import, the main call, and the result as a comment. This is where you earn the "2-minute local run" bar.

### API

Libraries only. Table format works well for small APIs (10 or fewer exports). For deep APIs, link out to `docs/`.

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

- What works.
- What doesn't yet.
- Who this is for right now.

This section is what passes the "first-paragraph audience filter." Don't hide it at the bottom if the project is early.

### License

One line at the bottom. `MIT (c) Author Name` or similar.

## Visual elements quick reference

Only include the elements the chosen archetype calls for. The archetype file overrides this list when there's a conflict.

| Element | Library | CLI | App | Framework | Side / Internal | Showcase |
| --- | --- | --- | --- | --- | --- | --- |
| Badge row | optional | optional | optional | recommended | skip | optional (skill-icon style) |
| Hero screenshot | skip | skip | required | optional | skip | optional |
| Terminal GIF / asciinema | skip | recommended | skip | skip | skip | optional |
| Mermaid diagram | skip | skip | skip | recommended | skip | optional |
| API table | recommended | skip | skip | skip | skip | skip |
| Command grid | skip | recommended | skip | skip | skip | skip |
| Features grid | skip | skip | recommended | skip | skip | skip |
| Comparison table | skip | skip | optional | recommended | skip | skip |
| Owner / on-call line | skip | skip | skip | skip | required (internal) | skip |
| Animated banner (capsule-render, etc.) | skip | skip | skip | skip | skip | recommended |
| Typing animation (readme-typing-svg) | skip | skip | skip | skip | skip | recommended |
| Stats / streak / activity cards | skip | skip | skip | skip | skip | optional |
| Skill icons (skillicons.dev) | skip | skip | skip | skip | skip | recommended |

"Recommended" means use it unless the project clearly doesn't need it. "Optional" means use it only if it earns its space. "Skip" means don't add it; it'll feel out of place.

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

## Picking the archetype when the project is ambiguous

Some projects sit between archetypes. Use these tiebreakers, in order:

1. **What does the user *do* with it?** Import it (Library), run a command (CLI), use a UI (App), build something with it (Framework), read it to figure out what it is (Side-project / Internal), look at the page itself as the work (Showcase).
2. **What's the primary distribution surface?** Package registry (Library), binary download or `npm i -g` (CLI), web/app store (App), package + docs site (Framework), monorepo path (Internal), the GitHub profile or portfolio repo itself (Showcase).
3. **Who's the typical reader?** Strangers from search (Library, App, Framework), strangers from a tweet or post (CLI, Side-project), coworkers (Internal), recruiters / collaborators / curious visitors (Showcase).

When in genuine doubt, default to Library (safest) for code-as-dependency projects, App for anything with a UI, and Side-project for anything with a single author and no clear audience yet. Default to Showcase only when the user explicitly asks for it.

## Combining archetypes

Avoid it. A README that's "Library + App + CLI" tries to serve three audiences and serves none. Pick the primary archetype and link to the other surfaces in a "See also" section if needed.
