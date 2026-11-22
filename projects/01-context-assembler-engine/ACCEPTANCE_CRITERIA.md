# Context Assembler Engine Acceptance Criteria

Project 01 reaches **Implemented** only when AC-001 through AC-010 pass. It reaches **Validated** only when AC-011 also passes with committed evidence.

| ID | Requirements | Acceptance criterion | Evidence expected |
|---|---|---|---|
| AC-001 | FR-001, FR-002 | Valid typed items are accepted; duplicate IDs, invalid metadata, empty required values, and unsupported types produce specific errors. | Unit tests |
| AC-002 | FR-003, QR-003 | A deterministic fake counter can replace the default counter without modifying assembly policy. | Interface and unit test |
| AC-003 | FR-004 | Usable budget equals total limit minus fixed overhead and reserved output; zero or negative usable budgets are rejected. | Boundary tests |
| AC-004 | FR-005, FR-006 | Repeated runs with identical inputs return byte-for-byte equivalent serialized results, including stable tie ordering. | Determinism test |
| AC-005 | FR-007, FR-008, QR-002 | Mixed truncatable and atomic items never exceed the usable budget; every omitted or shortened item has an explicit reason. | Boundary and invariant tests |
| AC-006 | FR-009 | Untrusted content remains labeled and distinctly delimited, and tests demonstrate that its text cannot alter the assembler's selection policy. | Adversarial synthetic tests |
| AC-007 | FR-010, QR-005 | The report includes counts, IDs, provenance, transformations, and decisions while logs exclude raw content by default. | Schema and log-capture tests |
| AC-008 | FR-011, QR-001 | The complete default test suite passes with network access unavailable and no credentials configured. | Test command output |
| AC-009 | QR-004 | Public interfaces pass the selected static type check and run on the documented minimum Python version. | CI or local validation output |
| AC-010 | QR-007 | Repository scan and fixture review find no secrets, personal data, commercial manuscripts, or unlicensed third-party text. | Review checklist and secret scan |
| AC-011 | QR-006 | At least one committed experiment report contains a predeclared hypothesis, reproducible command, environment, synthetic dataset description, raw results, and limitations. | Experiment report and artifacts |

## Proposed Validation Commands

Exact tooling will be selected during implementation and documented in project configuration. The intended check categories are:

```text
unit and boundary tests
static type checking
lint/format checking
documentation link checking
secret scanning
```

These are categories, not claims that tools or tests already exist.
