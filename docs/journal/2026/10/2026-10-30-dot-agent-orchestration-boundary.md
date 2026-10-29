# Dot, API Direct and Deterministic Orchestration Boundary

Date: 2026-10-30
Status: design decision / implementation handoff
Authority: [AI Agent and Deterministic Orchestration Architecture](../../design/ai-agent-deterministic-orchestration.md)

## Motivation

A project-specific Dot powered by Astra can be valuable for human interaction, clarifying intent, maintaining context and supervisory judgment. But designing around unusually cheap or unmetered autonomous local development would depend on potentially temporary product conditions. Instead use product-intended, explicitly metered execution channels for bulk work.

## Decision

Keep non-routine semantic supervision in Dot/another agent; put routine control in textus-orchestrator; put development workflow state, deterministic Git/SBT/test, review and Admission in sm-workflow. API Direct through textus-ai-runtime is separate from Agent Continuation through Codex/Dot/OpenClaw. Dot need not mediate API Direct calls.

textus-orchestrator remains a generic participant/capability dispatcher and correlation coordinator, not a second sm-workflow or GitHub work ledger. Existing Control Center and Development Center ownership is unchanged.

## Phase handoff

Phase 1 remains a minimal typed participant routing slice. Later Dot/OpenClaw adapters should use the same contract and must not expand Phase 1's closure conditions. CNCF Phase 80 and sm-workflow Phase 9 own the execution-interface and routing policy refinements respectively.

## Open validation

- Whether Dot can initiate and resume the required typed MCP/skill interactions within published permissions.
- Actual Dot deeper-work accounting and limits versus API Direct/Codex.
- End-to-end Candidate/Admission and execution evidence correlation.
- Agent replacement without Workflow semantics changes.
