# Cyber Agent Foundation

## 1. Overview

This document is the shared architecture for two sibling projects:

- **OffSec** — offensive-security agent (`docs/offsec/`)
- **DEFSec** — defensive-security agent (`docs/defsec/`)

They are not one monolithic application. They are separate repositories/workstreams
that share a common foundational architecture rather than depending on one another.

```text
                    Cyber Agent Foundation
                             │
              ┌──────────────┴──────────────┐
              │                             │
           OffSec                         DEFSec
              │                             │
       Offensive workflows          Defensive workflows
     Discover → Exploit           Analyze → Remediate
     Access → Post-Ex             Validate → Reassess
```

Either project is independently usable. Neither requires the other to function.
Where they meet is a shared vocabulary of objects (below) and, eventually, a
findings handoff: `OffSec finding → DEFSec remediation → validation → regression`.

---

## 2. Core Architectural Principle

> The model is replaceable.
> The tools are replaceable.
> The workflows are replaceable.
> The state remains persistent.

The core application must never depend directly on a particular model or a
particular security tool. No project should ever contain logic equivalent to:

```python
if model == Qwen3:
    ...
```

or

```text
run_nmap()
run_sqlmap()
run_nuclei()
```

Instead, everything domain-specific is a plugin behind a generic interface.

```text
                     ┌─────────────┐
                     │    User     │
                     └──────┬──────┘
                             │
                     ┌──────▼──────┐
                     │    Agent    │
                     │ Controller  │
                     └──────┬──────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
   ┌────▼────┐        ┌──────▼──────┐       ┌──────▼──────┐
   │  Model  │        │  Persistent  │       │   Plugin    │
   │Provider │        │    State     │       │  Registry   │
   └────┬────┘        └──────────────┘       └──────┬──────┘
        │                                            │
   ┌────▼──────┐                          ┌──────────▼──────────┐
   │ Local LLM │                          │  Capability Plugins  │
   │ Runtime   │                          │                      │
   └───────────┘                          └──────────────────────┘
```

---

## 3. Model Provider

Both projects must remain model-agnostic.

```text
ModelProvider
├── load()
├── unload()
├── generate()
├── stream()
├── tool_call()
├── metadata()
└── health_check()
```

Provider metadata should expose: `name, version, runtime, quantization,
context_length, tool_calling, hardware_requirements, capabilities`.

**Initial model candidate:** Qwen3 8B, 4-bit GGUF, via **llama.cpp**.
This is the first implementation target, not a permanent dependency — it must
be benchmarked (latency, VRAM, RAM, context, structured output, planning,
tool-calling) before being treated as the default. Other candidates: Llama,
Mistral, other open-weight models, cloud providers.

**Initial development hardware:** NVIDIA GTX 1660 Ti, 6 GB VRAM, 16 GB system
RAM. Sufficient for prototyping a small quantized model and building the
surrounding agent architecture — not for training a foundation model.

---

## 4. Plugin System

Every external capability is a plugin, discovered rather than hard-coded.

```text
ToolRegistry
discover() · install() · validate() · enable() · disable() · execute() · metadata()
```

```text
Plugin Lifecycle
Discover → Validate → Install → Enable → Use → Disable → Remove
```

A plugin exposes structured metadata: `name, version, description,
capabilities, input_schema, output_schema, requirements, dependencies`.

Plugin categories differ per project (see `offsec/architecture.md` and
`defsec/architecture.md`), but both share the same registry mechanics.

---

## 5. Persistent State

The LLM's context window is **not** the system's source of truth. Persistent
application state is authoritative; the model's context is temporary and
disposable.

**Initial database:** SQLite.

Shared concepts stored in state (each project extends this with domain
fields — see its own doc):

```text
Task / Objective
Plan
Asset
Finding
Evidence
Execution record
Error
Checkpoint
Timestamp
```

This lets a task survive context truncation, model restart, or process
restart, and be reconstructed from persisted state alone.

---

## 6. Execution Records / Evidence

"Evidence" means **machine-generated records of actual execution and
results** — tool output, scan results, captured responses, source-analysis
results, command output, timestamps, hashes, generated artifacts, execution
status.

It does **not** mean requiring the user to upload authorization documents.

```text
Execution
├── task
├── action
├── plugin
├── input
├── output
├── status
├── timestamp
└── artifacts
```

Purpose: reproducibility, auditing, debugging, state reconstruction, and —
critically — letting the application distinguish *what the model believes
happened* from *what the machine actually executed and returned*. This is
the architecture's primary defense against hallucination compounding across
a long-running task.

---

## 7. Findings

A normalized finding is the shared unit both projects reason and communicate
over.

```text
Finding
├── identifier
├── affected asset
├── domain
├── severity
├── observation
├── evidence
├── confidence
├── root cause          (DEFSec-focused)
├── remediation status  (DEFSec-focused)
├── validation status
└── related actions
```

The model is not the source of truth for these fields — structured
application state is.

---

## 8. Repository Layout Pattern

Both projects follow the same top-level shape; only the domain directories
(`findings/`, `remediation/` vs. `recon/`, `exploitation/`, etc.) differ.

```text
<project>/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── SECURITY.md
├── pyproject.toml
│
├── agent/
│   ├── controller/
│   ├── planner/
│   ├── executor/
│   ├── scheduler/
│   └── recovery/
│
├── models/
│   ├── interface/
│   ├── registry/
│   └── providers/
│
├── memory/
│   ├── state/
│   ├── checkpoints/
│   └── retrieval/
│
├── plugins/                # category subfolders differ per project
│
├── runtime/
│   └── adapters/
│
├── storage/
│   ├── schema/
│   └── migrations/
│
├── config/
├── tests/
├── docs/
└── scripts/
```

---

## 9. Shared Design Principles

- **Model independence** — changing the model must not require rewriting the agent.
- **Tool/capability independence** — adding a capability must not require modifying the core planner.
- **Persistent state** — long-running tasks must survive context limitations and restarts.
- **Resumability** — interrupted work must be recoverable.
- **Observability** — every meaningful operation produces an execution record.
- **Local-first** — the initial system operates without requiring cloud APIs.
- **Extensibility** — third parties should eventually be able to build plugins independently.
- **Progressive complexity** — the first release stays understandable and testable.
- **Evidence-gated action** — probable outcomes are not sufficient grounds to act; insufficient evidence means further investigation, not execution. (Sharpest form of this: OffSec's exploitation decision logic, see `offsec/architecture.md §Exploitation`.)

---

## 10. Development Philosophy

Build-first, not months of study before code:

```text
Build → Encounter Problem → Learn → Implement → Test → Measure → Document → Repeat
```

The objective at every stage is not a perfect autonomous system — it's an
architecture that gains capability progressively without the core being
rewritten each time.

---

## 11. Initial Local Software

Install only what Phase 0–1 need:

1. Linux development environment
2. Git
3. Python
4. Build tools required by the inference runtime
5. llama.cpp (or another compatible local runtime)
6. Qwen3 8B 4-bit GGUF
7. SQLite
8. NVIDIA driver/CUDA components appropriate to the machine
9. Normal development utilities

Do not install the wider security-tool ecosystem up front — the plugin
architecture exists specifically so capability is added incrementally.
