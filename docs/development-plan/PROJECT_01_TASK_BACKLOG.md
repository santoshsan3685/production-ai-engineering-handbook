# Project 01 Atomic Task Backlog

## Use of This Backlog

- Status values: `Planned`, `In progress`, `Blocked`, `Review`, `Approved`.
- Every task is one approval-gated session. Never advance automatically.
- Time values are learning estimates, not delivery commitments.
- File and symbol names are proposed until their defining task is approved.
- “Passes” below means evidence required before approval; it is not a claim about current results.

## M01 — Decisions and Traceability

### P01-M01-T01 — Build the requirements traceability and decision register

1. **Status:** Approved
2. **Objective:** Map `FR`, `QR`, and `AC` identifiers to planned components, tasks, and evidence.
3. **Why:** Prevent silent scope loss and expose unresolved decisions before code.
4. **Learn first:** Requirement traceability, verification versus validation.
5. **Dependencies:** Existing Project 01 specifications only.
6. **Scope:** Review every requirement; create one matrix and open-decision register.
7. **Files:** Modify this plan set or add a Project 01 traceability document only if approved.
8. **Symbols:** None.
9. **Input/output:** Requirement IDs in; complete mapping and gaps out.
10. **Edge cases:** One requirement mapping to multiple tests; acceptance evidence outside code.
11. **Security:** Preserve privacy and secret-scanning obligations in the mapping.
12. **Tests:** Documentation link and completeness review.
13. **Acceptance:** Every `FR-001`–`FR-011`, `QR-001`–`QR-007`, and `AC-001`–`AC-011` appears.
14. **Done:** User reviews gaps and approves the register.
15. **Evidence:** Approved [requirements traceability and decision register](PROJECT_01_TRACEABILITY.md).
16. **Complexity:** Beginner.
17. **Learning time:** 45–75 minutes.
18. **Interview preparation:** Traceability, definitions of done, evidence-based delivery.
19. **Out of scope:** Resolving decisions or writing code.
20. **Requirement links:** All requirements and acceptance criteria.

### P01-M01-T02 — Decide the token-counter boundary

1. **Status:** Planned
2. **Objective:** Record the counter protocol, identity, error contract, and reference-counter decision.
3. **Why:** `FR-003` requires provider isolation and reports must identify the counter.
4. **Learn first:** Python protocols, dependency inversion, tokenizer variability.
5. **Dependencies:** P01-M01-T01.
6. **Scope:** Compare protocol/callable/abstract-base-class options and reference-counter alternatives.
7. **Files:** `docs/adr/0001-token-counter-boundary.md`.
8. **Symbols:** Proposed `TokenCounter.count(text) -> int` and counter identity contract.
9. **Input/output:** Text in; non-negative token count out; failures explicit.
10. **Edge cases:** Empty text, Unicode, invalid return type, negative count, counter failure.
11. **Security:** No content logging at the boundary.
12. **Tests:** Specify contract tests; do not implement them yet.
13. **Acceptance:** ADR states decision, alternatives, consequences, and validation.
14. **Done:** ADR approved; unresolved provider accuracy is documented.
15. **Evidence:** Accepted/proposed ADR with review notes.
16. **Complexity:** Intermediate.
17. **Learning time:** 60–90 minutes.
18. **Interview preparation:** Dependency inversion, Protocol versus ABC, tokenizer trade-offs.
19. **Out of scope:** Provider SDK or tokenizer integration.
20. **Requirement links:** FR-003, FR-010, QR-003, AC-002.

### P01-M01-T03 — Decide priority and stable ordering

1. **Status:** Planned
2. **Objective:** Define priority representation, mandatory semantics, and deterministic tie-breaking.
3. **Why:** `FR-005` and `FR-006` cannot be tested without an explicit ordering policy.
4. **Learn first:** Stable sorting, total ordering, starvation, policy design.
5. **Dependencies:** P01-M01-T01.
6. **Scope:** Compare categorical/numeric priority and caller-order/ID/sequence tie-breaks.
7. **Files:** `docs/adr/0002-priority-and-ordering-policy.md`.
8. **Symbols:** Proposed `Priority`, optional mandatory representation, `ordering_key`.
9. **Input/output:** Valid items in; total deterministic order out.
10. **Edge cases:** Equal priorities, duplicate sequence values, mandatory item too large.
11. **Security:** Untrusted content cannot affect ordering except through validated metadata.
12. **Tests:** Specify stable-order and adversarial-content cases.
13. **Acceptance:** ADR defines all ties and impossible mandatory-item behavior.
14. **Done:** Policy is unambiguous and user-approved.
15. **Evidence:** ADR and example ordering table.
16. **Complexity:** Advanced.
17. **Learning time:** 75–120 minutes.
18. **Interview preparation:** Scheduling policies, deterministic systems, fairness trade-offs.
19. **Out of scope:** Implementing the sorter.
20. **Requirement links:** FR-005, FR-006, FR-009, AC-004, AC-006.

### P01-M01-T04 — Decide overflow and truncation policy

