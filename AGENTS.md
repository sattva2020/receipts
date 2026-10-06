# Agent guide

You are an agent asked to install or work on [receipts](https://github.com/sattva2020/receipts). The canonical skill is `skills/receipts/SKILL.md`. Everything else is packaging.

## Install for the user

Pick the runtime you are running in. Do only that one.

| Runtime | What to do |
| --- | --- |
| Claude Code | Run `claude plugin marketplace add sattva2020/receipts`, then `claude plugin install receipts@receipts`. Tell the user to restart Claude Code. |
| Claude Code (no plugins) | Copy `skills/receipts/` to `~/.claude/skills/receipts/`. |
| Codex | Copy `skills/receipts/` to `~/.codex/skills/receipts/` (or the project's `.agents/skills/`). |
| Cursor | Copy `.cursor/skills/receipts/` into the project's `.cursor/skills/`. |
| Anything that reads AGENTS.md / CLAUDE.md | Append the block from "Always-on snippet" in `README.md` to the project's instruction file. |

After installing, report with receipts: show the command you ran and its output, and list anything you could not verify.

## Repository map

| Path | Purpose |
| --- | --- |
| `skills/receipts/SKILL.md` | Source of truth for the rules. |
| `.cursor/skills/receipts/SKILL.md` | Mirror for Cursor. Keep identical to the canonical file. |
| `.claude-plugin/` | Claude Code plugin and marketplace manifests. |
| `evals/cases.md` | Scenarios for checking that the skill changes behavior. |

## Changing the rules

Edit `skills/receipts/SKILL.md`, then copy it over the Cursor mirror. Check with `diff skills/receipts/SKILL.md .cursor/skills/receipts/SKILL.md`.
