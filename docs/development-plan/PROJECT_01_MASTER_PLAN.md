# Project 01 Master Plan: Context Assembler Engine

## Planning Status

**Planning only. No implementation, tests, benchmarks, or project-completion claims exist.**

This plan is subordinate to the root `AGENTS.md`, the Project 01 requirements, and acceptance criteria. It proposes a development sequence without silently resolving open design decisions.

## Project Outcome

Create a Python 3.11+ library that deterministically validates, selects, truncates where permitted, orders, renders, and reports typed context items within an explicit token budget. Version 1 remains provider-neutral, offline, and free of model, tool, retriever, database, framework, or paid-API execution.

## Authoritative Scope

- Functional requirements: `FR-001` through `FR-011` in `projects/01-context-assembler-engine/REQUIREMENTS.md`.
- Quality requirements: `QR-001` through `QR-007` in the same document.
- Acceptance: `AC-001` through `AC-010` for **Implemented**; `AC-011` plus committed evidence for **Validated**.
- Out of scope: provider calls, retrieval/reranking, embeddings, LLM summarization, UI, persistence, deployment, and unsupported performance or quality claims.

## Current Assessment

- Project status: **Specified**; no source package, tests, fixtures, configuration, or executable tooling exists.
- Existing evidence: project README, requirements, and acceptance criteria only.
- Preferred dependency posture: standard library first; no dependency is approved by this plan.
- Current validation-tool names are intentionally undecided. Choosing test, lint, format, type, link, or secret-scanning tools requires a focused task and rationale.

## Proposed Architecture

```text
ContextItem[] + AssemblyConfig + TokenCounter
                    |
                    v
             pre-flight validation
                    |
                    v
        stable priority/order calculation
                    |
                    v
       include / truncate / exclude policy
                    |
                    v
          trust-aware deterministic render
                    |
                    v
        AssemblyResult + AssemblyReport
```

### Component Boundaries

| Component | Responsibility | Must not do |
|---|---|---|
| `models` | Immutable typed inputs, configuration, decisions, and results | Count tokens or choose items |
| `errors` | Specific domain exception hierarchy | Hide original error context |
| `tokenization` | `TokenCounter` protocol and approved deterministic counter | Import provider SDKs |
| `budget` | Compute usable budget and enforce arithmetic invariants | Select or render items |
| `validation` | Validate items, collection uniqueness, metadata, and configuration | Mutate inputs silently |
| `ordering` | Stable priority and tie-breaking keys | Apply overflow transformations |
| `overflow` | Atomic inclusion, permitted truncation, and exclusion decisions | Exceed budget or summarize with an LLM |
| `rendering` | Deterministic, trust-aware delimiters and final representation | Treat delimiters as complete injection protection |
| `reporting` | Provenance, counts, transformations, and reason codes | Duplicate raw content or secrets |
| `assembler` | Orchestrate pure components through one public entry point | Call networks, tools, retrievers, or models |

Module names are proposed and may be adjusted during the package-layout task without weakening these boundaries.

### Proposed Data Contracts

- `ContextItem`: identifier, item type, content, source metadata, trust classification, priority, and truncation permission.
- `AssemblyConfig`: total context limit, fixed overhead, reserved output tokens, and policy configuration approved by ADR.
- `TokenCounter`: injected protocol returning a non-negative integer for supplied text and exposing a counter identity for reports.
- `ItemDecision`: item identifier, original/final counts, outcome, transformation, and reason code.
- `AssemblyReport`: budget totals, counter identity, included/excluded identifiers, decisions, and provenance-safe metadata.
- `AssemblyResult`: rendered context plus report.

Exact field types, enum values, metadata restrictions, immutability, and serialization form remain task-level decisions.

## Error and Safety Strategy

- Reject invalid inputs before selection; do not repair malformed values silently.
- Use specific domain errors for item, collection, configuration, token-counter, and impossible-budget failures.
- Treat token-counter failures and negative/non-integer counts as boundary errors.
- Never return a result whose reported final input count exceeds usable input budget.
- Retain trust labels through decisions and rendering.
- Log identifiers, reason codes, aggregate token counts, latency, and optional cost estimates only; raw prompts, content, model output, authentication tokens, secrets, and personal data remain excluded by default.

## Architectural Alternatives Requiring Decisions

| Decision | Options to evaluate | Main trade-off |
|---|---|---|
| Token counter | character/word-like deterministic reference counter; tokenizer adapter later | Simplicity versus provider accuracy |
| Priority | categorical enum; bounded integer; policy object | Clarity versus flexibility |
| Tie-break | caller order; item identifier; explicit sequence | Intent preservation versus canonical serialization |
| Truncation | counter-aware prefix; item-type policy; exclusion only | Utility versus semantic damage |
| Mandatory semantics | priority only; explicit mandatory flag; reserved pools | Predictability versus risk of impossible budgets |
| Rendering | tagged plain text; structured sections | Readability versus escaping complexity |
| Serialization | standard-library dataclasses/enums; additional validation library | Dependency simplicity versus richer validation |

