# DEFSec — Architecture

Builds on `docs/00-foundation.md`. This file covers only what's specific to
the defensive-security agent: its lifecycle, plugin categories, and the
remediation/validation model.

## Lifecycle

```text
Observe → Analyze → Identify Finding → Determine Root Cause →
Generate Remediation → Apply Change → Validate → Regression Test →
Record Result → Report
```

The system distinguishes: a *proposed* remediation, an *applied*
remediation, a *validated* remediation, and a remediation that *failed
validation*.

## Plugin Categories

```text
plugins/
├── analyzers/       # interpret findings, determine root causes
├── remediation/      # generate proposed fixes
├── validators/       # determine whether a remediation actually worked
├── scanners/         # discover defensive weaknesses / verify system state
├── configuration/     # modify and validate security configuration
├── patchers/          # apply controlled code/dependency changes
├── workflows/         # coordinate multi-step defensive operations
└── exporters/         # reports, machine-readable results
```

## Security Domain Coverage (target, not required day one)

Web/API, network, Linux, Windows, cloud, containers, identity/directory
services, source code, dependencies, configuration, endpoint security,
infrastructure, security monitoring, vulnerability management.

## Remediation Model

A remediation is represented separately from the finding it addresses:

```text
Remediation
├── finding_id
├── type
├── rationale
├── proposed changes
├── affected files/configuration
├── prerequisites
├── risk
├── validation plan
└── rollback information
```

Remediation types: source-code patch, dependency update, configuration
change, access-control change, network-control change, security-policy
change, infrastructure change, monitoring/detection change. The model
selects among these based on evidence — not every finding is a coding
problem.

## Validation Model

A remediation is not successful merely because a file changed.

```text
Patch Generated → Patch Applied → System Builds/Starts →
Original Finding Re-tested → Finding Resolved? → Regression Tests → Final Status
```

Statuses: `PROPOSED`, `APPLIED`, `VALIDATED`, `FAILED`, `ROLLED_BACK`,
`PARTIALLY_VALIDATED`.

## Regression Testing

A remediation can create new problems. Maintain reusable per-finding tests:

```text
Finding F-001
├── Reproduction test
├── Remediation
├── Security regression test
└── Functional regression test
```

Goal: fix the security problem without silently introducing another one.

## DEFSec-Specific Design Principles

Beyond the shared principles in `00-foundation.md §9`:

- **Verification first** — a proposed fix is not equivalent to a verified fix.
- **Least necessary change** — remediation avoids unnecessary changes to unrelated components.
- **Domain independence** — the core must not assume every finding is a code vulnerability.

## Risks (DEFSec-specific)

| Risk | Mitigation |
|---|---|
| Incorrect remediation (doesn't address root cause) | Independent validation |
| Functional regression (fix breaks legitimate behavior) | Regression testing |
| Excessive changes | Minimal-change principle, explicit change plans |
| Model hallucination about the vulnerability | Structured evidence, deterministic analyzers, validation, persistent state |
| Plugin failure (malformed/incomplete tool output) | Schemas, validation, plugin isolation, execution status |

## Interoperability with OffSec

Repositories remain independent, but share compatible schemas for `Asset,
Finding, Evidence, Artifact, Execution, Assessment`, enabling a future
workflow:

```text
OffSec → Finding → DEFSec → Remediation → Validation → Regression
```

Neither repository requires the other to function.
