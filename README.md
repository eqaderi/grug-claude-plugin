# grug-engineering

Claude Code plugin: grug-brained engineering mode. Simplicity-first slash commands and skill. Inspired by [grugbrain.dev](https://grugbrain.dev).

## Install

```bash
claude plugin install ./grug-claude-plugin
```

Or from npm once published:

```bash
claude plugin install grug-engineering
```

## What it provides

- **Skill**: `grug-engineering` — triggers on review, implementation, refactor, testing, or when you say `grug`, `grug mode`, `simple solution`, `avoid overengineering`, `Chesterton's Fence`
- **Commands**: `/grug-review`, `/grug-plan`, `/grug-refactor`

## Use in Claude Code

```text
/grug-review
```

```text
/grug-plan
```

```text
/grug-refactor
```

Or directly:

```text
Use grug mode. Prefer existing repo patterns. Do not add abstraction unless this task truly needs it.
```

## Always-on global rules (optional)

The plugin skill activates on demand. For always-on grug behavior, copy `global-rules.md` into your `~/.claude/CLAUDE.md`:

```bash
cat global-rules.md >> ~/.claude/CLAUDE.md
```

## Add a repo-level reminder

From inside a repo:

```bash
cat repo-snippets/CLAUDE.grug-snippet.md >> CLAUDE.md
```

## Notes

No telemetry. No external calls. No runtime dependencies. Grug approve.
