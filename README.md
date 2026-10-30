# Digora

Skills and notes for working with AI coding agents, from daily use. Site: https://digora.dev

## Skills

| Skill | What it does |
|---|---|
| [`substantial`](skills/substantial/) | `/substantial` asks the agent what from the current session is worth saving before the session ends or is compacted, and saves only what you pick. What it caught in two weeks: [article](https://digora.dev/articles/one-question-before-closing/). |
| [`agree`](skills/agree/) | `/agree` records who agreed to which proposal in a project's plan files, keeping "Ann proposes that Bob does X" apart from "Bob agreed", marks relayed answers as unconfirmed, and lists what still waits for an answer. |

Skills are written for Claude Code (`SKILL.md` format). Install them in one of two ways:

- **As a plugin**, to get both skills and updates with one command (Claude Code 2.1.275 or later):
  `/plugin install digora --marketplace digora-dev/digora`. From the shell:
  `claude plugin marketplace add digora-dev/digora`, then `claude plugin install digora@digora`. Update with
  `claude plugin update digora@digora`. Plugin skills carry the plugin's name: `/digora:substantial`,
  `/digora:agree`.
- **As plain skills**, to keep the short names (`/substantial`) or pick one skill: symlink its folder into
  `~/.claude/skills/`; each skill's README has the exact command. Don't do both, or each skill loads twice.

## Rules

Sections to copy into a project's `AGENTS.md`, so every agent follows them, whichever tool it runs in.

| Rules | What they cover |
|---|---|
| [`proposals`](rules/proposals.md) | Proposed vs agreed: work given to someone else is a proposal until they agree, agreement names numbered items, a relayed answer stays unconfirmed until the person confirms it, and agents never record or commit agreement for anyone. |

## License

MIT, see [LICENSE](LICENSE).
