# OffSec — Team Role Assignment Matrix

## Purpose

This document defines recommended role assignments for OffSec teams of different sizes: **3**, **5**, **7**, **10**, **15**, and **20** people.

The same core responsibilities exist at every team size, but smaller teams combine roles while larger teams specialize them.

OffSec focuses on the offensive-security lifecycle:

```
Discover
   ↓
Enumerate
   ↓
Analyze
   ↓
Exploit
   ↓
Gain Access
   ↓
Establish Persistence
   ↓
Post-Exploitation
   ↓
Validate
   ↓
Report
```

### Core responsibility areas

1. Architecture / Technical Leadership
2. Agent & Orchestration
3. Model / AI Engineering
4. Reconnaissance & Enumeration
5. Vulnerability Research & Exploitation
6. Access / Persistence / Post-Exploitation
7. Validation & Evidence
8. Plugin / Tooling Engineering
9. Infrastructure / Runtime / Sandbox
10. Research / Evaluation / Documentation

---

## 1. Three-Person Team

A three-person team should avoid artificial specialization.

### Person 1 — Technical Lead / Architecture / Agent Core

**Owns:**

- overall architecture
- shared cyber-agent foundation
- agent controller
- workflow engine
- persistent state
- model-provider interface
- plugin interfaces
- execution policy
- integration and code review

**Primary areas:**

- `agent/`
- `models/`
- `memory/`
- `core/`

### Person 2 — Offensive Security / Reconnaissance / Exploitation

**Owns:**

- reconnaissance
- asset discovery
- enumeration
- service analysis
- vulnerability identification
- exploit research
- controlled exploitation
- finding normalization
- offensive-security methodology

**Primary areas:**

- `recon/`
- `enumeration/`
- `analysis/`
- `exploitation/`
- `findings/`

### Person 3 — Access / Post-Exploitation / Validation

**Owns:**

- controlled access workflows
- privilege escalation
- persistence testing
- post-exploitation
- lateral-movement workflows where applicable
- evidence collection
- validation
- cleanup
- offensive benchmarks
- test environments

**Primary areas:**

- `access/`
- `persistence/`
- `post_exploitation/`
- `validation/`
- `tests/`

### Three-Person Model

```
                 Person 1
        Architecture + Agent Core
                 │
          ┌──────┴──────┐
          │             │
       Person 2       Person 3
     Recon + Exploit  Access + Post-Ex
```

---

## 2. Five-Person Team

### Person 1 — Technical Lead / Architecture

- architecture
- shared foundation
- agent interfaces
- integration
- state model
- execution policy
- code review

### Person 2 — Agent / Model Engineering

- model providers
- context handling
- structured outputs
- planning
- task decomposition
- tool selection
- agent loops
- model evaluation

### Person 3 — Reconnaissance / Enumeration Engineer

- reconnaissance
- asset discovery
- service enumeration
- network mapping
- technology identification
- information gathering
- reconnaissance plugins

### Person 4 — Vulnerability Research / Exploitation Engineer

- vulnerability analysis
- exploit research
- exploit development/adaptation
- controlled exploitation
- exploit validation
- finding generation

### Person 5 — Access / Post-Exploitation / Validation Engineer

- access workflows
- privilege escalation testing
- persistence testing
- post-exploitation
- evidence collection
- validation
- cleanup
- benchmarks and test environments

---

## 3. Seven-Person Team

### Person 1 — Technical Lead / Architect

Owns architecture, interfaces, shared foundation, integration, and technical direction.

### Person 2 — Agent / Orchestration Engineer

**Owns:**

- agent controller
- workflow engine
- planning
- task execution
- recovery
- state transitions
- execution coordination

### Person 3 — Model / AI Engineer

**Owns:**

- model providers
- inference
- structured generation
- context management
- tool selection
- model evaluation

### Person 4 — Reconnaissance Engineer

**Owns:**

- reconnaissance
- asset discovery
- network/service enumeration
- technology fingerprinting
- attack-surface mapping

