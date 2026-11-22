# Repository Learning Principles

These principles apply to learning plans for all twelve engineering projects. They are independently worded for this repository and should be adapted to each project's documented scope rather than copied into artificial exercises.

## 1. Build From Fundamentals

Study the underlying algorithm, data representation, and failure modes before using a framework abstraction. Every learning plan should identify the prerequisite Python, mathematics, information-retrieval, machine-learning, or distributed-systems concepts that make the project understandable.

Expected evidence may include a small implementation, a worked example, a comparison with a baseline, or an explanation produced without relying on a library's terminology.

## 2. Design the System Before Selecting a Model

Treat models as components within a larger system. Start with inputs, outputs, trust boundaries, data flow, budgets, failure handling, observability, and operational constraints. Choose a model or managed service only after identifying the requirement it satisfies.

Learning plans should include architecture alternatives and explicit trade-offs among quality, latency, cost, privacy, reliability, maintainability, and delivery speed.

## 3. Progress From Local Correctness to Operations

Begin with deterministic, offline behavior and focused tests. Add packaging, interfaces, integration checks, deployment, CI/CD, monitoring, drift detection, or cloud services only when the project's scope requires them.

Production tooling is learned through justified increments, not as decoration. A project should not add an API server, container, cloud platform, vector database, agent framework, or paid service merely to appear production-oriented.

## 4. Connect Engineering Work to User and Business Outcomes

For each major decision, explain the user problem, affected stakeholder, expected outcome, measurable signal, and engineering cost. Distinguish a technical metric from a business result; do not invent causal impact.

Learning plans should practice communicating architecture and trade-offs in plain language for product, security, infrastructure, and leadership audiences.

## 5. Prefer Deliberate Depth Over Trend Chasing

Follow a coherent progression: concepts, primary or authoritative references, small experiments, implementation, testing, operational analysis, and reflection. Use certifications, courses, documentation, and coding assistants as learning tools—not substitutes for reasoning or evidence.

Explore alternatives and form independent conclusions. Do not reproduce tutorial projects, interview banks, or educational content without original analysis and appropriate attribution.

## 6. Work at a Sustainable Pace

Use bounded tasks, focused sessions, explicit stopping points, and regular review. Record uncertainty and failures without treating them as personal shortcomings. Avoid compressing complex engineering work into artificial deadlines driven by social-media demonstrations.

A learning plan should make progress observable while leaving room for rest, revision, and deeper investigation.

## Required Dimensions in Every Project Learning Plan

Each project learning plan must address these dimensions at the level appropriate to its scope:

| Dimension | Required question |
|---|---|
| Foundations | What must be understood without depending on a framework? |
| System design | Where are the components, boundaries, budgets, and failure paths? |
| Implementation | What is the smallest behavior that can be built and reviewed? |
| Testing and evaluation | What evidence distinguishes correctness, quality, and limitations? |
| Production engineering | Which operational capabilities are justified now, later, or out of scope? |
| Product reasoning | Which user or business problem does the work address, and how would impact be measured? |
| Communication | How will the design and trade-offs be explained to technical and non-technical stakeholders? |
| Independent learning | Which alternatives, experiments, and authoritative sources support original conclusions? |
| Sustainable practice | How is work divided into focused tasks with approval and stopping points? |
| Interview preparation | Which questions can be derived honestly from implemented and reviewed evidence? |

## Evidence and Originality Rules

- Separate planned learning, completed exercises, observed results, and interpretation.
- Record commands and outcomes actually observed; never fabricate benchmarks or business impact.
- Use synthetic, public-domain, or appropriately licensed data and examples.
- Cite sources used to verify facts while writing explanations and exercises independently.
- Keep third-party PDFs, proprietary material, and commercial manuscripts outside the public repository.
- Label hypothetical production scenarios and never present them as professional experience.
- Use coding assistants to explain, challenge, test, and review work; do not accept generated code without understanding its meaningful lines.

## Project-Level Adaptation

Not every project should use every technology. For example, Project 01 focuses on Python contracts, deterministic budgeting, validation, selection, and safe reporting; deployment platforms and LLM APIs remain unnecessary. Later projects may justify retrieval systems, agent orchestration, containers, CI/CD, monitoring, or cloud services through their own requirements and ADRs.

When a new project learning plan is created, start with the [project learning plan template](templates/project-learning-plan.md), replace its guidance with project-specific content, and link every learning outcome to planned tasks and evidence.
