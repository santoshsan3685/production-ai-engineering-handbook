# Project Naming Convention

## Repository Directories

Use `NN-short-descriptive-name`, where `NN` is a zero-padded roadmap number and the remainder is lowercase kebab-case.

Example: `projects/01-context-assembler-engine/`

Do not renumber a published project. If the roadmap changes, preserve its identifier and explain the change in the status tracker.

## Python Names

Use lowercase snake_case for importable packages and modules. The corresponding package for Project 01 will be `context_assembler_engine`. Do not include the numeric prefix in an import name.

Use:

- `PascalCase` for classes and exceptions
- `snake_case` for functions, variables, modules, and test names
- `UPPER_SNAKE_CASE` for true constants
- `test_<behavior>_<condition>` for test functions

## Documents and Records

- Project-level standard documents use uppercase names such as `README.md`, `REQUIREMENTS.md`, and `ACCEPTANCE_CRITERIA.md`.
- ADRs use `NNNN-short-decision-title.md`, beginning with `0001` within the repository.
- Experiments use `YYYY-MM-DD-short-experiment-name.md` so chronological order is explicit.
- Interview questions use `project-NN-topic-slug.md` when stored as individual files.
- Handbook chapters use `NN-topic-slug.md` once their order is stable.
