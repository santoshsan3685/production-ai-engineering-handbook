# Project 01 Requirements Traceability and Decision Register

## Document Status

- **Task:** `P01-M01-T01`
- **Status:** Approved planning artifact
- **Approved:** 2026-11-22
- **Project status:** Specified; implementation has not started
- **Purpose:** Connect every Project 01 requirement and acceptance criterion to planned architecture, tasks, verification, and evidence without implying that the evidence exists.

This document is a planning and review aid. It does not replace the authoritative requirements, acceptance criteria, task backlog, ADRs, or project status tracker.

## Authoritative Sources

- [Repository working agreement](../../AGENTS.md)
- [Repository overview](../../README.md)
- [Project status tracker](../../PROJECT_STATUS.md)
- [Project 01 overview](../../projects/01-context-assembler-engine/README.md)
- [Project 01 requirements](../../projects/01-context-assembler-engine/REQUIREMENTS.md)
- [Project 01 acceptance criteria](../../projects/01-context-assembler-engine/ACCEPTANCE_CRITERIA.md)
- [Project 01 master plan](PROJECT_01_MASTER_PLAN.md)
- [Project 01 task backlog](PROJECT_01_TASK_BACKLOG.md)
- [Project 01 learning plan](PROJECT_01_LEARNING_PLAN.md)
- [Project 01 execution guide](PROJECT_01_EXECUTION_GUIDE.md)

## Coverage Status Legend

- **Planned:** Tasks and intended evidence are identified, but no implementation or evidence exists.
- **Decision-blocked:** Planned coverage exists, but an unresolved policy or contract must be approved first.
- **Coverage concern:** The current task sequence or granularity may not be sufficient; review is required before dependent work.

No row is implemented, verified, validated, or complete at this stage.

## Coverage Summary

| Identifier group | Count | Present in plan | Current evidence |
|---|---:|---:|---|
| Functional requirements | 11 | 11 | Specification and planned tasks only |
| Quality requirements | 7 | 7 | Specification and planned tasks only |
| Acceptance criteria | 11 | 11 | Acceptance definitions only |

All identifiers have planned coverage. Several remain decision-blocked, and rendering-overhead sequencing is a material coverage concern.

## Functional Requirements Traceability

