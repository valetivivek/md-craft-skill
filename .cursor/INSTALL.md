# Installing md-craft for Cursor

Cursor 2.4+ supports the open Agent Skills standard. md-craft is a single skill at `skills/md-craft/`, so install is a clone plus one symlink (or a one-line GitHub Remote Rule import). Pick whichever path fits.

## Path A: One-time install via symlink

Cursor auto-discovers skills from `~/.cursor/skills/<name>/SKILL.md` (user-level, all projects) or `.cursor/skills/<name>/SKILL.md` (project-level, per-repo).

```bash
git clone https://github.com/valetivivek/md-craft-skill.git ~/.cursor/md-craft-skill
mkdir -p ~/.cursor/skills
ln -s ~/.cursor/md-craft-skill/skills/md-craft ~/.cursor/skills/md-craft
```

**Windows (PowerShell):**

```powershell
git clone https://github.com/valetivivek/md-craft-skill.git "$env:USERPROFILE\.cursor\md-craft-skill"
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.cursor\skills"
cmd /c mklink /J "$env:USERPROFILE\.cursor\skills\md-craft" "$env:USERPROFILE\.cursor\md-craft-skill\skills\md-craft"
```

Restart Cursor (or reload the window) so it re-scans skills.

### Verify

```bash
ls -la ~/.cursor/skills/md-craft
```

You should see a symlink (or junction on Windows) pointing at `skills/md-craft/` inside the cloned repo. `SKILL.md` and the `references/` folder should be visible through it.

In Cursor, open Settings (Cmd+Shift+J / Ctrl+Shift+J), navigate to Rules, and look for `md-craft` in the Agent Decides section.

### Updating

```bash
cd ~/.cursor/md-craft-skill && git pull
```

The skill updates instantly through the symlink.

### Uninstalling

```bash
rm ~/.cursor/skills/md-craft
```

Optionally delete the clone: `rm -rf ~/.cursor/md-craft-skill`.

## Path B: GitHub Remote Rule (no terminal required)

Cursor can import skills directly from a GitHub URL.

1. Open Cursor Settings (Cmd+Shift+J / Ctrl+Shift+J).
2. Go to Rules.
3. In the Project Rules section, click **Add Rule**.
4. Select **Remote Rule (Github)**.
5. Paste: `https://github.com/valetivivek/md-craft-skill`
6. Confirm. The skill loads into the project.

This installs the skill at the project level. To install globally, copy the imported folder into `~/.cursor/skills/` once Cursor finishes syncing.

## Path C: Cursor Marketplace (one-click install)

If md-craft has been listed on the Cursor Marketplace, install it from there:

1. Open [cursor.com/marketplace](https://cursor.com/marketplace) and search for `md-craft`.
2. Click Install.

If the plugin isn't listed yet, use Path A or Path B in the meantime.

## How Cursor triggers the skill

After install, the skill auto-fires when you ask Agent to write or improve any markdown file (README, PR template, CONTRIBUTING, CHANGELOG, docs). You can also invoke it explicitly by typing `/md-craft` in Agent chat.

The skill reads `.md-craft.json` from the repo root (if present) to skip the style question on later runs. First-run output: a short archetype + tone preview to confirm. Later runs: silent style choice plus a Phase 3 plan/diff before any writes.

## Compatibility note

Cursor also auto-loads skills from `~/.claude/skills/` and `~/.codex/skills/`. If you've already installed md-craft for Claude Code or Codex, Cursor will pick up that same install. You don't need to install twice.