1. **Status:** Planned
2. **Objective:** Define include, truncate, exclude, and atomic-item behavior.
3. **Why:** Budget safety depends on explicit transformations and reason codes.
4. **Learn first:** Invariants, lossy transformations, prefix truncation, atomicity.
5. **Dependencies:** P01-M01-T02, P01-M01-T03.
6. **Scope:** Decide truncatable types, truncation unit, minimum useful size, and exclusion reasons.
7. **Files:** `docs/adr/0003-overflow-and-truncation-policy.md`.
8. **Symbols:** Proposed `OverflowAction`, `DecisionReason`, truncation policy contract.
9. **Input/output:** Ordered item plus remaining budget in; explicit decision out.
10. **Edge cases:** Zero remaining budget, oversized atomic item, delimiter overhead, no valid truncation.
11. **Security:** Truncation must not create malformed trust delimiters.
12. **Tests:** Specify atomicity, exact-fit, off-by-one, and truncated-count cases.
13. **Acceptance:** ADR proves no policy path may intentionally exceed budget.
14. **Done:** Policy and residual semantic-loss risk approved.
15. **Evidence:** ADR with decision table.
16. **Complexity:** Advanced.
17. **Learning time:** 90–120 minutes.
18. **Interview preparation:** Capacity allocation, invariants, safe degradation.
19. **Out of scope:** Compression/summarization or implementation.
20. **Requirement links:** FR-007, FR-008, QR-002, AC-005.

## M02 — Package and Domain Contracts

### P01-M02-T01 — Select minimal project tooling and package layout

1. **Status:** Planned
2. **Objective:** Define the smallest executable Python package/test layout and justified tools.
3. **Why:** No package configuration or test runner currently exists.
4. **Learn first:** `src` layout, `pyproject.toml`, build versus development dependencies.
5. **Dependencies:** M01 approved.
6. **Scope:** Compare standard-library-only tests with focused external tools; document choices before install.
7. **Files:** Proposed project `pyproject.toml`, `src/context_assembler_engine/`, `tests/`; create only after approval.
8. **Symbols:** Package public namespace only.
9. **Input/output:** Constraints in; reviewed tool/layout decision out.
10. **Edge cases:** Running from repository root, editable install assumptions, Python 3.11.
11. **Security:** No implicit network/plugin behavior; pin approved direct dependencies.
12. **Tests:** Define one collection/import smoke test.
13. **Acceptance:** Every proposed dependency has rationale; commands are reproducible.
14. **Done:** User authorizes exact files and any installation separately.
15. **Evidence:** Reviewed configuration diff and dependency rationale.
16. **Complexity:** Intermediate.
17. **Learning time:** 60–90 minutes.
18. **Interview preparation:** Python packaging, dependency governance, test isolation.
19. **Out of scope:** Business logic or dependency installation without authorization.
20. **Requirement links:** QR-001, QR-003, QR-004, AC-008, AC-009.

### P01-M02-T02 — Define the domain error hierarchy

1. **Status:** Planned
2. **Objective:** Add specific exceptions for validation, budget, counter, and assembly failures.
3. **Why:** `FR-002` requires specific errors and failures must retain context safely.
4. **Learn first:** Exception inheritance, chaining, public error contracts.
5. **Dependencies:** P01-M02-T01.
6. **Scope:** Implement error types only, with safe identifiers/fields.
7. **Files:** `src/context_assembler_engine/errors.py`, focused error tests.
8. **Symbols:** `ContextAssemblerError`, `ValidationError`, `BudgetError`, `TokenCounterError` and approved subtypes.
9. **Input/output:** Invalid operation in; catchable domain error with safe metadata out.
10. **Edge cases:** Chained counter exception; error formatting without raw content.
11. **Security:** Exception messages exclude secrets and item content.
12. **Tests:** Inheritance, safe string form, exception chaining.
13. **Acceptance:** Errors are specific, stable, and contain no raw context.
14. **Done:** Focused tests pass and diff is explained line by line.
15. **Evidence:** Test output and reviewed diff.
16. **Complexity:** Beginner.
17. **Learning time:** 45–75 minutes.
18. **Interview preparation:** Error taxonomy, exception chaining, API contracts.
19. **Out of scope:** Validation logic.
20. **Requirement links:** FR-002, QR-005, AC-001, AC-007.

### P01-M02-T03 — Define context-item value types

1. **Status:** Planned
2. **Objective:** Implement immutable typed input vocabulary.
3. **Why:** `FR-001` requires explicit item identity, type, content, provenance, trust, priority, and truncation behavior.
4. **Learn first:** Dataclasses, enums, immutability, type hints, value objects.
5. **Dependencies:** P01-M01-T03, P01-M01-T04, P01-M02-T02.
6. **Scope:** Define fields and enum members only; validation remains M04.
7. **Files:** `models.py`, `tests/unit/test_models.py`.
8. **Symbols:** `ContextItem`, `ContextItemType`, `TrustLevel`, `Priority` or approved equivalents.
9. **Input/output:** Constructor values in; immutable item value out.
10. **Edge cases:** Unicode content, metadata mutability, enum serialization.
11. **Security:** Metadata schema excludes arbitrary secret-bearing objects where feasible.
12. **Tests:** Construction, equality, immutability, type/enum behavior.
13. **Acceptance:** Every `FR-001` field is represented with documented semantics.
14. **Done:** Focused tests pass and public fields are explained.
15. **Evidence:** Tests and reviewed API diff.
16. **Complexity:** Intermediate.
17. **Learning time:** 75–105 minutes.
18. **Interview preparation:** Domain modeling, immutable data, enum trade-offs.
19. **Out of scope:** Input rejection, selection, rendering.
20. **Requirement links:** FR-001, QR-004, AC-001.

### P01-M02-T04 — Define configuration, decision, report, and result contracts

