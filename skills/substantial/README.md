# substantial

`/substantial` asks the agent what from the current session is worth saving before the session ends or is
compacted, and saves only what the user picks. The instructions the agent follows are in `SKILL.md`; this file is
for people and is not loaded when the skill runs.

Install by symlinking, not copying, so a `git pull` updates it. From the root of your clone of this repo:
`ln -sfn "$PWD/skills/substantial" ~/.claude/skills/substantial`.

What it caught in 68 runs over two weeks, what it costs, and how it compares with the alternatives:
[One question I ask my coding agent before closing every session](https://digora.dev/articles/one-question-before-closing/).
What was checked before publishing, and what was corrected: [RESEARCH.md](RESEARCH.md).

## Example run (2026-10-26)

The session had changed a bot service's config through an apply script (the service refuses to start if its config
drifts from a checked shape), then moved the script into a personal runbooks folder. Both of those were already in a
commit, the runbook and memory, so the run skipped them. It listed four candidates, one line each, with a place to
save each one:

1. **Open item, memory note.** A staged template of the config checker didn't know the new key. Reinstalling the
   template would make the service refuse to start. Nothing recorded this except the chat.
2. **Test recipe, runbook.** How to dry-run on a copy of the config: swap the secret for a placeholder with `sed`,
   so the real one is never copied, and point the checker's hardcoded paths at the copy too. Otherwise the check
   fails on the copy for reasons unrelated to the change. This had taken a failed first attempt to find.
3. **Process step that had drifted, runbook.** The runbook said to log every change in a deferred-items file, which
   no one had updated for a week; the runbook's own rollback list had become the real log. The fix was to change
   the step.
4. **Rule, `AGENTS.md`.** Earlier the user had stopped a long chained test command because it was too much to read
   before approving. The run proposed a rule: keep each shell command short enough to review, and split test runs or
   put them in a script file. It was proposed as an edit for the user to approve, not saved to memory.

The user picked all four in a multi-select window.

What made it a good run:

- Each candidate was something the session would lose: an open item, a hard-won fact, a drifted process, a rule.
  Work already in a commit or a note was left out.
- Each line named its destination, matched to what it is: project state to memory, how-to to the project's
  runbook, a rule to `AGENTS.md`. The rule was proposed, not written.
- The saves were checked. One `sed` edit silently matched nothing, because the target sentence wrapped across two
  lines; its match count (0) showed that, and the edit was redone with the Edit tool.

## Limits

- It reads only what is still in context, so it has to run before `/clear`, not after.
- It relies on the agent's judgment that something is "already saved". A run can miss a fact it never noticed was
  new.
- Nothing is written until you answer. If the session is compacted or closed during that wait, the list is lost.
- Re-running it on a resumed session finds nothing new.
- All the numbers in the article come from one person's sessions.

## Ideas not built yet

1. **Write before asking.** Write the candidate list to a file first, so a compaction or a closed session during
   the wait doesn't lose it. save-before-compact's own audit found chat text cut off in 5 of 6 mid-skill
   compactions, while file writes had already landed.
2. **A "drop" candidate.** Today the skill can propose rewording a stale note, not deleting one.
3. **Unanswered questions as a kind.** Questions asked during the session and never answered get written down
   nowhere.
4. **A sharper test for rules.** Propose a rule only if the agent would decide differently without being told.
5. **Read the transcript file, not the context.** Then it would work after `/clear` too.

## Similar tools

- [save-before-compact](https://github.com/LippInc/save-before-compact): the closest design. Same question, same
  moment, same routing, but it saves on its own and reports afterwards instead of letting you pick.
- [consolidate](https://gist.github.com/eva-mishor/2ca6bfe8f3a2ee5170e996b292340ce0): five destinations; when a new
  fact contradicts a note, it shows both versions and asks which is current.
- [retro-skill](https://github.com/netresearch/retro-skill): routes each finding by "who should own this truth", at
  most ten proposals, each approved on its own.
- [Pensyve session-memory](https://github.com/major7apps/pensyve): takes the same kind of answer ("all", "1,3",
  "none") and handles what automatic capture missed.
- [session-wrap-up](https://github.com/xpepper/session-wrap-up): treats the moments you corrected the agent as the
  most valuable lessons, and scales the review to the size of the session.
- The human version: Cal Newport's
  [shutdown ritual](https://calnewport.com/drastically-reduce-stress-with-a-work-shutdown-ritual/) (2009).
