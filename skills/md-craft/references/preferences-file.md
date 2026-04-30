# Preferences file (`.md-craft.json`)

Per-repo memory for the md-craft skill. Lives at the repo root next to the README. Stores the archetype, visual element toggles, and accumulated notes from past corrections so later runs in the same repo can skip the style question.

## Why per-repo

Taste isn't a property of the user; it's a property of the project. The "right" tone for an enterprise repo is wrong for a side project, and a global preference applied silently is exactly the failure mode this file exists to prevent. Each project has its own answer; we store it next to the project.

## File location and format

- Path: `<repo-root>/.md-craft.json`
- Encoding: JSON (no comments). Keep it human-editable; the user should be able to read and tweak it without tooling.
- Add `.md-craft.json` to `.gitignore` only if the user explicitly asks; default is to commit it so the whole team gets consistent generated output.

## Schema

```jsonc
{
  "version": 1,
  "archetype": "library",
  "tone": "modern-clean",
  "visual": {
    "badges": "always",
    "heroScreenshot": "auto",
    "terminalGif": "skip",
    "mermaid": "skip",
    "comparisonTable": "skip",
    "emojis": "never",
    "animatedBanner": "skip",
    "typingSvg": "skip",
    "statsCards": "skip",
    "skillIcons": "skip"
  },
  "preferences": {
    "headingCase": "sentence",
    "exampleStyle": "minimal-runnable",
    "maxLines": 220,
    "packageManagers": ["npm", "pnpm"]
  },
  "notes": [
    "User dislikes generic 'Features' bullet lists; prefers paragraph plus code example.",
    "Always show install commands for both npm and pnpm.",
    "Keep README under 220 lines; longer content goes in docs/."
  ],
  "lastUpdated": "2026-04-30"
}
```

### Field reference


| Field                         | Required | Values                                                           | Notes                                                                                                                                                                                                               |
| ----------------------------- | -------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `version`                     | yes      | `1`                                                              | Schema version. Bump on breaking changes.                                                                                                                                                                           |
| `archetype`                   | yes      | `library`, `cli`, `app`, `framework`, `side-project`, `showcase` | One of the six. Drives structure and default visuals. `showcase` is opt-in (animated banners, typing SVGs, stats cards) and only set when the user explicitly asks for a profile-style or visually striking README. |
| `tone`                        | yes      | `modern-clean`, `narrative-personal`, `dry-operational`          | Voice. See `references/readme.md`.                                                                                                                                                                                  |
| `visual.<element>`            | optional | `always`, `auto`, `skip`                                         | Per-element override. `auto` defers to archetype defaults.                                                                                                                                                          |
| `preferences.headingCase`     | optional | `sentence`, `title`                                              | Heading style. Default sentence.                                                                                                                                                                                    |
| `preferences.exampleStyle`    | optional | `minimal-runnable`, `verbose`, `prose-with-snippets`             | How code examples should look.                                                                                                                                                                                      |
| `preferences.maxLines`        | optional | integer                                                          | Soft target for total README length. The skill warns the user before exceeding by more than 20%.                                                                                                                    |
| `preferences.packageManagers` | optional | array of strings                                                 | Which package managers to include in install blocks.                                                                                                                                                                |
| `notes`                       | optional | array of one-line strings                                        | Distilled corrections from past runs. Read at write time, treated as additional rules.                                                                                                                              |
| `lastUpdated`                 | optional | ISO date string                                                  | Updated on every write.                                                                                                                                                                                             |


Unrecognized fields are ignored. Don't fail on them; future versions may add fields.

## How the skill uses the file

### On the first run in a repo

1. Check for `.md-craft.json`. Doesn't exist.
2. Run Phase 2 normally: infer the most likely archetype from project context, show one or two preview options, ask the user to pick.
3. Ask the visual elements question only if the archetype default is ambiguous for this project (e.g. "App archetype usually has a hero screenshot. Do you have one to include, or should I leave a placeholder?").
4. After Phase 4 (writing), create `.md-craft.json` with the archetype, tone, and any explicit visual choices the user made. `notes` starts empty.

### On every later run in the same repo

1. Read `.md-craft.json` first, before any user message about style.
2. Use the stored archetype and tone as the answer to the Phase 2 question. Skip the preview-and-ask step.
3. Apply `notes` as additional writing rules during Phase 4.
4. Still run Phase 1 (gather context) and Phase 3 (show plan / diff). Silent input is fine; silent output is not.

### Capturing corrections (after writing)

After the file is written and the user reacts, the skill listens for two kinds of feedback:

1. **In-chat corrections**: "drop the emojis," "make the install section shorter," "keep this under 200 lines," "I always want a pnpm command too."
2. **Post-write edits**: if the user edits the file before the next message, diff against what was written. Material removals or rewrites are signal.

Distill each correction into a one-line note. Append to `notes[]`. Do not invent notes; only capture things the user said or visibly changed. Update `lastUpdated`.

### Cleaning up notes

When `notes` exceeds 12 entries or contains contradictions, propose a consolidation to the user before the next write:

> Your `.md-craft.json` has 14 notes, some contradicting. I want to consolidate them into 6 clearer rules before the next run. Show me the proposed list?

Don't consolidate silently. The user wrote those notes by correcting the skill; they should approve any merge.

## Example flows

### First run on a new library

```
$ ai "write a readme"

(skill reads CLAUDE.md, package.json, etc.)
(skill detects: this is an npm package with a small API)

> Looks like this is a library (npm package, single import surface). Want me to use the
> Library archetype with modern-clean tone, or pick something else?

User: yes that's right

(skill writes README)
(skill writes .md-craft.json with archetype: "library", tone: "modern-clean")
```

### Second run, same repo, two weeks later

```
$ ai "the readme is stale, refresh it"

(skill reads .md-craft.json: library + modern-clean, plus 2 notes)
(skill reads current README, package.json, recent commits)

> Plan for updating README.md:
> KEEP: hero, install
> REWRITE: API table (3 new exports added since last write)
> ADD: a one-line note about the new --strict flag
> Honoring your saved notes (no emojis, sentence-case headings, npm + pnpm install).
> Sound right?

User: yes

(skill writes; updates .md-craft.json lastUpdated)
```

### Capturing a correction

```
User (after a write): drop the badges, this project doesn't have a CI yet

(skill notes: "User does not want a badge row until CI exists")
(skill removes the badge row)
(skill appends to notes[] in .md-craft.json)
```

## Conflicts and edge cases

- **No `.md-craft.json` but the user says "use the same style as last time"**: ask once, then create the file.
- **Archetype mismatch**: if the user originally picked `library` but the repo has clearly become an app (added a UI, added a Dockerfile + Procfile), surface the mismatch in Phase 2 and let the user re-pick. Don't auto-change the archetype.
- **Multiple writers in one repo**: the file is per-repo, not per-user. If two contributors disagree on style, that's a team conversation, not a tooling problem.
- **CI environments**: the skill should still read the file in CI but never write to it. Writing requires user confirmation; CI has no user.

## What this file is not

- It is not a global config. There is no global counterpart by design.
- It is not a place to store unrelated metadata. Don't add fields the skill doesn't read.
- It is not a substitute for asking. If the file exists but the project has clearly changed (new framework, new audience), still ask.

