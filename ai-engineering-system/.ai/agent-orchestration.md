# Agent Orchestration Model

## Purpose

This document defines the workflow-centric orchestration model for the AI Engineering System.

Agents in this system represent stages of software engineering work, not seniority levels, job titles, programming languages, or role-playing personas. The model is intentionally simple, Markdown-based, vendor-neutral, and portable across OpenAI Codex, Claude Code, Cursor, and GitHub Copilot.

## Core Workflow Agents

| Agent | Primary question | Primary output |
| --- | --- | --- |
| Workflow Scout | Where does this workflow live? | `navigation-map.md` |
| Workflow Discovery | How does this workflow behave and why? | `.ai/discoveries/<workflow-name>/` |
| Impact Analysis | What will this change affect? | `impact-analysis.md` |
| Planner | How should implementation proceed? | `plan.md` |
| Reviewer | Is the implementation ready? | `review-report.md` |
| Knowledge Curator | What knowledge changed? | `knowledge-review.md` and updated knowledge |

## New Feature Flow

```text
User Request
↓
Workflow Scout
↓
Workflow Discovery
↓
Impact Analysis
↓
Planner
↓
Playbook Selection
↓
Skill Loading
↓
Implementation
↓
Reviewer
↓
Knowledge Curator
↓
Knowledge Updated
```

### New Feature Notes

- Use Workflow Scout when the feature area is not already obvious.
- Use Workflow Discovery when durable workflow knowledge is missing, stale, incomplete, or too shallow for the feature risk.
- Run Impact Analysis before implementation to identify affected files, tests, services, dependencies, integration points, and risks.
- The Planner selects the feature or new-feature playbook and the minimum relevant skills.
- Implementation follows the plan and updates tests with behavior.
- Reviewer validates architecture, design, complexity, coupling, tests, and knowledge drift.
- Knowledge Curator updates discoveries, global knowledge, and ADRs when needed.

## Bug Fix Flow

```text
User Request
↓
Workflow Scout
↓
Impact Analysis
↓
Planner
↓
Bug Fix Playbook
↓
Implementation
↓
Reviewer
↓
Knowledge Curator
```

### Bug Fix Notes

- Start with Workflow Scout when the failing path or owning workflow is unknown.
- Workflow Discovery is optional for small defects when existing knowledge is sufficient, but it should run if the workflow behavior is unclear.
- Impact Analysis should identify regression surface area and affected tests before coding.
- The Planner should select the bug-fix playbook and define the expected regression test.
- Knowledge Curator runs after review when the fix changes documented behavior, assumptions, or business rules.

## Refactor Flow

```text
User Request
↓
Workflow Discovery
↓
Impact Analysis
↓
Refactor Playbook
↓
Implementation
↓
Reviewer
↓
Knowledge Curator
↓
ADR Generation (if needed)
```

### Refactor Notes

- Refactors require understanding current behavior before changing structure.
- Workflow Discovery should establish the behavior that must remain stable.
- Impact Analysis should identify coupling, tests, data flow, and integration risks.
- The refactor playbook guides safe sequencing and validation.
- Reviewer should focus on behavior preservation, complexity reduction, coupling reduction, and test adequacy.
- Generate an ADR when the refactor introduces a significant architectural decision.

## Agent Selection Rules

### Workflow Scout

Run Workflow Scout when:

- The relevant workflow is unknown.
- The repository is large and the agent needs a fast navigation map.
- The user names a feature but not its code location.
- Existing discoveries do not identify entrypoints, services, tests, or integrations.

Skip Workflow Scout when:

- The task explicitly targets a known file or small local change.
- A current `navigation-map.md` or discovery already identifies the relevant path.

### Workflow Discovery

Run Workflow Discovery when:

- Workflow knowledge does not exist.
- Existing workflow knowledge is outdated, incomplete, or too shallow for the change.
- The task changes behavior, business rules, architecture, or integrations in a workflow.
- A refactor requires behavior preservation across a bounded workflow.

Skip or defer Workflow Discovery when:

- The change is trivial and already covered by accurate discoveries.
- The task is purely mechanical and does not require workflow understanding.

### Impact Analysis

Run Impact Analysis before every non-trivial change.

A change is non-trivial when it may affect:

- Runtime behavior.
- Public or internal contracts.
- Persistence or migrations.
- Tests or fixtures.
- API routes, events, jobs, or integrations.
- Architecture boundaries or dependencies.
- Business rules, permissions, validations, or state transitions.

### Planner

Run Planner before implementation.

The Planner must:

- Select the relevant playbook.
- Identify required skills.
- Define implementation steps.
- Define testing strategy.
- Define validation strategy.

The Planner must never implement code.

### Reviewer

Run Reviewer before completion.

Reviewer must validate:

- Architecture quality.
- SOLID and design quality.
- Complexity and coupling.
- Test coverage and validation evidence.
- Knowledge drift and ADR needs.

### Knowledge Curator

Run Knowledge Curator after implementation and review.

Knowledge Curator should update artifacts when implementation changes:

- Workflow steps, triggers, actors, outcomes, or failure modes.
- Architecture components, boundaries, dependencies, integrations, or data flow.
- Business rules, validations, permissions, thresholds, or state transitions.
- Assumptions, constraints, or open questions.
- Domain terminology or glossary concepts.

## Knowledge Lifecycle

```text
Discover
↓
Persist
↓
Reuse
↓
Update
```

### Discover

Agents investigate the smallest workflow necessary for the task. Discovery should focus on evidence-backed behavior, architecture, business rules, assumptions, open questions, and risks.

### Persist

Reusable findings are saved as Markdown artifacts:

- Repository-wide knowledge goes in `.ai/knowledge/`.
- Workflow-specific knowledge goes in `.ai/discoveries/<workflow-name>/`.
- Task-local notes go in `.ai/workspaces/<task-name>/`.

### Reuse

Discoveries are reusable assets. Before rediscovering code, agents should check whether a relevant discovery, navigation map, workspace, ADR, or knowledge file already exists.

Avoid rediscovering the same workflow whenever possible. Reuse makes the system scale across large codebases because each task starts from accumulated context instead of a blank slate.

### Update

Knowledge changes when implementation changes behavior, architecture, rules, assumptions, or terminology. The Knowledge Curator updates only affected artifacts and preserves unrelated context.

## Orchestration Principles

1. Keep agents workflow-centric rather than persona-centric.
2. Prefer bounded context over whole-repository ingestion.
3. Produce durable Markdown artifacts that humans can review.
4. Reuse existing discoveries before searching again.
5. Separate facts, assumptions, and open questions.
6. Run Impact Analysis before risky changes.
7. Plan before implementation.
8. Review before completion.
9. Curate knowledge after implementation so future work starts smarter.
