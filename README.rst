generated-code-harness
======================

This repository is archived after evaluating a standalone generated-code runner for Literalizer.
The shared runner is being retained inside Literalizer; a separate package did not provide enough benefit to justify its maintenance.
See `Literalizer PR #5693 <https://github.com/adamtheturtle/literalizer/pull/5693>`_ for the local implementation and decision record.
No PyPI release is planned.

The code and examples below remain available under the MIT license for reference.
The runner requires Python 3.12 or newer and has no runtime dependencies.
It provides temporary projects, ordered commands, captured output, and failure diagnostics that identify each source file.

Usage
-----

.. code-block:: python

    """Compile and consume a generator's Python output."""

    import sys

    from generated_code_harness import Step, run_project

    results = run_project(
        label="generated settings",
        files={
            "settings.py": "answer = 42\n",
            "consumer.py": "from settings import answer; print(answer)\n",
        },
        steps=[
            Step(
                args=[sys.executable, "-m", "py_compile", "settings.py"],
                failure_label="compile",
            ),
            Step(
                args=[sys.executable, "consumer.py"],
                failure_label="consume",
            ),
        ],
    )
    assert results[-1].stdout == "42\n"

Supply any compiler executable and version flags through ``Step.args``.
Commands run without a shell in a fresh temporary directory.
A nonzero exit raises ``AssertionError`` containing the fixture label, command, output and project files.
The directory is removed on success and failure.

The caller chooses assertions and execution policy.
Use pytest-regressions for source snapshots independently of compilation, pass only compiler commands for compile-only checks, or inspect returned outputs using your own semantic equality rules.
Keep related modules in one project and compiler step when batching is supported.
Toolchain installation, timeouts and process-tree supervision remain with callers; wrap commands or supervise the complete invocation when those are required.

See the `documentation <https://adamtheturtle.github.io/generated-code-harness/>`_ for the API and project boundary.
