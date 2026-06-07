# AI Engineering System

When solving a task:

1. Load relevant principles.
2. Load relevant skills.
3. Load the appropriate playbook.
4. Prefer simple solutions.
5. Avoid unnecessary abstractions.
6. Keep plans and discoveries persisted.

Repository structure:

```text
agents/
principles/
skills/
playbooks/
templates/
knowledge/
discoveries/
workspaces/
```


Workflow orchestration:

1. Use `agent-orchestration.md` for non-trivial task flow and agent selection rules.
2. Run Workflow Scout when the relevant workflow is unknown.
3. Run Workflow Discovery when workflow knowledge is missing, stale, or needed for behavior preservation.
4. Run Impact Analysis before every non-trivial change.
5. Run Planner before implementation; the Planner only produces plans and must not implement code.
6. Run Reviewer before completion.
7. Run Knowledge Curator after implementation and review to update discoveries, knowledge, and ADRs when needed.
8. Prefer reusing existing discoveries before rediscovering a workflow.
