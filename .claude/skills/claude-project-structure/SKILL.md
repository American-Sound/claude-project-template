---
name: claude-project-structure
description: "Set up and maintain a multi-session project's Claude-facing structure: a one-line CLAUDE.md pointer, logs/ (dated work log), memories/ (project decisions and state), notes/ (subject documentation). Use when starting a new multi-session project, when asked to set up project docs, a project knowledgebase, persistent context, contextual persistence, session continuity, or a resumable project, when asked to continue from here, and whenever working inside a directory that already has this logs/memories/notes layout."
---

# Rules

1. At session start, read `memories/MEMORY.md` then every file in `memories/`. Read nothing else until a task needs it.
2. After doing any work, append to today's `logs/MM-DD-YYYY.md`.
3. Never read a `logs/` file without a reason. The only reasons: the user references it, a memory references it, or a note references it.
4. Never put user-specific information in `memories/` or `notes/`. Assume every such project is public facing.
5. Ask before creating a git repo, and ask track-vs-gitignore. Decide neither.
6. Write `notes/` with the `documentation` skill.

# Structure

```
./           project root
./CLAUDE.md  one line, pointing at this skill
./logs/      dated work logs, MM-DD-YYYY.md
./memories/  project decisions and state, one fact per file, plus MEMORY.md
./notes/     subject documentation, one file per subject
```

# Setup steps

In order. Steps 1 and 2 are questions, not actions.

1. Run `git rev-parse --git-dir` in the working directory. If there is no repo, ask whether to create one. Do not run `git init` unless told to.
2. Once a repo exists (pre-existing or just created), ask: track `CLAUDE.md`, `logs/`, `memories/`, and `notes/` in git, or add them to `.gitignore`. Apply the answer.
3. Create `CLAUDE.md` if absent. Its only line:

   ```
   Use the claude-project-structure skill to understand this directory and how to interact with it
   ```

   If `CLAUDE.md` already exists, add that line and leave the rest of the file alone.
4. Create `logs/`, `memories/`, and `notes/`. Leave them empty. No placeholder files,
   with one exception: if step 2 decided to track them in git, add an empty `.gitkeep`
   to `memories/` and `notes/`. Git does not track empty directories, so without it a
   clone is missing both. `logs/` needs none; step 2's decision is recorded there as
   the first entry, so the directory is never empty. If the directories are
   gitignored, or there is no repo, add nothing.

# logs/

- One file per day, named `MM-DD-YYYY.md` (March 4 2026 is `03-04-2026.md`). Zero-pad month and day.
- Before writing, check whether today's file exists. Append if it does, create it if it does not.
- Entry content: what was tried, what was found, what was decided and why, the outcome.
- Append only. Once a day has passed, never rewrite that day's file. Correct it in a later entry.
- Write-mostly. Rule 3 governs reads.

# memories/

One fact per file, plus `MEMORY.md` as the index.

File format:

```markdown
---
name: <short-kebab-case-slug>
description: <one-line summary, used to decide relevance during recall>
---

<the fact, then **Why:** and **How to apply:** lines. Link related memories
with [[their-name]]. Cite the work it came out of as logs/MM-DD-YYYY.md.>
```

`MEMORY.md` holds one line per memory: `- [Title](file.md) - hook`. No frontmatter, no memory content.

- Store: decisions and the reasoning behind them, problems hit and how they were resolved, constraints, anything a fresh session needs to pick up where the last one left off.
- Never store: user preferences, personal details, credentials, anything identifying.
- Convert relative dates to absolute.
- Before adding a memory, check for a file that already covers it and update that instead. Delete memories that turn out to be wrong.
- Every memory cites its evidence: the `logs/MM-DD-YYYY.md` file where the work happened, and any `notes/` page holding the detail. A `[[wikilink]]` with no matching file yet is fine; it marks a memory worth writing.

# notes/

- One file per subject, written with the `documentation` skill.
- Name by subject matter. `ls notes/` alone must tell a reader what is in each file.
- Audience is both a human looking for documentation and a later session recalling something already researched or learned.
- Cite the `logs/MM-DD-YYYY.md` entries the note's content came out of.

# Gotchas

- `logs/` uses MM-DD-YYYY, not ISO. It sorts wrong under `ls`. Find today's file by constructing its name, not by position in a listing.
- This layout has no changelog index. Current project state lives in `memories/`, history in `logs/`.
- A memory or note referencing a log file is the only sanctioned way back into `logs/`. Write those references when creating the memory or note, or that day's work becomes unreachable.
- `CLAUDE.md` stays at one line. Behavior rules belong in this skill, not in the project's CLAUDE.md.
- `memories/` is project-scoped. Anything about the user rather than the project belongs in Claude's own memory directory, not here.

# Example

User: "Set up persistent project docs for this repo."

Skill applied. `git rev-parse --git-dir` fails, so ask before touching anything:

"No git repo here. Two questions:
1. Create one?
2. Either way: track `CLAUDE.md`, `logs/`, `memories/`, and `notes/` in git, or add them to `.gitignore`?"

User: "Yes, and track them."

Then: `git init`, write `CLAUDE.md` with the single pointer line, create empty `logs/`, `memories/`, `notes/`, and append the first entry to `logs/03-04-2026.md` recording the initialization and the tracking decision. Add a memory for the tracking decision only if it constrains later work.
