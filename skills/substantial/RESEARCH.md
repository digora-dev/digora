# Research before publishing

What was checked before `/substantial` and its article went public (2026-10-27 to 2026-10-28), what held, and
what was corrected. The article itself: [One question I ask my coding agent before closing every
session](https://digora.dev/articles/one-question-before-closing/).

## What was done

1. **Prior-art review** (Claude Fable, 2026-10-27). Given the skill, a first draft of the article and the web: 54 of
   100 web calls used (21 searches, 33 fetches). Every source is labelled "fetched", "full text via search result"
   or "snippet only", so weak sources are easy to spot. It found 14 related designs and practices and 8
   alternatives, and asked why the idea isn't built into Claude Code.
2. **Independent check** (Grok 4.7, 2026-10-27). Given the same draft as a text "found on Hacker News", with 10
   searches, and asked whether anything in it is noteworthy. It re-checked the linked tools against their files
   and the claims against the current Claude Code docs and issues.
3. **Weighing the two**, with every claim about the machine or the counts checked first-hand rather than taken
   from either review.
4. **Recount from transcripts.** Scripts counted runs from the session logs: a run is a user-typed
   `/substantial`, deduplicated by timestamp so a resumed session isn't counted twice. One model pass sorted the
   candidate lines into kinds.

## What held

- The idea is a known pattern, not an invention. At least six independent Claude Code skills or gists (March to
  October 2026) list candidates at session end, route them, and write only what the person approves. The human
  form is Cal Newport's shutdown ritual (2009).
- **save-before-compact** is the closest design, and the difference is the pick: it writes on its own and reports
  afterwards. Both reviews confirmed this from its files.
- The pick is the part worth keeping. Requests to confirm memory writes were closed without it, a confirmation
  dialog sits behind a disabled flag, and retro-skill reports an always-on candidate stream that ended at 1011
  pending, 0 approved.
- Not built in: the pick, destinations outside the memory directory, and a hook that makes the model take a turn
  at exit.
- No source found names stale notes as a main kind of catch. Elsewhere they are treated as background
  maintenance.

## What was corrected

| Claim in the first draft | Finding | Now |
|---|---|---|
| Stale notes are the most frequent kind | Recount over 14 days: 27 of 135 candidates; open items (51) and hard-won facts (41) are more common. Stale fixes appear in 25 of 53 runs that offered anything | "About one candidate in five", not "most frequent" |
| Last week: 19 runs with candidates, 8 with nothing, 7 cut short | Recount: 27, 5, 1 resumed re-run, 2 cut short. A first recount also matched tool results that only quoted the command (78 instead of 68) | Numbers from the scripts, method stated |
| None of the similar tools has users beyond its author | Came from an unreadable star count. The GitHub API showed 22 stars for retro-skill and 97 for the Pensyve server | Dropped |
| `PreCompact` and `SessionEnd` run shell commands only | They also run HTTP and MCP-tool hooks; what they can't run is a prompt or agent hook | Corrected |
| save-before-compact "asks the same question" | It sweeps at the same moment, then writes on its own | Reworded |
| The whole combination exists nowhere | Not found in one review; Grok named further near-matches | "Not found", not "doesn't exist" |
| Requests for confirmation were declined | Closed by a stale bot, by the reporter, or with a `permissions.ask` workaround | Named as closed, not refused |
| `SKILL.md` says nothing about existing notes | It says to update rather than duplicate, but has no stale-note kind | Narrowed |
| The skill routes open items to a to-do list | Not in `SKILL.md`; that routing came from the author's wider rules | `SKILL.md` lists memory, project notes and `AGENTS.md` only |

## Still open

- **Background sessions and memory.** The docs say auto memory is off in a background session. On the author's
  machine, background sessions still get the memory instructions, and 7 of 22 background-job transcripts contain
  writes into the memory directory. Whether the docs mean only the separate background extractor is a guess.
- **Gating memory writes.** One issue says memory writes are auto-approved; another says `permissions.ask` on
  Write/Edit can gate them. They may differ by version. Not tested.
- **The hotkey effect.** How often the question would be skipped without a key is not measured, here or anywhere
  the review looked.
- **One person's data.** All counts come from one person's sessions; the kinds come from a single model pass.
- **Why it isn't built in** is an inference. No vendor statement was found either way. The plainest explanation
  may be that nobody has asked for this exact combination.

The review's suggested changes that weren't adopted are listed under "Ideas not built yet" in the
[README](README.md).
