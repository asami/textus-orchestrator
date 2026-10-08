# Phase 1: Continuation Participant Routing Vertical Slice

Status: planned
Planned: 2026-10-08
Depends on: CNCF Phase 77 Continuation baseline, CNCF Phase 90 Candidate-Admission baseline

## Goal

Establish the smallest useful Textus Orchestrator subsystem that can receive an external-participation requirement, resolve a participant/capability binding, dispatch the typed request, accept a typed result/decision, and return it to the owning completion/resume Operation without owning the Workflow's internal progression semantics.

## Initial vertical slice

```text
Owning Workflow
  -> Continuation / typed external requirement
  -> Textus Orchestrator
  -> Participant Resolver
       -> HUMAN_DECISION
       -> SOFTWARE_ENGINEERING
  -> bound participant/subsystem
  -> typed Result/Decision
  -> owning completion/resume Operation
```

Initial bindings:

- HUMAN_DECISION -> Control Center-backed human interaction provider (a deterministic fake provider is sufficient for executable specification before UI integration);
- SOFTWARE_ENGINEERING -> sm-workflow public application Operations.

Dot/Astra and OpenClaw/local-LLM providers are follow-up integrations, not required to prove the core abstraction.

## Requirements

1. Reuse CNCF typed Workflow/Continuation/Result/Decision contracts; do not create a second continuation protocol.
2. Reuse CNCF Candidate-Admission semantics where the request is an Admission decision; do not move Admission authority into Orchestrator.
3. Define a minimal semantic Capability/Participant requirement and resolver/binding contract.
4. Keep provider/product identity out of owning Workflow semantics.
5. Dispatch only bounded registered capabilities; no arbitrary command/prompt execution API.
6. Correlate request, participant execution and returned result/evidence.
7. Do not select the owning Workflow's next state; submit the result through the owning completion/resume Operation.
8. Prove participant replacement does not alter owning Workflow semantics.
9. Provide deterministic test providers for Human and software-engineering routes.
10. Define the Control Center handoff for human presentation and the sm-workflow handoff for software-engineering execution.
11. Preserve one-shot/local development mode where practical while establishing the resident subsystem boundary.

## Non-goals

- Dot/OpenClaw production integration.
- Building a general autonomous agent.
- Reimplementing sm-workflow or TEAI.
- Owning GitHub Pull Request/Admission semantics.
- Building Control Center UI.
- Direct Codex invocation from Orchestrator.
