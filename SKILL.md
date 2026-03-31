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

### Context checkpoint

After each `inspect -> act -> verify` loop, estimate current context pressure from the active thread, loaded references, recent tool output, and the number of open branches.

- `< 40%`: continue executing.
- `40-60%`: compact working notes or trim the next step's context input before continuing.
- `> 60%`: compact immediately or split the remaining independent work to focused sub-agents. Do not continue by stacking more context into the same agent.

Treat context pressure above 40% as the start of a weaker operating zone. Do not wait for obvious failure before reducing load.

### 3. Choose an execution loop

Prefer short loops:

`inspect -> act -> verify -> continue`

Use tools for evidence, not speculation. If the task branches, finish or eliminate one branch before opening another.

If the work spans 3 or more independent subdomains, consider specialized sub-agents instead of forcing one generalist to carry the full task. Give each sub-agent the minimum context needed for its slice, keep its deliverable bounded, and keep the main agent responsible for coordination and final acceptance.

Use automatic failure detection inside the loop. Treat these triggers as hard stops:

- `Loop detection`: if 3 consecutive actions are the same type and produce no new evidence, pause and repair the harness before continuing.
- `Context overflow detection`: run the Context checkpoint after every execute-verify cycle and obey its thresholds.
- `Premature completion detection`: if the mandatory gates in `Section 4` are not passed, do not claim completion.

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

Mandatory gates. These are completion blockers, not suggestions:

- `Coding tasks`: run at least one dry-run, compile, test, or lint check that exercises the changed path before declaring completion.
- `File modification tasks`: inspect the diff and confirm only the intended scope changed.
- `Delete or overwrite tasks`: read the current target first and confirm the destructive action before executing it.

If a mandatory gate fails or cannot be executed, do not enter `Section 6` as a completed task. Report the task as blocked, partial, or needing approval instead.

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

Persist that learning:

- Append `Harness improvement for next time` to `{baseDir}/references/harness-improvements.md` in append mode after each completed or blocked task.
- If you discover a reusable failure mode or a reusable verification technique, update the relevant section in `{baseDir}/references/harness-playbook.md`.
- If running inside OpenClaw and a memory tool is available, mirror the highest-value lesson into the memory system.

If the environment does not allow writing, say that the persistence step is pending instead of silently skipping it.

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
- Prefer focused sub-agents with restricted context over a single generalist carrying full context.
- Prefer harness fixes over endlessly rewriting the prompt.

## Anti-Patterns

Avoid these failure modes:

- Starting work without a clear success condition.
- Reading everything before doing anything.
- Calling tools without a hypothesis for why they help.
- Stopping after editing without verification.
- Declaring success when mandatory gates were skipped.
- Claiming completion when key checks were skipped.
- Ignoring context pressure until the agent enters the Dumb Zone with hallucinations, looping, or malformed tool calls.
- Keeping 3 or more independent subdomains in one overloaded generalist instead of splitting bounded sub-agents.
- Using a large generic wall of instructions instead of structured docs and targeted context.
- Escalating to more agents or more model power before improving the harness.

## Reference

For checklists and reusable templates, read `{baseDir}/references/harness-playbook.md` when the task is long, ambiguous, or high risk. Persist reusable lessons in `{baseDir}/references/harness-improvements.md`.
