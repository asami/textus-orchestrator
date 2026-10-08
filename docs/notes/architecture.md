# Textus Orchestrator Architecture

Status: initial architecture
Date: 2026-10-08

## Purpose

Textus Orchestrator routes semantic work and external participation to the appropriate capability provider while preserving the owning subsystem's authority.

Its central use case is Human-in-the-Loop orchestration built on CNCF Workflow/Continuation/Admission rather than an outer application-specific approval loop.

## Position

```text
Human
  |
Slack / Web / Mobile / Watch
  |
Textus Control Center
  |
Textus Orchestrator
  |
  +-- Human participant
  +-- Dot / Astra-class semantic participant
  +-- OpenClaw / Local LLM operational participant
  +-- sm-workflow Subsystem
  |      +-- Codex workers
  +-- TEAI / deterministic integration
```

## Core separation

- CNCF Workflow/Operation owns abstract semantic execution contracts.
- CNCF Admission owns Candidate acceptance semantics and authority/policy.
- CNCF Continuation owns suspension/resume mechanics and external-participation IoC.
- Textus Orchestrator owns participant/capability resolution, dispatch and return routing.
- Textus Control Center owns integrated management/presentation, including Admission Inbox.
- sm-workflow owns software-development workflow semantics.
- TEAI owns enterprise/application integration semantics.

Human, Dot, OpenClaw, Codex and deterministic providers are participants/capability providers; they are not workflow authorities merely because they execute work.

## Human-in-the-Loop

Human-in-the-Loop is a normal participant route.

```text
Owning Workflow
  -> semantic requirement / Admission Gap
  -> Continuation when external participation is required
  -> Textus Orchestrator
  -> Human participant binding
  -> typed Decision/Result
  -> owning completion/resume Operation
  -> Workflow continues
```

The Orchestrator does not infer the Workflow's next state. Slack/Web/Mobile/Watch are replaceable interaction surfaces and do not become Workflow or Admission authority.

## Capability routing

Initial semantic routing categories include:

- SOFTWARE_ENGINEERING -> sm-workflow Subsystem;
- HUMAN_DECISION -> Human participant through Control Center interaction;
- DEEP_RESEARCH / ARCHITECTURE / SPECIFICATION / BROAD_REVIEW -> Dot/Astra-class provider when available;
- OPERATIONAL_AGENT -> OpenClaw, normally backed by a local LLM;
- ENTERPRISE_INTEGRATION -> TEAI.

These are routing responsibilities, not fixed product chains. Provider names must remain configuration/binding details where practical.

OpenClaw is not the normal programming intermediary. A software-engineering request originating from OpenClaw/Slack enters sm-workflow; sm-workflow binds Codex.

Dot and OpenClaw may run concurrently and should be used for complementary capabilities.

## sm-workflow Subsystem

sm-workflow evolves from a one-shot/CLI deployment into a resident Subsystem that centrally owns running development workflows, worker bindings, review/admission progression and development status.

The public Skill/Application Operation contract does not change because of this deployment change.

Conceptually:

```text
Skill / CLI / MCP / Orchestrator
          |
          v
same typed sm-workflow Operations
          |
     transport binding
       /        \
 one-shot     resident
 runtime      sm-workflow Subsystem
```

A Codex chat/session may register/bind as a worker execution context. sm-workflow issues typed WorkOrder/Continuation requests and receives Result/Evidence. The chat/session is replaceable; sm-workflow remains authority.

## Authority and durability

No canonical workflow, admission, project or integration state exists only in Orchestrator or agent memory.

The Orchestrator should persist only the orchestration state required for reliable routing/correlation. Owning subsystem state remains authoritative.

## Initial implementation principle

Do not begin by building a generic autonomous AI agent. Start with a deterministic participant-routing vertical slice over existing CNCF typed contracts. Add JudgmentAction only where participant/capability selection genuinely requires semantic judgment.
