# `.ai` System Workspace

This directory contains the reusable operating system for agent-assisted engineering work.

## Directory purpose

- `agents/`: reusable agent role definitions and operating instructions.
- `principles/`: concise engineering principles that guide decisions.
- `skills/`: reusable agent capabilities with decision rules and checklists.
- `playbooks/`: task workflows that compose principles and skills.
- `templates/`: stable document formats for recurring outputs.
- `knowledge/`: durable cross-workflow knowledge such as glossary, domain notes, architecture principles, and ADRs.
- `discoveries/`: persisted workflow and feature-area discoveries.
- `workspaces/`: temporary task-specific planning and execution notes.

## Portability rules

- Write instructions in English.
- Use Markdown as the default artifact format.
- Reference files by relative path.
- Avoid assuming a specific IDE, agent runtime, package manager, or programming language unless a playbook explicitly requires it.