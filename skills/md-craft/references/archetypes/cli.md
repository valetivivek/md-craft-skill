# CLI archetype

For command-line tools, terminal utilities, and binaries. The reader is somebody who heard about the tool, wants to see it run, and decide whether to install it.

## When to pick this archetype

- The main user surface is a command typed into a terminal.
- The project ships a binary, a global npm/pip install, a Homebrew formula, or similar.
- The thing readers want to see is not an API table; it's the tool actually doing something.

If the project is both a CLI and a library, pick this archetype only when most users run the command rather than `import` it.

## Default tone

Modern-clean, with one allowance: a slightly punchier hero. CLI READMEs can have a one-line "this is the cool thing" tagline because the tool is concrete and demoable. Avoid actual marketing prose.

Sentence-case headings. Real commands, not pseudo-commands.

## Visual elements toolkit

CLI READMEs are the most visual archetype. Use:

- **Hero block**: name, one-line tagline, install command for the most common platform.
- **Demo**: pick one of these, in order of preference if the project supports it:
  1. **Terminal recording**: VHS (`*.tape` rendered to GIF), asciinema, or a recorded GIF. Embed at the top.
  2. **Code block of a real session**: prompt, command, real output. Use a `console` or `bash` block.
  3. **Static screenshot** of the terminal (last resort, use only if recording is hard to set up).
- **Install grid**: short table or fenced block per package manager. Include Homebrew, npm/yarn/pnpm, pipx, cargo, scoop, asdf, whatever applies. Don't pad with managers the project doesn't actually publish to.
- **Command grid**: table of subcommands with one-line descriptions. Up to ~12 rows; if there are more, link to `--help` or a docs page.
- **Common recipes**: 3 to 5 short examples, each with a one-line "do X" header and a code block.
- **Optional badge row**: build, version, license. Skip downloads if the count is small.
- **No mermaid** unless the tool's flow is genuinely non-obvious.

## Section structure

```md
# <name>

<one-line tagline>

<demo: GIF, asciinema, or session block>

## Install

```bash
brew install <name>          # macOS / Linux
npm i -g <name>              # cross-platform
```

## Quick start

<smallest useful command, with expected output>

## Commands

| Command | Description |
| --- | --- |
| `<name> init` | ... |
| `<name> build` | ... |
| `<name> deploy` | ... |

## Recipes

### <Recipe 1 title>
<short context>

```bash
<command>
```

### <Recipe 2 title>
...

## Configuration

<only if the CLI has non-trivial config; show example file, link to full reference>

## Status

<one paragraph>

## License

<one line>
```

## Mini example skeleton

```md
# tunl

Open a public HTTPS tunnel to anything running on localhost. One command, no signup.

![demo](docs/demo.gif)

## Install

```bash
brew install tunl                    # macOS / Linux
npm i -g tunl                        # cross-platform
```

## Quick start

```bash
$ tunl 3000
> https://prairie-otter-2381.tunl.app -> http://localhost:3000
> ready in 240ms
```

## Commands

| Command | Description |
| --- | --- |
| `tunl <port>` | Open a tunnel to localhost:<port> |
| `tunl status` | Show active tunnels |
| `tunl close <id>` | Close a tunnel |
| `tunl auth <token>` | Sign in for stable subdomains |

## Recipes

### Stable subdomain

```bash
tunl auth $TUNL_TOKEN
tunl 3000 --subdomain staging
# https://staging.tunl.app -> http://localhost:3000
```

### Inspect requests

```bash
tunl 3000 --inspect
# Opens http://localhost:4040 with request logs
```

## Status

Stable. Used by ~2k developers. macOS and Linux supported, Windows in beta.

## License

MIT
```

## Anti-patterns specific to CLIs

- **No demo at all**: a CLI README without any visible command-output is asking the reader to imagine the tool. Don't.
- **Generated `--help` dumps as the only documentation**. Useful as a reference, not as the README's main body.
- **Fake terminal screenshots** with hand-typed prompts that don't match what the tool actually prints.
- **"Configuration" sections that list 30 flags** with no examples. Show the 3 flags people actually use; link to the full list.
- **Install instructions for package managers the project doesn't publish to.** Don't list `apt install` if there's no apt package.
