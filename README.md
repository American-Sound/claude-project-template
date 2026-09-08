# Claude Project Template

Starting point for a multi-session Claude Code project. Clone or copy it, then work in
place; Claude reads `CLAUDE.md`, which points at the bundled
`claude-project-structure` skill for how to use the rest.

## Layout

```
CLAUDE.md   Points Claude at the claude-project-structure skill. Modify as you please.
logs/       Dated work logs, MM-DD-YYYY.md, append only
memories/   Project decisions and state, one fact per file, plus MEMORY.md index
notes/      Subject documentation, one file per subject
.claude/    Project-scoped skills (see below)
```

Current project state lives in `memories/`, history in `logs/`. There is no changelog.

## Bundled skills

- `claude-project-structure` - defines the layout above and the rules for writing to it
- `documentation` - house style for anything written into `notes/`

## Use

1. Copy this directory, or use it as a GitHub template.
2. If you care, delete `logs/09-08-2026.md` and anything else left over from the template itself.
3. Start working. Claude appends to `logs/` and `memories/` as it goes.
