# OpenClaw Harness Engineering Skill

An OpenClaw skill that applies Harness Engineering to complex agent tasks.

Instead of jumping straight from request to answer, this skill pushes the agent to:

- define a clear task contract
- gather only the context needed for the current step
- work in short `inspect -> act -> verify -> continue` loops
- control risk before high-impact actions
- verify results before declaring success

## What This Skill Is For

Use this skill when an agent is working on tasks that are:

- multi-step
- ambiguous
- high-risk
- easy to derail
- easy to finish too early without real validation

Typical use cases:

- coding and debugging
- repo migrations
- operational tasks
- technical research
- automation workflows

## Why Harness Engineering

Harness Engineering is the idea that strong agent performance does not come only from a better prompt or a better model.

A reliable agent also needs a good surrounding system:

- task definition
- context selection
- tool use
- validation
- risk gates
- closure and feedback loops

This skill packages those habits into a reusable OpenClaw skill.

It also adds hard gates around context pressure, validation, and closure so the agent is less free to "feel done" without evidence.

## Repository Layout

```text
.
|-- SKILL.md
|-- agents/
|   `-- openai.yaml
`-- references/
    |-- harness-improvements.md
    `-- harness-playbook.md
```

- `SKILL.md`: the main skill instructions
- `agents/openai.yaml`: UI and invocation metadata
- `references/harness-playbook.md`: extra checklist and playbook for longer or riskier tasks
- `references/harness-improvements.md`: persistent log of harness improvements learned from completed tasks

## Install

Copy or clone this repository into a skill folder that OpenClaw loads.

The repo root is the skill root, so the target folder should end up looking like:

```text
<your-openclaw-skills-dir>/harness-engineering/
  SKILL.md
  agents/openai.yaml
  references/harness-playbook.md
```

If you are cloning directly into a skills directory:

```bash
git clone https://github.com/Linsongrong/openclaw-harness-skill.git harness-engineering
```

## How To Use

Invoke it explicitly when you want the agent to slow down and work with stronger structure:

```text
Use $harness-engineering to handle this task with a clear task contract, focused context, and explicit verification.
```

Example prompts:

- `Use $harness-engineering to debug why this service passes unit tests but fails in staging.`
- `Use $harness-engineering to refactor this repo safely and show me what was verified.`
- `Use $harness-engineering to research this topic and separate evidence from assumptions.`

## Core Behaviors

This skill teaches the agent to:

- define the goal, deliverable, constraints, and stop condition
- avoid bloated context
- stop and compact when context pressure gets too high
- use tools for evidence instead of speculation
- verify with mandatory gates before claiming success
- be explicit about gaps and residual risk
- persist reusable lessons for the next run

## Notes

- This skill is intentionally generic so it can help a general-purpose agent across coding, research, and ops tasks.
- For longer or riskier work, the skill points the agent to `references/harness-playbook.md` for deeper checklists.

## Source Inspiration

- [OpenAI: Harness engineering](https://openai.com/index/harness-engineering/)
- [OpenAI: Unlocking the Codex harness](https://openai.com/index/unlocking-the-codex-harness/)