1. **Status:** Planned
2. **Objective:** Model assembly inputs and observable outputs without implementing behavior.
3. **Why:** Budget/report requirements need stable typed contracts before algorithms.
4. **Learn first:** API design, result objects, reason codes, provenance minimization.
5. **Dependencies:** P01-M02-T03.
6. **Scope:** Add immutable config/result types and documented invariants.
7. **Files:** `models.py`, focused model tests.
8. **Symbols:** `AssemblyConfig`, `ItemDecision`, `AssemblyReport`, `AssemblyResult`, outcome/reason enums.
9. **Input/output:** Typed field values in; immutable serializable values out.
10. **Edge cases:** Empty decision sets, zero counts, optional provenance, stable field order.
11. **Security:** Reports reference IDs/metadata but do not duplicate raw item content.
12. **Tests:** Construction, equality, immutability, safe representation.
13. **Acceptance:** Contracts cover `FR-004`, `FR-007`, and `FR-010` observables.
14. **Done:** Focused tests pass; no algorithm is embedded in data classes.
15. **Evidence:** Test output and contract review.
16. **Complexity:** Intermediate.
17. **Learning time:** 75–105 minutes.
18. **Interview preparation:** DTOs, domain results, explainability contracts.
19. **Out of scope:** Validation and serialization format guarantee.
20. **Requirement links:** FR-004, FR-007, FR-010, AC-003, AC-005, AC-007.

## M03 — Token and Budget Boundaries

### P01-M03-T01 — Implement the token-counter protocol

1. **Status:** Planned
2. **Objective:** Encode the approved counter boundary with no provider dependency.
3. **Why:** Assembly policy must depend on an abstraction, not a tokenizer SDK.
4. **Learn first:** Structural typing, runtime versus static protocol checks.
5. **Dependencies:** P01-M01-T02, P01-M02-T01.
6. **Scope:** Protocol and counter identity only.
7. **Files:** `tokenization.py`, `tests/unit/test_tokenization_contract.py`.
8. **Symbols:** Approved `TokenCounter` protocol.
9. **Input/output:** String in; non-negative integer contract out.
10. **Edge cases:** Empty input and nonconforming fake implementations.
11. **Security:** Protocol exposes no logging side effect.
12. **Tests:** Conforming deterministic fake accepted by consumers/type checker.
13. **Acceptance:** Fake counter substitutes without changing dependent policy.
14. **Done:** Contract test and selected type check pass.
15. **Evidence:** AC-002-focused output and diff.
16. **Complexity:** Intermediate.
17. **Learning time:** 60–90 minutes.
18. **Interview preparation:** Ports and adapters, structural typing.
19. **Out of scope:** Concrete provider tokenizers.
20. **Requirement links:** FR-003, QR-003, QR-004, AC-002.

### P01-M03-T02 — Implement the deterministic reference counter

1. **Status:** Planned
2. **Objective:** Provide the approved offline counter for examples and tests.
3. **Why:** Version 1 needs reproducible behavior without a provider SDK.
4. **Learn first:** Deterministic text processing, Unicode caveats, documented approximations.
5. **Dependencies:** P01-M03-T01 and ADR 0001.
6. **Scope:** One reference algorithm and its identity; no accuracy claims.
7. **Files:** `tokenization.py`, focused counter tests.
8. **Symbols:** Approved reference-counter class.
9. **Input/output:** Text in; repeatable non-negative count out.
10. **Edge cases:** Empty/whitespace-only text, Unicode, line endings, repeated spaces.
11. **Security:** Never log text; bound pathological processing if needed.
12. **Tests:** Example table, determinism, Unicode, empty input.
13. **Acceptance:** Algorithm is documented as an estimate and counter identity is stable.
14. **Done:** Focused tests pass and limitations are reviewed.
15. **Evidence:** Test output and documented examples.
16. **Complexity:** Intermediate.
17. **Learning time:** 60–90 minutes.
18. **Interview preparation:** Determinism, tokenizer mismatch, approximation risk.
19. **Out of scope:** Benchmarking against commercial tokenizers.
20. **Requirement links:** FR-003, FR-005, QR-001, AC-002, AC-004.

### P01-M03-T03 — Implement usable-budget calculation

1. **Status:** Planned
2. **Objective:** Compute total minus fixed overhead minus reserved output exactly.
3. **Why:** All later selection relies on a proven budget invariant.
4. **Learn first:** Integer invariants, boundary-value analysis, pure functions.
5. **Dependencies:** P01-M02-T02, P01-M02-T04.
6. **Scope:** One pure calculation and impossible-budget rejection.
7. **Files:** `budget.py`, `tests/unit/test_budget.py`.
8. **Symbols:** Proposed `calculate_usable_input_budget(config) -> int`.
9. **Input/output:** Valid integer limits in; positive usable budget out.
10. **Edge cases:** Exact zero, negative values, booleans-as-ints, very large integers.
11. **Security:** Reject resource-abusive/unbounded values if a maximum is approved.
12. **Tests:** Normal, exact-fit arithmetic, zero/negative usable, invalid numeric types.
13. **Acceptance:** Formula matches `AC-003`; impossible configurations raise specific errors.
14. **Done:** Boundary tests pass and arithmetic is explained.
15. **Evidence:** AC-003-focused test output.
16. **Complexity:** Beginner.
17. **Learning time:** 45–75 minutes.
18. **Interview preparation:** Invariants, off-by-one failures, boundary testing.
19. **Out of scope:** Item selection.
20. **Requirement links:** FR-004, QR-002, AC-003.

### P01-M03-T04 — Validate token-counter results

1. **Status:** Planned
2. **Objective:** Convert counter boundary failures into safe, specific domain failures.
3. **Why:** An injected dependency can fail or violate its contract.
4. **Learn first:** Defensive boundaries, exception chaining, Python numeric type traps.
5. **Dependencies:** P01-M02-T02, P01-M03-T01.
6. **Scope:** Checked counter invocation wrapper only.
7. **Files:** `tokenization.py`, focused boundary tests.
8. **Symbols:** Proposed `count_tokens(counter, text) -> int` wrapper.
9. **Input/output:** Counter/text in; validated count or chained `TokenCounterError` out.
10. **Edge cases:** Negative, float, bool, exception, nondeterministic fake.
11. **Security:** Error/log output excludes supplied text.
12. **Tests:** Each invalid return and wrapped failure.
13. **Acceptance:** Invalid counter behavior never enters budget arithmetic silently.
14. **Done:** Focused tests pass; cause preservation reviewed.
15. **Evidence:** Boundary-test output and safe error examples.
16. **Complexity:** Intermediate.
17. **Learning time:** 60–90 minutes.
18. **Interview preparation:** Trust boundaries, adapter validation, failure translation.
19. **Out of scope:** Detecting all nondeterministic counters automatically.
20. **Requirement links:** FR-002, FR-003, QR-003, QR-005, AC-002.

