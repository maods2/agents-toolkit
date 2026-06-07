# AI Engineering System

A portable, Markdown-first operating system for agent-assisted software engineering.

The AI Engineering System helps coding agents work like careful engineering teammates: they start with principles, discover only the relevant workflow, plan from evidence, implement with the right skills, review the result, and keep project knowledge synchronized for the next contributor.

It is designed to sit inside a real software project as a lightweight `.ai/` directory. The artifacts are intentionally plain Markdown so they can be read by humans, reused by different agent tools, reviewed in pull requests, and improved over time.

## Why this exists

Most agent workflows fail for one of two reasons:

1. **Too little context**: the agent changes code before understanding the business workflow, existing architecture, tests, risks, and conventions.
2. **Too much context**: the agent attempts to ingest the whole repository and loses focus on the specific workflow that matters.

This system takes a different approach: **bounded, durable context**.

Agents should not rediscover the same facts every time. They should build up reusable knowledge assets, keep those assets close to the codebase, and use them to make future work faster and safer.

## Repository structure

```text
.ai/
├── AGENTS.md                 # Default operating instructions for agents
├── agents/                   # Reusable agent roles, such as Knowledge Curator
├── principles/               # Always-loaded engineering rules
├── skills/                   # Reusable specialized capabilities
├── playbooks/                # End-to-end task workflows
├── templates/                # Standard artifact formats
├── knowledge/                # Durable repository-wide context
├── discoveries/              # Durable workflow-specific discoveries
└── workspaces/               # Temporary task-specific working notes
```

## Core Concepts

The system is organized around a small set of concepts that layer from broad guidance to task-specific execution.

### Principles

**Principles are always-loaded engineering rules.**

They capture the standards the agent should follow regardless of the task. Principles are intentionally concise and stable. They guide judgment when the agent is designing, editing, testing, reviewing, or documenting code.

Examples:

- Clean Code
- Architecture Principles
- Software Engineering Principles
- Testing Standards

Principles answer questions such as:

- What does maintainable code look like here?
- How should dependencies be managed?
- What level of test coverage is expected?
- What tradeoffs are acceptable?

### Skills

**Skills are reusable specialized knowledge.**

A skill is loaded when a task needs a specific capability. Skills provide decision rules, checklists, and execution guidance without forcing every task to carry every possible instruction.

Examples:

- TDD
- Design Patterns
- Clean Architecture
- Refactoring
- Workflow Scout
- Workflow Discovery

Skills answer questions such as:

- How should this feature be developed test-first?
- Which design patterns are appropriate for this problem?
- How do we safely refactor this code?
- How do we discover a workflow without scanning the entire repository?

### Playbooks

**Playbooks are task workflows.**

A playbook composes principles, skills, templates, and agent roles into an execution path for a particular type of work.

Examples:

- New Feature
- Bug Fix
- Refactor
- Architecture Review
- Research Feature
- Knowledge Maintenance

Playbooks answer questions such as:

- What steps should the agent follow for this kind of task?
- Which skills are likely required?
- Which artifacts should be produced?
- What should be true before implementation starts?

### Knowledge

**Knowledge is repository-wide durable context.**

Knowledge files store information that should survive beyond a single task and apply across many workflows. They should be treated as part of the repository, not as private agent memory.

Examples:

- Business Domain
- Glossary
- Architecture Principles
- Architecture Decision Records (ADRs)

Knowledge answers questions such as:

- What does this business term mean?
- What architectural constraints must all features respect?
- Which decisions have already been made and why?
- Which assumptions are accepted across the project?

### Discoveries

**Discoveries are workflow-specific durable knowledge.**

A discovery captures what the agent learned about a bounded workflow or feature area. Discoveries are more specific than global knowledge and should be reused whenever future work touches the same workflow.

Examples:

```text
.ai/discoveries/customer-onboarding/
.ai/discoveries/payment-processing/
.ai/discoveries/inventory-reconciliation/
```

A discovery commonly includes:

```text
workflow.md
architecture.md
business-rules.md
assumptions.md
open-questions.md
```