| ID and concise meaning | Related AC | Planned component | Backlog tasks | Intended test or validation | Required evidence | Dependencies | Coverage | Ambiguities, gaps, or risks |
|---|---|---|---|---|---|---|---|---|
| **FR-001 — Typed context items** | AC-001 | `models`, `validation`, public facade | P01-M02-T03, P01-M04-T01, P01-M06-T04, P01-M07-T01 | Model construction/immutability tests; valid and invalid item tests; acceptance scenarios | Reviewed public contract, focused test output, AC matrix row | D-002, D-004, D-007; package layout | Decision-blocked | Exact item types, priority type, metadata value types, and mandatory semantics are unresolved. |
| **FR-002 — Specific input validation** | AC-001, AC-003 | `errors`, `budget`, `validation` | P01-M02-T02, P01-M03-T03, P01-M03-T04, P01-M04-T01, P01-M04-T02, P01-M04-T03, P01-M07-T01 | Error hierarchy tests; invalid budget, duplicate ID, unsupported type, blank field, malformed metadata, and failure-precedence tests | Commands and outputs for unit/boundary/acceptance tests; safe error examples | D-007, D-008, D-009; model and error contracts | Decision-blocked | Accepted metadata, empty collection behavior, maximum sizes, and validation precedence are not yet defined. |
| **FR-003 — Injected token-counter boundary** | AC-002 | `tokenization` port and adapter boundary | P01-M01-T02, P01-M03-T01, P01-M03-T02, P01-M03-T04, P01-M07-T01 | Protocol substitution test with deterministic fake; invalid-return and wrapped-failure tests | ADR, interface/type-check evidence, focused unit-test output | D-001; tooling decision | Decision-blocked | Protocol shape, identity field, reference algorithm, and provider-accuracy limitations require approval. |
| **FR-004 — Usable budget calculation** | AC-003, AC-005 | `models`, `budget`, pre-flight validation, rendering-cost contract | P01-M02-T04, P01-M03-T03, P01-M04-T03, P01-M06-T01, P01-M06-T02, P01-M07-T01 | Arithmetic boundary tests; zero/negative rejection; final rendered-count agreement | AC-003 output, rendering-overhead examples, budget-invariant evidence | D-006, D-009; config contract | Coverage concern | The formula is clear, but delimiter/escaping overhead is decided after selection in the current sequence. |
| **FR-005 — Deterministic selection and result** | AC-004 | `tokenization`, `ordering`, `selection`, canonical serialization | P01-M03-T02, P01-M05-T01, P01-M05-T05, P01-M05-T06, P01-M07-T02 | Repeated selection tests; invariant tests; byte-equivalent canonical serialization | Reproducible commands, deterministic fixtures, serialized output comparison | D-001, D-002, D-003, D-010 | Decision-blocked | “Identical input” and canonical serialization rules need precise definitions; injected counter determinism is assumed, not enforceable in general. |
| **FR-006 — Priority and stable tie-breaking** | AC-004 | `models`, `ordering` | P01-M01-T03, P01-M02-T03, P01-M05-T01, P01-M05-T05, P01-M07-T02 | ADR example table; equal-priority and stable-tie tests | Accepted ADR, ordering-test output, canonical result evidence | D-002, D-003, D-004 | Decision-blocked | Priority representation, caller-order semantics, and mandatory behavior are unresolved. |
| **FR-007 — Include, truncate, or exclude** | AC-005 | decision/result models, `overflow`, `selection` | P01-M01-T04, P01-M02-T04, P01-M05-T02, P01-M05-T03, P01-M05-T04, P01-M05-T05, P01-M05-T06, P01-M07-T01 | Exact-fit, over-budget, truncation, exclusion-reason, mixed-policy, and invariant tests | Overflow ADR, decision table, focused and acceptance-test outputs | D-005, D-006; counter and ordering policies | Coverage concern | Truncation must account for final rendering overhead, but rendering policy currently follows selection implementation. |
| **FR-008 — Atomic non-truncatable items** | AC-005 | item contract, `overflow`, `selection` | P01-M01-T04, P01-M02-T03, P01-M05-T03, P01-M05-T04, P01-M05-T06, P01-M07-T01 | Full-or-excluded tests; mixed atomic/truncatable invariants | ADR, atomicity-test output, AC-005 scenario evidence | D-004, D-005 | Decision-blocked | Behavior for an oversized item considered “mandatory” is undefined because mandatory status is not an authoritative requirement. |
| **FR-009 — Trust labels and distinct delimiters** | AC-006 | item contract, `ordering`, `rendering` | P01-M01-T03, P01-M05-T01, P01-M06-T01, P01-M06-T02, P01-M07-T01 | Adversarial instruction/delimiter cases; trust-label retention; selection-policy independence | Rendering ADR, synthetic adversarial-test output, documented residual risk | D-006, D-007; selected item model | Decision-blocked | Escaping and delimiter format are unresolved; tests cannot prove prompt-injection immunity and must not claim to. |
| **FR-010 — Provenance-safe assembly report** | AC-007 | result contracts, `reporting`, safe diagnostics, serialization | P01-M01-T02, P01-M02-T04, P01-M06-T03, P01-M07-T01, P01-M07-T02 | Report schema tests; include/exclude/transformation cases; captured-log negative assertions | Schema output, log-capture output, safe sample report, serialization evidence | D-001, D-007, D-010; decision reason codes | Decision-blocked | Provenance fields, counter identity, metadata redaction, and canonical report serialization need definition. |
| **FR-011 — Assembly only; no execution** | AC-008 | pre-flight boundary, public facade, offline quality gate | P01-M04-T03, P01-M06-T04, P01-M07-T01, P01-M07-T03 | Dependency/import review; offline integration suite; network-disabled execution | Test command/output, dependency review, offline checklist | D-011; completed facade | Planned | Offline enforcement method and exact tooling remain unresolved; absence of calls must be verified, not inferred from intent. |

## Quality Requirements Traceability