## M04 — Validation

### P01-M04-T01 — Validate individual context items

1. **Status:** Planned
2. **Objective:** Reject missing/blank fields, unsupported values, and malformed metadata.
3. **Why:** Invalid content must fail before counting or selection.
4. **Learn first:** Validation boundaries, normalization versus rejection.
5. **Dependencies:** P01-M02-T02, P01-M02-T03.
6. **Scope:** One-item validation; no collection rules.
7. **Files:** `validation.py`, `tests/unit/test_item_validation.py`.
8. **Symbols:** Proposed `validate_item(item) -> None`.
9. **Input/output:** Item in; no mutation on success, specific error on failure.
10. **Edge cases:** Blank Unicode, invalid metadata keys/values, unsupported enums/types.
11. **Security:** Bound metadata/content size if approved; never echo raw content in errors.
12. **Tests:** Valid item plus one focused case per invalid field.
13. **Acceptance:** Relevant `AC-001` item cases produce specific errors.
14. **Done:** Tests pass and accepted/rejected values are documented.
15. **Evidence:** Validation-test output.
16. **Complexity:** Intermediate.
17. **Learning time:** 75–105 minutes.
18. **Interview preparation:** Input validation, Unicode, fail-fast design.
19. **Out of scope:** Duplicate IDs or budget validation.
20. **Requirement links:** FR-001, FR-002, QR-005, AC-001.

### P01-M04-T02 — Validate item collections

1. **Status:** Planned
2. **Objective:** Reject duplicate identifiers and invalid collection shapes deterministically.
3. **Why:** Reports and decisions require unique item identity.
4. **Learn first:** Set-based uniqueness, iterable consumption, ordering preservation.
5. **Dependencies:** P01-M04-T01.
6. **Scope:** Materialize/validate the approved collection type and uniqueness only.
7. **Files:** `validation.py`, `tests/unit/test_collection_validation.py`.
8. **Symbols:** Proposed `validate_items(items) -> tuple[ContextItem, ...]`.
9. **Input/output:** Supported collection in; order-preserving immutable sequence out.
10. **Edge cases:** Empty input, duplicate IDs with different content, generator reuse, `None`.
11. **Security:** Apply approved collection-size limit to resist resource abuse.
12. **Tests:** Empty-policy case, duplicates, stable input order, invalid members.
13. **Acceptance:** Duplicate IDs always raise the documented specific error.
14. **Done:** Focused tests pass and materialization choice is explained.
15. **Evidence:** AC-001 collection-test output.
16. **Complexity:** Intermediate.
17. **Learning time:** 60–90 minutes.
18. **Interview preparation:** Collections, complexity, stable ordering.
19. **Out of scope:** Priority sorting.
20. **Requirement links:** FR-002, FR-005, AC-001, AC-004.

### P01-M04-T03 — Implement pre-flight assembly validation

1. **Status:** Planned
2. **Objective:** Validate config, collection, and counter availability before assembly.
3. **Why:** Failures should occur before partial decisions or output exist.
4. **Learn first:** Orchestration boundaries, transactional thinking, fail-fast behavior.
5. **Dependencies:** P01-M03-T03, P01-M03-T04, P01-M04-T02.
6. **Scope:** Compose existing validators without selecting items.
7. **Files:** `validation.py`, focused pre-flight tests.
8. **Symbols:** Proposed `preflight_validate(items, config, counter)`.
9. **Input/output:** Assembly inputs in; validated values/usable budget or error out.
10. **Edge cases:** Multiple simultaneous errors, empty collection, impossible budget.
11. **Security:** No content in diagnostics; reject before expensive processing.
12. **Tests:** Valid composition and precedence of each failure class.
13. **Acceptance:** No selection path runs with invalid configuration/items/counter.
14. **Done:** Tests pass and error precedence is documented.
15. **Evidence:** Pre-flight test output.
16. **Complexity:** Intermediate.
17. **Learning time:** 60–90 minutes.
18. **Interview preparation:** Validation pipelines, failure atomicity.
19. **Out of scope:** Assembly output.
20. **Requirement links:** FR-002, FR-004, FR-011, QR-002, AC-001, AC-003, AC-008.

## M05 — Selection and Overflow

### P01-M05-T01 — Implement stable item ordering

1. **Status:** Planned
2. **Objective:** Order validated items using ADR 0002.
3. **Why:** Selection must be reproducible and explainable.
4. **Learn first:** Python stable sort, key functions, total ordering.
5. **Dependencies:** P01-M01-T03, P01-M04-T02.
6. **Scope:** Pure ordering function only.
7. **Files:** `ordering.py`, `tests/unit/test_ordering.py`.
8. **Symbols:** Proposed `order_items(items) -> tuple[ContextItem, ...]`.
9. **Input/output:** Valid items in; stable ordered tuple out.
10. **Edge cases:** Equal priority/tie values, empty/single input, adversarial content.
11. **Security:** Sort only validated metadata, never content instructions.
12. **Tests:** Policy examples, stability, repeated invocation, untrusted-content case.
13. **Acceptance:** Output exactly matches ADR examples and `AC-004` tie behavior.
14. **Done:** Focused tests pass; complexity is explained.
15. **Evidence:** Ordering-test output.
16. **Complexity:** Intermediate.
17. **Learning time:** 60–90 minutes.
18. **Interview preparation:** Stable sorting, deterministic policies.
19. **Out of scope:** Budget decisions.
20. **Requirement links:** FR-005, FR-006, FR-009, AC-004, AC-006.

