Contributing
============

Use the pinned uv version from ``pyproject.toml`` and Python 3.14 for development.

.. code-block:: console

    uv sync --group dev
    uv run prek install
    uv run pytest --cov --cov-report=term-missing
    uv run prek run --all-files --group fast
    uv run prek run --all-files --group typecheck
    uv run prek run --all-files --group pylint
    uv run prek run --all-files --group docs

Source and tests require complete statement and branch coverage.
Public APIs require complete type information, checked by Mypy, Pyright, Pyrefly, and ty.
Ruff, Pylint, documentation checks, dependency checks, and package metadata checks run through prek.
CI tests Python 3.12 through 3.15 on Linux and Windows.
Exercise behavior through the public API with real compiler or interpreter processes.

Add user-facing changes to ``newsfragments/<issue>.change.md``.
To release, assemble Towncrier notes, validate the exact commit, tag it with a calendar version, and publish a GitHub release.
The release workflow tests, builds, checks, and publishes the wheel and source distribution using PyPI trusted publishing.
