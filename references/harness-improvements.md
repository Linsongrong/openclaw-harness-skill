# Harness Improvements Log

Append one short entry after each completed or blocked task.

Use this template:

```text
## YYYY-MM-DD - Task name
Outcome:
Evidence:
Harness improvement for next time:
Reusable failure mode or verification trick:
Memory synced:
```

Keep entries concise and reusable. Prefer one improvement per entry over a long narrative dump.

## 2026-03-31 - Harden harness skill gates
Outcome:
Clarified automatic-detection rules as hard stops, mirrored mandatory verification gates into the playbook, tightened closure persistence wording, and normalized section references to ASCII so the gate references stay readable across terminals.
Evidence:
Updated `SKILL.md`, `references/harness-playbook.md`, and this log, then ran `quick_validate.py` and got `Skill is valid!`
Harness improvement for next time:
Prefer ASCII section references such as `Section 4` when a skill must survive mixed terminal encodings.
Reusable failure mode or verification trick:
When converting guidance into hard gates, mirror the same completion blockers in both the main skill and the playbook and preserve broader skipped-check guardrails so closure logic cannot drift.
Memory synced:
Not available in this environment.
