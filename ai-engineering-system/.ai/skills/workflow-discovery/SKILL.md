---
name: workflow-discovery
description: Document one workflow or feature area in depth. Use when an agent must understand business rules, architecture, assumptions, risks, and implementation touchpoints before making changes.
---

# Workflow Discovery

## Purpose

Build a persisted understanding of a bounded workflow or feature area.

## When to use

Use this skill after workflow scout or whenever a change requires reliable context about an existing workflow.

## Decision rules

- Keep discovery scoped to one workflow.
- Separate facts, assumptions, and questions.
- Capture business rules explicitly.
- Store output under discoveries/<workflow-name>/.
- Prefer evidence-linked notes over broad summaries.

## Anti-patterns

- Creating a full repository inventory.
- Mixing implementation plans into discovery facts.
- Leaving business rules implicit.
- Failing to record uncertainty.

## Checklist

- Create the discovery folder.
- Fill workflow, architecture, business rules, assumptions, and open questions.
- Link evidence where possible.
- Identify change risks.
- Summarize recommended next steps.
