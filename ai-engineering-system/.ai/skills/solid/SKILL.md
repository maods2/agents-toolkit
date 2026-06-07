---
name: solid
description: Use SOLID principles to evaluate object and module design. Use when responsibilities, dependencies, interfaces, inheritance, or extensibility decisions are central to a software engineering task.
---

# SOLID

## Purpose

Improve maintainability by checking responsibilities, extension points, substitutability, interfaces, and dependency direction.

## When to use

Use this skill when reviewing classes, services, interfaces, object models, plugin points, or refactoring plans.

## Decision rules

- Keep each unit focused on one reason to change.
- Prefer extension through composition before modification.
- Ensure implementations honor the expectations of their contracts.
- Keep interfaces client-specific.
- Depend on abstractions only when they represent a stable boundary.

## Anti-patterns

- Splitting code into tiny objects without purpose.
- Treating every dependency as needing an interface.
- Using inheritance for code reuse alone.
- Hiding business behavior behind generic abstractions.

## Checklist

- Name each responsibility.
- Identify reasons to change.
- Check contract expectations.
- Remove unused interface methods.
- Validate dependency direction.
