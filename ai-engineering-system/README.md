# AI Engineering System

A portable agent workflow system for software engineering, MLOps pipelines, and research-oriented development.

This project stores reusable guidance for agentic development workflows. It is designed to work as a lightweight layer above coding agents and assistants such as Codex, Cursor, Claude Code, and GitHub Copilot.

## Structure

```text
.ai/
├── AGENTS.md
├── agents/
├── principles/
├── skills/
├── playbooks/
├── templates/
├── knowledge/
├── discoveries/
└── workspaces/
```

## How to use

1. Start with a playbook that matches the task.
2. Load only the principles and skills referenced by that playbook.
3. Persist discoveries, assumptions, open questions, and durable knowledge before implementation.
4. Keep task workspaces small, explicit, and disposable.
5. Improve the system incrementally after real project usage.

## Design goals

- Keep context concise and task-relevant.
- Prefer simple, portable Markdown artifacts.
- Avoid vendor-specific assumptions unless a project explicitly opts in.
- Support software engineering first, then extend into Python, MLOps, and research workflows.
