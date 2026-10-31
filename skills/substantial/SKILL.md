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
2. If nothing qualifies, say so in one line and stop.
3. Otherwise, list each candidate as one line and name where it would go:
   - an auto-memory file (project state, references);
   - the project's own README or notes, if it belongs to a project;
   - `AGENTS.md`, for rules (propose these, don't write them).

   A correction shows both versions and what backs the new one, so the user does not have to check it:

   `3. Correct <note>: says "<old text, quoted from the file>" -> now "<new>" (<command or file that showed it>, checked <date>)`

   Mark it `unchecked` when nothing in this session backs the new version. Ask about a repo's state only
   when git could not settle it.

   Then ask which ones to save.
4. Save only what the user picks. Follow the memory format and update an existing memory rather than
   adding a duplicate. Never save credentials. Write a state as what was checked, with an identifier and a
   date ("pushed a1b2c3, checked 2026-10-31"), never a bare "done": the next session can check that.
