# Senior AI Engineer Interview Competency Matrix

## Purpose

This matrix maps the twelve-project roadmap to the capabilities commonly assessed in senior AI engineering interviews: fundamentals, Python implementation, retrieval, agents, evaluation, service reliability, observability, security, cloud architecture, and technical leadership.

It is independently authored as an employer-neutral preparation framework. It is not a reconstruction of any company's interview process, and it does not imply that planned projects or skills have been completed.

## Evidence States

| State | Meaning |
|---|---|
| **Planned** | The competency is mapped to future work; no implementation evidence exists. |
| **Implemented** | Relevant code and focused tests exist and have been reviewed. |
| **Validated** | Acceptance checks or reproducible experiments support the claim. |
| **Interview-ready** | The learner can explain, implement, debug, compare alternatives, and cite repository evidence without overstating experience. |

Interview readiness is not awarded by reading a document or importing a framework. It requires explanation, implementation, debugging, trade-off reasoning, and evidence.

## Competency Domains

| Domain | Senior-level capability | Primary projects | Evidence expected |
|---|---|---|---|
| Python engineering | Design typed interfaces, async boundaries, errors, tests, packages, and maintainable modules | 01, 05, 06, 08, 12 | Reviewed code, focused tests, debugging notes, design rationale |
| Context engineering | Allocate limited context deterministically with provenance, trust, and budget controls | 01, 10, 11 | Budget invariants, adversarial tests, safe reports, ADRs |
| Information retrieval | Explain and implement lexical/vector retrieval, reranking, structured content, and relevance evaluation | 02, 03, 04, 09 | Retrieval baselines, Recall@K/MRR/nDCG results, failure analysis |
| Knowledge and multi-hop retrieval | Model relationships and answer questions requiring evidence across sources | 03, 04 | Graph/data design, multi-hop test set, traceable citations |
| Agentic systems | Decide when agents add value; design tools, state, control flow, recovery, and human approval | 04–08, 10 | State diagrams, tool contracts, trajectory tests, recovery evidence |
| Evaluation | Separate retrieval, generation, tool, trajectory, latency, and cost evaluation | 09, plus every project | Versioned datasets, baselines, reproducible commands, limitations |
| API and integration design | Build validated, failure-aware service boundaries only when justified | 06, 10–12 | API contracts, validation tests, timeout/retry behavior, integration evidence |
| Reliability and operations | Handle timeouts, retries, idempotency, checkpointing, monitoring, and degraded behavior | 05, 06, 09–12 | Failure-injection tests, recovery evidence, operational runbooks |
| Security and privacy | Treat inputs/model outputs as untrusted; enforce authorization and data minimization outside models | 01, 06, 07, 10–12 | Threat model, negative tests, permission checks, privacy review |
| Model/platform architecture | Compare managed APIs, self-hosting, routing, caching, deployment, and cost controls | 11, 12 | ADRs, measured trade-offs, capacity/cost model, deployment design |
| Product reasoning | Connect engineering metrics to user needs while avoiding invented business impact | Every project | Problem statement, outcome hypothesis, measurable signals, limitations |
| Leadership communication | Explain ownership, decisions, trade-offs, incidents, and collaboration clearly | Every project, especially 12 | Evidence-backed project narratives, ADR defense, retrospective |

## Project-to-Interview Map

All projects are currently either specified or planned. The rows below describe intended preparation, not completed achievements.

| # | Project | Primary interview competencies | Expected portfolio evidence | Representative discussion prompt |
|---:|---|---|---|---|
| 01 | Context Assembler Engine | Python protocols, typed contracts, deterministic budgeting, validation, stable ordering, safe diagnostics | Requirements traceability, ADRs, unit/invariant tests, budget report, experiment | How would you guarantee that assembled context never exceeds a model budget while preserving high-priority content? |
| 02 | Hybrid Retrieval System | TF-IDF/BM25 foundations, embeddings, vector search, fusion, reranking, retrieval metrics | Lexical baseline, vector comparison, fusion ADR, versioned evaluation set | When can lexical retrieval outperform embeddings, and how would you evaluate a hybrid design? |
| 03 | GraphRAG Pipeline | Graph modeling, entity/relation extraction, multi-hop retrieval, tables/structured data | Graph schema, provenance design, multi-hop fixtures, retrieval/citation evaluation | How would you retrieve evidence that must be joined across documents and tables? |
| 04 | Agentic RAG | Query classification, adaptive retrieval, rewriting, self-correction, stopping rules | Control-flow diagram, deterministic policy tests, trajectory evaluation | When should a query use direct retrieval, multi-step retrieval, or no retrieval? |
| 05 | Durable Agent System | State machines, checkpointing, retries, timeouts, idempotency, recovery | State model, failure-injection tests, restart/replay evidence | How do you recover an interrupted agent without repeating a consequential action? |
| 06 | MCP Tool Server | Async Python, tool schemas, validation, permissions, protocol boundaries | Tool contracts, async tests, timeout/error behavior, authorization checks | How would you expose tools safely to an LLM-driven client? |
| 07 | Agent Memory | Working/episodic/semantic memory, retention, retrieval, privacy, deletion | Memory taxonomy ADR, lifecycle tests, relevance/privacy evaluation | What belongs in agent memory, and how do you prevent stale or sensitive memories from causing harm? |
| 08 | Multi-Agent System | Coordination, reducers/aggregation, task ownership, conflict resolution, HITL | Coordination protocol, state transitions, human-approval tests, failure scenarios | When is a multi-agent design justified over one deterministic workflow? |
| 09 | Agent Evaluation | Retrieval/generation/trajectory metrics, regression sets, experiment tracking, observability | Versioned datasets, baseline reports, trace schema, regression gates | How would you evaluate an agent whose final answer is correct but whose tool trajectory is unsafe? |
| 10 | Security Gateway | Prompt injection, authorization, input/output controls, auditability, least privilege | Threat model, adversarial fixtures, policy tests, safe logs | Why must authorization remain outside the model, even when tool calls look valid? |
| 11 | Model Routing Gateway | Routing, caching, fallbacks, model selection, latency/cost/quality trade-offs | Routing ADR, cache correctness tests, fallback experiments, aggregate telemetry | When should a system route to a smaller model, and how would you prove the policy helps? |
| 12 | Architecture Deep Dive | Service/API design, deployment topology, CI/CD, observability, cloud trade-offs, capacity planning | System diagrams, deployment ADRs, operational plan, benchmark methodology | Compare serverless and orchestrated-container deployment for a latency-sensitive AI service. |