### P01-M05-T02 — Implement exact-fit and full-inclusion decisions

1. **Status:** Planned
2. **Objective:** Include a complete item when its counted cost fits remaining budget.
3. **Why:** This is the smallest positive selection behavior.
4. **Learn first:** Pure decision functions, remaining-capacity invariants.
5. **Dependencies:** P01-M03-T04, P01-M04-T03, P01-M05-T01.
6. **Scope:** Full inclusion only; overflow delegates to later tasks.
7. **Files:** `overflow.py`, focused inclusion tests.
8. **Symbols:** Proposed `decide_full_inclusion(item, remaining, counter)`.
9. **Input/output:** Item/budget in; include decision and updated remainder out.
10. **Edge cases:** Exact fit, empty content policy, zero remaining, count boundary.
11. **Security:** Decision metadata omits content.
12. **Tests:** Below/exact/above budget and counter failure.
13. **Acceptance:** Included count never exceeds starting remainder.
14. **Done:** Focused tests pass and invariant is stated.
15. **Evidence:** Inclusion boundary-test output.
16. **Complexity:** Beginner.
17. **Learning time:** 45–75 minutes.
18. **Interview preparation:** Greedy allocation, invariants, exact-fit testing.
19. **Out of scope:** Truncation and collection iteration.
20. **Requirement links:** FR-007, QR-002, AC-005.

### P01-M05-T03 — Implement atomic-item exclusion

1. **Status:** Planned
2. **Objective:** Exclude non-truncatable items that do not fit, with an explicit reason.
3. **Why:** `FR-008` prohibits partial atomic content.
4. **Learn first:** Atomicity, decision records, safe fallback behavior.
5. **Dependencies:** P01-M01-T04, P01-M05-T02.
6. **Scope:** One overflow branch for atomic items.
7. **Files:** `overflow.py`, focused atomic tests.
8. **Symbols:** Approved exclusion decision/reason.
9. **Input/output:** Oversized atomic item in; excluded decision, unchanged budget out.
10. **Edge cases:** Mandatory atomic item, zero budget, item larger than total limit.
11. **Security:** Exclusion report carries ID/count, not raw content.
12. **Tests:** Full-or-excluded invariant and reason correctness.
13. **Acceptance:** No atomic item is shortened under any tested path.
14. **Done:** Focused tests pass; impossible mandatory behavior matches ADR.
15. **Evidence:** Atomicity-test output.
16. **Complexity:** Beginner.
17. **Learning time:** 45–75 minutes.
18. **Interview preparation:** Atomic operations, graceful degradation.
19. **Out of scope:** Truncatable items.
20. **Requirement links:** FR-007, FR-008, QR-002, AC-005.

### P01-M05-T04 — Implement deterministic permitted truncation

1. **Status:** Planned
2. **Objective:** Shorten only allowed items to an approved, budget-safe representation.
3. **Why:** `FR-007` requires an explicit truncate path when policy permits.
4. **Learn first:** Counter-aware search, monotonicity assumptions, Unicode slicing risk.
5. **Dependencies:** P01-M01-T04, P01-M03-T04, P01-M05-T02.
6. **Scope:** Approved deterministic truncation algorithm for one item.
7. **Files:** `overflow.py`, `tests/unit/test_truncation.py`.
8. **Symbols:** Proposed `truncate_to_budget(item, remaining, counter)`.
9. **Input/output:** Truncatable item/budget in; shortened content decision or exclusion out.
10. **Edge cases:** No useful prefix, counter non-monotonicity, Unicode, marker/delimiter overhead.
11. **Security:** Preserve escaping boundary; no semantic/compression claims.
12. **Tests:** Exact fit, one-over, tiny budget, Unicode, deterministic repeat, reported counts.
13. **Acceptance:** Final counted representation fits and transformation is explicit.
14. **Done:** Focused tests pass; algorithm/complexity limitations documented.
15. **Evidence:** Truncation-test output.
16. **Complexity:** Advanced.
17. **Learning time:** 90–150 minutes.
18. **Interview preparation:** Search algorithms, monotonic contracts, lossy transformations.
19. **Out of scope:** LLM summarization or meaning preservation guarantees.
20. **Requirement links:** FR-007, FR-008, QR-002, AC-005.

### P01-M05-T05 — Implement the collection selection loop

1. **Status:** Planned
2. **Objective:** Apply ordering and per-item policies across the complete collection.
3. **Why:** Individual decisions must compose without exceeding budget.
4. **Learn first:** Greedy algorithms, state transitions, pure orchestration.
5. **Dependencies:** P01-M05-T01 through P01-M05-T04.
6. **Scope:** Iterate ordered items; accumulate decisions and remaining budget.
7. **Files:** `selection.py`, `tests/unit/test_selection.py`.
8. **Symbols:** Proposed `select_items(items, usable_budget, counter)`.
9. **Input/output:** Valid items/budget in; selected representations and all decisions out.
10. **Edge cases:** Empty input, all excluded, mixed atomic/truncatable, exact exhaustion.
11. **Security:** Content never controls loop policy; resource limits respected.
12. **Tests:** Synthetic scenario matrix covering every outcome and priority interaction.
13. **Acceptance:** Each input gets exactly one decision; total final count stays within budget.
14. **Done:** Focused scenario tests pass and state changes are explained.
15. **Evidence:** Selection-test output and scenario table.
16. **Complexity:** Advanced.
17. **Learning time:** 90–150 minutes.
18. **Interview preparation:** Greedy policy trade-offs, state machines, complexity.
19. **Out of scope:** Rendering or report schema assembly.
20. **Requirement links:** FR-005–FR-008, QR-002, AC-004, AC-005.