### Person 5 — Vulnerability Researcher / Exploitation Engineer

**Owns:**

- vulnerability analysis
- exploit research
- exploit development/adaptation
- exploitation workflows
- exploit evidence

### Person 6 — Access / Persistence Engineer

**Owns:**

- initial-access workflows
- privilege escalation
- persistence
- credential/access workflows
- controlled post-access operations

### Person 7 — Post-Exploitation / Validation Engineer

**Owns:**

- post-exploitation workflows
- evidence collection
- objective validation
- attack-chain reconstruction
- cleanup
- regression/safety testing
- offensive benchmarks

---

## 4. Ten-Person Team

| Person | Primary Role                          | Main Ownership                                      |
|--------|---------------------------------------|-----------------------------------------------------|
| 1      | Technical Lead                        | Architecture, integration, standards                |
| 2      | Agent Core Engineer                   | Controller, planner, execution loop                 |
| 3      | Model Engineer                        | Providers, inference, structured outputs            |
| 4      | State / Memory Engineer               | Persistence, checkpoints, artifacts                 |
| 5      | Reconnaissance Engineer               | Discovery, enumeration, attack-surface mapping      |
| 6      | Vulnerability Research Engineer       | Vulnerability analysis and research                 |
| 7      | Exploitation Engineer                 | Exploit development, adaptation, execution          |
| 8      | Access / Post-Exploitation Engineer   | Access, privilege escalation, persistence           |
| 9      | Validation / Evidence Engineer        | Validation, evidence, attack-chain verification     |
| 10     | Plugin / Runtime / Research Engineer  | Tool adapters, sandbox, benchmarks, documentation   |

---

## 5. Fifteen-Person Team

### Leadership / Architecture

**Person 1 — Technical Lead**  
Architecture, technical direction, integration, engineering standards, and cross-team coordination.

**Person 2 — Systems Architect**  
Interfaces, performance, reliability, execution architecture, and shared infrastructure.

### Agent / AI

**Person 3 — Agent Engineer**  
Agent loop, planning, workflow execution, recovery, and task lifecycle.

**Person 4 — Model Engineer**  
Model providers, inference, structured generation, context handling, and local/cloud model integration.

**Person 5 — AI Evaluation Engineer**  
Model benchmarks, tool-selection experiments, context experiments, output-quality measurements, and model comparison.

### Reconnaissance / Analysis

**Person 6 — Reconnaissance Engineer**  
Asset discovery, reconnaissance workflows, network/service enumeration, and attack-surface mapping.

**Person 7 — Application / Web Security Engineer**  
Application discovery, API analysis, web-security testing, and application attack paths.

**Person 8 — Network / Infrastructure Security Engineer**  
Network services, hosts, infrastructure, authentication services, configuration weaknesses, and infrastructure attack paths.

### Exploitation / Access

**Person 9 — Vulnerability Research Engineer**  
Vulnerability research, root-cause analysis, exploitability assessment, and exploit research.

**Person 10 — Exploitation Engineer**  
Exploit development, exploit adaptation, controlled execution, exploit reliability, and exploitation plugins.

**Person 11 — Access / Privilege Escalation Engineer**  
Initial access, privilege escalation, credential-access workflows, and access validation.

### Post-Exploitation / Validation

**Person 12 — Persistence / Post-Exploitation Engineer**  
Persistence testing, post-exploitation workflows, objective execution, and attack-chain continuation.

**Person 13 — Validation / Evidence Engineer**  
Attack validation, evidence collection, reproducibility, cleanup, and verification.

### Platform / Research

**Person 14 — Plugin / Tooling / Runtime Engineer**  
Plugin SDK, tool adapters, execution runtime, sandboxing, CI/CD, packaging, and deployment.

**Person 15 — Research / Documentation Engineer**  
Benchmarks, experiments, methodology, reproducibility, technical documentation, and project reporting.

---

## 6. Twenty-Person Team

### Architecture