| ID and concise meaning | Related AC | Planned component | Backlog tasks | Intended test or validation | Required evidence | Dependencies | Coverage | Ambiguities, gaps, or risks |
|---|---|---|---|---|---|---|---|---|
| **QR-001 — Offline default tests** | AC-008 | project tooling, fake/reference counter, test suite | P01-M02-T01, P01-M03-T02, P01-M05-T06, P01-M07-T03 | Full default suite with network unavailable and no credentials | Approved command, tool versions, actual output, environment note | D-001, D-011 | Decision-blocked | Test runner and network-isolation mechanism are not selected. |
| **QR-002 — Final input never exceeds usable budget** | AC-005 | `budget`, pre-flight validation, `overflow`, `selection`, `rendering`, facade | P01-M01-T04, P01-M03-T03, P01-M04-T03, P01-M05-T02, P01-M05-T03, P01-M05-T04, P01-M05-T05, P01-M05-T06, P01-M06-T01, P01-M06-T02, P01-M06-T04, P01-M07-T01 | Arithmetic boundaries; exact-fit; mixed outcomes; rendered-overhead agreement; broad invariants | Focused outputs, invariant command/cases, AC-005 scenario evidence | D-005, D-006, D-009 | Coverage concern | Final representation overhead is a critical dependency currently decided too late. |
| **QR-003 — Core policy isolated from adapters** | AC-002 | package boundaries, `TokenCounter` port, pure policy modules, facade | P01-M01-T02, P01-M02-T01, P01-M03-T01, P01-M03-T04, P01-M06-T04 | Fake substitution; import/dependency review; unit tests without external I/O | ADR, dependency diagram, contract/type-check output | D-001, D-011 | Decision-blocked | Exact package/module layout and enforcement mechanism remain proposed. |
| **QR-004 — Python 3.11+ typed public interfaces** | AC-009 | project configuration, models, protocol, public facade | P01-M02-T01, P01-M02-T03, P01-M02-T04, P01-M03-T01, P01-M06-T04, P01-M07-T03 | Minimum-version run; selected static type check over public API | Python/tool versions, commands, actual outputs, reviewed public API | D-011; approved package layout | Decision-blocked | Type checker, strictness, supported version range, and CI/local evidence format are undefined. |
| **QR-005 — Metadata-only diagnostics by default** | AC-007 | errors, validation, counter adapter, result contracts, `reporting` | P01-M02-T02, P01-M02-T04, P01-M03-T04, P01-M04-T01, P01-M06-T03, P01-M07-T01 | Safe exception-string tests; captured-log assertions using sentinel content/secrets | Log-capture output, schema review, safe diagnostic examples | D-007; approved logging fields | Decision-blocked | Metadata itself may contain sensitive values; allowlist/redaction policy is unresolved. |
| **QR-006 — Reproducible support for performance/quality claims** | AC-011 | experiment plan, environment/data record, raw artifacts | P01-M08-T01, P01-M08-T02 | Predeclared experiment review; exact-command execution; practical reproducibility rerun | Planned then completed experiment report, environment, synthetic data description, raw results, limitations | Completed M07 evidence; D-011 for commands | Planned | The first falsifiable question and metric are not chosen; a deterministic experiment must avoid tautological “proof.” |
| **QR-007 — Original, licensed, private-data-free fixtures/docs** | AC-010 | fixtures, repository checks, experiment and publishing review | P01-M05-T06, P01-M07-T03, P01-M08-T01, P01-M08-T02, P01-M08-T03 | Fixture/source review; secret scan; license/originality checklist; artifact inspection | Review checklist, scan output, cited sources/licenses, clean artifact review | D-011; fixtures and documents must exist | Decision-blocked | Secret-scanning tool and process for license/originality review remain undefined. |

## Acceptance Criteria Traceability

