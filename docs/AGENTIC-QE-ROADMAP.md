# Agentic Quality Engineering Roadmap

## Vision

Evolve Quality Engineering from isolated automation scripts into an **observable, evidence-producing validation system** in which agents can assist with analysis, generation, orchestration and diagnosis while humans retain release accountability.

## Target pipeline

```text
Test Data
   ↓
Agent Evals
   ↓
Automated Execution
   ↓
Differential Testing
   ↓
Observability
   ↓
Evidence
   ↓
Risk-based Release Decision
```

## Architectural principle

An agent should not be trusted because it produced a plausible test. It should be evaluated by whether its output is:

- traceable to an explicit requirement or risk;
- executable and deterministic enough for the use case;
- able to distinguish expected from unexpected behavior;
- observable during execution;
- reviewable through retained evidence;
- bounded by permissions and environment controls;
- measured against known evaluation cases.

---

## Stage 0 — Deterministic Quality Foundation

Before adding agents, establish:

- versioned test assets;
- repeatable environment setup;
- controlled test data;
- automation entry points;
- result schemas;
- evidence retention;
- clear PASS / FAIL / BLOCKED semantics.

**Exit criterion:** conventional automation is reliable enough that an agent can orchestrate it without hiding instability.

---

## Stage 1 — Test Data Capability

Treat test data as a first-class capability.

### Goals

- known datasets mapped to risk scenarios;
- reproducible setup and cleanup;
- synthetic/sanitized data where necessary;
- source and expected-target representations for data workflows;
- provenance for generated test data.

### Evidence

```text
Dataset ID
Scenario / risk
Generation source
Input values
Expected transformation/output
Environment
Cleanup policy
```

---

## Stage 2 — Agent Evals

Before an agent can participate in validation, evaluate the agent itself.

### Example eval dimensions

- requirement interpretation accuracy;
- scenario relevance;
- risk coverage;
- hallucination rate;
- invalid-step rate;
- correct tool selection;
- expected-result quality;
- reproducibility;
- unsafe / unauthorized action rate.

### Golden set

Maintain a curated set of known tickets/changes with human-reviewed:

- risks;
- scenarios;
- expected results;
- test data;
- known defects;
- acceptable evidence.

Compare new agent outputs against that baseline.

---

## Stage 3 — Automated Execution

Agents orchestrate approved deterministic tools rather than directly improvising uncontrolled actions.

```text
Agent plan
   ↓
Policy / permission check
   ↓
Approved test adapter
   ↓
Execution engine
   ↓
Structured result
```

Possible adapters:

- Playwright;
- API clients;
- SQL validation;
- ETL reconciliation scripts;
- performance tooling;
- log/metric queries.

**Control:** the execution layer must return machine-readable status and artifacts.

---

## Stage 4 — Differential Testing

For data and transformation-heavy systems, compare observations rather than relying only on static expected values.

Examples:

- source vs target;
- old implementation vs new implementation;
- baseline build vs candidate build;
- expected transformation vs actual transformation;
- API version A vs version B.

Capture:

```text
Comparison key
Baseline
Candidate
Difference
Tolerance / rule
Classification
```

This is especially valuable for ETL, reporting, exports, migrations and backward-compatibility validation.

---

## Stage 5 — Test Observability

Automation without observability creates opaque failures.

Collect as applicable:

- test run ID;
- scenario / risk ID;
- timestamps and duration;
- environment/build;
- agent/tool version;
- prompts/instructions or generated-plan reference;
- requests/responses;
- logs;
- traces;
- screenshots/video;
- database comparisons;
- retry history;
- failure classification.

### Desired question

A reviewer should be able to answer:

> Why did this validation reach this result, and what evidence supports it?

---

## Stage 6 — Evidence Layer

Normalize heterogeneous execution output into a consistent evidence record.

```json
{
  "validationId": "VAL-001",
  "risk": "Precision loss during transformation",
  "status": "PASS",
  "environment": "candidate",
  "observed": "0.00",
  "expected": "0.00",
  "artifacts": [],
  "residualRisk": "Other precision scales not covered"
}
```

The schema should support both human review and downstream automation.

---

## Stage 7 — Risk-based Release Decision

The release decision consumes evidence; it does not replace engineering/product accountability.

Potential inputs:

- critical/high-risk scenario results;
- unresolved defect severity;
- changed-component risk;
- regression coverage;
- blocked validation;
- flaky/uncertain evidence;
- production observability readiness;
- rollback capability;
- accepted residual risk.

### Example output

```text
Release signal: CONDITIONAL GO
Confidence: Medium
Critical risks: 5/5 passed
High risks: 8/9 passed, 1 blocked
Known defects: 1 medium
Residual risk: downstream export path not validated
Required human decision: accept blocked export risk or defer release
```

---

## Human-in-the-loop controls

Human approval should remain mandatory when:

- an agent changes test scope materially;
- an agent proposes destructive actions;
- production or sensitive data is involved;
- expected behavior is ambiguous;
- evidence conflicts across sources;
- a high-risk failure is being overridden;
- a release recommendation depends on accepted residual risk.

---

## PoC success criteria

A useful PoC should prove more than AI-generated test cases.

It should demonstrate:

1. a real change enters the pipeline;
2. risks are identified;
3. approved test data is prepared;
4. agent output is evaluated;
5. deterministic tools execute validation;
6. baseline/candidate behavior can be compared where relevant;
7. telemetry and artifacts are collected;
8. evidence is normalized;
9. a risk-based release signal is produced;
10. a human can audit the path from change → evidence → decision.

That end-to-end traceability is the core of **Agentic Quality Engineering**.
