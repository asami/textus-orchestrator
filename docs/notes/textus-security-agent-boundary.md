# Textus Security Agent Boundary

Status: initial security architecture projection
Updated: 2026-10-14
Canonical architecture: goldenport-cncf/docs/design/textus-security-architecture.md

textus-orchestrator treats AI agents, dots/OpenClaw-style services, Codex and
local models as execution participants, not trusted administrators.

Delegation should carry the least authority needed for the selected operation,
repository/workspace and duration. Possession of a host credential or access to
an orchestrator does not imply unrestricted subsystem, Git, shell, filesystem,
network or DataStore authority.

Human approval and workflow Continuation boundaries remain explicit for actions
whose authority is not already admitted. The orchestrator must not silently
upgrade a participant's capability because a task is difficult or an agent
requests broader access.

Agent/model output enters normal sm-workflow/CNCF admission and review
boundaries. Model identity is not evidence of correctness or security.

Credentials and secrets should be passed by bounded provider/runtime mechanisms
and omitted from prompts, logs and durable orchestration records wherever
possible.

Security incidents or recurring authority problems discovered through
orchestration are journaled and fed back to the canonical CNCF security
architecture when they expose a Textus-wide design issue.
