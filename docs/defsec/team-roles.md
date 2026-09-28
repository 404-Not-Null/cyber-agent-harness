# DEFSec — Team Role Assignment Matrix

## Purpose

This document defines recommended role assignments for DEFSec teams of different sizes: 3, 5, 7, 10, 15, and 20 people.

The same core responsibilities exist at every team size, but smaller teams combine roles while larger teams specialize them.

Core responsibility areas:

1. Architecture / Technical Leadership
2. Agent & Orchestration
3. Model / AI Engineering
4. Defensive Security Analysis
5. Remediation Engineering
6. Validation & Regression Testing
7. Plugin / Tooling Engineering
8. Infrastructure / Runtime
9. Research / Evaluation
10. Documentation / Release

---

# 1. Three-Person Team

A three-person team should avoid artificial specialization.

## Person 1 — Technical Lead / Architecture / Agent Core

**Owns:**
- overall architecture;
- shared foundation integration;
- agent controller;
- workflow engine;
- persistent state;
- model-provider interface;
- plugin interfaces;
- code review and technical standards.

**Primary areas:**
```text
agent/
models/interface/
memory/
core architecture
```

## Person 2 — Defensive Analysis / Remediation

**Owns:**
- finding normalization;
- root-cause analysis;
- remediation planning;
- remediation strategies;
- code/configuration remediation;
- defensive-domain research;
- finding and remediation schemas.

**Primary areas:**
```text
findings/
remediation/
analysis/
```

## Person 3 — Validation / Plugins / Testing

**Owns:**
- validator plugins;
- scanner integrations;
- patch/configuration adapters;
- regression testing;
- test environments;
- execution evidence;
- CI/testing;
- defensive benchmarks.

**Primary areas:**
```text
plugins/
validation/
tests/
```

### Three-Person Model

```text
Person 1
Architecture + Agent Core
        │
        ├──────────────┐
        │              │
Person 2              Person 3
Analysis +             Plugins +
Remediation            Validation
```

---

# 2. Five-Person Team

## Person 1 — Technical Lead / Architecture

- architecture;
- shared foundation;
- interfaces;
- agent controller;
- state model;
- integration;
- code review.

## Person 2 — Agent / Model Engineering

- model providers;
- prompting and context;
- structured outputs;
- planning;
- tool selection;
- agent loops;
- model evaluation.

## Person 3 — Defensive Analysis / Security Research

- vulnerability analysis;
- root-cause analysis;
- security-domain research;
- finding normalization;
- remediation reasoning.

## Person 4 — Remediation Engineering

- patch generation;
- configuration remediation;
- dependency remediation;
- infrastructure remediation;
- remediation plugins;
- rollback mechanisms.

## Person 5 — Validation / Testing / Infrastructure

- validators;
- regression testing;
- sandbox environments;
- CI;
- execution infrastructure;
- benchmarks;
- validation evidence.

---

# 3. Seven-Person Team

## Person 1 — Technical Lead / Architect

Owns architecture, interfaces, shared foundation, integration, and technical direction.

## Person 2 — Agent / Orchestration Engineer

Owns the agent controller, workflow engine, planning, task execution, recovery, and state transitions.

## Person 3 — Model / AI Engineer

Owns model providers, inference, structured generation, context handling, and model evaluation.

## Person 4 — Defensive Security Researcher

Owns vulnerability analysis, root-cause analysis, findings, defensive-domain research, and remediation reasoning.

## Person 5 — Remediation Engineer

Owns code patches, dependency remediation, configuration changes, infrastructure remediation, and remediation plugins.

## Person 6 — Validation / Regression Engineer

Owns validators, security re-testing, regression testing, functional testing, rollback testing, and validation evidence.

## Person 7 — Platform / Plugin / DevOps Engineer

Owns plugin SDK, tool adapters, execution runtime, CI/CD, sandboxing, packaging, and deployment.

