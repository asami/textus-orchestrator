# Shared Orchestrator and Development Center boundary

Date: 2026-10-10
Status: architecture clarification

## Decision

Keep one Textus Orchestrator for both operational and software-development participant/capability execution.

Do not interpret this as merging the operational and development management domains.

- Textus Control Center owns the operational Human-in-the-Loop surface.
- Textus Development Center owns the software-development Human-in-the-Loop surface.
- GitHub Projects/Issues/Pull Requests are the initial system of record for durable development work.
- sm-workflow remains authority for software-development Workflow semantics.
- Textus Orchestrator owns only the routing/dispatch/correlation/continuation needed to invoke participants and capabilities.

The Orchestrator must not become a duplicate GitHub work database or a second sm-workflow state store.

## Development interaction

A Development Center action may request semantic execution through Textus Orchestrator, for example AI review, escalation, or starting an admitted development capability. The resulting durable development state is written through the appropriate owning system rather than being invented as Orchestrator-owned project state.

The architecture therefore distinguishes:

- Work plane: GitHub Projects / Issues / Pull Requests;
- Execution plane: Textus Orchestrator and execution providers;
- Development Workflow: sm-workflow;
- Human development surface: Textus Development Center.

This preserves one reusable orchestration infrastructure without coupling Control Center and Development Center domain models.
