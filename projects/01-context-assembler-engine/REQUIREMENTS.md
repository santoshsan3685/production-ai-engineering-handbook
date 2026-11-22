# Context Assembler Engine Requirements

## Purpose

These requirements define version 1 behavior without prescribing every implementation detail. Requirement IDs are stable and should be referenced by tests, ADRs, and experiments.

## Functional Requirements

- **FR-001 — Typed input:** The engine shall accept context items containing a unique identifier, item type, content, source metadata, trust classification, and priority.
- **FR-002 — Input validation:** The engine shall reject invalid budgets, duplicate identifiers, unsupported item types, empty required fields, and malformed metadata with specific errors.
- **FR-003 — Token counter boundary:** Token measurement shall use an injected token-counter interface so provider-specific tokenizers can be added without changing assembly policy.
- **FR-004 — Budget calculation:** The engine shall calculate the usable input budget from the total context limit, fixed overhead, and reserved output tokens, and reject impossible configurations.
- **FR-005 — Deterministic selection:** Given identical inputs, configuration, and token-counter behavior, the engine shall return identical output and report data.
- **FR-006 — Priority policy:** The engine shall process context according to a documented priority and stable tie-breaking policy.
- **FR-007 — Overflow policy:** The engine shall apply an explicit per-item policy—include, truncate when allowed, or exclude—without silently exceeding the budget.
- **FR-008 — Atomic items:** Items marked non-truncatable shall be either fully included or excluded.
- **FR-009 — Trust boundaries:** Untrusted content shall retain its trust label and be distinctly delimited in the assembled representation; documentation shall state that delimiting is not a complete prompt-injection defense.
- **FR-010 — Assembly report:** The result shall include budget totals, included and excluded item identifiers, token counts, applied transformations, reasons for exclusion, and source provenance without duplicating secret content.
- **FR-011 — No execution:** Version 1 shall assemble context only and shall not invoke a model, tool, retriever, or paid API.

## Quality Requirements

- **QR-001 — Offline tests:** The default test suite shall run without network access, credentials, or paid services.
- **QR-002 — Budget safety:** The reported final input token count shall never exceed the computed usable input budget.
- **QR-003 — Testability:** Core policy shall be isolated from file, network, provider, and framework adapters.
- **QR-004 — Compatibility:** The project shall target Python 3.11 or newer and expose typed public interfaces.
- **QR-005 — Observability:** Diagnostics shall use metadata and identifiers; raw context content shall not be logged by default.
- **QR-006 — Performance evidence:** Any performance or quality claim shall link to a reproducible experiment containing environment, data, method, and raw results.
- **QR-007 — Originality and privacy:** Fixtures and documentation shall be original, synthetic, public-domain, or appropriately licensed and shall contain no personal, proprietary, or private manuscript data.

## Constraints

- Prefer the Python standard library for the first implementation.
- No provider SDK is required for version 1.
- Dependency additions require a documented rationale and must not introduce an implicit network call.
- Token-count estimates are tokenizer-specific; reports must identify the counter implementation used.

## Traceability

Each acceptance criterion in [ACCEPTANCE_CRITERIA.md](ACCEPTANCE_CRITERIA.md) references one or more requirement IDs. Implementation tests should include these IDs in test docstrings or names where practical.