| ID and concise meaning | Related requirements | Planned component | Backlog tasks | Intended test or validation | Required evidence | Dependencies | Coverage | Ambiguities, gaps, or risks |
|---|---|---|---|---|---|---|---|---|
| **AC-001 — Typed inputs and specific validation errors** | FR-001, FR-002 | models, errors, validation, acceptance scenarios | P01-M02-T02, P01-M02-T03, P01-M04-T01, P01-M04-T02, P01-M04-T03, P01-M07-T01 | Unit and acceptance tests for every named valid/invalid class | Test names mapped to FR IDs; commands and actual outputs | D-002, D-007, D-008, D-009 | Decision-blocked | “Malformed metadata,” supported item types, and empty collection behavior need exact definitions. |
| **AC-002 — Fake counter substitution** | FR-003, QR-003 | token-counter protocol and boundary | P01-M01-T02, P01-M03-T01, P01-M03-T02, P01-M03-T04, P01-M07-T01 | Consumer contract test using deterministic fake without policy modification | ADR, interface/type-check output, focused test output | D-001, D-011 | Decision-blocked | What constitutes “without modifying policy” should be demonstrated at the public consumer boundary. |
| **AC-003 — Correct usable-budget arithmetic** | FR-004 | config model, `budget`, pre-flight validation | P01-M02-T04, P01-M03-T03, P01-M04-T03, P01-M07-T01 | Normal, exact-zero, negative, invalid type, and boundary tests | AC-003-focused command and output | D-009; config/error contracts | Planned | Python `bool` as `int`, maximum values, and zero-usable rejection require explicit tests. |
| **AC-004 — Byte-equivalent deterministic results** | FR-005, FR-006 | ordering, selection, result serialization | P01-M01-T03, P01-M05-T01, P01-M05-T05, P01-M05-T06, P01-M07-T02 | Stable ties; repeated calls; metadata ordering; canonical byte comparison | ADR, deterministic fixtures, command/output, compared serialized artifacts | D-002, D-003, D-010 | Decision-blocked | Canonical format and equivalence scope across processes/Python versions are unresolved. |
| **AC-005 — Budget-safe mixed overflow behavior** | FR-007, FR-008, QR-002 | budget, overflow, selection, rendering | P01-M01-T04, P01-M05-T02, P01-M05-T03, P01-M05-T04, P01-M05-T05, P01-M05-T06, P01-M06-T01, P01-M06-T02, P01-M07-T01 | Exact-fit, tiny-budget, atomic, truncatable, all-excluded, transformation-reason, and invariant tests | Overflow ADR, focused/invariant outputs, AC scenario matrix | D-005, D-006, D-009 | Coverage concern | Rendering overhead must be part of the same invariant; current dependency order does not guarantee this. |
| **AC-006 — Trust label/delimiter and policy independence** | FR-009 | ordering, trust-aware renderer, acceptance scenarios | P01-M01-T03, P01-M05-T01, P01-M06-T01, P01-M06-T02, P01-M07-T01 | Synthetic text imitating instructions/delimiters; stable selection; distinct escaped rendering | Rendering ADR, adversarial test command/output, residual-risk documentation | D-006, D-007 | Decision-blocked | Tests can show policy independence for designed cases, not prove universal prompt-injection safety. |
| **AC-007 — Complete report and content-free logs** | FR-010, QR-005 | result model, reporting, diagnostics | P01-M02-T02, P01-M02-T04, P01-M06-T03, P01-M07-T01 | Schema tests; include/exclude/truncate cases; captured logs with sentinel content/secrets | Schema output, log-capture output, reviewed field list | D-007, D-010 | Decision-blocked | Provenance allowlist and metadata redaction rules remain unresolved. |
| **AC-008 — Default suite offline without credentials** | FR-011, QR-001 | package/test tooling, facade, quality gate | P01-M02-T01, P01-M04-T03, P01-M06-T04, P01-M07-T01, P01-M07-T03 | Run full default suite in network-disabled/credential-free environment | Exact command, environment, tool versions, actual output | D-011; completed suite | Decision-blocked | Offline enforcement and test runner have not been selected. |
| **AC-009 — Static typing and minimum Python version** | QR-004 | configuration, typed API, quality gate | P01-M02-T01, P01-M02-T03, P01-M02-T04, P01-M03-T01, P01-M06-T04, P01-M07-T03 | Selected static type check plus Python 3.11 execution | Commands, versions, actual output, reviewed exceptions/suppressions | D-011; complete public API | Decision-blocked | Type checker, settings, and Python-version matrix are unresolved. |
| **AC-010 — No secrets/private/unlicensed material** | QR-007 | fixtures, repository review, secret/license checks | P01-M05-T06, P01-M07-T03, P01-M08-T03 | Secret scan; fixture/source/license and private-material review | Scan output, checklist, source/license record, reviewed diff | D-011; fixtures/docs exist | Decision-blocked | A scan cannot prove originality or licensing; human review criteria must be explicit. |
| **AC-011 — Committed reproducible experiment** | QR-006 | experiment design, execution, raw artifacts | P01-M08-T01, P01-M08-T02 | Predeclared hypothesis review; exact-command run; practical rerun | Committed report and artifacts with environment, data, command, raw results, and limitations | AC-001–AC-010 evidence reviewed; experiment question selected | Planned | No experiment has been designed or run; failure/inconclusive results must remain accurately labeled. |

## Open-Decision Register

