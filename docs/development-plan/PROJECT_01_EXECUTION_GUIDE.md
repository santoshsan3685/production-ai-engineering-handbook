# Project 01 Execution Guide

## Operating Principle

One backlog task equals one focused learning and implementation session. Codex must mentor, propose, and explain; it must not automatically complete the project or move to the next task. The user reviews and explicitly approves every task transition.

The root `AGENTS.md`, Project 01 requirements, acceptance criteria, approved ADRs, and task backlog govern execution. If they conflict, stop, identify the exact conflict, and request a decision rather than inventing behavior.

## Before Starting a Task

1. Confirm the exact task ID and that all dependencies are approved.
2. Re-read the linked `FR`, `QR`, `AC`, ADR, and affected files.
3. Inspect the working tree; preserve unrelated and user-owned changes.
4. State the task objective, exact scope, exclusions, assumptions, and security implications.
5. Teach the “Learn first” concepts using a small example and check the user's understanding.
6. Propose the minimal design, expected file diff, public symbols, inputs, outputs, and errors.
7. Ask for a material design choice only when documentation does not resolve it.
8. Wait for explicit approval before editing implementation files.

## Test-First Task Workflow

For each implementation behavior:

1. **Explain the requirement:** Translate the linked requirement into observable behavior.
2. **Present the design:** Show the smallest interface and why it respects boundaries.
3. **Define examples:** Agree on normal, boundary, invalid, and security-sensitive cases.
4. **Add one focused failing test:** Confirm the failure is for the intended missing behavior, not setup.
5. **Implement the minimum:** Add only enough code to satisfy that test.
6. **Run the focused test:** Report the exact command and actual output.
7. **Explain every meaningful line:** Cover types, control flow, errors, imports, and alternatives.
8. **Add boundary/failure tests:** Include the task's listed edge and security cases.
9. **Refactor only with a reason:** Preserve behavior and rerun focused tests after each refactor.
10. **Run relevant regression checks:** Broaden only to checks affected by the change.
11. **Review the diff:** Look for scope creep, duplication, leakage, weak names, and unsupported claims.
12. **Update evidence and learning notes:** Record actual results and unresolved limitations.
13. **Stop for approval:** Do not begin the next task.

If the selected test framework is not yet configured, complete `P01-M02-T01` first. Never invent a command or install a package implicitly.

## Codex Mentoring Rules

Codex must:

- work only on the named task and describe any necessary scope expansion before acting;
- prefer questions and small examples that help the user reason, rather than presenting a large finished solution;
- show a focused test before the corresponding behavior implementation;
- explain Python syntax and design choices at the user's requested depth;
- offer alternatives with concrete trade-offs, marking proposals as proposals;
- preserve deterministic, offline execution and injected external boundaries;
- report only commands actually run and results actually observed;
- stop after the task review and wait for explicit approval.

Codex must not:

- implement multiple backlog tasks in one session unless the user explicitly changes the scope;
- install dependencies, call paid APIs, access external services, deploy, commit, push, or publish without explicit authorization;
- silently revise requirements, ADRs, acceptance criteria, or status;
- log or expose prompts, context content, model output, authentication tokens, credentials, secrets, personal data, or private manuscripts;
- claim performance, completion, test success, or professional experience without evidence;
- turn hypothetical interview scenarios into purported production experience.

## Code Review Checklist

### Scope and Architecture

- Does the diff implement only the approved task?
- Is domain logic separate from provider, network, file, framework, and logging adapters?
- Is the public API smaller than or equal to the approved design?
- Are new dependencies absent or explicitly authorized and justified?

### Python Quality

- Are names descriptive and public interfaces typed?
- Are functions cohesive and failure modes explicit?
- Are inputs left unmodified unless mutation was approved?
- Are exception messages safe and causes preserved?

### Correctness and Tests

- Does at least one test fail before the behavior exists and pass afterward?
- Are normal, boundary, invalid, and relevant security cases covered?
- Are tests deterministic, offline, synthetic/licensed, and free of credentials?
- Do assertions verify behavior rather than implementation trivia?
- Do requirement IDs appear in names/docstrings or traceability evidence where practical?

### AI and Security Boundaries

- Can untrusted content influence only documented data fields, not policy or control flow?
- Is the usable-budget invariant maintained at every step?
- Are atomic items never partially included?
- Are reports/logs limited to identifiers, reason codes, aggregate counts, latency, and approved estimates?
- Does documentation avoid implying delimiters make prompt injection impossible?

### Documentation and Evidence

- Do docs describe actual behavior and known limits?
- Are commands, versions, and actual results recorded?
- Are planned checks distinguished from passed checks?
- Are sources/license obligations and originality requirements satisfied?

## Task Completion and Approval

A task may move from `Planned` to `Review` only when:

- its acceptance criterion and definition of done are satisfied;
- focused tests/checks have actual recorded outcomes;
- the diff contains no unrelated changes;
- security and privacy considerations were reviewed;
- the learning record explains the result and limitations.

A task moves to `Approved` only after the user reviews the code, test evidence, line-by-line explanation, and diff. Approval of one task authorizes no later task.

If blocked, record the blocker and stop. Do not weaken a requirement to make a task pass. If a defect is found outside the active task, record a proposed backlog item and ask before editing it.

## Module and Project Completion

- A module completes when all of its tasks are approved and its learning checkpoint is reviewed.
- `Implemented` requires evidence for `AC-001` through `AC-010`; it is not inferred from code volume.
- `Validated` additionally requires `AC-011` with reviewed, committed experiment evidence.
- Project status changes require a separate documentation diff and explicit approval.
- Interview, learning, and handbook publication statuses remain distinct from technical implementation status.

## Suggested Git Discipline

Codex must not commit or push unless explicitly authorized. When the user chooses to commit:

- keep one approved task or one coherent documentation decision per commit;
- review `git diff` and `git status` before staging;
- stage explicit paths, especially in a working tree with unrelated changes;
- use an imperative message referencing the task, for example `P01-M03-T03 validate usable budget`;
- never include secrets, private/commercial manuscripts, generated caches, or unrelated files;
- do not rewrite shared history or force-push.

An ADR may be committed separately before the implementation it governs. A failing test may share a commit with its minimal implementation when the final commit is green and the learning record preserves the red/green evidence.

## Session Handoff Template

At the end of every task, report:

```text
Task: <ID and title>
Status: Review | Blocked
Requirements: <FR/QR/AC IDs>
Files changed: <explicit paths>
Design decision: <what and why>
Checks run: <exact commands>
Observed results: <actual results, including failures>
Security/privacy review: <findings>
Known limitations: <remaining issues>
Learning summary: <what the user can now explain>
Diff review: <scope and notable lines>
Next task: <ID only; not started>
Approval requested: yes
```

## Prompt Template for a Single Task

```text
Act as my senior Python mentor for Project 01. Work only on <TASK_ID> from
docs/development-plan/PROJECT_01_TASK_BACKLOG.md.

First inspect the task, its dependencies, linked requirements, current code, and
applicable ADRs. Do not edit files yet. Explain the requirement, prerequisite
concepts, minimal design, inputs/outputs, edge cases, security considerations,
expected diff, and the first focused failing test. Ask me to approve the design.

After approval, use the test-first workflow in PROJECT_01_EXECUTION_GUIDE.md.
Explain every meaningful line, run only relevant approved checks, review the diff,
update the learning record, and stop for my explicit approval. Do not start another
task, install dependencies, call external/paid APIs, commit, push, or change status.
```
