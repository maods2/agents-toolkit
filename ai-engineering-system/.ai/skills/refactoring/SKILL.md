---
name: refactoring
description: Improve code structure without changing behavior. Use when simplifying code, removing duplication, clarifying names, improving boundaries, or preparing for a feature safely.
---

# Refactoring

## Purpose

Change internal structure while preserving external behavior and confidence.

## When to use

Use this skill when the goal is maintainability, readability, modularity, or preparation for a future change.

## Decision rules

- Characterize current behavior before changing structure.
- Prefer small, reversible transformations.
- Separate behavior changes from structural changes.
- Keep commits and notes focused.
- Stop when the code is clearer for the next task.

## Anti-patterns

- Refactoring without tests or characterization.
- Mixing feature work with broad cleanup.
- Renaming without improving meaning.
- Creating abstractions for hypothetical future needs.

## Checklist

- Identify the behavior to preserve.
- Establish safety checks.
- Choose one refactoring target.
- Apply a small transformation.
- Run checks.
- Document any remaining risk.
