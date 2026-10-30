# Digora

Skills and notes for working with AI coding agents, from daily use. Site: https://digora.dev

## Skills

| Skill | What it does |
|---|---|
| [`substantial`](skills/substantial/) | `/substantial` asks the agent what from the current session is worth saving before the session ends or is compacted, and saves only what you pick. What it caught in two weeks: [article](https://digora.dev/articles/one-question-before-closing/). |

Skills are written for Claude Code (`SKILL.md` format). Install them in one of two ways:

- **As a plugin**, to get updates with one command (Claude Code 2.1.275 or later):
  `/plugin install digora --marketplace digora-dev/digora`. From the shell:
  `claude plugin marketplace add digora-dev/digora`, then `claude plugin install digora@digora`. Update with
  `claude plugin update digora@digora`. Plugin skills carry the plugin's name: `/digora:substantial`.
- **As plain skills**, to keep the short names (`/substantial`) or pick one skill: symlink its folder into
  `~/.claude/skills/`; each skill's README has the exact command. Don't do both, or each skill loads twice.

## License

MIT, see [LICENSE](LICENSE).