| Decision | What must be decided | Why it matters | Requirements affected | Alternatives | Important trade-offs | Recommended ADR or task | Blocking? | Resolve no later than |
|---|---|---|---|---|---|---|---|---|
| **D-001 — Token-counter contract** | Protocol shape, identity, invalid-return behavior, and deterministic reference algorithm | Counting is an external variability boundary and appears in reports | FR-003, FR-005, FR-010; QR-001, QR-003; AC-002, AC-004 | `Protocol`, ABC, callable; character/word-like counter; no shipped default | Structural flexibility versus explicit runtime contract; simplicity versus provider accuracy | ADR 0001 via P01-M01-T02 | Yes | Before P01-M03-T01 and P01-M02-T04 counter fields |
| **D-002 — Priority representation** | Categorical enum, bounded integer, or policy value object | Typed items and selection ordering require stable semantics | FR-001, FR-005, FR-006; AC-001, AC-004 | Enum; integer; separate policy object | Clarity and validation versus extensibility | ADR 0002 via P01-M01-T03 | Yes | Before P01-M02-T03 |
| **D-003 — Stable tie-break** | Caller order, item ID, or explicit sequence | Byte-equivalent deterministic output requires total ordering | FR-005, FR-006; AC-004 | Stable input order; lexical ID; explicit sequence | Caller intent versus canonical behavior and extra input complexity | ADR 0002 via P01-M01-T03 | Yes | Before P01-M05-T01; ideally before item contract approval |
| **D-004 — Mandatory semantics** | Whether “mandatory” exists in version 1 and how impossible mandatory items fail | The plan mentions mandatory/system content, but requirements define only priority and atomicity | FR-001, FR-006, FR-008; AC-001, AC-005 | Out of scope; highest priority only; explicit flag; reserved pool | Minimal scope versus stronger preservation guarantee and impossible-budget behavior | ADR 0002 via P01-M01-T03; confirm scope against requirements | Yes if retained | Before P01-M02-T03 and P01-M01-T04 approval |
| **D-005 — Truncation policy** | Truncatable types, unit, minimum useful size, marker, and failure behavior | Determines semantic loss and budget safety | FR-007, FR-008; QR-002; AC-005 | Exclusion only; prefix truncation; item-type strategies | Safety and simplicity versus context utilization; linear versus monotonic-search assumptions | ADR 0003 via P01-M01-T04 | Yes | Before P01-M05-T02 through P01-M05-T04 |
| **D-006 — Rendering and overhead** | Canonical format, delimiters, escaping, trust labels, and cost accounting | Final rendered size and trust boundary depend on it | FR-004, FR-007, FR-009; QR-002; AC-005, AC-006 | Tagged text; structured sections; pre-render each item; reserve measured wrapper overhead | Readability versus escaping complexity; early coupling versus provable budget safety | ADR 0004 via P01-M06-T01, but dependency/order should be reviewed | Yes | Before P01-M05-T02 and especially P01-M05-T04/T05, not after them |
| **D-007 — Metadata contract** | Allowed keys/value types, mutability, serialization, provenance allowlist, and redaction | Affects validation, deterministic output, privacy, and reporting | FR-001, FR-002, FR-009, FR-010; QR-005; AC-001, AC-006, AC-007 | Closed dataclass; typed mapping; restricted JSON-like mapping | Strong guarantees versus extensibility; provenance utility versus leakage | Add explicit decision to P01-M02-T03/P01-M02-T04 or create ADR if durable | Yes | Before P01-M02-T03 approval |
| **D-008 — Empty input behavior** | Whether zero items returns an empty result/report or raises an error | Validation and public API behavior must agree | FR-002, FR-005, FR-010; AC-001, AC-004, AC-007 | Valid empty result; validation error | Composability versus early misuse detection | Decide in P01-M04-T02 with contract noted in P01-M02-T04 | Yes | Before P01-M04-T02 |
| **D-009 — Resource limits** | Maximum content, metadata, item count, and numeric budget bounds | Prevents unbounded CPU/memory use and defines validation edges | FR-002, FR-004; QR-002; AC-001, AC-003, AC-005 | No library maximum; configurable limits; fixed conservative defaults | General-purpose library flexibility versus denial-of-service resistance and testability | Add policy decision before P01-M04-T01; ADR if limits become public contract | Yes | Before P01-M04-T01 and P01-M03-T03 final approval |
| **D-010 — Canonical serialization** | Format, field ordering, metadata ordering, encoding, and stability scope | AC-004 requires byte-for-byte equivalent serialized results | FR-005, FR-010; AC-004, AC-007 | Canonical JSON; explicit text/binary serializer; stable dataclass projection | Standard-library simplicity versus schema control; current-version versus cross-version guarantee | P01-M07-T02, with constraints fed back to P01-M02-T04 | Yes | Define constraints before P01-M02-T04; implement/verify by P01-M07-T02 |
| **D-011 — Development and quality tools** | Test runner, type checker, formatter/linter, link checker, secret scanner, and offline enforcement | Evidence commands must be reproducible and dependencies justified | QR-001, QR-004, QR-007; AC-008, AC-009, AC-010 | Standard library only; focused external tools; local plus CI later | Dependency cost versus stronger automation and developer experience | P01-M02-T01 | Yes for implementation | Before creating test/config scaffolding |
| **D-012 — Learning records** | Final location and minimal format without progress duplication | Learning evidence must remain discoverable without becoming another tracker | Repository learning/reflection policy; supports interview integration | One file per task under `docs/learning/project-01/`; one cumulative project journal; notes embedded in backlog | Granularity and reviewability versus maintenance overhead | Adopt path convention during P01-M01-T01 approval; create no files yet | No | Before first implementation task closes |

