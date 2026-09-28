# OffSec — Project Report

Builds on `docs/00-foundation.md` and `docs/offsec/architecture.md`. This
file covers motivation, risks, and success criteria specific to the
offensive-security agent — it does not repeat shared architecture.

## 1. Executive Summary

OffSec is the offensive-security agent in the Cyber Agent Foundation. It
separates language model, agent controller, persistent state, offensive
capabilities, analyzers, workflows, exploitation mechanisms, and execution
records, rather than being a chatbot with a fixed command list.

Two milestones, both **estimates for sequencing, not fixed commitments**:

- **~January:** Phases 0–7 — recon/enumeration through real plugins,
  structured findings, evidence-backed next-step recommendations. No
  exploitation runs yet.
- **~Next December:** Phases 8–9 — exploitation orchestration via vetted
  providers and v1–v3 generated PoCs, access maintenance, post-exploitation
  analysis, with covering tracks kept human-approved.

Advanced iterative exploit generation (v4–v5) and reliable handling of
memory-corruption or complex protocol vulnerabilities are explicitly out of
scope for the December milestone.

## 2. Motivation (OffSec-specific)

Beyond the shared motivations in the foundation doc (context limits,
hallucination, hard-coded tools, model lock-in — see `00-foundation.md §9`):

**Narrow security coverage.** The objective is not a tool that only
understands HTTP or a handful of vulnerability classes. Security domains
must be extensible via plugins, not hard-coded into the core.

## 3. Cybersecurity Coverage

Web, API, application, network, Linux, Windows, cloud, container, identity,
directory services, source-code, binary analysis, reverse engineering,
malware analysis, OSINT, wireless, vulnerability research, configuration
auditing, CTF/labs. None of these are hard-coded into the core — they arrive
as plugins.

## 4. Operational Model

```text
Objective → Plan → Select Capability → Execute →
Record Actual Result → Update Persistent State → Re-plan → Continue
```

This is an orchestration platform, not a `Question → LLM → Generated Answer`
conversational interface.

## 5. Technical Risks (OffSec-specific)

Beyond the shared risks in the foundation doc (local model performance,
context degradation, hallucination, plugin instability, scope explosion,
model lock-in):

### 5.1 Exploitation reliability and scope safety

Freshly generated exploitation code has no track record against the target,
unlike a vetted framework module. Running unverified generated code against
a live, authorized system risks instability, service disruption, or
violating a program's rules against destructive testing.

**Mitigation** — see `architecture.md §Risk`: route known vulnerabilities to
vetted providers, reserve generation for logic established tooling can't
cover, treat insufficient evidence as a stop condition, keep
access-maintenance/covering-tracks human-approved, cap generated-provider
maturity at v1–v3 for now.

## 6. Initial Success Criteria

Not: *"The AI can perform every offensive-security operation."*

1. Local model runs.
2. Model accessed through a provider interface.
3. Agent performs a multi-step task.
4. State exists outside the model context.
5. Task survives restart.
6. Capability installs as a plugin.
7. Agent discovers the plugin.
8. Agent invokes the plugin.
9. Results are persisted.
10. Agent reconstructs the task from persisted results.
11. Another model can eventually replace the first without rewriting the core.

A second criteria set applies once exploitation is built (`architecture.md
§Exploitation`): the agent correctly routes a known vulnerability to a
vetted provider, correctly generates a scoped test for application-specific
logic, and correctly declines to act when evidence is insufficient — these
are not interchangeable outcomes.

## 7. First-Week Development Plan

**Day 1:** create repository/structure, install inference runtime, obtain
Qwen3 quantized model, run local inference, measure baseline performance.

**Days 2–3:** model provider, configuration, minimal agent controller.

**Days 4–5:** SQLite state store, task model, checkpoints, restart/resume.

**Days 6–7:** plugin interface, first example plugin, structured execution
records, end-to-end task.

Goal of week one is architectural validation, not feature count.

## 8. Immediate Next Action

```text
Repository → Local inference → Model provider abstraction →
Minimal agent loop → Persistent state → Plugin architecture
```