**Person 1 — Technical Director / Lead Architect**  
Overall architecture, technical direction, cross-team integration, and major design decisions.

**Person 2 — Systems Architect**  
System interfaces, performance, reliability, execution infrastructure, and shared component design.

### Agent Platform

**Person 3 — Agent Controller Engineer**  
Controller, execution loop, task lifecycle, and agent runtime.

**Person 4 — Workflow / Planning Engineer**  
Planning, workflow graphs, task decomposition, recovery logic, and attack-chain orchestration.

**Person 5 — State / Memory Engineer**  
Persistent state, checkpoints, artifact storage, evidence state, and long-running task state.

### AI / Models

**Person 6 — Model Runtime Engineer**  
Local inference, provider abstraction, model lifecycle, and resource management.

**Person 7 — Model Evaluation Engineer**  
Model benchmarks, quality measurements, tool-selection evaluation, and experiments.

**Person 8 — Context / Prompt Engineering Researcher**  
Context construction, structured prompting, memory retrieval, reasoning workflows, and model-behavior evaluation.

### Reconnaissance

**Person 9 — Reconnaissance Engineer**  
Asset discovery, reconnaissance workflows, attack-surface mapping, and information collection.

**Person 10 — Enumeration / Network Security Engineer**  
Network discovery, service enumeration, protocol analysis, host enumeration, and infrastructure mapping.

### Vulnerability Research

**Person 11 — Vulnerability Research Engineer**  
Vulnerability discovery, research, exploitability analysis, and vulnerability correlation.

**Person 12 — Application Security Engineer**  
Web/API/application security analysis, application attack paths, and application exploitation research.

### Exploitation

**Person 13 — Exploit Development Engineer**  
Exploit development, adaptation, reliability, exploit-chain construction, and exploit plugins.

**Person 14 — Exploitation Operations Engineer**  
Controlled exploitation, target interaction, access acquisition, execution workflows, and operational evidence.

### Access / Post-Exploitation

**Person 15 — Privilege Escalation Engineer**  
Privilege escalation research, credential/access workflows, and privilege-validation techniques.

**Person 16 — Persistence / Post-Exploitation Engineer**  
Persistence testing, post-exploitation workflows, objective execution, and attack-chain continuation.

### Validation / Platform

**Person 17 — Offensive Validation Engineer**  
Independent attack validation, evidence verification, reproducibility, cleanup, and final attack-chain confirmation.

**Person 18 — Plugin / Tooling Engineer**  
Plugin SDK, tool adapters, capability interfaces, integrations, and exporters.

### Runtime / Research

**Person 19 — Runtime / Sandbox / DevOps Engineer**  
Execution environments, isolation, sandboxing, CI/CD, containers, resource controls, and deployment.

**Person 20 — Research / Benchmark / Documentation Engineer**  
Benchmarks, datasets, experiments, comparative evaluation, reproducibility, documentation, and release artifacts.

---

## 7. Role Scaling Principle

Roles should scale by responsibility, not by simply adding people to the same task.

```
3 people
↓
Broad offensive ownership

5 people
↓
Basic specialization

7 people
↓
Attack-lifecycle specialization

10 people
↓
Subsystem ownership

15 people
↓
Domain specialization

20 people
↓
Independent offensive-security tracks
```

The architecture should remain the same while ownership becomes more granular.

---

## 8. Ownership Rules

Every critical subsystem should eventually have:

```
Primary Owner
      +
Secondary / Backup Owner
```

No critical component should depend on only one person's knowledge.

**Examples:**

| Subsystem        | Primary                    | Backup                     |
|------------------|----------------------------|----------------------------|
| Agent Core       | Agent Engineer             | Technical Lead             |
| Reconnaissance   | Recon Engineer             | Network Security Engineer  |
| Exploitation     | Exploitation Engineer      | Vulnerability Research Engineer |
| Post-Exploitation| Post-Exploitation Engineer | Access Engineer            |
| Validation       | Validation Engineer        | Research Engineer          |
| Plugin SDK       | Plugin Engineer            | Runtime Engineer           |