## Plan Quality Review

### Missing Requirement Coverage

No identifier is absent from the backlog. Presence is not completion: all implementation and evidence remain pending. The traceability rows above expose the decisions that must be resolved before planned coverage becomes executable.

### Duplicate or Contradictory Coverage

- Unit tasks and P01-M07-T01 both reference AC-001 through AC-008. This is intentional layering: focused tests establish component behavior, while the acceptance matrix checks end-to-end coverage.
- P01-M05-T01 and P01-M07-T02 both address determinism. This is also intentional: stable ordering is one cause; canonical byte serialization is the acceptance-level observation.
- No contradiction with the root `AGENTS.md` was found.
- `PROJECT_STATUS.md` owns project status; backlog task states own task workflow. This traceability document must not add a third progress status.

### Dependency and Sequencing Concern

P01-M06-T01 currently depends on P01-M05-T05, but it decides delimiter, escaping, and rendering overhead. P01-M05-T02 through P01-M05-T05 cannot conclusively establish final budget safety until that overhead contract exists. Before M05 implementation, revise the dependency plan or approve an earlier rendering-cost contract. This task records the concern but does not modify the backlog.

### Task Granularity Concerns

- P01-M07-T03 combines offline execution, static typing, privacy review, secret scanning, and repository-quality gates. Review whether it should be split before execution so each check and failure can be learned independently.
- P01-M08-T03 combines learning records, interview material, documentation reconciliation, and status updates. Review whether it should become separate evidence, educational-content, and status-handoff tasks.
- P01-M08-T01 permits an optional fixture generator inside an experiment-design task. If code is required, create a separate approved implementation task rather than hiding code inside documentation planning.

### Evidence Sufficiency Concerns

- AC-004 requires canonical byte serialization, not only object equality or repeatable sorting.
- AC-006 can demonstrate that tested text does not affect policy; it cannot prove immunity to all prompt injection.
- AC-010 needs both automated scanning and human source/license/originality review. A secret scanner alone is insufficient.
- AC-011 requires committed evidence. A local report without its raw artifacts and reproducible command cannot satisfy it.
- Planned commands, test names, and expected outputs are not evidence that checks passed.

### Security, Privacy, and Originality Coverage

The plan covers offline operation, paid-API exclusion, safe error/log behavior, synthetic or licensed fixtures, secret scanning, private-material exclusion, prompt-injection limitations, and originality review. Metadata redaction and explicit resource limits need decisions before validation and reporting implementation.

## Critical Path Implications

The current critical path remains:

```text
traceability → policy ADRs → package/data contracts → token and budget
→ validation → selection/overflow → rendering/reporting → system evidence
→ experiment → learning/interview/status handoff
```

The rendering/overhead decision must move ahead of budget-sensitive selection implementation or be represented by an earlier approved cost contract. D-001 through D-011 identify the latest safe resolution point for other blocking decisions.

## Learning-Record Convention

Recommended future path:

```text
docs/learning/project-01/P01-MXX-TXX.md
```

Each record should contain the task ID, problem, concepts, alternatives, errors, commands actually run, observed results, security/privacy review, interview lesson, and remaining questions. It should not contain a progress status field. Project status remains in `PROJECT_STATUS.md`; task status remains in the backlog.

No learning directory or record is created by this task.

## Approval and Maintenance Rules

- This document was reviewed and approved for planning use under `P01-M01-T01` on 2026-11-22.
- Approving this document does not approve any open decision or ADR.
- Update a row when its task mapping, accepted decision, test strategy, or evidence location changes.
- Do not change a coverage row to verified or validated without commands and repository evidence.
- `P01-M01-T02` remains unstarted and requires a separate, explicitly approved task session.
