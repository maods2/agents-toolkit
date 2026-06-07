# Playbook: Knowledge Maintenance

## Use when

A feature, bug fix, refactor, or architecture change may make repository knowledge stale.

## References

- Agent: `agents/knowledge-curator.md`
- Skill: `skills/knowledge-curation/`
- Templates: `templates/knowledge-review.md`, `templates/adr.md`
- Knowledge areas: `knowledge/`, `discoveries/`

## Inputs

Use whichever inputs are available:

- Workspace context.
- Discovery artifacts.
- Knowledge artifacts.
- Git diff.
- Implementation plan.
- Pull request description.

## Workflow

1. Establish the change boundary from the git diff, plan, and PR description.
2. Identify impacted workflows, business concepts, assumptions, and architecture areas.
3. Select only the relevant discovery and knowledge artifacts.
4. Compare current artifacts against the implementation evidence.
5. Update impacted `workflow.md`, `architecture.md`, `business-rules.md`, `assumptions.md`, `open-questions.md`, `glossary.md`, or related knowledge files.
6. Generate an ADR under `knowledge/adr/` if the change is architecturally significant.
7. Produce `knowledge-review.md` using the template.
8. Verify that every update has a clear reason tied to code, plan, or PR evidence.

## Review criteria

- No unrelated knowledge files were modified.
- No business rules were invented.
- Historical information was preserved or explicitly marked as superseded.
- New assumptions and open questions are separated from confirmed facts.
- Architectural changes are documented at the right level of detail.