### P01-M05-T06 — Add selection invariant tests

1. **Status:** Planned
2. **Objective:** Test broad synthetic combinations for budget, atomicity, uniqueness, and determinism.
3. **Why:** Example tests alone may miss composition failures.
4. **Learn first:** Invariant/property-oriented testing, generated versus table-driven data.
5. **Dependencies:** P01-M05-T05 and approved test tooling.
6. **Scope:** Deterministic synthetic cases; add a property library only with separate authorization.
7. **Files:** `tests/invariants/test_selection_invariants.py` or approved equivalent.
8. **Symbols:** Test helpers/factories only.
9. **Input/output:** Synthetic item/config combinations in; invariant assertions out.
10. **Edge cases:** Zero items, repeated priorities, maximum sizes, all outcome mixtures.
11. **Security:** Synthetic licensed data only; bounded generation.
12. **Tests:** Budget safety, atomicity, one-decision-per-ID, stable repeats, no input mutation.
13. **Acceptance:** Each invariant maps to a requirement and fails on a demonstrated mutation/fault where practical.
14. **Done:** Invariant suite passes with reproducible seed/cases.
15. **Evidence:** Commands, output, and case/seed record.
16. **Complexity:** Advanced.
17. **Learning time:** 90–150 minutes.
18. **Interview preparation:** Property testing, invariants, test effectiveness.
19. **Out of scope:** Performance benchmarks or random unbounded fuzzing.
20. **Requirement links:** FR-005, FR-007, FR-008, QR-001, QR-002, AC-004, AC-005.

## M06 — Rendering, Reporting, and Orchestration

### P01-M06-T01 — Decide trust-aware rendering and escaping

1. **Status:** Planned
2. **Objective:** Define deterministic format, delimiters, escaping, and overhead accounting.
3. **Why:** `FR-009` requires visible trust boundaries without overstating protection.
4. **Learn first:** Prompt injection, escaping, canonical formats, defense in depth.
5. **Dependencies:** P01-M05-T05.
6. **Scope:** Compare tagged text/structured sections; decide format and residual risks.
7. **Files:** `docs/adr/0004-trust-aware-rendering.md`.
8. **Symbols:** Proposed renderer/escape contract.
9. **Input/output:** Selected representations in; canonical rendered text definition out.
10. **Edge cases:** Content containing delimiters, mixed trust, truncation at marker boundary.
11. **Security:** State explicitly that delimiters do not neutralize prompt injection.
12. **Tests:** Specify adversarial delimiter/instruction cases and overhead counting.
13. **Acceptance:** ADR defines escaping and how rendered overhead enters budget.
14. **Done:** ADR approved before renderer implementation.
15. **Evidence:** ADR with examples and threat limitations.
16. **Complexity:** Advanced.
17. **Learning time:** 75–120 minutes.
18. **Interview preparation:** Prompt injection, canonicalization, trust boundaries.
19. **Out of scope:** Content filtering or injection-proof claims.
20. **Requirement links:** FR-004, FR-009, QR-002, AC-006.

### P01-M06-T02 — Implement deterministic trust-aware rendering

1. **Status:** Planned
2. **Objective:** Render selected items exactly as approved and count final representation.
3. **Why:** The output must preserve trust labels and remain within budget.
4. **Learn first:** Pure rendering, escaping, canonical serialization.
5. **Dependencies:** P01-M06-T01, P01-M03-T04, P01-M05-T05.
6. **Scope:** Renderer only; no orchestration facade.
7. **Files:** `rendering.py`, `tests/unit/test_rendering.py`.
8. **Symbols:** Proposed `render_items(selected, counter) -> RenderedContext`.
9. **Input/output:** Selected items in; deterministic text and final count out.
10. **Edge cases:** Empty selection, embedded delimiters, Unicode, mixed trust, overhead overflow.
11. **Security:** Escape delimiters; retain labels; never execute content.
12. **Tests:** Golden examples, adversarial text, repeatability, final-count agreement.
13. **Acceptance:** Untrusted text cannot alter selection metadata/policy and is distinctly delimited.
14. **Done:** Focused tests pass; residual injection risk documented.
15. **Evidence:** AC-006 test output and reviewed examples.
16. **Complexity:** Advanced.
17. **Learning time:** 90–150 minutes.
18. **Interview preparation:** Safe rendering, escaping, prompt-injection limits.
19. **Out of scope:** Model invocation or security classification.
20. **Requirement links:** FR-009, QR-002, AC-005, AC-006.

### P01-M06-T03 — Build the report and safe diagnostics

1. **Status:** Planned
2. **Objective:** Produce complete provenance/decision reports and content-free logs.
3. **Why:** `FR-010` and `QR-005` require explainability without leakage.
4. **Learn first:** Structured logging, observability versus privacy, schema stability.
5. **Dependencies:** P01-M02-T04, P01-M05-T05, P01-M06-T02.
6. **Scope:** Report assembly and logging events only.
7. **Files:** `reporting.py`, `tests/unit/test_reporting.py`.
8. **Symbols:** Proposed `build_report(...)`, logger event helpers.
9. **Input/output:** Budget/counter/decisions in; immutable report and safe metadata events out.
10. **Edge cases:** All excluded, truncation, counter error, sensitive content resembling credentials.
11. **Security:** Allow aggregate token counts; forbid raw content, auth tokens, secrets, personal data.
12. **Tests:** Schema assertions and captured-log negative assertions for sentinel secrets/content.
13. **Acceptance:** All required fields exist; logs/report do not duplicate content.
14. **Done:** AC-007-focused tests pass and fields are documented.
15. **Evidence:** Schema and log-capture output.
16. **Complexity:** Intermediate.
17. **Learning time:** 75–120 minutes.
18. **Interview preparation:** Safe observability, data minimization, auditability.
19. **Out of scope:** External telemetry backend or cost billing.
20. **Requirement links:** FR-010, QR-005, AC-007.

