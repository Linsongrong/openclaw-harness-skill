# Harness Playbook

Load this file when the task is multi-step, ambiguous, risky, or likely to drift.

## 1. Task Contract Checklist

Answer these before doing substantial work:

- What is the real goal?
- What exact artifact or outcome should be delivered?
- What constraints matter most?
- Which tools are available?
- Which tools are missing or blocked?
- What counts as done?
- What could go wrong if the agent is careless?

## 2. Context Pack Checklist

Collect only what supports the next step:

- source files directly involved
- local docs or runbooks
- logs, traces, screenshots, or metrics
- external docs or official references
- environment facts such as OS, cwd, branch, or service state

Do not load broad background material unless it changes the decision.

## 3. Execution Loop Checklist

Use this loop:

1. Inspect the current state.
2. Form a narrow hypothesis.
3. Take the smallest useful action.
4. Verify what changed.
5. Decide whether to continue, branch, or stop.

If the loop repeats without new evidence, pause and change the harness:

- gather better context
- reduce scope
- pick a different tool
- ask for the missing permission
- rewrite the verification plan

Automatic triggers:

- `Loop detection`: if 3 consecutive actions are the same type and there is no new evidence, stop the loop and repair the harness before trying again.
- `Context overflow detection`: after each execute-verify cycle, estimate context pressure. Under `40%`, continue. At `40-60%`, compact notes or reduce the next context pack. Above `60%`, compact immediately or split the remaining independent work to focused sub-agents.
- `Premature completion detection`: before declaring completion, confirm every mandatory gate in the active task type has passed.

## 4. Verification Ladder

Prefer stronger evidence over weaker evidence:

1. Direct execution or test pass
2. Build or static analysis success
3. Output diff plus targeted inspection
4. Runtime evidence such as logs, traces, screenshots, or metrics
5. Source review only

Do not claim certainty higher than the strongest evidence you actually have.

## 5. Risk Ladder

If running inside OpenClaw, the host agent's `AGENTS.md` risk decision tree takes precedence. This ladder applies only when no such policy exists.

- Prefer reversible actions over irreversible ones.
- Read the current target before destructive writes, overwrites, or deletes.
- Preview or dry-run changes before high-impact execution whenever possible.
- Pause for approval before destructive, irreversible, or costly actions.

When in doubt, choose the safer reversible path.

## 6. Closure Template

Use this shape for your final internal check:

```text
Outcome:
Evidence:
Known gaps:
Risks still open:
Next best action:
Harness improvement for next time:
```

After closure:

- Append the final `Harness improvement for next time` to `{baseDir}/references/harness-improvements.md`.
- If the lesson is broadly reusable, fold it back into this playbook.
- If memory tooling exists, mirror the highest-value lesson there too.

## 7. Automatic Detection and Harness Repair

When a trigger fires, use the matching repair:

`Loop detection`

- tighten the task contract
- reduce scope to one hypothesis at a time
- switch tools or add a stronger evidence source
- rewrite the verification plan before resuming

`Context overflow detection`

- compact working notes
- reduce the next context pack
- split remaining independent work to focused sub-agents if pressure stays high
- stop adding new branches until pressure drops

`Premature completion detection`

- block completion
- run or re-run the missing mandatory gates
- downgrade the status to blocked or partial if the gates cannot pass

`Polished but weak output`

- require source-backed claims
- prefer tool output over fluent narration
- add a stronger verification step before resuming
