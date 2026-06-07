# Playbook: Refactor

## Use when

Code structure must improve without changing external behavior.

## References

- Principles: `principles/clean-code.md`, `principles/architecture.md`, `principles/testing.md`
- Skills: `skills/refactoring/`, `skills/solid/`, `skills/design-patterns/`

## Workflow

1. Define the maintainability problem.
2. Identify behavior that must remain unchanged.
3. Establish safety checks or characterization tests.
4. Choose one small refactoring target.
5. Apply the change and run checks.
6. Repeat only while clarity improves.
7. Record any deferred behavior changes separately.
