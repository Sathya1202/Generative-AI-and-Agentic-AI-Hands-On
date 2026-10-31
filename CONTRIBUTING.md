# Contributing and extending the learning notes

- Preserve upstream attribution and license notices when modifying course-derived material.
- Keep secrets in local `.env`; never add real credentials to notebooks, source files, screenshots or commits.
- Add a Markdown explanation before substantial code changes: intent, inputs, outputs and design trade-offs.
- Prefer small, runnable notebook cells and include validation/edge-case checks.
- Clear outputs before committing if they may contain personal data, API responses or secrets.
- Record dependency changes in `pyproject.toml` and regenerate `uv.lock` with `uv lock`.