---

# 4. Ten-Person Team

| Person | Primary Role | Main Ownership |
|---|---|---|
| 1 | Technical Lead | Architecture, integration, standards |
| 2 | Agent Core Engineer | Controller, planner, execution loop |
| 3 | Model Engineer | Providers, inference, structured outputs |
| 4 | Memory / State Engineer | Persistence, checkpoints, artifacts |
| 5 | Security Analysis Engineer | Findings, root cause, correlation |
| 6 | Remediation Engineer | Patches, dependencies, configuration |
| 7 | Validation Engineer | Security validation, re-testing |
| 8 | Plugin / Tooling Engineer | SDK, adapters, integrations |
| 9 | Infrastructure / Runtime Engineer | Sandbox, CI/CD, containers, resources |
| 10 | Research / Evaluation / Documentation | Benchmarks, experiments, reports |

---

# 5. Fifteen-Person Team

## Leadership / Architecture

### Person 1 — Technical Lead

Architecture, technical direction, integration, and engineering standards.

### Person 2 — Systems Architect

Interfaces, performance, reliability, shared components, and cross-team design.

## Agent / AI

### Person 3 — Agent Engineer

Agent loop, planning, workflow execution, and recovery.

### Person 4 — Model Engineer

Model providers, inference, structured generation, and local/cloud model integration.

### Person 5 — AI Evaluation Engineer

Model benchmarks, context experiments, output quality, and model comparison.

## Security Analysis

### Person 6 — Vulnerability Analysis Engineer

Findings, evidence, root-cause analysis, and security research.

### Person 7 — Application Security Engineer

Web/API, application logic, dependencies, and application remediation analysis.

### Person 8 — Infrastructure / Network Security Engineer

Network, host, infrastructure, cloud/container, and configuration security.

## Remediation

### Person 9 — Code Remediation Engineer

Source-code patches, dependency changes, and code-level fixes.

### Person 10 — Infrastructure Remediation Engineer

Configuration, network controls, identity, infrastructure, and policy changes.

## Validation

### Person 11 — Security Validation Engineer

Vulnerability re-testing and validation framework.

### Person 12 — Regression / Test Engineer

Functional regression, security regression, test automation, and rollback testing.

## Platform

### Person 13 — Plugin / Tooling Engineer

Plugin SDK, integrations, adapters, and exporters.

### Person 14 — Runtime / DevOps Engineer

Execution runtime, sandboxing, CI/CD, packaging, and deployment.

## Research / Documentation

### Person 15 — Research & Documentation Engineer

Benchmarks, experiments, reproducibility, technical documentation, and project reporting.

---

# 6. Twenty-Person Team

## Architecture

### Person 1 — Technical Director / Lead Architect

Overall architecture, technical direction, cross-team integration, and major design decisions.

### Person 2 — Systems Architect

System interfaces, performance, reliability, and shared infrastructure design.

## Agent Platform

### Person 3 — Agent Controller Engineer

Controller, execution loop, task lifecycle, and agent runtime.

### Person 4 — Workflow / Planning Engineer

Planning, workflow graphs, task decomposition, and recovery logic.

### Person 5 — State / Memory Engineer

Persistent state, checkpoints, artifact storage, retrieval, and long-running task state.

## AI / Models

### Person 6 — Model Runtime Engineer

Local inference, provider abstraction, model lifecycle, and resource management.

### Person 7 — Model Evaluation Engineer

Model benchmarks, quality measurements, structured output evaluation, and experiments.

### Person 8 — Context / Prompt Engineering Researcher

Context construction, prompt strategies, tool-use reasoning, and agent behavior experiments.

## Security Analysis

### Person 9 — Vulnerability Researcher

Security research, vulnerability analysis, root-cause investigation, and findings.

### Person 10 — Application / API Security Engineer

Application and API findings, analysis, and defensive strategies.

### Person 11 — Network / Infrastructure Security Engineer

