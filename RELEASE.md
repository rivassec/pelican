Release type: patch

Enable the `S` (flake8-bandit) Ruff rule set, addressing the `# TODO: "S"`
note in `pyproject.toml`. Adds a `pelican/tests/*` ignore for rules that
are universally appropriate to suppress in tests (asserts, hardcoded test
values, subprocess fixtures, loopback bindings) and adds inline `# noqa`
suppressions, each with a justification comment, on the existing library
findings.

No behavior changes; this commit only enables the lint and documents why
each existing finding is acceptable. Two `S101` and one `S504`
suppressions in `pelican/tools/pelican_import.py` and `pelican/server.py`
flag latent issues that warrant follow-up (asserts used as control flow
or invariant checks are stripped under `python -O`; `ssl.wrap_socket` is
deprecated since Python 3.12) and are intentionally deferred to keep
this commit purely lint-enabling.
