# Project 01 Learning Plan

## Purpose

This plan sequences learning immediately before the task that uses it. It is not a requirement to master every topic in advance. For each task, explain the concept in plain language, work one small example, predict the test outcome, and record questions before implementation.

No listed artifact or interview answer exists merely because it is planned here.

## Learning Record Format

After each approved implementation task, record:

- task ID and requirement addressed;
- the engineering problem in your own words;
- new Python, architecture, testing, and security concepts;
- alternatives considered and why one was chosen;
- errors encountered, diagnosis, and fix;
- commands actually run and observed outcomes;
- one thing you could now explain in an interview;
- remaining uncertainty and next approved task.

The final location for task notes is decided in `P01-M01-T01`; do not create a competing status tracker.

## Per-Task Study Map

| Task | Study immediately before | Small learning exercise | Interview capability developed |
|---|---|---|---|
| P01-M01-T01 | Functional/non-functional requirements; verification versus validation; traceability | Map one FR to a unit test, integration test, and acceptance artifact | Explain how evidence prevents false completion claims |
| P01-M01-T02 | Dependency inversion; `Protocol`, ABC, and callable trade-offs; tokenizer variability | Sketch three counter interfaces and identify coupling | Defend an injectable provider-neutral boundary |
| P01-M01-T03 | Stable sorting; total order; priority queues; starvation | Manually order tied items under two policies | Discuss deterministic scheduling and fairness |
| P01-M01-T04 | Capacity invariants; atomicity; lossy truncation | Build a four-row include/truncate/exclude decision table | Explain safe degradation under a hard budget |
| P01-M02-T01 | `src` layout; `pyproject.toml`; runtime/dev dependencies; offline tests | Trace how an import resolves from root versus installed package | Explain Python packaging and dependency governance |
| P01-M02-T02 | Exception trees; chaining with `raise ... from`; safe messages | Design catch behavior for one validation and one counter error | Explain error contracts without information leakage |
| P01-M02-T03 | Dataclasses, enums, frozen values, type aliases | Model one item, then try an illegal mutation | Compare immutable domain objects with dictionaries |
| P01-M02-T04 | Result/DTO design; reason codes; safe `repr`; provenance | Sketch a report that explains exclusion without content | Discuss explainability and data minimization |
| P01-M03-T01 | Structural typing and dependency injection | Write a tiny fake that satisfies a protocol conceptually | Compare Protocol, ABC, and duck typing |
| P01-M03-T02 | Deterministic text algorithms; Unicode; approximation | Count the same strings under character and word-like rules | Explain why model token counts are tokenizer-specific |
| P01-M03-T03 | Pure functions; integer validation; boundary analysis | Calculate normal, zero, and negative usable budgets by hand | Identify off-by-one and invalid-budget risks |
| P01-M03-T04 | Defensive adapters; bool-as-int behavior; exception translation | Classify five invalid counter behaviors | Explain validation at an untrusted dependency boundary |
| P01-M04-T01 | Input validation; rejection versus normalization; Unicode whitespace | Define accepted/rejected examples for each field | Explain fail-fast validation and safe errors |
| P01-M04-T02 | Iterable materialization; sets; complexity; order preservation | Detect duplicate IDs while retaining first-seen order | Discuss collection invariants and time complexity |
| P01-M04-T03 | Pre-flight checks; failure atomicity; error precedence | Order validation steps and justify which error appears first | Explain transactional thinking without a database |
| P01-M05-T01 | Python stable sort and key functions | Predict tied output before running a test | Explain reproducibility in selection systems |
| P01-M05-T02 | Greedy allocation and remaining-capacity state | Walk through below-fit, exact-fit, and over-fit cases | Derive and defend the budget invariant |
| P01-M05-T03 | Atomicity and explicit fallback decisions | Explain why partial system instructions may be unsafe | Discuss full-or-nothing context policies |
| P01-M05-T04 | Counter-aware truncation; monotonic search; Unicode slicing | Compare linear and binary search assumptions | Discuss algorithm choice when the counter is injectable |
| P01-M05-T05 | State transitions; functional core; complexity | Trace a mixed five-item selection by hand | Explain greedy policy limitations and alternatives |
| P01-M05-T06 | Invariants; table-driven/property-oriented tests; reproducible seeds | Turn “never exceed budget” into a quantified property | Explain why examples and invariants complement each other |
| P01-M06-T01 | Prompt injection; escaping; canonical rendering; defense in depth | Create content that imitates a delimiter and design an escape | Explain why delimiters reduce ambiguity but do not ensure safety |
| P01-M06-T02 | Pure renderers; canonical text; overhead accounting | Calculate content plus delimiter cost manually | Discuss rendering correctness under hard limits |
| P01-M06-T03 | Structured logs; privacy; observability; aggregate token telemetry | Separate safe fields from content/secrets in a sample event | Explain what token usage can be logged safely |
| P01-M06-T04 | Facade pattern; dependency injection; orchestration | Draw call order and mark pure versus boundary components | Explain functional core/imperative shell architecture |
| P01-M07-T01 | Acceptance tests; traceability; test pyramid | Map one AC across unit and integration evidence | Explain when an acceptance test adds value |
| P01-M07-T02 | Canonical serialization; byte equivalence; metadata order | Serialize logically equal maps in two orders conceptually | Discuss deterministic output beyond object equality |
| P01-M07-T03 | Static typing; offline isolation; secret/license scanning | Identify what each quality gate can and cannot prove | Design practical CI quality gates |
| P01-M08-T01 | Hypotheses; variables; baselines; threats to validity | Rewrite a vague performance claim as a falsifiable question | Design a reproducible engineering experiment |
| P01-M08-T02 | Raw observations versus interpretation; uncertainty; negative results | Separate a sample result table from its conclusions | Explain benchmark integrity and limitations |
| P01-M08-T03 | Technical reflection; interview rubrics; source/originality review | Turn one real defect into a debugging question and rubric | Communicate authentic project evidence without overstating experience |

