# QA Validation Framework

A reusable validation structure for defects, features, regressions and integration/data changes.

## 1. Context

**Change / ticket:**  
**Business intent:**  
**Technical surface:**  
**Dependencies:**  
**Known risk:**

## 2. Environment

- Environment:
- Build / version / commit:
- Configuration / feature flags:
- Browser / client / service version where relevant:
- Data source / destination where relevant:

If an environment detail is unknown, mark it explicitly rather than assuming it.

## 3. Scope

### In scope
Describe the behavior and risks being validated.

### Out of scope
Record adjacent behavior intentionally not covered.

## 4. Preconditions

Define access, permissions, configuration, test data, upstream state and any setup required for repeatability.

## 5. Risk-based scenarios

| ID | Scenario | Risk covered | Priority | Layer |
|---|---|---|---|---|
| VAL-01 | Primary expected behavior | Functional regression | Critical | Best-fit layer |
| VAL-02 | Boundary / alternate state | Data or state defect | High | Best-fit layer |
| VAL-03 | Negative / invalid condition | Error handling | High | Best-fit layer |
| VAL-04 | Related regression path | Change impact | Medium | Best-fit layer |

## 6. Expected results

Expected results should be observable and testable. Avoid statements such as “works correctly.”

Prefer:

> The exported value retains two decimal places and matches the source value `0.00`.

Over:

> Export works.

## 7. Evidence

Evidence may include:

- screenshot or video;
- request/response payload;
- database query/result;
- source-to-target comparison;
- logs / trace;
- report/PDF output;
- automated run/report;
- configuration evidence.

Each artifact should be tied to a validation step and expected result.

## 8. Result classification

Use one of:

- **PASS** — observed result matches expected result.
- **FAIL** — observed result contradicts expected result.
- **BLOCKED** — validation cannot be completed because of a documented dependency/environment issue.
- **NOT RUN** — scenario intentionally not executed; reason required.

## 9. Defect triage

Before classifying an automation failure as a product defect, separate possible causes:

```text
Product defect
Test defect
Test-data defect
Environment/configuration issue
Dependency/service issue
Expected-behavior ambiguity
```

## 10. Residual risk

Record anything that remains uncertain:

- untested platforms;
- unavailable integrations;
- production-only behavior;
- incomplete data coverage;
- deferred non-functional testing;
- known defects accepted for release.

## 11. QA decision

Conclude with a decision supported by evidence:

```text
QA decision: PASS | FAIL | PASS WITH KNOWN RISK | BLOCKED
Release recommendation:
Residual risk:
Evidence references:
```

The decision is not a substitute for product/business ownership. It is a structured Quality Engineering signal for release governance.
