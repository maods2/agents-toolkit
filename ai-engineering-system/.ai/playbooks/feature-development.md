# Playbook: Feature Development

## Use when

A feature requires discovery, planning, implementation, and review across an existing workflow.

## References

- Principles: `principles/software-engineering.md`, `principles/clean-code.md`, `principles/architecture.md`, `principles/testing.md`
- Skills: `skills/workflow-scout/`, `skills/workflow-discovery/`, `skills/tdd/`, `skills/refactoring/`, `skills/clean-architecture/`

## Workflow

1. Workflow Scout: identify the bounded workflow, trigger, actors, outcome, and likely entry points.
2. Workflow Discovery: persist facts, business rules, architecture notes, assumptions, and questions.
3. Impact Analysis: list affected contracts, files, tests, data, dependencies, and risks.
4. Planning: define acceptance criteria and the smallest useful implementation slice.
5. TDD: add or update behavior tests before implementation where practical.
6. Implementation: make focused changes and keep boundaries explicit.
7. Review: run checks, compare against acceptance criteria, and persist follow-up discoveries.
