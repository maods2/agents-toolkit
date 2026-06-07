---
name: clean-architecture
description: Apply dependency direction, boundary design, and use-case-centric structure for maintainable software systems. Use when designing modules, reviewing architecture, separating business rules from frameworks, or reducing coupling.
---

# Clean Architecture

## Purpose

Structure systems so business rules remain independent from delivery mechanisms, databases, frameworks, and external services.

## When to use

Use this skill when a task involves module boundaries, dependency direction, use cases, adapters, ports, or long-term maintainability.

## Decision rules

- Put business policies near the center of the design.
- Make dependencies point toward stable business rules.
- Hide frameworks and external systems behind adapters.
- Keep interface contracts small and use-case-oriented.

## Anti-patterns

- Creating layers without a real boundary.
- Letting database schemas define the domain model.
- Passing framework objects through core business logic.
- Adding abstractions before volatility is understood.

## Checklist

- Identify core business rules.
- Identify external mechanisms.
- Define input and output boundaries.
- Check dependency direction.
- Record trade-offs and assumptions.
