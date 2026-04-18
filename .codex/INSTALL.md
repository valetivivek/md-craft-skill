# Installing md-craft for Codex

Codex CLI picks up skills placed under `~/.agents/skills/`. md-craft ships as a single skill at `skills/md-craft/`, so install is clone + one symlink.

## Prerequisites

- Git
- Codex CLI

## Installation

1. **Clone the repo:**
   ```bash
   git clone https://github.com/valetivivek/md-craft-skill.git ~/.codex/md-craft-skill
   ```

2. **Symlink the skill into Codex's skills directory:**
   ```bash
   mkdir -p ~/.agents/skills
   ln -s ~/.codex/md-craft-skill/skills/md-craft ~/.agents/skills/md-craft
   ```

   **Windows (PowerShell):**
   ```powershell
   New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.agents\skills"
   cmd /c mklink /J "$env:USERPROFILE\.agents\skills\md-craft" "$env:USERPROFILE\.codex\md-craft-skill\skills\md-craft"
   ```

3. **Restart Codex** (quit and relaunch the CLI) so it picks up the new skill.

## Verify

```bash
ls -la ~/.agents/skills/md-craft
```

You should see a symlink (or junction on Windows) pointing to `skills/md-craft/` inside the cloned repo. `SKILL.md` and the `references/` folder should be visible through it.

## Updating

```bash
cd ~/.codex/md-craft-skill && git pull
```

The skill updates instantly through the symlink. No re-linking needed.

## Uninstalling

```bash
rm ~/.agents/skills/md-craft
```

Optionally delete the clone: `rm -rf ~/.codex/md-craft-skill`.
