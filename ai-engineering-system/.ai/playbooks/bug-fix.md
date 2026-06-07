# Playbook: Bug Fix

## Use when

Existing behavior is incorrect, unstable, or inconsistent with requirements.

## References

- Principles: `principles/software-engineering.md`, `principles/testing.md`
- Skills: `skills/workflow-scout/`, `skills/tdd/`, `skills/refactoring/`

## Workflow

1. Reproduce or characterize the bug.
2. Record expected behavior and observed behavior.
3. Identify the smallest affected workflow area.
4. Add a regression test when practical.
5. Fix the root cause with the smallest safe change.
6. Run relevant checks.
7. Document unresolved risk or follow-up work.
