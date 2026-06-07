---
name: python
description: Apply Python-specific engineering practices. Use when designing, implementing, testing, or reviewing Python backend, data, automation, or research code.
---

# Python Engineering

## Purpose

Keep Python code explicit, typed where useful, testable, and maintainable.

## When to use

Use this skill for Python modules, APIs, scripts, services, notebooks converted to code, or package structure decisions.

## Decision rules

- Prefer clear functions and modules over clever metaprogramming.
- Use type hints for public boundaries and non-obvious data structures.
- Isolate IO from pure logic.
- Keep dependency management explicit.
- Make scripts safe to rerun when possible.

## Anti-patterns

- Hiding errors with broad exception handling.
- Putting production logic only in notebooks.
- Using global mutable state as workflow context.
- Overusing dynamic imports or reflection.

## Checklist

- Identify runtime and packaging assumptions.
- Define module boundaries.
- Add or update focused tests.
- Check typing or linting when available.
- Document operational entry points.
