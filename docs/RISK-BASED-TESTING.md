# Risk-based Testing

## Purpose

Risk-based testing allocates validation effort according to the consequence and probability of failure, rather than distributing effort evenly across features.

## Lightweight risk model

Score each factor from 1 to 5:

- **Impact (I)** — business/user consequence if the behavior fails.
- **Likelihood (L)** — probability of failure based on complexity, history and change.
- **Exposure (E)** — frequency / breadth of use in production.
- **Detectability (D)** — difficulty of detecting the failure before users are affected. Higher = harder to detect.

A simple prioritization score:

```text
Risk Score = Impact × Likelihood × Exposure × Detectability
```

The score is a prioritization aid, not a mathematical truth.

## Example bands

| Score | Suggested interpretation |
|---:|---|
| 1–49 | Low |
| 50–149 | Medium |
| 150–299 | High |
| 300–625 | Critical |

Teams should calibrate thresholds with real defect and production data.

## Inputs that increase risk

- large or cross-cutting change;
- data transformations or migrations;
- money, identity, permissions or compliance;
- historically unstable component;
- multiple downstream integrations;
- low observability;
- difficult rollback;
- high-volume user path;
- recent architecture or dependency change;
- ambiguous acceptance criteria.

## Mapping risk to validation

### Critical
- primary + alternate + negative paths;
- integration/data validation;
- regression around change surface;
- automation when repeatable;
- explicit evidence and residual-risk review;
- non-functional testing when relevant.

### High
- primary and meaningful alternate paths;
- targeted regression;
- automation for repeatable stable checks;
- evidence sufficient for release review.

### Medium
- targeted functional coverage;
- representative boundary checks;
- regression based on change impact.

### Low
- focused smoke / exploratory validation as appropriate;
- avoid expensive automation with weak return.

## ETL / data-quality example

For an ETL change, risk should be evaluated across:

```text
Source fidelity
      ↓
Transformation rule correctness
      ↓
Null / decimal / date / enum handling
      ↓
Destination mapping
      ↓
Row/count reconciliation
      ↓
Differential comparison
      ↓
Downstream consumer impact
```

Useful validations include row counts, field-level comparisons, reconciliation totals, null behavior, precision/scale, duplicate detection and before/after differential checks.

## Release use

A risk score does not decide whether to release. It informs:

- how much evidence is needed;
- which layers should be tested;
- what must be automated;
- which residual risks require explicit acceptance.
