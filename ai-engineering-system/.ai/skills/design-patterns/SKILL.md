---
name: design-patterns
description: Select and apply design patterns pragmatically. Use when recurring design forces appear, such as object creation, behavior variation, orchestration, adaptation, or decoupling.
---

# Design Patterns

## Purpose

Use known patterns as vocabulary for recurring design problems, not as mandatory structure.

## When to use

Use this skill when the same design force appears repeatedly or a pattern can simplify communication and implementation.

## Decision rules

- Start from the problem, not the pattern name.
- Prefer the simplest pattern that resolves the force.
- Keep pattern participants visible and named.
- Document why the pattern is useful in this context.

## Anti-patterns

- Applying patterns to look sophisticated.
- Introducing factories, strategies, or observers before variation exists.
- Hiding straightforward logic behind excessive indirection.
- Mixing multiple patterns without clear ownership.

## Checklist

- Describe the design force.
- List simpler alternatives.
- Choose the minimal pattern.
- Name participants.
- Verify the result is easier to change or test.
