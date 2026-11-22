# Project 01: Context Assembler Engine

## Status

**Specified — implementation has not started.**

## Problem

AI applications often assemble instructions, user input, retrieved evidence, conversation history, and tool results without a deterministic policy. The resulting prompt can exceed its context budget, lose high-value information, mix trusted and untrusted content, or become impossible to explain and test.

## Goal

Build a provider-neutral Python engine that selects, orders, truncates, and reports context items under an explicit token budget. The first version will be deterministic and offline: it will not call an LLM or depend on a paid API.

## Proposed Flow

```text
typed context items
        ↓
validation and trust labeling
        ↓
priority-aware budget allocation
        ↓
deterministic assembly
        ↓
assembled context + provenance/budget report
```

## Initial Scope

- Typed context items with source, trust level, priority, and content
- Pluggable token-counting interface with an offline deterministic implementation
- Reserved output budget and validated input limits
- Stable ordering and explicit overflow policy
- Provenance and inclusion/exclusion reasons in an assembly report
- Unit tests and property-oriented invariants using synthetic fixtures

## Out of Scope for Version 1

- Model-provider API calls or prompt execution
- Retrieval, reranking, embeddings, or vector databases
- Automatic summarization with an LLM
- Web UI, deployment infrastructure, or multi-tenant persistence
- Claims about answer quality or latency without reproducible experiments

## Intended Layout

The implementation phase may introduce this structure after design approval:

```text
src/context_assembler_engine/
tests/
examples/
```

No empty implementation scaffolding is treated as completed work.

## Key Documents

- [Requirements](REQUIREMENTS.md)
- [Acceptance criteria](ACCEPTANCE_CRITERIA.md)
- [Repository contribution rules](../../AGENTS.md)
- [Documentation templates](../../docs/templates/README.md)

## Design Questions to Resolve

1. Which token-counter contract best isolates provider-specific behavior?
2. Should priority be categorical, numeric, or represented by separate budget pools?
3. Which item types may be truncated, and which must be included atomically?
4. How should untrusted content be delimited without pretending delimiters eliminate prompt injection?
5. What report fields provide useful explainability without leaking sensitive content?

## Planned Delivery Sequence

1. Record ADRs for token counting and overflow policy.
2. Define public types and synthetic test fixtures.
3. Implement validation and deterministic assembly.
4. Add unit, invariant, and boundary tests.
5. Run a reproducible experiment against predefined context mixtures.
6. Publish the handbook chapter only after evidence is available.
