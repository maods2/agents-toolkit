---
name: knowledge-curation
description: Keep repository knowledge synchronized with implementation changes. Use after features, bug fixes, refactors, architecture changes, or pull request preparation when Codex must compare git diffs, implementation plans, PR descriptions, discoveries, and knowledge artifacts to detect stale documentation, new business rules, new assumptions, new domain concepts, architecture changes, and required ADRs.
---

# Knowledge Curation

## Purpose

Maintain accurate repository knowledge by updating only the artifacts impacted by implementation changes.

## When to use

Use this skill after a code change, configuration change, refactor, feature implementation, bug fix, architecture change, or PR draft when knowledge artifacts may have become stale.

## Required inputs

Prefer these inputs when available:

- Workspace context.
- Existing discovery artifacts under `.ai/discoveries/`.
- Existing knowledge artifacts under `.ai/knowledge/`.
- Git diff.
- Implementation plan.
- Pull request description.

## Decision rules

- Treat code, tests, configuration, implementation plans, and PR descriptions as evidence to compare against knowledge artifacts.
- Update only files connected to the changed workflow, business rule, assumption, domain concept, or architecture decision.
- Add business rules only when the diff or plan clearly supports them.
- Record uncertain interpretations as assumptions or open questions.
- Generate ADRs only for significant architectural decisions.
- Prefer incremental edits over rewrites.
- Preserve historical knowledge unless it is explicitly superseded; when superseding, mark the reason.

## Staleness signals

Look for changes to:

- Workflow triggers, actors, steps, outcomes, or error paths.
- Validations, permissions, thresholds, calculations, state transitions, or policies.
- APIs, events, commands, schemas, integrations, adapters, queues, or storage ownership.
- Dependency direction, module boundaries, bounded contexts, deployment topology, or sync/async behavior.
- New domain names, aliases, acronyms, entities, metrics, or lifecycle states.
- New operational constraints or assumptions introduced by tests, code comments, configuration, or plans.

## Output rules

Produce a `knowledge-review.md` report using `templates/knowledge-review.md`.

Update only impacted artifacts, commonly:

- `workflow.md`
- `architecture.md`
- `business-rules.md`
- `assumptions.md`
- `open-questions.md`
- `glossary.md`
- `business-domain.md`
- `architecture-principles.md`

For major architectural decisions, create `knowledge/adr/ADR-XXXX-title.md` using `templates/adr.md`.

## Anti-patterns

- Scanning every discovery folder when the affected workflow is known.
- Rewriting knowledge files for style only.
- Inventing business rules to make documentation feel complete.
- Deleting older context instead of marking it superseded.
- Treating implementation guesses as confirmed domain knowledge.
- Creating ADRs for minor implementation details.
- Updating unrelated glossary or discovery files because names are similar.

## Checklist

- Identify changed behavior, contracts, data flow, dependencies, and domain terms.
- Select only impacted discovery and knowledge artifacts.
- Compare existing statements against evidence from the diff, plan, and PR description.
- Update stale facts incrementally.
- Add new business rules only with evidence.
- Add assumptions and open questions when evidence is incomplete.
- Generate an ADR if the architecture change is significant.
- Write the knowledge review report.
- Verify every modified file has a clear reason tied to the change.
