# AI Engineering System Project Instructions

When working in this project:

1. Read `.ai/AGENTS.md` first.
2. Load only the principles, skills, playbooks, and templates relevant to the task.
3. Keep generated workflow artifacts under `.ai/discoveries/` or `.ai/workspaces/`.
4. Prefer concise Markdown over tool-specific configuration.
5. Avoid implementation-specific instructions unless the task explicitly asks for them.

## Workflow orchestration

Use `.ai/agent-orchestration.md` as the default orchestration model for non-trivial engineering tasks. Agents represent workflow stages, not role-playing personas or seniority levels.

Default stage order for new feature work:

1. Workflow Scout creates or updates `navigation-map.md` when the relevant code path is unknown.
2. Workflow Discovery creates or updates `.ai/discoveries/<workflow-name>/` when durable workflow knowledge is missing or stale.
3. Impact Analysis creates or updates `impact-analysis.md` before non-trivial changes.
4. Planner creates `plan.md` and must not implement code.
5. Implementation follows the selected playbook and loaded skills.
6. Reviewer creates `review-report.md` before completion.
7. Knowledge Curator updates affected discoveries, knowledge, and ADRs after review.

Keep workflow artifacts under `.ai/discoveries/` or `.ai/workspaces/` and prefer reusing existing discoveries before rediscovering code.
