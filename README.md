# self-contained-work-packages

Split planned work into packages that someone with no prior context can pick up and finish: state what and why, never how.

This repository is one agent skill: the instructions are in [SKILL.md](SKILL.md). It describes a way of working, not a tool integration, so it works with any tracker, repository host or agent that can read a skill file.

## Install

Clone it, then link the folder into your agent's skills directory.

```bash
git clone https://github.com/garusis/self-contained-work-packages.git
ln -s "$(pwd)/self-contained-work-packages" ~/.claude/skills/self-contained-work-packages   # Claude Code
ln -s "$(pwd)/self-contained-work-packages" ~/.codex/skills/self-contained-work-packages    # Codex
```

## Related

[blind-spec-review](https://github.com/garusis/blind-spec-review) is how a set of packages is proven before it is handed over.