## Retrieval and RAG Preparation Standard

Projects 02–04 and 09 should prepare the learner to:

- explain TF-IDF, BM25, dense embeddings, similarity, fusion, and reranking without hiding behind a framework;
- distinguish indexing, candidate retrieval, ranking, context assembly, generation, and citation verification;
- handle narrative text, tables, metadata, and cross-document relationships deliberately;
- design simple, multi-hop, and adversarial evaluation queries;
- measure retrieval with appropriate metrics such as Precision@K, Recall@K, MRR, or nDCG;
- evaluate generation separately for groundedness, citation support, correctness, and abstention;
- diagnose whether a failure originated in ingestion, retrieval, ranking, context construction, or generation.

Metric selection must match the product question. A metric name without a defined dataset, relevance judgment, aggregation method, and baseline is not evidence.

## Agentic-System Preparation Standard

Projects 04–10 should prepare the learner to:

- identify when a deterministic workflow is preferable to an agent;
- explain tool contracts, state, routing, termination, retries, timeouts, and human approval;
- separate model proposals from authorization and consequential execution;
- reason about checkpointing, replay, idempotency, and partial failure;
- evaluate task success, tool choice, argument validity, recovery, safety, latency, token use, and cost;
- analyze an execution trajectory rather than judging only the final answer.

Specific orchestration frameworks may be studied after these concepts are understood. Framework vocabulary is not a substitute for explaining the underlying state transitions.

## Coding and Implementation Preparation

Across the roadmap, practice small exercises that can be explained line by line:

- typed value objects and validation;
- iterator and collection behavior;
- exception design and chaining;
- stable sorting and deterministic serialization;
- async functions, task cancellation, concurrency limits, and timeouts;
- bounded retries with backoff and non-retryable failures;
- dependency injection and test doubles;
- API request/response contracts where a service boundary is justified;
- structured logs that contain operational metadata but not secrets or raw private content.

Interview coding practice should begin with standard Python and focused tests. A framework should be introduced only when the exercise is genuinely about framework behavior.

## System-Design Preparation

For each applicable project, practice drawing and explaining:

1. Inputs, outputs, actors, and user goal
2. Data ingestion and storage boundaries
3. Online request path and offline processing path
4. Model, retrieval, tool, and policy boundaries
5. Trust, authorization, and privacy boundaries
6. Latency, throughput, context, token, and cost budgets
7. Retry, timeout, fallback, and recovery behavior
8. Evaluation datasets and release gates
9. Logs, metrics, traces, alerts, and incident diagnosis
10. Deployment alternatives and capacity assumptions

Do not begin with a cloud product name. Establish requirements first, then compare managed services, self-hosting, serverless functions, and container orchestration against those requirements.

## Leadership and Managerial Preparation

Every completed project should support an evidence-backed narrative covering:

- the problem and why it mattered;
- your individual decisions and contributions;
- alternatives considered and stakeholders involved;
- a difficult failure, disagreement, or uncertainty;
- the evidence used to choose or revise the design;
- security, cost, reliability, and operational consequences;
- what you would change with more time or different constraints.

Use a concise situation–task–action–result structure, but never invent business results, production traffic, team ownership, or incidents. Repository projects are portfolio evidence, not substitutes for professional experience.

## Interview-Readiness Rubric

Score each competency from 0 to 4 using observable evidence:

| Score | Observable capability |
|---:|---|
| 0 | No current explanation or evidence |
| 1 | Can define terminology with significant prompting |
| 2 | Can explain and implement a small example with focused tests |
| 3 | Can debug failures, compare alternatives, and cite validated project evidence |
| 4 | Can lead a system-design discussion, challenge assumptions, quantify trade-offs, and communicate limitations clearly |

A score of 3 is a practical readiness target for a project's primary competencies. Score 4 should be reserved for demonstrated depth, not assigned because a document exists.

## Preparation Workflow Per Project

1. Learn the foundations without relying on a framework.
2. Define the user problem, requirements, and measurable signals.
3. Compare architecture alternatives and record consequential decisions.
4. Implement one bounded behavior with focused tests.
5. Add failure, security, and operational scenarios.
6. Establish a baseline before optimization.
7. Run reproducible evaluation and record limitations.
8. Create original conceptual, coding, debugging, production, and system-design questions from the evidence.
9. Practice a five-minute architecture explanation and a two-minute project narrative.
10. Update competency scores only when observable evidence improves.

## Current Gap Assessment

As of the repository's current state:

- Project 01 is specified and in architecture planning; its implementation evidence does not yet exist.
- Projects 02–12 remain planned placeholders.
- No project should currently be presented as implemented, validated, deployed, or production-proven.
- The immediate preparation priority remains disciplined execution of Project 01, not simultaneous framework study across all twelve projects.

This matrix should be revisited after each project milestone. Updates must link readiness claims to code, tests, ADRs, experiments, or reviewed documentation.
