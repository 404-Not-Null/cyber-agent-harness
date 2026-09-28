# OffSec — Roadmap

Every phase is tagged `[SOLO]` or `[NEEDS TEAM]`. The tag is the honest
answer to "can I do this alone right now," not an aspiration — a phase only
gets `[NEEDS TEAM]` once it genuinely needs parallel hands (multiple
plugin domains built at once, dedicated infra/sandbox work, etc.), not
because it "would go faster with people."

**Everything through Phase 7 is solo-doable.** That's deliberate: it's what
you can start on today, before anyone else is on board. Phases 8+ are marked
per-task since some post-exploitation/access work benefits from a second
person for review even at small scale.

The milestone dates below (January, next December) are **estimates for
sequencing, not commitments** — they exist to order the work, not to promise
a delivery date.

---

## Phase 0 — Foundation `[SOLO]`

- Create repository, license, docs.
- Define `ModelProvider` interface.
- Define tool-plugin interface.
- Define state requirements.
- Define plugin manifests.

**Exit condition:** you can explain how to add a new model or tool without
touching the core agent.

## Phase 1 — Local Model Runtime `[SOLO]`

- Install local inference runtime (llama.cpp).
- Load Qwen3 8B 4-bit GGUF, test generation/streaming/context/structured output/tool-calling.
- Measure RAM, VRAM, inference speed.

**Deliverable:** `ModelProvider → QwenProvider`.
**Exit condition:** the rest of the app talks to the model only through the provider interface.

## Phase 2 — Agent Loop `[SOLO]`

```text
User Objective → Create Plan → Select Capability → Execute →
Record Result → Update State → Re-plan → Continue
```

**Exit condition:** the agent completes a controlled multi-step task.

## Phase 3 — Persistent State `[SOLO]`

- SQLite store for tasks, objectives, plans, actions, outputs, findings, errors, checkpoints, timestamps.

**Exit condition:** stop and restart the agent without losing task state.

## Phase 4 — Plugin System `[SOLO]`

- Categories: Model, Tool, Analyzer, Workflow, Exploit, Exporter.
- Lifecycle: Discover → Validate → Install → Enable → Use → Disable → Remove.

**Exit condition:** a new capability installs without touching the agent core.

## Phase 5 — First Capability Plugins `[SOLO]`

Prove the mechanics with a small number of plugins, not the whole ecosystem:
discovery, schema validation, execution, structured output, persistence,
error handling.

**Exit condition:** multiple independently-implemented capabilities work through the same interface.

## Phase 6 — Execution Records `[SOLO]`

Persistent history of what actually happened (not an authorization-document
system):

```text
Task → Action (input, tool, output, timestamp, status) → Finding (description, source, confidence, related actions)
```

**Exit condition:** the agent can reconstruct what actually happened during a previous run.

## Phase 7 — Recon/Enumeration Domain Expansion `[SOLO]`

Priority order for the first (~January) milestone: **Web/API first, Network
second** — those give the recon/enumeration milestone real coverage fastest.
Remaining domains (Linux, Windows, source-code, cloud, containers, identity,
binary/reverse-engineering, malware, OSINT, wireless, vuln research, config
auditing, CTF/labs) follow as capacity allows — this order is a practical
sequence, not a ranking.

Every domain's output must be machine-structured findings plus a detailed,
evidence-backed next-step plan (see `architecture.md`) — that's the
interface Phase 8 consumes directly.

**Exit condition:** the agent performs recon/enumeration through real
plugins, persists structured findings, and produces evidence-backed
next-step recommendations. No exploitation yet.

---

*Everything above this line: you can build it alone. Below: still
soloable in the sense that one person can start it, but items benefit from a
second reviewer as they get access to riskier operations — noted per-task.*

---

## Phase 8 — Exploitation Orchestration `[SOLO, review recommended]`

- Exploitation Planner routing: known vuln → vetted provider; app-specific → generated PoC; ambiguous → more enumeration; insufficient evidence → no action.
- Wrap established/vetted frameworks for documented vulnerabilities.
- Build Generated PoC Provider to v1–v3 maturity only (v4/v5 explicitly deferred).
- Every attempt (success or fail) feeds the execution-record system.
- Planner's only input is Stage 7 output — never unstructured observations.

**Exit condition:** the agent selects and executes the right exploitation
mechanism for a documented finding, and correctly declines when evidence is
insufficient.

*A second reviewer on the routing logic (especially the "don't act" branch)
is worth having before running this against anything live — solo is fine for
building it.*

## Phase 9 — Access Maintenance & Post-Exploitation `[NEEDS TEAM for scale, SOLO to start]`

- Access-maintenance as its own provider category, scoped to authorized engagements.
- Post-exploitation findings (privilege context, lateral-movement candidates, sensitive-data location) as structured records.
- Covering tracks: **assisted only** — agent proposes, human approves execution. Not an automation target now or later without a deliberate separate decision.

**Exit condition:** the agent can propose, and with approval carry out,
access-maintenance and post-exploitation steps, with covering tracks staying
human-gated throughout.

*This is where a second person genuinely helps — reviewing proposed
post-exploitation actions before approval is a natural two-person check, not
a nice-to-have.*

## Phase 10 — Multi-Model Support `[NEEDS TEAM to go fast, SOLO to start]`

Add a second model provider (Llama, Mistral, other open-weight models) once
the first is reliable. Registry should support selection by VRAM, RAM,
context length, tool support, latency, reasoning performance, quantization.

## Phase 11 — Benchmarking `[SOLO or NEEDS TEAM — scales either way]`

Project-specific benchmark across reasoning, agent behavior, reliability,
performance (tokens/sec, startup time, VRAM, RAM, CPU).

## Phase 12 — Long-Running Workflows `[SOLO]`

Job queue, checkpoints, pause/resume, cancellation, timeouts, failure
recovery, resource limits.

## Phase 13 — Plugin Ecosystem `[NEEDS TEAM]`

Stable public plugin API, docs, templates, example plugins, versioning, test
harness. This is genuinely a "more hands make it real" phase — one person
writing a plugin SDK in isolation tends to guess wrong about what external
contributors need.

## Phase 14 — Performance & Hardware Scaling `[NEEDS TEAM]`

Only after real benchmarks: larger models, more VRAM, GPU offloading,
multi-GPU, model routing, optimized quantization, dedicated hardware.

## Phase 15 — Release Candidate `[NEEDS TEAM]`

Stabilize plugin API, harden error handling, test model replacement/plugin
failure/interrupted tasks/restart-resume, document installation/architecture/plugin development.

## Phase 16 — Public Release `[NEEDS TEAM]`

Source, architecture docs, install docs, model setup, plugin SDK, example
plugins, benchmark results, roadmap, contribution guide.

---

## First-Week Target `[SOLO]`

By end of week one:

- repository initialized
- local model running
- provider abstraction working
- basic agent loop working
- SQLite state store working
- one example plugin
- execution records stored
- restart/resume demonstrated

Not every cybersecurity domain in week one. Architecture first.

## Long-Term Success Condition

> Install a model plugin and capability plugins, give the agent a
> security-research objective, let it plan and execute, stop it, restart it,
> and have it reconstruct the task from persistent state — without
> rewriting the core for each new model or tool. At the exploitation stage:
> correctly route a known vulnerability to a vetted provider, correctly
> generate a scoped test for application-specific logic, and correctly
> decline to act when evidence is insufficient.