### P01-M06-T04 — Implement the public assembler facade

1. **Status:** Planned
2. **Objective:** Compose pre-flight, ordering, selection, rendering, and reporting through one API.
3. **Why:** Consumers need a cohesive entry point while internal components remain testable.
4. **Learn first:** Facade pattern, dependency injection, functional core/imperative shell.
5. **Dependencies:** P01-M04-T03, P01-M05-T05, P01-M06-T02, P01-M06-T03.
6. **Scope:** Orchestration only; reuse existing logic without duplication.
7. **Files:** `assembler.py`, package exports, `tests/integration/test_assembler.py`.
8. **Symbols:** Proposed `ContextAssembler` or `assemble_context(...)` approved during review.
9. **Input/output:** Items/config/counter in; `AssemblyResult` out or specific error.
10. **Edge cases:** Empty input, mixed outcomes, exact budget, injected failure, repeated call.
11. **Security:** No external I/O; no raw-content logging; untrusted content remains data.
12. **Tests:** End-to-end synthetic success and failure cases using a fake counter.
13. **Acceptance:** `FR-011` holds; result/report counts agree and budget is safe.
14. **Done:** Integration tests pass and facade is explained line by line.
15. **Evidence:** Integration-test output and dependency diagram.
16. **Complexity:** Advanced.
17. **Learning time:** 90–150 minutes.
18. **Interview preparation:** Facades, dependency injection, orchestration boundaries.
19. **Out of scope:** CLI, API server, retriever, model, tool, storage.
20. **Requirement links:** FR-001–FR-011, QR-002, QR-003, AC-001–AC-008.

## M07 — System Verification

### P01-M07-T01 — Build the acceptance scenario matrix

1. **Status:** Planned
2. **Objective:** Map and execute focused scenarios for `AC-001` through `AC-008`.
3. **Why:** Unit tests must combine into requirement-level evidence.
4. **Learn first:** Acceptance testing, traceability, test pyramid.
5. **Dependencies:** P01-M06-T04.
6. **Scope:** Add missing scenario tests; do not duplicate unit coverage without purpose.
7. **Files:** Integration/acceptance tests and traceability record.
8. **Symbols:** Test fixtures/builders only.
9. **Input/output:** Synthetic scenarios in; mapped pass/fail evidence out.
10. **Edge cases:** Invalid input, exact budget, mixed outcomes, adversarial content, safe logs.
11. **Security:** Synthetic data; sentinel-secret negative tests.
12. **Tests:** One or more explicit scenarios per AC with requirement IDs.
13. **Acceptance:** Matrix has no unmapped `AC-001`–`AC-008` row.
14. **Done:** Relevant suite passes and output is recorded honestly.
15. **Evidence:** Matrix, commands, and actual output.
16. **Complexity:** Advanced.
17. **Learning time:** 90–150 minutes.
18. **Interview preparation:** Acceptance strategy, traceability, test layering.
19. **Out of scope:** AC-009/010 tooling and AC-011 experiment.
20. **Requirement links:** AC-001–AC-008 and their linked requirements.

### P01-M07-T02 — Verify canonical determinism and serialization

1. **Status:** Planned
2. **Objective:** Prove repeated equivalent inputs yield byte-equivalent serialized results.
3. **Why:** `AC-004` is stronger than Python object equality.
4. **Learn first:** Canonical serialization, ordering, reproducibility.
5. **Dependencies:** P01-M06-T04.
6. **Scope:** Approve/implement one serialization method and determinism test.
7. **Files:** Serialization helper if needed and determinism integration tests.
8. **Symbols:** Proposed `serialize_result(result) -> bytes|str`.
9. **Input/output:** Result in; stable canonical representation out.
10. **Edge cases:** Metadata ordering, enums, Unicode, repeated process/run if feasible.
11. **Security:** Serialization does not add raw content to report fields beyond intended rendered output.
12. **Tests:** Repeated run, reordered metadata, tie cases, stable byte comparison.
13. **Acceptance:** Identical approved inputs/config/counter yield byte-equivalent results.
14. **Done:** AC-004 evidence passes and canonical rules are documented.
15. **Evidence:** Determinism command/output.
16. **Complexity:** Advanced.
17. **Learning time:** 75–120 minutes.
18. **Interview preparation:** Reproducibility, canonicalization, deterministic APIs.
19. **Out of scope:** Cross-version guarantee unless explicitly designed.
20. **Requirement links:** FR-005, FR-010, AC-004.

### P01-M07-T03 — Verify offline, typing, privacy, and repository quality gates

