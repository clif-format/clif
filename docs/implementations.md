# CLIF Implementations

This page registers CLIF 1.0 implementations and their conformance level, in
the style of the TOML and YAML implementation lists. To list a project, open
a PR adding it here with a link and the conformance row it passed.

## Conformance levels

| Level | Requirement |
| --- | --- |
| **Validator** | Parses the ABNF grammar and enforces every semantic constraint of the specification; reports line-numbered, categorized errors. |
| **Parser** | Tolerant parser: accepts valid documents and ignores unknown `x-` fields with warnings. |
| **Serializer** | Produces canonical CLIF 1.0 (§17 Serialization), including the file name convention. |
| **Converter** | Bidirectional mapping to another format (XLIFF, PO, Fluent, JSON, CSV), documented lossy conversions. |

## Reference implementation

| Project | Language | Level | Notes |
| --- | --- | --- | --- |
| [clif-python](../../clif-python) (`pyclif`) | Python 3.11+ | Validator, Parser, Serializer, Converter | MIT, zero runtime dependencies, 3 319 LOC; bidirectional converters for XLIFF, PO, Fluent, JSON, YAML, CSV, Android, iOS |
| [clif-test/tools/clif_validator.py](../../clif-test/tools/clif_validator.py) | Python 3.11+ | Validator, Serializer (test helpers) | Reference validator used by the conformance fixtures |

## Test and benchmark tooling

| Project | Location |
| --- | --- |
| Conformance fixtures (valid/invalid) | [clif-test/tests/fixtures](../../clif-test/tests/fixtures) |
| Token benchmark | [clif-test/tools/token_benchmark.py](../../clif-test/tools/token_benchmark.py) |
| Edit robustness protocol | [clif-test/tests/edit-robustness](../../clif-test/tests/edit-robustness) |
| Translation quality corpus | [clif-test/tests/quality](../../clif-test/tests/quality) |
| **CLARION benchmark** (format-vs-format) | [clif-test/BENCHMARK.md](../../clif-test/BENCHMARK.md) — summary with graphs of the measured evidence + public data bundle |
| Benchmark data bundle (raw + computed) | [clif-test/benchmark/clarion-2026-09-02](../../clif-test/benchmark/clarion-2026-09-02) |
| Benchmark tooling | [clif-test/tools/audit_report.mjs](../../clif-test/tools/audit_report.mjs) (audit + unified metrics), [clif-test/tools/qe_score.py](../../clif-test/tools/qe_score.py) (reference-free QE), [clif-test/tools/package_benchmark.py](../../clif-test/tools/package_benchmark.py) (public bundle) |

## Third-party implementations

None registered yet. Please submit a PR with a fixture-suite result.