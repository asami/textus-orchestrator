# AI Agent and Deterministic Orchestration Architecture

Status: proposed architectural direction
Date: 2026-10-30
Owner: textus-orchestrator
Related: CNCF Phase 80, sm-workflow Phase 9, textus-orchestrator Phase 1

## Purpose and boundary

Use AI agents (Dot/Astra, OpenClaw or future agents) for human dialogue, intent clarification, non-routine interpretation and judgment. Put repeatable coordination in textus-orchestrator: participant/capability resolution, authorized dispatch, scheduling integration, correlation, result delivery and follow-up. Do not repeatedly spend model inference on deterministic coordination.

This does **not** make the orchestrator the authority for application Workflow progression, development project records, Admission or Git/SBT execution. Preserve existing ownership: CNCF Workflow owns state transitions/Continuation, sm-workflow owns development workflow and deterministic operations, GitHub Projects/Issues/PRs own durable development work, Control Center and Development Center own their respective human-facing surfaces.

## Reference topology

```text
Human <-> Dot (Astra) / other interactive agent
               | typed request / proposed judgment
               v
       textus-orchestrator
       participant binding / dispatch / correlation
               |
               v
           sm-workflow
        development execution / Admission
          |                     |
          v                     v
     API Direct           Agent Continuation
     textus-ai-runtime    Codex / other agent
     Luna / Terra / Sol
          \                     /
           deterministic validation, Review, commit
```

The diagram is a responsibility view, not an assertion that Dot currently exposes a public remote-invocation API.

## Responsibility contract

- **Dot/agent**: interpret ambiguous user intent, preserve relevant long-term context, present alternatives, seek approval, make bounded non-routine judgments; it is not the authoritative workflow engine.
- **textus-orchestrator**: resolve participants, route admitted requests, correlate results, manage routine coordination and scheduling hooks, deliver notifications/decisions through authorized surfaces; it does not invent application authority or store a duplicate project/workflow ledger.
- **sm-workflow**: execute accepted development plans with typed WorkOrders, deterministic Git/SBT/test, Review, Candidate-Admission and Takeover.
- **textus-ai-runtime**: invoke API Direct models and record execution evidence through CNCF AI Audit.
- **CNCF**: generic Workflow/Continuation/ExecutionRequirement/ExecutionEvidence contracts and authorization.

## Economics and resilience

Do not rely on temporary Dots launch allowances, local-command loopholes, or undocumented unlimited work. Dot's native inference is principally reserved for the human-facing, non-routine supervisory role; bulk implementation uses explicitly metered API Direct or admitted Codex/agent execution. Treat the exact Dots usage policy and ability to invoke/resume external work as integration questions, not guaranteed properties. The same orchestration and development contracts must work with OpenClaw or another agent if Dot is unavailable or uneconomic.

## Candidate-Admission and security

AI proposals are candidates, not instructions with authority. Route them through typed contracts and owning Admission; do not expose arbitrary shell or repository mutation to the agent. sm-workflow owns deterministic operations and validation. Retain correlation and execution evidence for cost/quality evaluation without using AI Audit as a second workflow database.

## Delivery alignment

- textus-orchestrator Phase 1 retains its small HUMAN_DECISION / SOFTWARE_ENGINEERING participant-routing vertical slice; Dot/OpenClaw remain later adapters.
- CNCF Phase 80 provides generic execution interface capability/evidence when actual integration demonstrates a gap, keeping API Direct versus Agent Continuation orthogonal to INLINE/DELEGATED.
- sm-workflow Phase 9 configures provider routing and bounded Takeover. Do not hardcode Dot/Terra/Sol into Workflow semantics.
- Integration validation must prove authorized handoff, no duplicate state authority, interchangeable human-facing agents, and metered execution paths.
