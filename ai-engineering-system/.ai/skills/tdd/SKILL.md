---
name: tdd
description: Guide test-first development for software changes. Use when implementing new behavior, fixing bugs, defining acceptance criteria, or protecting business rules with regression tests.
---

# Test-Driven Development

## Purpose

Drive implementation from expected behavior using short red-green-refactor cycles.

## When to use

Use this skill when behavior can be specified before or during implementation and tests can provide meaningful feedback.

## Decision rules

- Write the smallest failing test that captures the behavior.
- Make it pass with the simplest implementation.
- Refactor only after the test is green.
- Keep tests focused on observable behavior.
- Add edge cases after the main behavior is stable.

## Anti-patterns

- Writing broad tests that fail for many unrelated reasons.
- Testing private implementation details.
- Refactoring while tests are red.
- Treating snapshots as a substitute for assertions.

## Checklist

- Define expected behavior.
- Write or update a failing test.
- Run the relevant test.
- Implement the smallest fix.
- Run the full relevant test set.
- Refactor and rerun tests.