Discoveries answer questions such as:

- Where does this workflow start and end?
- Which services, repositories, APIs, jobs, or events participate?
- What business rules govern the workflow?
- What assumptions or open questions remain?
- What risks should future work consider?

### Workspaces

**Workspaces are temporary feature-specific context.**

A workspace stores planning notes, impact analysis, implementation plans, review notes, and knowledge-review reports for one task. Workspaces are useful during execution but should remain small and task-focused.

Examples:

```text
.ai/workspaces/add-customer-validation/
.ai/workspaces/fix-payment-timeout/
.ai/workspaces/refactor-reporting-adapters/
```

Workspaces answer questions such as:

- What is the exact task goal?
- Which files are impacted?
- What is the implementation plan?
- What risks were reviewed?
- What knowledge updates were made after implementation?

### Agents

**Agents are reusable roles with responsibilities.**

Agent role definitions describe how a specialized agent should behave. For example, the Knowledge Curator is responsible for comparing implementation changes against existing knowledge and updating only the artifacts that are affected.

Agents answer questions such as:

- Who reviews whether documentation is stale?
- Who checks whether an ADR is needed?
- Who keeps discoveries and knowledge synchronized with code changes?

## Recommended Agent Workflow

Use this workflow when applying the system to a real software engineering task.

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
Playbook
↓
Skills
↓
Implementation
↓
Reviewer
↓
Knowledge Curator
↓
Updated Knowledge
```

### 1. User Request

The user describes the change, bug, refactor, architecture question, or research goal.

The agent should clarify the task boundary before editing code. A good request is converted into a named workflow or feature area, such as `customer-onboarding` or `payment-processing`.

### 2. Workflow Scout

The Workflow Scout quickly maps the relevant area without scanning the whole repository.

Responsibilities:

- Identify the workflow name, trigger, actors, and outcome.
- Find likely entry points.
- Locate services, repositories, handlers, jobs, commands, API routes, or UI screens.
- Identify existing tests.
- Record assumptions and open questions.
- Recommend where deeper discovery should focus.

The goal is not to understand everything. The goal is to find the narrow path from trigger to outcome.

### 3. Workflow Discovery

Workflow Discovery documents the bounded workflow in more detail and persists it under `.ai/discoveries/<workflow-name>/`.

Responsibilities:

- Describe the workflow steps.
- Map architecture and data flow.
- Capture business rules explicitly.
- Separate facts from assumptions.
- List open questions and risks.
- Link to evidence when possible.

This turns one-time investigation into a reusable asset.

### 4. Impact Analysis

Impact Analysis connects discovery to the requested change.

Responsibilities:

- Identify impacted files, interfaces, tests, data contracts, migrations, jobs, or integrations.
- Assess risks and edge cases.
- Identify backwards compatibility concerns.
- Identify documentation or ADR impacts.
- Recommend validation steps.

Impact analysis prevents implementation from becoming guesswork.

### 5. Planner

The Planner converts the request and impact analysis into an implementation plan.

Responsibilities:

- Break work into small, reviewable steps.
- Choose the relevant playbook.
- Identify required skills.
- Specify test strategy.
- Call out sequencing constraints.
- Note rollback or migration considerations when relevant.

### 6. Playbook

The selected playbook provides the task workflow.

Responsibilities:

- Define the expected execution path for the task type.
- Ensure required artifacts are created or updated.
- Keep the agent from skipping discovery, tests, review, or knowledge updates.

For example, a new feature should generally follow the New Feature playbook, while a behavior regression should follow the Bug Fix playbook.

### 7. Skills

Skills are loaded only when needed by the task.

Responsibilities:

- Provide specialized guidance for implementation.
- Prevent generic coding behavior when a domain-specific approach is needed.
- Supply checklists for practices such as TDD, refactoring, clean architecture, or design patterns.

### 8. Implementation

Implementation changes code, tests, configuration, and task-local documentation according to the plan.

Responsibilities:

- Make the smallest effective code change.
- Follow loaded principles and skills.
- Update tests alongside behavior.
- Keep workspace notes current when the plan changes.
- Avoid unrelated refactors.

### 9. Reviewer

The Reviewer checks the result before the task is considered complete.

Responsibilities:

- Compare implementation against the request and plan.
- Review tests, edge cases, and failure modes.
- Check architecture boundaries and dependencies.
- Look for unintended behavior changes.
- Confirm the task is ready for knowledge curation.

### 10. Knowledge Curator

The Knowledge Curator keeps documentation synchronized with implementation.

Responsibilities:

- Compare the git diff and implementation summary against existing discoveries and knowledge.
- Update affected workflow discoveries.
- Update global knowledge when new domain rules, glossary terms, or architecture constraints are introduced.
- Create an ADR for significant architecture decisions.
- Produce a knowledge-review report in the task workspace.

### 11. Updated Knowledge

The task ends with durable, reusable knowledge.

Future agents and contributors should be able to reuse the updated `.ai/knowledge/` and `.ai/discoveries/` artifacts instead of repeating the same investigation.

## Example: Adding a New Feature

Feature request:

> Add international customer validation during onboarding.

This example shows how a real task moves through the system.

### Step 1: Create a workspace

Create a task workspace:

```text
.ai/workspaces/customer-validation/
```

Suggested initial files:

```text
.ai/workspaces/customer-validation/request.md
.ai/workspaces/customer-validation/impact-analysis.md
.ai/workspaces/customer-validation/implementation-plan.md
.ai/workspaces/customer-validation/knowledge-review.md
```

The workspace captures task-local context: the request, assumptions, impacted files, plan, review notes, and post-implementation knowledge updates.

### Step 2: Run Workflow Scout

Use the Workflow Scout skill to quickly map customer onboarding.

Expected output:

- Entrypoints, such as onboarding API routes, UI forms, commands, events, or background jobs.
- Services, such as customer onboarding services, validation services, and identity or address verification clients.
- Repositories, such as customer, address, country, tax, or compliance persistence components.
- Tests, such as onboarding unit tests, integration tests, contract tests, and validation fixtures.
- Unknowns, such as country-specific requirements or incomplete domain terminology.

Example workspace note:

```text
Workflow: customer-onboarding
Trigger: New customer submits onboarding form
Outcome: Customer account is created, rejected, or marked pending review
Likely entrypoints:
- Onboarding controller / route
- Customer creation service
- Customer validation module
- Existing onboarding tests
Open questions:
- Which countries are supported at launch?
- Are validation failures blocking or reviewable?
- Are country-specific rules configured or hard-coded today?
```

### Step 3: Run Workflow Discovery

Create or update the workflow discovery:

```text
.ai/discoveries/customer-onboarding/
├── workflow.md
├── architecture.md
├── business-rules.md
└── assumptions.md
```

The discovery should capture facts about the current workflow before implementation begins.

Example contents:

- `workflow.md`: onboarding trigger, actors, steps, success states, failure states, and handoffs.
- `architecture.md`: relevant modules, dependencies, validation flow, data ownership, and external integrations.
- `business-rules.md`: required fields, validation rules, duplicate checks, review states, and country restrictions.
- `assumptions.md`: unresolved questions, inferred behavior, launch constraints, and risks.

This discovery becomes the durable map for future customer-onboarding work.

### Step 4: Run Impact Analysis

Create or update:

```text
.ai/workspaces/customer-validation/impact-analysis.md
```

The impact analysis should identify:

- Impacted routes, handlers, services, validators, repositories, and tests.
- New or changed validation contracts.
- Country-specific business rules.
- Persistence or schema changes, if any.
- API response changes and backwards compatibility risks.
- Operational risks, such as third-party validation provider failures.
- Documentation and ADR impacts.

Example risks:

- Existing domestic validation may assume a single address format.
- Some countries may require different postal-code, tax, or identity fields.
- API clients may rely on current validation error shapes.
- A new validation provider may introduce timeout and retry behavior.

### Step 5: Generate an implementation plan

Create or update:

```text
.ai/workspaces/customer-validation/implementation-plan.md
```

A good plan might include:

1. Add failing tests for international onboarding validation.
2. Introduce a country-aware validation policy or strategy.
3. Extend customer onboarding validation without changing unrelated workflow steps.
4. Preserve existing domestic validation behavior.
5. Add integration or contract tests for validation errors.
6. Update discovery and knowledge artifacts through the Knowledge Curator.

The plan should be small enough to review and specific enough to implement safely.

### Step 6: Load required skills

For this feature, the agent should load only the relevant skills, such as:

- `clean-architecture`
- `design-patterns`
- `tdd`

Possible skill usage:

- Use `tdd` to drive behavior through failing tests first.
- Use `clean-architecture` to keep validation policy separate from transport and persistence concerns.
- Use `design-patterns` if country-specific validation requires a Strategy, Policy, or Specification pattern.

### Step 7: Implement the feature

Implementation should follow the plan and keep scope narrow.

Expected implementation behavior:

- Add tests for supported international validation cases.
- Add tests for unsupported countries or missing country-specific fields.
- Implement country-aware validation in the appropriate domain or application layer.
- Preserve existing customer onboarding behavior.
- Avoid broad rewrites of unrelated onboarding code.

### Step 8: Review the implementation

Before completion, review:

- Does the code satisfy the original feature request?
- Do tests cover success, failure, and edge cases?
- Are validation rules located in the right architectural layer?
- Did any API contracts change?
- Were assumptions resolved or recorded?
- Is an ADR required for any new validation architecture or external dependency?

### Step 9: Run Knowledge Curator

After implementation, run the Knowledge Curator.

Update affected artifacts when necessary:

- `.ai/discoveries/customer-onboarding/architecture.md`
- `.ai/discoveries/customer-onboarding/business-rules.md`
- `.ai/discoveries/customer-onboarding/assumptions.md`
- `.ai/knowledge/glossary.md`
- `.ai/knowledge/business-domain.md`
- `.ai/knowledge/architecture-principles.md`
- `.ai/knowledge/adr/ADR-XXXX-title.md`

For this example, the curator might:

- Add new country-specific onboarding rules to `business-rules.md`.
- Update `architecture.md` with a new validation policy component.
- Resolve assumptions about supported countries.
- Add glossary terms such as "international customer validation" or "supported onboarding country".
- Create an ADR if a new external validation provider or architectural pattern was introduced.

The task is complete only when code, tests, and knowledge are all aligned.

## Knowledge Lifecycle

Knowledge in this system follows a simple lifecycle:

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

Agents investigate the smallest workflow necessary for the current task. Discovery should focus on facts, evidence, business rules, risks, and uncertainty.

### Persist

Useful findings are written to `.ai/discoveries/`, `.ai/knowledge/`, or `.ai/workspaces/` depending on their scope.

- Repository-wide facts go in `.ai/knowledge/`.
- Workflow-specific facts go in `.ai/discoveries/`.
- Task-local plans and notes go in `.ai/workspaces/`.

### Reuse

Future tasks should start by checking existing knowledge and discoveries. If `.ai/discoveries/customer-onboarding/` already exists, an agent working on onboarding should reuse it before searching the codebase from scratch.

Avoid rediscovering the same workflow repeatedly. Reuse is what makes the system compound over time.

### Update

When implementation changes behavior, architecture, business rules, or assumptions, the Knowledge Curator updates the affected artifacts.

Knowledge should evolve incrementally. Do not rewrite everything just because a small rule changed. Preserve historical context and document significant decisions with ADRs.

## How knowledge accumulates over time

The first task in a workflow may require more discovery because little context exists. After that, every task should make future tasks easier.

Example progression:

1. A payment bug fix creates `.ai/discoveries/payment-processing/workflow.md`.
2. A later refund feature reuses the payment-processing discovery and adds refund-specific business rules.
3. A third task changes payment retry behavior and the Knowledge Curator updates the workflow architecture and creates an ADR.
4. Future payment tasks now start with a richer understanding of payment states, retries, integrations, and risks.

This turns agent work into a compounding asset instead of a series of isolated conversations.

## Reusing discoveries across future features

Before starting a feature, agents should ask:

- Is there already a discovery for this workflow?
- Is there a related discovery that covers adjacent behavior?
- Which facts are still current?
- Which assumptions need confirmation?
- Which open questions affect this task?

If a discovery exists, use it as the starting point. Update it only when the new task reveals new facts or changes existing behavior.

For example, after `customer-onboarding` has been discovered once, future requests such as these should reuse it:

- Add referral-code validation during onboarding.
- Add business customer onboarding.
- Change onboarding review states.
- Add onboarding fraud checks.
- Localize onboarding error messages.

Each task may create its own workspace, but the shared workflow discovery continues to accumulate durable knowledge.

## Keeping documentation synchronized

Documentation stays synchronized through the Knowledge Curator.

The curator should run near the end of a task, after implementation and before final handoff. It compares the change against existing artifacts and updates only what is affected.

The curator looks for changes to:

- Workflow steps, triggers, actors, outcomes, and failure modes.
- Business rules, validations, permissions, thresholds, and state transitions.
- Architecture components, boundaries, dependencies, data flow, and integrations.
- Assumptions, constraints, unresolved questions, and operational requirements.
- Domain vocabulary that belongs in the glossary or business-domain knowledge.

The Knowledge Curator should not invent facts, promote assumptions into facts, or rewrite unrelated documentation. Its job is synchronization, not documentation churn.

## Scaling to Large Repositories

The AI Engineering System is designed for large codebases.

The goal is **not** to understand the entire repository. The goal is to understand only the workflow relevant to the current task.

Use a layered context model:

```text
Global Knowledge
↓
Workflow Knowledge
↓
Feature Knowledge
```

Mapped to directories:

```text
.ai/knowledge/
↓
.ai/discoveries/
↓
.ai/workspaces/
```

### Global Knowledge

Global knowledge applies across the repository. It includes business domain context, glossary terms, architecture principles, and ADRs.

Use it to understand project-wide rules before entering a workflow.

### Workflow Knowledge

Workflow knowledge applies to a bounded workflow, such as onboarding, payment processing, search indexing, report generation, or inventory reconciliation.

Use it to avoid repeated discovery and to understand the path from trigger to outcome.

### Feature Knowledge

Feature knowledge applies to one task. It lives in a workspace and includes request notes, impact analysis, implementation plans, review notes, and knowledge-review output.

Use it to keep the current task explicit without polluting durable knowledge with temporary details.

## Definition of Done

A task is not complete until:

- Code is implemented.
- Tests are updated.
- Discoveries are reviewed.
- Knowledge artifacts are updated when necessary.
- Architectural decisions are documented.

Documentation is part of the implementation.

A high-quality agent contribution should leave the repository in a state where the next human or agent can understand what changed, why it changed, how it was validated, and which knowledge artifacts now represent the truth.

## How to use this repository

1. Copy or keep the `.ai/` directory at the root of your software project.
2. Read `.ai/AGENTS.md` before starting agent work.
3. Select the playbook that matches the task.
4. Load only the principles and skills relevant to that playbook and task.
5. Create a task workspace under `.ai/workspaces/`.
6. Reuse existing `.ai/knowledge/` and `.ai/discoveries/` artifacts before rediscovering code.
7. Persist new discoveries and assumptions before risky implementation.
8. Implement and test the change.
9. Run the Knowledge Curator and update affected artifacts.
10. Review code, tests, and documentation together.

## Design goals

- Keep context concise and task-relevant.
- Prefer simple, portable Markdown artifacts.
- Avoid vendor-specific assumptions unless a project explicitly opts in.
- Support software engineering first, while remaining extensible to Python, MLOps, and research workflows.
- Make agent work auditable through files that can be reviewed in pull requests.
- Turn repeated discovery into durable repository knowledge.
