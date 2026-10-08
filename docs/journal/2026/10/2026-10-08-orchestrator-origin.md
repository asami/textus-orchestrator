# Textus Orchestrator Origin

Date: 2026-10-08
Status: architectural decision

The combined Dot/OpenClaw/Codex discussion exposed an orchestration responsibility that should not belong to sm-workflow or Textus Control Center.

sm-workflow should remain software-development-specific. Control Center should remain the integrated management/presentation plane. A separate Textus Orchestrator therefore owns cross-participant capability routing.

The architecture deliberately supports both Dot and OpenClaw:

- OpenClaw + local LLM for low-cost continuous operational/EAI work;
- Dot/Astra-class reasoning for research, specification, architecture, broad semantic review and persistent context management;
- sm-workflow + Codex for software engineering;
- Human participants through Admission/Continuation when authority is required.

A key design result is that Human-in-the-Loop becomes a normal orchestration route rather than an exceptional outer loop. CNCF Continuation provides IoC, CNCF Admission supplies acceptance semantics, and Textus Orchestrator binds the required participant.

sm-workflow's future resident Subsystem deployment does not require a Skill API redesign. Existing typed application Operations remain the contract; one-shot CLI/MCP and resident subsystem operation are transport/deployment choices.
