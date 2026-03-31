---
name: harness-engineering
description: Apply Harness Engineering to complex, multi-step, or high-risk agent work by building a task contract, selecting the right context, using tools deliberately, and verifying results before stopping. Use for coding, debugging, research, ops, migrations, or automation tasks where drift, weak validation, or premature completion are likely.
metadata: {"openclaw":{"always":true,"homepage":"https://openai.com/index/harness-engineering/"}}
---

# Harness Engineering

Use this skill to turn a vague request into a controlled execution loop. Treat the model as only one part of the system. Improve outcomes by shaping the task contract, context, tools, validation, and risk gates around the work.

## Operating Rule

Do not jump straight from request to answer. Build a lightweight harness first, then execute inside it.

For simple one-step tasks, keep the harness minimal. For long, risky, or ambiguous tasks, make the harness explicit in your working notes and keep updating it as the task evolves.

## Workflow

### 1. Define the task contract

Capture:

- the real goal
- the expected deliverable
- important constraints
- available tools and missing tools
- risk level
- the stop condition

State assumptions only when they matter. If the task can be completed by direct inspection, do not over-plan it.

### 2. Build the minimum useful context

- Gather only the files, docs, logs, APIs, or web sources needed for the current step.
- Prefer structured sources over long free-form memory.
- Summarize findings into short working notes before continuing.
- Avoid opening many branches at once unless they are truly independent.

### 3. Choose an execution loop

Prefer short loops:

`inspect -> act -> verify -> continue`

Use tools for evidence, not speculation. If the task branches, finish or eliminate one branch before opening another. Use sub-agents only for bounded, non-overlapping side tasks when the runtime supports them.

### 4. Verify before declaring success

Run the strongest cheap validation available:

- tests
- lint
- build
- search
- diff review
- screenshots
- logs
- metrics
- source cross-checks

If you cannot verify, say exactly what is unverified and why. Do not let "looks right" replace evidence.

### 5. Control risk

- Slow down before destructive, irreversible, or high-cost actions.
- Ask for approval when the runtime or policy requires it.
- Prefer reversible changes and keep a clear trail of what changed.
- Treat third-party skills, scripts, and remote systems as untrusted until checked.

### 6. Close the loop

Summarize:

- outcome
- evidence
- remaining risk
- the next best action

If repeated friction came from poor context, weak tooling, or missing checks, name the harness improvement that would help next time.

## Response Shape

When the task is substantial, organize your internal execution around this compact frame:

```text
Task contract: goal | deliverable | constraints | stop condition
Context pack: files/docs/logs/web sources actually needed
Execution plan: next 1-3 actions only
Verification plan: how success will be checked
Risk gates: actions that need extra care or approval
```

Do not dump this template to the user mechanically. Use it to guide your own execution and surface only the parts that help the user.

## Default Behaviors

- Prefer evidence over intuition.
- Prefer narrow context over bloated context.
- Prefer iterative verification over long uninterrupted execution.
- Prefer explicit assumptions over hidden guesses.
- Prefer reversible actions over destructive ones.
- Prefer harness fixes over endlessly rewriting the prompt.

## Anti-Patterns

Avoid these failure modes:

- Starting work without a clear success condition.
- Reading everything before doing anything.
- Calling tools without a hypothesis for why they help.
- Stopping after editing without verification.
- Claiming completion when key checks were skipped.
- Using a large generic wall of instructions instead of structured docs and targeted context.
- Escalating to more agents or more model power before improving the harness.

## Reference

For checklists and reusable templates, read `{baseDir}/references/harness-playbook.md` when the task is long, ambiguous, or high risk.