Network, host, infrastructure, and configuration security.

### Person 12 — Cloud / Container / Identity Security Engineer

Cloud, containers, IAM, directory services, and identity controls.

## Remediation

### Person 13 — Code Remediation Engineer

Source patches, dependency remediation, secure coding changes, and code-level fixes.

### Person 14 — Configuration / Infrastructure Remediation Engineer

Configuration, network controls, infrastructure, identity, and policy remediation.

## Validation

### Person 15 — Security Validation Engineer

Security re-testing, validation framework, and evidence collection.

### Person 16 — Regression / QA Engineer

Functional regression, security regression, automated testing, and rollback validation.

## Platform / Plugins

### Person 17 — Plugin SDK Engineer

Plugin architecture, SDK, adapters, and integration standards.

### Person 18 — Runtime / DevOps / Sandbox Engineer

Execution runtime, sandboxing, CI/CD, containers, packaging, and resource controls.

## Research / Release

### Person 19 — Security Research / Benchmark Engineer

Datasets, benchmarks, experiments, comparative evaluation, and research methodology.

### Person 20 — Documentation / Reproducibility / Release Engineer

Documentation, examples, reproducibility, release management, developer experience, and research artifacts.

---

# 7. Role Scaling Principle

Roles should scale by **responsibility**, not by simply adding people to the same task.

```text
3 people
↓
Broad ownership

5 people
↓
Basic specialization

7 people
↓
Lifecycle specialization

10 people
↓
Subsystem ownership

15 people
↓
Domain specialization

20 people
↓
Independent engineering and research tracks
```

---

# 8. Ownership Rules

Every critical subsystem should eventually have:

```text
Primary Owner
      +
Secondary / Backup Owner
```

No critical component should depend on only one person's knowledge.

Examples:

```text
Agent Core
Primary: Agent Engineer
Backup: Technical Lead

Validation
Primary: Validation Engineer
Backup: QA Engineer

Plugin SDK
Primary: Plugin Engineer
Backup: Platform Engineer
```

---

# 9. Cross-Team Responsibilities

Regardless of team size, every member should participate in:

- code review;
- documentation;
- testing;
- issue tracking;
- security review;
- reproducibility;
- relevant architecture discussions.

Specialization should not create isolated silos.

---

# 10. Recommended GitHub Ownership Mapping

A mature repository can map ownership approximately as:

```text
/agent/          → Agent team
/models/         → AI team
/memory/         → State team
/findings/       → Security analysis team
/remediation/    → Remediation team
/validation/     → Validation team
/plugins/        → Plugin/platform team
/runtime/        → Infrastructure team
/tests/          → QA/validation team
/docs/           → Documentation/research team
```

The exact mapping should follow the actual team composition.

---

# 11. Small-Team Rule

For teams of 3–7 people, do not create artificial departments.

One person should own several related areas.

For example:

```text
Person 1:
Architecture + Agent Core + Model Interface

Person 2:
Security Analysis + Remediation

Person 3:
Plugins + Validation + Testing
```

This is preferable to creating many nominal roles with no meaningful ownership.

---

# 12. Large-Team Rule

For teams of 10–20 people:

- define subsystem ownership;
- define interfaces between teams;
- require integration tests;
- maintain shared schemas;
- use code review;
- maintain backup ownership;
- document architectural decisions.

The technical lead should coordinate architecture rather than becoming the bottleneck for every implementation decision.

---

# 13. Final Principle

Team size should change **how responsibilities are distributed**, not the architecture of DEFSec.

The system should remain:

```text
Model-Agnostic
Tool-Agnostic
Plugin-Based
Stateful
Testable
Verifiable
Modular
```

Whether DEFSec is developed by three people or twenty, the core objective remains:

> Build a defensive agent that can understand security findings, determine appropriate remediation, execute controlled changes, and provide evidence that the resulting system is actually safer.
