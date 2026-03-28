---
name: agent-workflow-audit
description: Audit the current repository for agent workflow efficiency. Use when the user wants Codex to try setup, build, test, lint, run, or other obvious project commands and report where the agent instructions, AGENTS.md, README, or scripts are wasting context tokens, causing avoidable command exploration, or leaving important steps implicit. This skill optimizes the workflow and instructions for agents; it should not fix product code unless explicitly asked.
license: MIT
metadata:
  author: Diego Petrucci
  version: "1.0"
---

# Agent Workflow Audit

Audit whether a repository is efficient for an agent to operate in. Follow the instructions as written, try the expected commands, and report where the workflow wastes tokens, commands, or attention.

## Goal

Find ways to make the agent workflow more efficient, including:

- vague instructions that force the agent to guess
- commands that are too broad or imprecise
- unnecessary exploratory steps the repo could avoid by being explicit
- undocumented prerequisites, environment variables, or services
- mismatches between docs and actual scripts
- repeated context the agent should not need to rediscover

Do not fix application code or failing tests unless the user later asks. The primary output is an audit of the workflow and the instructions that shape agent behavior.

## Workflow

### On trigger

1. Read agent-facing instructions in priority order: `AGENTS.md`, user-supplied instructions, `README` files, package/tool manifests, and obvious config files.
2. Infer the intended workflow for the repo: install, environment setup, build, lint, test, run, or other standard checks.
3. Tell the user which commands you plan to try and why those commands are the most direct path.

### During execution

1. Run the documented commands first, exactly as written.
2. If a necessary step is undocumented but strongly implied by the repo, take the most conservative reasonable next step and label it as an inference and a workflow gap.
3. Keep a log of every inefficiency, including:
   - missing prerequisites
   - unclear command names or ordering
   - undocumented required tools, services, files, or environment variables
   - commands that fail because the instructions were incomplete
   - scripts whose purpose is not obvious
   - contradictory instructions across files
   - places where the agent had to search, infer, or retry unnecessarily
4. Distinguish clearly between:
   - an instruction or prompt-design problem
   - a command design problem
   - an environment problem
   - an actual code or test failure
5. If one command fails, continue with adjacent non-destructive checks when they can still reveal workflow inefficiencies.

### Reporting

Report the audit in four parts:

1. Commands attempted
2. What caused wasted tokens, wasted commands, or ambiguity
3. Concrete instruction improvements, with explicit commands and more direct wording when possible
4. Remaining assumptions or unknowns

## Behavior constraints

- Prefer explicit shell commands over vague prose when suggesting improvements.
- Do not silently invent setup steps; mark inferred steps as assumptions.
- Optimize for agent efficiency, not human-friendly narrative.
- Call out instructions that could be compressed without losing meaning.
- Do not fix product code just to get the workflow green.
- If the user later wants help improving docs or `AGENTS.md`, update those instructions directly.
