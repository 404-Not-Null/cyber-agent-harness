# DEFSec — Roadmap

Every phase is tagged `[SOLO]` or `[NEEDS TEAM]`, the same convention as
`offsec/roadmap.md`. Phases 0–8 are solo-doable — start here before anyone
else is on board.

---

## Phase 0 — Foundation `[SOLO]`

- Initialize repository; define architecture, shared data structures, `ModelProvider`, plugin interfaces, findings schema, remediation schema, validation schema.

**Exit condition:** a defensive workflow can be represented without hard-coding a particular model or security tool.

## Phase 1 — Local Model Runtime `[SOLO]`

Use the shared foundation's model candidate. Measure latency, VRAM, RAM,
context, structured output, planning, code/configuration reasoning.

**Exit condition:** DEFSec accesses the model exclusively through `ModelProvider`.

## Phase 2 — Defensive Agent Loop `[SOLO]`

```text
Finding → Analysis → Remediation Plan → Validation Plan → Execution → Result → State Update
```

Controller contains no domain-specific remediation logic.

## Phase 3 — Persistent State `[SOLO]`

SQLite-backed state: assets, findings, evidence, remediation plans, changes,
validation, regression tests, errors, checkpoints.

**Exit condition:** a remediation task can be interrupted and resumed.

## Phase 4 — Plugin System `[SOLO]`

Analyzer, Remediation, Validator, Scanner, Configuration, Patcher, Workflow,
Exporter plugins.

**Exit condition:** a new defensive capability installs without modifying the DEFSec core.

## Phase 5 — Finding Analysis `[SOLO]`

Structured analysis: what was observed, which component is affected, likely
root cause, supporting evidence, missing information, applicable remediation
categories. The model reasons over structured observations, not raw
conversational history alone.

## Phase 6 — Remediation Planning `[SOLO]`

```text
Finding → Root Cause → Possible Remediations → Risk/Impact →
Recommended Change → Validation Plan
```

## Phase 7 — Automated Remediation `[SOLO, review recommended]`

Introduce controlled remediation plugins, distinguishing Generate / Apply /
Validate / Rollback. A generated patch is not automatically correct.

*A second reviewer on apply/rollback logic is worth having before running
this against anything real — solo is fine for building it.*

## Phase 8 — Validation `[SOLO]`

```text
Before → Finding exists → Apply remediation → After →
Re-run relevant test → Compare results
```

Validator provides machine-readable status.

---

*Everything above: one person can build and run it. Below: still startable
solo, but genuinely benefits from more people as domain and plugin surface
area grows.*

---

## Phase 9 — Regression Testing `[SOLO to start, NEEDS TEAM to scale]`

Test original vulnerability, related functionality, expected application
behavior, build/startup, relevant security controls, per finding.

> Fix the security problem without silently introducing another problem.

## Phase 10 — Defensive Domain Expansion `[NEEDS TEAM]`

Web/API, Network, Linux, Windows, Cloud, Containers, Identity, Source Code —
each domain is real, parallel work once it's more than one or two domains at
a time.

## Phase 11 — OffSec/DEFSec Interoperability `[SOLO]`

Establish compatible schemas (`Asset, Finding, Evidence, Artifact,
Execution, Assessment`) per `architecture.md §Interoperability`. Neither
repository requires the other.

## Phase 12 — Multi-Model Evaluation `[NEEDS TEAM to go fast, SOLO to start]`

Compare model providers on the same defensive tasks: root-cause
identification, remediation quality, patch correctness, configuration
correctness, validation planning, regression awareness, structured output,
hallucination rate, execution efficiency.

## Phase 13 — Long-Running Remediation `[SOLO]`

Job queue, checkpoints, pause/resume, failure recovery, rollback, resource
limits, cancellation.

## Phase 14 — Public Plugin Ecosystem `[NEEDS TEAM]`

Plugin SDK, templates, docs, compatibility rules, test harness, example
defensive plugins.

## Phase 15 — Release Candidate `[NEEDS TEAM]`

Stabilize APIs, improve error handling, test model replacement/plugin
failures/rollback/interrupted tasks/validation failures/regression failures,
document architecture.

## Phase 16 — Public Release `[NEEDS TEAM]`

Source, architecture, plugin SDK, model setup, example workflows,
benchmarks, defensive methodology, contribution guide.

---

## Initial Milestone `[SOLO]`

```text
Finding → Analysis → Remediation proposal → Change generation →
Validation → Regression test → Report
```

More important than supporting a large number of defensive tools
immediately.

## Long-Term Success Criteria

> Take a structured security finding and: understand it, identify its root
> cause, determine possible remediation strategies, generate an appropriate
> change, apply it when permitted, validate the original issue, perform
> regression testing, roll back when necessary, preserve complete execution
> history, produce a final defensive report — independent of any single
> model, security product, scanner, patching mechanism, or cloud provider.