1. **Status:** Planned
2. **Objective:** Produce evidence for `AC-008`, `AC-009`, and `AC-010` using approved tools.
3. **Why:** Implementation completion includes more than functional behavior.
4. **Learn first:** Offline test isolation, static typing, secret scanning, license/data review.
5. **Dependencies:** P01-M07-T01, P01-M07-T02 and authorized tooling.
6. **Scope:** Run documented checks without network/credentials; review fixtures and repository scope.
7. **Files:** Tool configuration only if approved; validation record.
8. **Symbols:** None unless typing fixes are separately reviewed.
9. **Input/output:** Repository and commands in; captured actual outcomes out.
10. **Edge cases:** Tool unavailable, false-positive secret, environment-dependent output.
11. **Security:** Do not print secrets; stop and rotate if a real secret is found.
12. **Tests:** Full default suite offline, static type check, lint/format/link/secret checks as selected.
13. **Acceptance:** Evidence shows Python 3.11 compatibility, offline execution, and clean reviewed fixtures.
14. **Done:** Actual results and limitations are recorded; failures are not relabeled as passes.
15. **Evidence:** Commands, versions, output summaries, review checklist.
16. **Complexity:** Intermediate.
17. **Learning time:** 75–120 minutes.
18. **Interview preparation:** CI quality gates, supply-chain/privacy controls.
19. **Out of scope:** Deployment or paid services.
20. **Requirement links:** QR-001, QR-004, QR-007, AC-008, AC-009, AC-010.

## M08 — Evidence and Learning Outputs

### P01-M08-T01 — Design the first reproducible experiment

1. **Status:** Planned
2. **Objective:** Predeclare a falsifiable deterministic context-mixture experiment.
3. **Why:** `AC-011` requires method and success criteria before results.
4. **Learn first:** Experimental design, baselines, variables, validity threats.
5. **Dependencies:** P01-M07-T03.
6. **Scope:** Hypothesis, synthetic data, environment, metrics, command, threshold; no execution yet.
7. **Files:** `docs/experiments/YYYY-MM-DD-context-allocation-policy.md` using template.
8. **Symbols:** Optional small synthetic fixture generator planned separately within this task if needed.
9. **Input/output:** Approved implementation/policy in; reproducible protocol out.
10. **Edge cases:** Dataset too small, tautological metric, hardware-dependent claims.
11. **Security:** Synthetic/licensed data only; no private manuscripts or personal data.
12. **Tests:** Validate experiment command and artifact paths without claiming results.
13. **Acceptance:** Hypothesis, baseline, variables, controls, thresholds, and limitations are predeclared.
14. **Done:** Experiment design reviewed before running.
15. **Evidence:** `Planned` experiment report.
16. **Complexity:** Advanced.
17. **Learning time:** 90–150 minutes.
18. **Interview preparation:** Experiment design, metric selection, causal limits.
19. **Out of scope:** Running the experiment or inventing expected numbers.
20. **Requirement links:** QR-006, AC-011.

### P01-M08-T02 — Execute and report the approved experiment

1. **Status:** Planned
2. **Objective:** Run the frozen protocol and record raw observations and limitations.
3. **Why:** Validation requires reproducible evidence, not illustrative numbers.
4. **Learn first:** Environment capture, raw versus interpreted results, uncertainty.
5. **Dependencies:** P01-M08-T01 approved.
6. **Scope:** Execute exact command, retain small raw artifacts, analyze without changing thresholds post hoc.
7. **Files:** Approved experiment report and raw artifact path.
8. **Symbols:** No production behavior changes; fixes become separate tasks.
9. **Input/output:** Frozen protocol/data in; raw results and analysis out.
10. **Edge cases:** Failed run, inconclusive result, environmental noise, unexpected defect.
11. **Security:** Inspect artifacts for content/secrets before committing.
12. **Tests:** Re-run reproducibility check where practical.
13. **Acceptance:** Report contains environment, data, command, raw results, interpretation, and threats.
14. **Done:** Evidence reviewed; inconclusive/failed outcomes remain honestly labeled.
15. **Evidence:** Actual command output, raw artifact, completed report.
16. **Complexity:** Advanced.
17. **Learning time:** 90–180 minutes.
18. **Interview preparation:** Benchmark integrity, reproducibility, interpreting negative results.
19. **Out of scope:** Performance claims beyond the measured environment.
20. **Requirement links:** QR-006, AC-011.

### P01-M08-T03 — Produce learning, interview, and status handoff

1. **Status:** Planned
2. **Objective:** Convert reviewed engineering evidence into original learning/interview material and accurate status.
3. **Why:** The repository connects implementation work to mentoring, portfolio, and publishing goals.
4. **Learn first:** Technical reflection, interview rubric design, evidence-backed writing.
5. **Dependencies:** P01-M08-T02 and reviewed implementation evidence.
6. **Scope:** Learning record, scoped interview package, documentation reconciliation, proposed status update.
7. **Files:** Approved learning-note path, `interview-prep/` artifact(s), project README, `PROJECT_STATUS.md`; handbook remains separate if not ready.
8. **Symbols:** None.
9. **Input/output:** Code/tests/ADRs/experiment evidence in; traceable original materials out.
10. **Edge cases:** Optional publication unfinished, hypothetical scenario, implementation limitation.
11. **Security:** No private/commercial manuscript content; verify sources/licenses and remove sensitive data.
12. **Tests:** Link check, originality/source review, evidence-link review.
13. **Acceptance:** Claims link to evidence; simulations are labeled; status does not exceed criteria.
14. **Done:** User approves each artifact and any status change separately.
15. **Evidence:** Learning record, interview mapping, documentation checks, reviewed tracker diff.
16. **Complexity:** Intermediate.
17. **Learning time:** 120–180 minutes.
18. **Interview preparation:** All module topics; communicating trade-offs and failures.
19. **Out of scope:** Automatic publication, commercial distribution, or claiming professional production experience.
20. **Requirement links:** All requirements; especially QR-006, QR-007, AC-010, AC-011.

## Critical Path

`P01-M01-T01` → policy ADRs → M02 contracts → M03 token/budget → M04 validation → M05 selection → M06 integration → M07 verification → M08 experiment/evidence.

Parallel work is intentionally limited for learning: documentation notes may follow an approved task, but no later implementation task begins before its stated dependencies and explicit user approval.
