# OffSec — Architecture

Builds on `docs/00-foundation.md`. This file covers only what's specific to
the offensive-security agent: its lifecycle, plugin categories, and the
exploitation decision system.

## Lifecycle

```text
Discover → Enumerate → Analyze → Exploit → Gain Access →
Establish Persistence → Post-Exploitation → Validate → Report
```

## Plugin Categories

```text
plugins/
├── tools/         # recon/enumeration capabilities
├── analyzers/      # interpret tool output
├── workflows/       # reusable multi-step processes
├── exploits/       # see Exploitation below
└── exporters/
```

## Security Domain Coverage (target, not required day one)

Web, API, Application, Network, Linux, Windows, Cloud, Containers, Identity,
Active Directory, Source Code, Binary Analysis, Reverse Engineering, Malware
Analysis, OSINT, Wireless, Vulnerability Research, Configuration Auditing,
CTF/Labs. New domains arrive as plugins — the core agent stays unchanged.

## Exploitation

Exploitation follows the same non-dogmatic principle as the rest of the
architecture: choose the mechanism the evidence actually supports, don't
default to "always use established tools" or "always generate new code."

```text
                    Vulnerability Analysis
                             │
                             ▼
                    Exploitation Planner
                             │
              ┌──────────────┴──────────────┐
              │                             │
      Known vulnerability             Target-specific
      / established technique         vulnerability/logic
              │                             │
              ▼                             ▼
       Vetted tool/module             Generate PoC/test
              │                       Validate/analyze
              └──────────────┬──────────────┘
                             ▼
                    Controlled Execution → Actual Result → Result Analyzer
```

### Decision logic

```text
Known Vulnerability          → established/vetted capability
Application-specific behavior → generated test/PoC
Unknown/ambiguous observation → further enumeration/analysis
Insufficient evidence         → don't exploit; gather more information
```

The last branch matters most. "This is probably exploitable" is not
sufficient evidence to act against a real target. When evidence is
incomplete, the output is a structured statement of what's missing, not an
attempt:

```text
Evidence insufficient.
Required observations: A, B, C
Next recommended investigation: ...
```

### Provider categories

```text
ExploitProvider
├── Established/Vetted Provider     # wraps known, community-maintained frameworks
├── Generated PoC Provider          # target-specific tests, app logic no module anticipates
├── Web/API Test Generator
├── Custom Research Provider
└── Future providers
```

Established/vetted providers are the safe default for documented
vulnerabilities — predictable behavior against a live authorized target is a
requirement, not a nice-to-have. Generated providers earn their place by
covering what established tooling structurally can't (e.g. an authorization
check tied to a specific parameter relationship), not by replacing it.

### Maturity levels (generated providers)

```text
v1  Generate simple web/API test
v2  Generate target-specific PoCs
v3  Generate multi-step application tests
v4  Iterative generate → execute → observe → revise
v5  Advanced exploit-development workflows
```

v4/v5 — especially memory corruption and complex protocol vulnerabilities —
are materially harder than v1–v3 and are not an early milestone.

### Dependency on earlier stages

Recon/enumeration/analysis must output machine-structured findings plus
detailed, evidence-backed next-step plans — not free text. That's what lets
the Exploitation Planner consume that output directly instead of requiring
the recon system to be redesigned later.

## Post-Exploitation

Access maintenance and post-exploitation data-gathering (privilege context,
lateral-movement candidates, sensitive-data location) are structured
findings like everything else. **Covering tracks is an assisted action**:
the agent proposes what to clean up and why; execution requires explicit
human approval. Not a candidate for full automation at this stage, or later,
without a deliberate separate decision.

## Risk: exploitation reliability and scope safety

Freshly generated exploitation code has no track record against the target,
unlike a vetted framework module. Running unverified generated code against
a live, authorized system risks instability, service disruption, or
violating a program's rules against destructive testing.

Mitigations:
- route known vulnerabilities to established/vetted providers, not generated code;
- reserve generated PoCs for application-specific logic established tooling can't cover;
- treat insufficient evidence as a stop condition, not a reason to attempt anyway;
- keep access-maintenance and covering-tracks human-approved, not autonomous;
- cap generated-provider maturity at v1–v3 for the near-term milestone — v4/v5 carry the most risk and least reliability.
