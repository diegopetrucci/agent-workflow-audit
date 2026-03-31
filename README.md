# Agent Workflow Audit

An [agent skill](https://agentskills.io/home) that stress-tests a repo's agent-facing workflow and reports where instructions, commands, or context are wasteful, ambiguous, or missing.

## What it does

When you want to optimize a repository for agent execution, this skill follows the documented workflow and looks for waste. It:

- Reads `AGENTS.md`, `README`, and other agent-facing instructions
- Tries the documented install, build, test, lint, and run commands
- Flags vague instructions, redundant steps, and avoidable command exploration
- Distinguishes token waste, command waste, environment gaps, and actual code failures
- Recommends more explicit, lower-friction instructions without fixing product code

## Installation

### As a Claude Code plugin

```shell
/plugin marketplace add diegopetrucci/ai-agents-skills
/plugin install agent-workflow-audit@diegopetrucci-claude-plugins
```

### As a skill

```bash
npx skills add https://github.com/diegopetrucci/agent-workflow-audit --skill agent-workflow-audit
```

## Usage

Trigger the skill when you want to optimize the agent workflow for the current repository:

- **Claude Code:** `/agent-workflow-audit`
- Or say: "audit this repo for agent waste", "optimize the agent workflow", or "try the build and test flow and report unclear instructions"

## More Skills Like This

Found this skill useful? Browse all my hand-crafted ones in the [AI Agents skills](https://github.com/diegopetrucci/ai-agents-skills) repo.

## License

MIT
