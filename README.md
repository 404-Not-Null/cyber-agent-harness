# Cyber Agent Harness

Planning and architecture for two sibling, model-agnostic, plugin-based
cybersecurity agents built on a shared foundation:

- **[OffSec](docs/offsec/)** — offensive-security agent (recon → exploit → post-exploit).
- **[DEFSec](docs/defsec/)** — defensive-security agent (analyze → remediate → validate).

Both are independently usable; neither depends on the other to function.
Start with the shared architecture, then read whichever domain you're
working on.

## Reading order

1. [`docs/00-foundation.md`](docs/00-foundation.md) — shared architecture: model-provider abstraction, plugin system, persistent state, execution records, findings schema. Read this first regardless of which agent you're building.
2. [`docs/offsec/architecture.md`](docs/offsec/architecture.md) / [`docs/defsec/architecture.md`](docs/defsec/architecture.md) — domain-specific lifecycle and plugin categories.
3. [`docs/offsec/roadmap.md`](docs/offsec/roadmap.md) / [`docs/defsec/roadmap.md`](docs/defsec/roadmap.md) — phased build plan, each phase tagged `[SOLO]` or `[NEEDS TEAM]`.
4. [`docs/offsec/report.md`](docs/offsec/report.md) / [`docs/defsec/report.md`](docs/defsec/report.md) — motivation, risks, research questions, success criteria.
5. [`docs/offsec/team-roles.md`](docs/offsec/team-roles.md) / [`docs/defsec/team-roles.md`](docs/defsec/team-roles.md) — role assignment matrices for 3–20 person teams, for when people join.

## Status

Documentation/architecture stage. No code yet. Phases 0–7 (OffSec) and 0–8
(DEFSec) are solo-doable — that's the intended starting point before a team
forms.
