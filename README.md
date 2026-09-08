# claude-project-template

Starting point for a multi-session Claude Code project. Clone or copy it, then work in
place; Claude reads `CLAUDE.md`, which points at the bundled
`claude-project-structure` skill for how to use the rest.

## Layout

```
CLAUDE.md   one line, points Claude at the claude-project-structure skill
logs/       dated work logs, MM-DD-YYYY.md, append only
memories/   project decisions and state, one fact per file, plus MEMORY.md index
notes/      subject documentation, one file per subject
.claude/    project-scoped skills (see below)
```

Current project state lives in `memories/`, history in `logs/`. There is no changelog.

## Bundled skills

`.claude/skills/` shadows the global `~/.claude/skills/`, so these versions win inside
this repo:

- `claude-project-structure` - defines the layout above and the rules for writing to it
- `documentation` - house style for anything written into `notes/`

They are forked copies. Edits to the global skills do not propagate here.

## Use

1. Copy this directory, or use it as a GitHub template.
2. Delete `logs/09-08-2026.md` and anything else left over from the template itself.
3. Start working. Claude appends to `logs/` and `memories/` as it goes.
