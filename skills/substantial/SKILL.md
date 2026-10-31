---
name: substantial
description: >-
  Ask "Is there anything else substantial that is worth saving for later from
  the context of this session?" and act on the answer. Use when the user runs
  /substantial, or asks what from this session is worth keeping before
  closing or compacting it.
---

# Substantial

Answer this question about the current session:

> Is there anything else substantial that is worth saving for later from the context of this session?

0. Before any tool call, write this line on its own, so the background-session list shows the session
   as finalizing:

   `Finalizing: reviewing the session for things worth saving.`

1. Look back over the session for things that would be lost when it ends or is compacted, and that are
   not already in a file, a commit, or memory:
   - unfinished work: its state and the next step;
   - decisions made, with the reason behind each;
   - facts found by testing or investigation that took real effort;
   - pointers to external things (URLs, ticket IDs, MR links).

   Skip anything the repo or git history already records, and anything that only mattered to this
   conversation.

   While checking whether something is already saved, read the note it would go into. A note that this
   session showed to be wrong is a candidate too: a correction. If a note or a candidate says work was
   committed, pushed or merged, check the repo first (`git -C <repo> status`, `git -C <repo> log @{u}..`)
   and go by what git shows, not by what the note says.

   Read `declined-candidates.md` in the auto-memory directory, if it exists. Skip a candidate the user
   declined before, unless this session brought new evidence for it; then propose it marked
   `re-proposed: <the new evidence>`.
2. If nothing qualifies, say so in one line and stop.
3. Otherwise, list each candidate as one line, with a level, and name where it would go:
   - an auto-memory file (project state, references);
   - the project's own README or notes, if it belongs to a project;
   - `AGENTS.md`, for rules (propose these, don't write them).

   Levels. The level is earned by evidence, not by how sure you feel:
   - `high`: a state, a pointer or a fact that carries its evidence from this session: an identifier
     (commit hash, URL, ticket, `file:line`) or the command that showed it and what it showed, with the date.
     No evidence in the line, no `high`.
   - `mid`: inferred from the session, not checked.
   - `low`: a guess, an idea, an open question.

   Never saved without asking, whatever the level: rules (`AGENTS.md` proposals), corrections that change an
   existing note, and deleting anything. A correction shows both versions and what backs the new one:

   `3. [high, ask] Correct <note>: says "<old text, quoted from the file>" -> now "<new>" (<command or file that showed it>, checked <date>)`

   Mark it `unchecked` when nothing in this session backs the new version. Ask about a repo's state only
   when git could not settle it.
4. Save every `high` line that goes to the auto-memory directory and is not in the never-without-asking
   group now, before asking, and mark it `[high, saved]` in the list. A `high` line for a project's notes
   stays `ask`: the memory review doesn't see those files. Add a line or a new note; don't rewrite what a
   note already says. End each saved line with `(auto-saved <UTC date>)`: the next memory review quotes
   those lines in full and asks keep or revert. If a save fails, leave the line unsaved and say why.

   Then ask which of the remaining lines to save. In a pick list, order them `high`, `mid`, `low`, and end
   each `high` line's label with `(Recommended)`.
5. Save only what the user picks. Follow the memory format and update an existing memory rather than
   adding a duplicate. Never save credentials. Write a state as what was checked, with an identifier and a
   date ("pushed a1b2c3, checked 2026-10-31"), never a bare "done": the next session can check that.

   Append each line the user did not pick to `declined-candidates.md` in the auto-memory directory, one
   line each: `- <UTC date> <the candidate line>`. Create it with the memory frontmatter (`type: feedback`)
   and an index line if it is missing, and drop lines older than 90 days while you are there.
