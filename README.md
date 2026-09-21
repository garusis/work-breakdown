# work-breakdown

Split work one level down into packages that someone with no prior context can pick up: state what and why, never how.

It works at two sizes, one per run:

- **Big packages** (epics, phases): the big picture plus enough to split them well later. Deliberately light, and never a hidden task list.
- **Small packages** (tasks, tickets): everything needed to start and to finish.

You decide when to come back to a big package and split it; the skill never goes a level deeper on its own.

This repository is one agent skill: the instructions are in [SKILL.md](SKILL.md). It describes a way of working, not a tool integration, so it works with any tracker, repository host or agent that can read a skill file.

## Install

Clone it, then link the folder into your agent's skills directory.

```bash
git clone https://github.com/garusis/work-breakdown.git
ln -s "$(pwd)/work-breakdown" ~/.claude/skills/work-breakdown   # Claude Code
ln -s "$(pwd)/work-breakdown" ~/.codex/skills/work-breakdown    # Codex
```

## Related

[blind-spec-review](https://github.com/garusis/blind-spec-review) is how a set of packages is proven before it is handed over.
