# Security Policy

CLIF is a data format.

## Scope

- Ambiguities in the specification that could cause parser differentials or
  injection (e.g. strings containing markup).
- The reference validator and benchmark scripts in the
  [clif-test](https://github.com/clif-format/clif-test) project.

## Out of scope

- Runtime localization engines that consume CLIF data.
- ICU MessageFormat evaluation. ICU syntax is untrusted payload; consumers
  must evaluate it only through a hardened ICU implementation with resource
  limits.

## Handling requirements

Implementations of CLIF MUST:

- treat documents as untrusted data;
- enforce limits on file size, line length, string length, and dotted group
  path depth;
- escape `<`, `>`, `&`, and quotes before rendering strings in HTML/XML UI.