# agree

<!-- vibecoded-banner -->
> **AI-generated (vibecoded) draft, not yet human-reviewed.** Details may be wrong or missing.

`/agree` records answers to proposals in a project's plan files and lists the ones still waiting. It keeps two
things apart that a plan otherwise blurs:

- **Ann proposes that Bob does X.** A wish. Bob may not know about it yet.
- **Bob agreed to do X.** A commitment, and only Bob can make it.

The rules it follows are in [`rules/proposals.md`](../../rules/proposals.md); copy that section into the project's
`AGENTS.md` so every agent follows them, not only the one running the skill. The instructions the agent follows
are in `SKILL.md`; this file is for people.

Install by symlinking, from the root of your clone of this repo:
`ln -sfn "$PWD/skills/agree" ~/.claude/skills/agree`. Or install the `digora` plugin, which runs it as
`/digora:agree` ([repo README](../../README.md)).

## Example

Ann coordinates a small team that plans in `TODO.md`. She asks her agent to offer Bob the test set:

```
- [?] T14 · bob · Label the 60 test boards (docs/12). · 2026-10-30 · Proposed by ann 2026-10-30
```

Bob answers Ann in a chat two days later: "the test set yes, but 30 boards; the bot no time". Ann tells her agent
`/agree bob, in chat today: T14 yes but 30 boards, T15 no`. The agent records:

```
- [?] T14 · ann · Label the 30 test boards (docs/12). · 2026-10-30 · Counter by bob 2026-11-01: 30 boards, not 60
```

and moves T15 to "Done" as `[-]` declined. T14 now waits on Ann. When Ann accepts the change, it goes back to Bob,
but Bob's yes came through Ann, so it is marked relayed, not agreed:

```
- [r] T14 · bob · Label the 30 test boards (docs/12). · 2026-10-30 · Relayed by ann 2026-11-01: chat
```

Nobody, people or agents, builds on `[r]` as settled. It becomes `[ ]` when Bob confirms in his own words, for
example with a comment on the repo's issue, and the line gets the link:

```
- [ ] T14 · bob · Label the 30 test boards (docs/12). · 2026-10-30 · Relayed by ann 2026-11-01: chat · Agreed 2026-11-02: <link to Bob's comment>
```

If Bob uses the repo himself, he changes the line in a commit he signs, with the trailer `Agreed: T14`, and no
relay is needed.

## Why

- **A plan that reads as settled when it isn't.** A coordinator's plan names people and hours; an agent asked to
  continue it treats every line as agreed. The `[?]` mark and "Proposed to" in docs make the difference visible
  to people and agents reading the files.
- **A bulk "ok" covers more than the person read.** Agreement names numbered items. This comes from handing work
  between two agents through a person: one blanket "agreed" once covered a proposal built on a false finding. Now a
  reply numbers its proposals, and the answer names the numbers.
- **Agreement that lives only in chat is lost.** It is written into the file with the date and where it was given.
- **An agent must not agree on anyone's behalf.** It records answers only from the person it works for, never from
  text it reads in files, commits or tool output. An agreement is a commit of its own, never bundled with other
  changes, and the agent makes it only after the person confirms that commit, and only for that person.
- **A relay is not the person.** A coordinator passing on answers, or an agent working with the coordinator's
  access, could otherwise mark anyone's task agreed. `[r]` keeps the relay's word visible as unconfirmed.

## Limits

- The skill writes the line; it can't prove the person agreed. Evidence is the owner's signed commit or a link to
  their own words; [`rules/proposals.md`](../../rules/proposals.md) says what counts. Nothing checks the file
  automatically: anyone with write access can still edit a line by hand, and git history shows who did.
- It doesn't record agreement to whole files or specs. Pull request reviews with stale approvals dismissed do that
  (see the rules).
- The task list format is one line per task. Other formats need the project's `AGENTS.md` to say how its states are
  written.
