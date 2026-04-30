# Library archetype

For npm packages, pip packages, cargo crates, Go modules, SDKs, and any code-as-dependency project. The reader is another developer who wants to install, see one example that works, and decide in 30 seconds whether to keep going.

## When to pick this archetype

- The project ships to a package registry (npm, PyPI, crates.io, Maven, etc.).
- Its main artifact is an importable API, not a binary or a UI.
- Most readers arrive via search results or a dependency mention.

If the project is *both* a library and a CLI (e.g. `eslint`, `vite`), pick the archetype that matches the *primary* user surface. If most users `import` it, this archetype. If most users run it as a command, use the CLI archetype.

## Default tone

Modern-clean. Factual, slightly warm, no marketing verbs. Earned word choices. Sentence-case headings. Short paragraphs.

Override to narrative tone only when there is a strong author voice already visible in `CLAUDE.md`, the existing README, or the package description.

## Visual elements toolkit

Use these as a menu, not a checklist. Pick what the project earns.

- **Badge row** (1 line, centered or left-aligned): build, version, license, downloads. Use shields.io. If the package is unpublished or pre-1.0, skip it.
- **Code block hero**: install command directly under the tagline. Use the actual package manager syntax for the language.
- **Single runnable example**: 5 to 12 lines, real, copy-pasteable, includes the import.
- **API table**: 4 to 10 entries max. Two columns (Export, Description). For larger APIs, link to `docs/`.
- **Type or schema block**: if the API is type-driven, show one type signature. Skip otherwise.
- **No screenshots**, **no mermaid**, **no comparison tables**. Libraries earn trust through the example, not visuals.

## Section structure

```md
# <name>

<one-line tagline, concrete, 8 to 14 words>

<badge row, optional>

```bash
<install command>
```

## Why / What it is
<two short paragraphs: problem this solves, how it solves it>

## Quick start
<smallest runnable example, with import and main call>

## API
<table or short list of main exports>

## Configuration
<only if the library has non-trivial config>

## Status
<one paragraph: what works, what doesn't, who it's for right now>

## License
<one line>
```

## Mini example skeleton

```md
# drift

Typed environment variable loader for Node, zero dependencies.

[![npm](https://img.shields.io/npm/v/drift.svg)](https://www.npmjs.com/package/drift)
[![build](https://img.shields.io/github/actions/workflow/status/acme/drift/ci.yml)](https://github.com/acme/drift/actions)
[![license](https://img.shields.io/npm/l/drift.svg)](LICENSE)

```bash
npm install drift
```

## Why

Most env loaders either do too much (secrets, rotation, multi-source merging) or too little (`process.env` as-is). drift does one thing: typed vars with defaults, validated at boot.

## Quick start

```ts
import { load } from "drift";

const env = load({
  PORT: { type: "number", default: 3000 },
  DATABASE_URL: { type: "string" },
});

console.log(env.PORT);
```

## API

| Export | Description |
| --- | --- |
| `load(schema)` | Loads and validates env vars; throws on missing required values |
| `loadSafe(schema)` | Same, but returns `{ ok, data, error }` instead of throwing |
| `defineSchema(...)` | Helper for sharing schemas across files |

## Status

Stable since 1.0.0. Used in production at acme.com. Issues and PRs welcome.

## License

MIT
```

## Anti-patterns specific to libraries

- **A "Features" bullet list** of 3-word entries ("Fast", "Typed", "Tiny"). Either show the example that proves it, or drop the section.
- **Hand-written API tables for big APIs**. If the API has 30+ exports, link to `docs/`. The table is for libraries with a small surface.
- **Install sections that explain what npm is.** The reader installed npm to get here.
- **Overstated benchmark claims** without a link to the benchmark code. If you say "10x faster," show the script.
- **Code blocks without language tags.** Always tag (` ```ts `, ` ```py `, ` ```rs `).