---

## 9. Cross-Team Responsibilities

Regardless of team size, every member should participate in:

- code review
- documentation
- testing
- issue tracking
- security review
- reproducibility
- evidence preservation
- architecture discussions where relevant

Specialization should not create isolated silos.

The offensive lifecycle should remain connected:

```
Recon
  ↓
Enumeration
  ↓
Vulnerability Analysis
  ↓
Exploitation
  ↓
Access
  ↓
Persistence
  ↓
Post-Exploitation
  ↓
Validation
  ↓
Evidence
```

---

## 10. Recommended GitHub Ownership Mapping

A mature OffSec repository can map ownership approximately as:

| Path                   | Team                        |
|------------------------|-----------------------------|
| `/agent/`              | Agent team                  |
| `/models/`             | AI team                     |
| `/memory/`             | State team                  |
| `/recon/`              | Reconnaissance team         |
| `/enumeration/`        | Enumeration team            |
| `/analysis/`           | Vulnerability research team |
| `/exploitation/`       | Exploitation team           |
| `/access/`             | Access team                 |
| `/privilege/`          | Privilege escalation team   |
| `/persistence/`        | Persistence team            |
| `/post_exploitation/`  | Post-exploitation team      |
| `/findings/`           | Findings/evidence team      |
| `/validation/`         | Validation team             |
| `/plugins/`            | Plugin/tooling team         |
| `/runtime/`            | Infrastructure/runtime team |
| `/tests/`              | QA/validation team          |
| `/docs/`               | Documentation/research team |

The exact mapping should follow the actual repository structure as it develops.

---

## 11. Small-Team Rule

For teams of **3–7 people**, do not create artificial departments.

One person should own several closely related areas.

**Example:**

- **Person 1:** Architecture + Agent Core + Model Interface
- **Person 2:** Reconnaissance + Vulnerability Analysis + Exploitation
- **Person 3:** Access + Persistence + Post-Exploitation + Validation

This is preferable to creating many nominal roles with no meaningful ownership.

---

## 12. Large-Team Rule

For teams of **10–20 people**:

- define subsystem ownership
- define interfaces between teams
- require integration tests
- maintain shared schemas
- use code review
- maintain backup ownership
- document architectural decisions
- maintain reproducible offensive test environments
- preserve structured evidence throughout an attack chain

The technical lead should coordinate architecture rather than becoming the bottleneck for every implementation decision.

---

## 13. Relationship to DEFSec

OffSec and DEFSec are sibling systems built around the shared cyber-agent foundation.

```
                 Shared Cyber-Agent Core
                         │
              ┌──────────┴──────────┐
              ▼                     ▼
           OffSec                 DEFSec
         Offensive              Defensive
              │                     │
      Discover / Exploit      Analyze / Remediate
      Access / Post-Ex        Validate / Reassess
              │                     │
              └──────────┬──────────┘
                         ▼
                  Security Feedback
```

OffSec focuses on discovering and validating weaknesses through controlled offensive workflows.

DEFSec focuses on understanding those weaknesses, producing remediation, and validating the resulting system.

The repositories remain independently usable while sharing appropriate foundational components and interfaces.

---

## 14. Final Principle

Team size should change how responsibilities are distributed, not the fundamental architecture of OffSec.

The system should remain:

- **Model-Agnostic**
- **Tool-Agnostic**
- **Plugin-Based**
- **Stateful**
- **Testable**
- **Verifiable**
- **Modular**
- **Evidence-Driven**

The long-term objective is an offensive-security agent capable of moving through a structured lifecycle:

```
Observe
   ↓
Discover
   ↓
Enumerate
   ↓
Analyze
   ↓
Exploit
   ↓
Access
   ↓
Persist
   ↓
Post-Exploit
   ↓
Validate
   ↓
Report
```

The model provides reasoning and planning; deterministic capabilities perform tool execution, enforce execution constraints, collect evidence, maintain state, and verify results.