Mandatory context, system-instruction preservation, conversation history, retrieved documents, and tool results are not separate algorithms in the current requirements. They may be represented as typed items only after item types and priority semantics are approved. Compression is out of scope if it means model-based summarization; deterministic truncation alone is required.

## Module Roadmap

| Module | Objective | Tasks | Depends on | Completion evidence |
|---|---|---:|---|---|
| M01 Decisions and traceability | Resolve blocking policies without code | 4 | Specifications | Traceability review and accepted/proposed ADRs |
| M02 Package and domain contracts | Establish minimal typed public vocabulary | 4 | M01 | Reviewed package/config plan and contract tests |
| M03 Token and budget boundaries | Isolate counting and prove budget arithmetic | 4 | M02 | Focused unit/boundary tests |
| M04 Validation | Reject malformed inputs predictably | 3 | M02, M03 | Validation and error tests |
| M05 Selection and overflow | Select, truncate, and exclude deterministically | 6 | M01–M04 | Policy, invariant, and boundary tests |
| M06 Rendering, reporting, orchestration | Produce safe output and explain decisions | 4 | M05 | Rendering, report, logging, integration tests |
| M07 System verification | Verify cross-cutting acceptance criteria | 3 | M06 | Determinism, offline, typing, and security evidence |
| M08 Evidence and learning outputs | Record experiment and derived learning material | 3 | M07 | Experiment, learning, interview, and status artifacts |

Total: **8 modules, 31 tasks**. All implementation tasks begin in `Planned` state.

## Delivery Milestones

1. **Design ready:** M01 complete; blocking policies explicitly accepted.
2. **Contracts ready:** M02 complete; public vocabulary and package boundary reviewed.
3. **Budget core ready:** M03–M04 complete; arithmetic and input rejection proven in focused tests.
4. **Policy engine ready:** M05 complete; selection invariants proven.
5. **Integrated implementation candidate:** M06 complete; end-to-end result exists without external calls.
6. **Implemented evidence candidate:** M07 complete and `AC-001`–`AC-010` evidence reviewed. Status changes remain a separate approved action.
7. **Validated evidence candidate:** M08 experiment satisfies `AC-011`; no status claim until artifacts are committed and reviewed.

## Dependency Graph and Critical Path

```text
M01 -> M02 -> M03 -> M04 -> M05 -> M06 -> M07 -> M08
             \---------------> M05
```

The critical path runs through the policy ADRs, data contracts, token/budget boundary, validation, selection/overflow behavior, orchestration, system verification, and experiment. Documentation and interview notes can be prepared alongside completed modules but cannot claim unobserved results.

## Documentation and Traceability Strategy

- Requirements remain authoritative in the project directory; do not duplicate or renumber them here.
- Each backlog task maps to requirement and acceptance IDs and records deliverable evidence.
- Significant decisions use `docs/adr/NNNN-short-decision-title.md` and the repository ADR template.
- Task learning notes should record problem, concepts, alternatives, errors, test evidence, and reflection; final location is an open decision in M01.
- Experiment reports use `docs/experiments/YYYY-MM-DD-short-experiment-name.md` and retain raw, non-private artifacts when small enough for Git.
- Original interview questions use the repository template and cite actual code/tests after those artifacts exist.
- A handbook chapter begins only after implementation/evaluation evidence exists; generated text remains `DRAFT` until reviewed.

## Risks and Mitigations

| Risk | Impact | Planned mitigation |
|---|---|---|
| Token counts differ from provider tokenizers | Misleading capacity assumptions | Identify counter in every report; make boundary injectable |
| Truncation breaks meaning or delimiters | Unsafe or low-value context | Restrict by item policy; test delimiter closure; prefer exclusion for atomic items |
| Priority semantics starve useful items | Poor selection behavior | ADR, explicit tie-break, synthetic scenario matrix |
| Untrusted text resembles instructions/delimiters | Prompt-injection or rendering ambiguity | Escape/delimit and preserve trust; document residual risk |
| Reports/logs leak content | Privacy/security failure | Store identifiers and counts, not raw content; capture-log tests |
| Over-engineering | Learning and maintenance cost | Standard library first; one behavior per task |
| False completion claims | Portfolio credibility loss | Trace every claim to commands and committed evidence |

## Open Questions

1. What priority representation and tie-break rule should version 1 adopt?
2. Is “mandatory” an explicit field, a priority class, or out of scope for version 1?
3. Which item types may be truncated, and what counter-aware truncation contract is feasible?
4. What deterministic reference counter should ship, if any?
5. What metadata value types are safe and serializable?
6. What exact rendered format and escaping rules preserve trust boundaries?
7. Which standard-library or external test/type/lint tools will be selected? No tool is approved merely by appearing in the root technology direction.
8. Where should task-level learning records live without creating a second status tracker?

These are resolved through the first four planning/design tasks, with explicit user approval before implementation proceeds.
