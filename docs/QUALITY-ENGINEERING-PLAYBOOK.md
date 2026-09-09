# Quality Engineering Playbook

## Objective

Build quality into the delivery system so that teams receive fast, trustworthy feedback and can explain release risk with evidence.

## Operating model

### 1. Understand the change
Capture the business behavior, technical surface, integrations, data movement, dependencies and failure modes affected by the change.

### 2. Translate change into risk
Ask:
- What can fail?
- Who or what is affected?
- How severe is the impact?
- How likely is regression?
- How easily would the failure be detected outside QA?

### 3. Choose the cheapest reliable validation layer
Prefer the lowest layer that can prove the behavior:
- static / code-level checks;
- unit/component;
- API/service;
- data/ETL;
- integration;
- UI/E2E;
- performance/resilience;
- exploratory validation.

### 4. Design for repeatability
Define deterministic preconditions, test data, environment assumptions, expected results and cleanup.

### 5. Automate where repetition creates leverage
Automate when validation is repeatable, valuable, sufficiently stable and benefits from rapid feedback. Do not automate merely because a test exists.

### 6. Preserve evidence
A result should be diagnosable without relying on memory. Capture logs, traces, screenshots, payloads, queries, data comparisons and execution metadata as appropriate.

### 7. Assess residual risk
Passing tests do not erase untested risk. Explicitly record what remains unvalidated, blocked, deferred or environment-dependent.

### 8. Make the release signal explainable
A release decision should combine:
- automated results;
- exploratory findings;
- defect severity;
- change scope;
- production exposure;
- observability readiness;
- rollback/recovery options;
- residual risk.

## Quality gates

A useful quality gate answers a decision question. Examples:

| Gate | Decision question |
|---|---|
| Build | Does the change compile and satisfy static/unit checks? |
| Integration | Do critical contracts and data paths remain valid? |
| Regression | Are priority business risks still covered? |
| Release | Is the observed evidence acceptable for the remaining risk? |

## Anti-patterns

- Measuring QA primarily by number of test cases.
- Treating all tests as equal priority.
- Running large E2E suites when API/data checks would isolate risk faster.
- Retrying flaky tests until green without root-cause analysis.
- Calling a feature “QA passed” while material scope remains blocked.
- Attaching evidence with no relationship to an expected result.
- Using AI-generated tests without review, provenance or evaluation.

## Definition of useful QA output

A strong QA output is not “tested successfully.” It states:

1. what risk was evaluated;
2. how it was evaluated;
3. what evidence was observed;
4. what remains uncertain;
5. what release decision that evidence supports.
