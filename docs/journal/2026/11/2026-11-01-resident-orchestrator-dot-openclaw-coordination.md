# Resident Textus Orchestrator with Dot and OpenClaw Participants

Date: 2026-11-01
Status: Architecture exploration / proposed operating scenario
Related: Phase 1 Continuation Participant Routing; AI Agent and Deterministic Orchestration Architecture; CNCF Workflow / Continuation / Candidate-Admission; sm-workflow; Development Center

## Direction

Run one persistent textus-orchestrator CNCF subsystem/server process as the common coordination point for both Dot and OpenClaw. The participants are complementary, not competing orchestrators. The server owns deterministic participant routing, authorized dispatch, scheduling/monitoring coordination and execution correlation, while the owning Workflow retains progression and Admission authority. It must not become a second sm-workflow or GitHub work ledger.

- Dot/Astra: human dialogue, intent clarification, high-level review, semantic investigation and judgment, subject to actual Dot permissions/allowances.
- OpenClaw: controllable recurring agent execution, local LLM routing, inexpensive preliminary classification and optional API-backed inference.
- textus-orchestrator: durable coordination, participant/capability resolution, Continuation handoff and notifications.
- sm-workflow: typed development workflow, heavy tests, Git/SBT, validation, CBD Support review integration and admission.
- textus-ai-runtime: explicitly metered API Direct inference.

## Logical interaction

```text
                 Human
                   |
                Dot/Astra
                   |      OpenClaw / local LLM
                   |          |
                   +-----+----+
                         |
              textus-orchestrator
               (resident subsystem)
                         |
             CNCF typed Continuation
             / Result / Evidence
                         |
             sm-workflow + CBD Support
             heavy tests / reviews / validation
                         |
              findings / candidates
                         |
          Development Center / Human Admission
```

Neither agent must communicate directly with the other. A participant may initiate an admitted workflow and later another participant may handle its semantic Continuation, without changing Workflow semantics. Actual ownership of workflow state and GitHub work remains in the appropriate subsystem.

## Initial quality-monitoring scenario

1. A scheduled, authorized workflow triggers sm-workflow heavy tests. SBT/test execution is deterministic and does not itself require LLM tokens, unless the tests call AI.
2. Collect typed diagnostics, logs and test evidence without requiring a resident AI to wait during long execution.
3. CBD Support and deterministic checks perform their admitted review steps. OpenClaw/local LLM can classify bounded findings.
4. Where high-level semantic judgment is needed, issue a typed Continuation for Dot/Astra or another admitted capable participant.
5. Return typed results/evidence to the owning completion operation. Findings become candidates, not automatically authorized code changes.
6. Development Center/Human reviews proposals; accepted fixes proceed through sm-workflow.

## Execution economics and authority

Use Dot for bounded semantic work, not as an undocumented unlimited coding engine. Prefer deterministic scheduling/test execution in the server; use explicitly metered API Direct or Codex for bulk inference/development where appropriate. A Dot-initiated local command or MCP call may start an authorized orchestrator operation without creating a Codex task, but actual billing and permission behavior require testing.

Proactive Dot research may not automatically mutate external systems; distinguish proactive observation from explicitly authorized recurring tasks. There is currently no verified general Dot API for server-initiated delivery of arbitrary Continuations. Candidate integration: Dot polls/requests pending typed work through an approved Plugin/MCP path, with permissions and practical availability validated on a real installation. Do not claim autonomous server push to Dot is already implemented.

## Engineering principles

- Single resident coordination server, multiple replaceable participants.
- Existing CNCF Workflow/Continuation protocol, no duplicate agent-specific state machine.
- Preserve WorkOrder identity, execution evidence, idempotency, authorization, Admission and independent review.
- Participant outages or model changes must not erase owning workflow state.
- Keep cost/quality/decline/escalation evidence for future routing feedback.
- Heavy tests and expensive reviews run when scheduled/justified; do not repeat unchanged work blindly.
- Do not enlarge current Phase 1 completion scope solely to integrate Dot/OpenClaw; refine subsequent implementation phases after interface verification.

## Verification candidates

- One resident process can serve both participant adapters and maintain correlated pending/completed work.
- Dot can obtain and return typed Continuation through a permitted mechanism, without assuming a public Dot API.
- OpenClaw can handle equivalent work with local/API model routing.
- A heavy test can finish asynchronously while no AI participant remains occupied.
- Human approval and development state remain in owning systems.
- Costs and permissions of Dot-native versus Codex/API execution are measured.
