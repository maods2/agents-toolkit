---
name: workflow-scout
description: Quickly map a workflow or feature area without scanning an entire repository. Use at the beginning of discovery to identify entry points, actors, data flow, files, and unknowns.
---

# Workflow Scout

## Purpose

Create a lightweight first map of a workflow so deeper discovery can focus on the right area.

## When to use

Use this skill before workflow discovery, impact analysis, bug fixes, feature planning, or architecture review in an unfamiliar area.

## Decision rules

- Search for named entry points and user-facing terms first.
- Follow the narrow path from trigger to outcome.
- Capture evidence with file references when available.
- Stop when enough context exists for targeted discovery.

## Anti-patterns

- Scanning the entire repository by default.
- Treating guesses as facts.
- Ignoring business terminology.
- Expanding scope before naming the workflow boundary.

## Checklist

- Name the workflow.
- Identify trigger, actors, and outcome.
- List likely entry points.
- Trace core data flow.
- Record assumptions and open questions.
- Recommend next discovery targets.
