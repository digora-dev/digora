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
2. If nothing qualifies, say so in one line and stop.
3. Otherwise, list each candidate as one line and name where it would go:
   - an auto-memory file (project state, references);
   - the project's own README or notes, if it belongs to a project;
   - `AGENTS.md`, for rules (propose these, don't write them).

   Then ask which ones to save.
4. Save only what the user picks. Follow the memory format and update an existing memory rather than
   adding a duplicate. Never save credentials.
