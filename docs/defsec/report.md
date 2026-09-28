# DEFSec — Project Report

Builds on `docs/00-foundation.md` and `docs/defsec/architecture.md`. Covers
motivation, research questions, evaluation, and success criteria specific to
the defensive-security agent.

## 1. Executive Summary

DEFSec is the defensive counterpart to OffSec. The central idea: finding a
vulnerability is only part of the security problem. A defensive system
should also understand the finding, propose an appropriate remediation,
implement or prepare the change, and verify the vulnerability is actually
resolved.

## 2. Motivation

Traditional security tooling often separates vulnerability discovery,
reporting, remediation, and validation. DEFSec explores whether an agent can
connect these stages while preserving structured state and independently
verifiable execution results — closing the gap between:

```text
"This is vulnerable."
```

and:

```text
"This is why it is vulnerable, this is the appropriate remediation,
this change was applied, and this test demonstrates the issue is resolved."
```

## 3. Agentic Behavior

DEFSec qualifies as agentic when it repeatedly: Observe → Reason → Select
capability → Act → Observe result → Update state → Continue. The model
supplies flexible reasoning; plugins provide deterministic capabilities;
persistent state preserves the task; the controller coordinates the
process.

## 4. Research Questions

- **RQ1** Can a local language model reliably transform structured security findings into actionable remediation plans?
- **RQ2** Can a model-generated remediation be automatically validated rather than merely reviewed syntactically?
- **RQ3** Can persistent structured state improve long-running defensive workflows?
- **RQ4** How does remediation quality vary between different model providers?
- **RQ5** Can the same defensive architecture operate across multiple cybersecurity domains?
- **RQ6** Can automated regression testing reduce the risk of incorrectly declaring a vulnerability fixed?

## 5. Evaluation

Evaluation must measure more than convincing prose. Potential metrics:
root-cause accuracy, remediation correctness, patch success rate, validation
accuracy, regression detection, false remediation rate, rollback success,
tool/plugin selection, structured output validity, task completion,
execution latency, resource usage. A remediation should ideally be evaluated
against an actual test environment, not judged solely by an LLM.

## 6. Initial Success Criteria

DEFSec's first major milestone is achieved when it can:

1. receive a structured finding;
2. analyze the finding;
3. identify a probable root cause;
4. propose remediation;
5. generate an appropriate change;
6. validate the change;
7. run regression tests;
8. persist all results;
9. recover an interrupted task;
10. produce a final report.

The system does not need to support every security domain to demonstrate
the architecture.

## 7. Long-Term Vision

```text
Security Assessment → Finding → DEFSec Analysis → Remediation →
Validation → Regression → Continuous Monitoring
```

Combined with OffSec:

```text
                  Shared Foundation
                         │
          ┌──────────────┴──────────────┐
          │                             │
        OffSec                        DEFSec
      Discover/Enumerate/           Analyze/Remediate/
      Exploit/Post-exploit          Validate/Re-test/Monitor
```

The two systems form complementary offensive and defensive platforms
without either repository depending directly on the other.

## 8. Final Architectural Principle

> The model is replaceable.
> The tools are replaceable.
> The remediation mechanisms are replaceable.
> The validation mechanisms are replaceable.
> The state remains persistent.
