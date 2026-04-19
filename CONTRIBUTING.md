# Contributing to md-craft

Thanks for landing here. md-craft is a small skill with a focused scope, so most contributions fall into one of three buckets.

## Ways to contribute

**Bug reports.** If the skill writes something that breaks its own rules (invents an install command, adds a Star History badge you didn't approve, slips an em dash into an output file), open an issue with the prompt you used and the output it produced.

**Reference fixes.** The `skills/md-craft/references/` files are where the concrete patterns live. If a pattern is wrong, missing, or contradicts the SKILL.md workflow, a PR that fixes the reference is welcome.

**New style presets.** The README explicitly invites proposals for new presets (for example "data-oriented" or "showcase"). Use the style preset issue template so the discussion stays concrete.

## Dev setup

There is no build step. The skill is markdown plus references.

1. Fork and clone.
2. Edit `skills/md-craft/SKILL.md` or files under `skills/md-craft/references/`.
3. If you are testing locally as a Claude Code plugin, add this repo as a marketplace from your local path, then reload plugins.
4. Open a PR against `main`.

## Before opening a PR

- Keep changes scoped. One idea per PR.
- Do not add em dashes to output-facing examples in the references (the skill forbids them in generated files; the references should practice what they preach on examples).
- If the change affects the SKILL.md workflow or the README's promised behavior, update both.
- If you add a new reference file, link it from SKILL.md's "File-type specifics" list.

## Questions

Open an issue. There is no Slack, Discord, or private channel.

## License

By contributing, you agree that your contributions will be licensed under the MIT License in [LICENSE](LICENSE).
