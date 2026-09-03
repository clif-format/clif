<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="logos/clif-wordmark-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="logos/clif-wordmark-light.svg">
    <img alt="CLIF: The Contextual Localization Integrated Format"
         src="logos/clif-wordmark-light.svg"
         width="50%">
  </picture>

  <p align="center">The Contextual Localization Integrated Format.</p>

  <p align="center">
    <a href="spec/clif-1.0.0.md">Specification</a> •
    <a href="docs/">Documentation</a> •
    <a href="CONTRIBUTING.md">Contributing</a>
  </p>
</div>


## Overview

CLIF is a Contextual Localization Integrated Format, a line-oriented, context-first working file for the whole localization lifecycle. It is designed for both human translators and LLM workflows, solving the usual trade-off between machine-friendly syntax and complete context. CLIF avoids multi-line closing tags and keeps token cost low, while carrying context from family to group to entry and standardizing tags, widths, and ICU support.

All text in this specification is normative unless otherwise labeled.

## Example

Here is a minimal CLIF file:

```clif
CLIF 1.0
namespace: demo
clan: settings
source-language: en-US
target-language: zh-CN

[video]
type: label

<resolution>
source: "Resolution"
target: "分辨率"
type: noun
status: final
```

The four header fields `namespace`, `clan`, `source-language`, and `target-language` are required. Each entry has a stable ID, `source`, `type`, and `status`; group metadata is inherited by entries. See the [specification](spec/clif-1.0.0.md) for the complete syntax.

## Why CLIF?

CLIF is built for the whole translation lifecycle and for LLM-driven translation workflows. It addresses common pain points of traditional localization formats:

- **AI-safe syntax**: No multi-line open/close pairs; every construct is a line, so a model or human can add, move, or delete lines without breaking the document.
- **Context-first**: One file is one clan with family-level `info`/`standard`/`dependency`, inherited group context, and per-entry context; translators never work in the dark.
- **Enforced attributes**: Closed, validator-enforced vocabularies for `type`, `emotion`, and `status` turn vague inputs into typed data; `type` and `status` are required on every entry, and `emotion` defaults from `type`.
- **Low token cost**: Short lowercase keys, minimal structural punctuation, no repeated open/close tags, and no per-entry braces make CLIF cheaper to send to LLMs.
- **Full ICU support**: Unicode MessageFormat MF1 and MF2 are preserved verbatim inside strings; the dialect is auto-detected.
- **Human- and machine-friendly**: Markdown-like readability, tolerant `:` / `=` assignment, single-pass parser, and normative ABNF grammar.

See the [comparison](docs/comparison.md) and [design rationale](docs/design-rationale.md) for full details.

## Measured evidence

CLIF claims are not editorial: the separate [clif-test](../clif-test)
project measures the format against XLIFF, PO, Fluent, JSON, YAML, CSV, Android
and iOS on the same corpus, the same model and the same context payload
(960 real translation calls, 16 documents, 392 entries, public raw evidence and
computed review data):

- **Token cost** — with the same context payload carried, CLIF is 11%–196%
  cheaper than every other format (XLIFF +123%, CSV +196%).
- **Context fidelity** — 100% round-trip retention vs 97.6% (PO loses header
  title/info/standard) and 67.3% (plain JSON).
- **Quality** — with the same context payload, translation quality is identical (the
  format does not change the model); CLIF advantage is that the context payload is
  structurally guaranteed and survives editing.

Summary: [BENCHMARK.md](../clif-test/BENCHMARK.md) • public data bundle:
[benchmark/clarion-2026-09-02](../clif-test/benchmark/clarion-2026-09-02) •
reference implementation: [clif-python](../clif-python).

## Contributing

CLIF follows a specification-first workflow. Contributions are welcome in the normative specification, ABNF grammar, reference validator, conformance fixtures, and documentation.

- Open an issue or pull request with the proposed change.
- Add conformance fixtures before changing the validator or grammar.
- Keep the ABNF grammar and specification in sync.
- Use the `x-` prefix for provisional extension fields until they become standard.

See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

## License

CLIF is released under the MIT License, in the same spirit as TOML, YAML, and XLIFF. The format may be freely implemented. See [LICENSE](LICENSE) for the full license text.

The CLIF logo is Copyright © 2026 CLIF contributors and is also licensed under the MIT License. See [logos/README.md](logos/README.md).

## Wiki / Documentation

This README is only a starting point. The normative details and extended design material live in the repository:

- [Specification](spec/clif-1.0.0.md) — the complete normative definition of CLIF 1.0.
- [ABNF grammar](spec/abnf/clif-1.0.abnf) — the machine-readable normative grammar.
- [Design rationale](docs/design-rationale.md) — why the syntax is designed this way.
- [AI safety](docs/ai-safety.md) — how CLIF stays safe under LLM editing.
- [Prompt assembly](docs/prompt-assembly.md) — recommended prompting pattern for translation models.
- [Comparison](docs/comparison.md) — detailed comparison with other localization formats.
- [Implementations](docs/implementations.md) — implementation registry and conformance levels.
- [Standards library](references/standards-library.md) — external standards that CLIF reuses.
