# Dots, OpenClaw, and Textus EAI: Responsibility Boundaries

Date: 2026-11-11
Status: architectural discussion / implementation feasibility pending

## Decision direction

Treat Dots primarily as a **ChatGPT-hosted Chat Interface for Textus Orchestrator**, not as the default execution engine. Treat OpenClaw as an optional, self-hosted autonomous agent. Prefer deterministic Textus EAI (TEAI) integration and ordinary CNCF operations before invoking any agent.

```text
Human <-> ChatGPT / Dots (Chat IF)
                    |
             Continuation Protocol
                    |
             Textus Orchestrator <----> OpenClaw (agent participant)
                    |
             +------+----------+
             |      |          |
           TEAI   Control    sm-workflow
                  Center
```

The Orchestrator handles **work direction**, Control Center handles **operational management/presentation**, and TEAI handles integration. These boundaries are complementary, not hierarchical replacements.

## Ingestion and event handling

- TEAI independently detects new Gmail/Slack messages using provider events/webhooks or polling, retrieves messages/threads, applies deterministic filtering/transformation, and manages retention, logs, and lifecycle under policy.
- TEAI can run scheduled integration work independently; Orchestrator coordinates work spanning subsystems.
- TEAI can register material with Knowledge Lake through the appropriate controlled integration boundary.
- Agents should not be required for routine message ingestion or polling. Semantic interpretation, ambiguity resolution, or human approval may trigger a Continuation.
- Dots may read Slack/Gmail as part of an interactive ChatGPT conversation when permitted, but this is distinct from the canonical TEAI ingestion path.

## Participant specialization

| Responsibility | Preferred owner |
| --- | --- |
| ChatGPT conversation, human consultation and approval interface | Dots |
| Autonomous agent work and optional local-tool integration | OpenClaw |
| Email/Slack event detection, collection, transformation, retention | TEAI |
| Work coordination, participant binding and continuation routing | Textus Orchestrator |
| System operations and supervision | Control Center |
| Software development workflow and worker selection | sm-workflow |
| Straightforward inference | Direct local LLM/provider where suitable |

Dots and OpenClaw may both be connected concurrently. Route by capability, required human interaction, locality, availability, security and total cost rather than by a fixed universal priority. Keep both replaceable Continuation participants. Dots' special value is the established ChatGPT conversation surface (including mobile); OpenClaw's is self-hosted operational flexibility.

## Continuation interaction

Example: Slack/email arrives -> TEAI ingests -> owning workflow identifies a decision gap -> Orchestrator dispatches a typed Continuation to Dots for human consultation or to OpenClaw for autonomous work -> typed result returns to owning workflow -> admission/resumption occurs under the owning subsystem's authority.

Use correlation IDs, assignment/lease state, timeout, deduplication and idempotent completion to avoid duplicate commits when participants overlap or fail over. Do not store canonical workflow state in Dots/OpenClaw memory.

## Cost hypothesis and cautions

- Dots is potentially inexpensive as a thin Chat IF under an existing ChatGPT Pro allowance, but **zero incremental cost is a hypothesis, not a verified billing guarantee**. Autonomous tasks, connected-app actions, quotas and delegated Codex/Work usage may be metered differently.
- OpenClaw software can be used without a license charge, but hosting, local compute, paid model APIs and operations are not necessarily free.
- TEAI deterministic ingestion avoids paying for agent reasoning on every event.
- Measure actual usage and establish explicit per-provider quotas/budgets before relying on cost assumptions.

## Validation items

1. Verify whether Dots can receive externally initiated Continuations and resume a specific ChatGPT chat through supported official interfaces. A conceptual Continuation Protocol does not itself establish this capability.
2. Verify Dots' external action/Plugin permissions and whether an Orchestrator endpoint can be called automatically.
3. Confirm Dots billing and limits for proactive work and external connector calls.
4. Implement TEAI Gmail/Slack event ingestion independently; define event replay, deduplication, access scopes and retention.
5. Prototype one end-to-end Continuation round trip, initially with an available participant, before committing to Dots-specific delivery.
6. Evaluate routing policy and fallback behavior across Dots, OpenClaw, direct LLM and deterministic processing.

This note records architectural intent; it does not claim these integrations are already implemented.
