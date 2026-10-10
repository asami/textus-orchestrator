# Continuous development review routing

Date: 2026-10-10
Status: use-case alignment

Low-cost persistent semantic reviewers such as Dots or local LLMs may act as continuous development-quality sensors.

Textus Orchestrator may route/schedule such semantic review capability and later dispatch selected Development Work Requests, but it does not own the resulting development backlog. Actionable durable work belongs in GitHub Projects/Issues/Pull Requests and is presented by Textus Development Center.

The preferred separation is:

    continuous semantic provider
      -> finding / proposal
      -> GitHub Issue or PR
      -> Development Center human selection
      -> Development Work Request
      -> Orchestrator / sm-workflow / Codex when automated dispatch is used

The first Development Center integration may stop before Orchestrator dispatch and generate a handoff for manual paste into Codex Console. This is a valid staged implementation, not a requirement to automate Codex session control immediately.