## Module Learning Outcomes

### M01 — Decisions and Traceability

You can translate specifications into verifiable work, distinguish decisions from assumptions, and defend an ADR using alternatives and consequences.

### M02 — Package and Domain Contracts

You can explain Python package boundaries, immutable typed models, specific errors, and why domain contracts should not contain orchestration logic.

### M03 — Token and Budget Boundaries

You can explain tokenizer variability, dependency inversion, defensive adapters, and hard integer budget invariants.

### M04 — Validation

You can design fail-fast validation that preserves ordering, rejects ambiguity, and avoids leaking raw content.

### M05 — Selection and Overflow

You can trace and critique a deterministic greedy policy, reason about atomicity and truncation, and express correctness as invariants.

### M06 — Rendering, Reporting, and Orchestration

You can explain trust boundaries, prompt-injection limitations, safe observability, and how a facade composes testable components.

### M07 — System Verification

You can connect unit, integration, acceptance, typing, privacy, and offline evidence without claiming that any single check proves production readiness.

### M08 — Evidence and Learning Outputs

You can predeclare and execute a reproducible experiment, report negative or inconclusive outcomes honestly, and derive original interview material from real work.

## Interview Preparation by Module

| Module | Conceptual | Coding/debugging | Production/architecture |
|---|---|---|---|
| M01 | Requirements, ADRs, deterministic policy | Diagnose ambiguous acceptance criteria | Choose priority/overflow policy under conflicting constraints |
| M02 | Type hints, immutability, errors | Refactor dictionary inputs into typed contracts | Govern dependencies and public API evolution |
| M03 | Tokenizers, protocols, budget math | Fix off-by-one and invalid-counter failures | Isolate model-provider behavior |
| M04 | Validation and failure precedence | Debug duplicates, Unicode blanks, generators | Bound untrusted input and resource use |
| M05 | Sorting, greedy selection, atomicity | Implement/test one decision function | Trade quality, fairness, and determinism under capacity |
| M06 | Prompt injection, rendering, reporting | Find content leakage in logs/reports | Design safe context assembly boundaries |
| M07 | Test strategy and canonical output | Diagnose flaky/non-deterministic results | Define evidence for implementation readiness |
| M08 | Experimental validity and originality | Reproduce an unexpected result | Communicate limitations and publication readiness |

Each question must be independently authored after its supporting evidence exists. Hypothetical production scenarios must be labeled as such and must not be presented as personal production experience.

## Learning Checkpoints

At each module boundary, pause and answer without notes:

1. What invariant did this module establish?
2. Which requirement and acceptance criterion does it support?
3. What alternative was rejected, and why?
4. What could still fail in production?
5. Which test demonstrates behavior, and which claim remains unverified?

Proceed only after reviewing the diff, evidence, and your explanation with Codex.
