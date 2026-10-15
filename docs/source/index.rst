generated-code-harness
======================

.. include:: ../../README.rst
   :start-after: ======================

API
---

.. automodule:: generated_code_harness
   :members:

Project boundary
----------------

This project was extracted from `Literalizer <https://github.com/adamtheturtle/literalizer>`_.
It handles project files, ordered commands and failure diagnostics.
Rendering, compiler adapters, language versions, snapshots, fixture ownership and semantic assertions remain with callers.

``pytest-regressions`` supplies snapshot comparisons without another snapshot format or plugin here.
LLVM lit/FileCheck provides command-driven test files and pattern matching; this package instead composes directly with Python-generated projects and pytest assertions.
Trybuild remains useful for Rust/Cargo UI tests, while Doccmd runs tools over documentation code blocks.

The tests include an independent schema-to-dataclass generator, separate compile-only checks, a copied-module example without installed dependencies, and caller-defined output comparisons that distinguish booleans, integers and negative zero.
Literalizer uses the package for round-trip programs and batched TypeScript consumer probes.

Development
-----------

.. include:: ../../CONTRIBUTING.rst
   :start-after: ============
