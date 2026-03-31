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

## 4. Verification Ladder

Prefer stronger evidence over weaker evidence:

1. Direct execution or test pass
2. Build or static analysis success
3. Output diff plus targeted inspection
4. Runtime evidence such as logs, traces, screenshots, or metrics
5. Source review only

Do not claim certainty higher than the strongest evidence you actually have.

## 5. Risk Ladder

Treat actions differently by impact:

- Read-only inspection: usually safe
- Local reversible edits: usually safe with verification
- External writes or remote side effects: use extra care
- Destructive, irreversible, or costly actions: stop for approval when required

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

## 7. Common Fixes When the Agent Struggles

If the agent keeps drifting:

- tighten the task contract
- cut down the context pack
- shorten the execution loop

If the agent stops too early:

- make verification mandatory
- define a clearer stop condition

If the agent thrashes:

- reduce branching
- switch to one hypothesis at a time
- add a stronger evidence source

If the agent produces polished but weak answers:

- require source-backed claims
- prefer tool output over fluent narration
