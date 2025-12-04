# Agent Workflow

Guidelines:
- Do **not** add `from __future__ import annotations` to agent code.
- This is a uv-managed project; prefix CLI commands with `uv run` when executing tools locally, and add dependencies with `uv add`.
- If you need external library docs (e.g., pydantic ai), use the Context7 MCP docs tool to search before coding.
- Coding style: do not code defensively—this is a research project, and certain failures (imports, dependency versions, etc.) are expected.
- Place imports at the top of the file unless there is an absolute need to defer them.
- Testing: write end-to-end tests only; do not use mocking.
- Avoid casting unless it is absolutely necessary; instead of casts, `Any`, or `type: ignore`, prefer adding proper stubs or entries in a `typings/` folder (or install stub packages) so the types stay precise.
- Always run `python` via `uv run python`; do not invoke `python` directly.
- Keep shared constants in `src/consts.py`.
- Keep functions isolated to their general purpose, without unrelated topics or dependencies.
- Long functions are fine when the logic is not reused in more than two other places; prefer inlining that code when it lacks wider reuse.
- Avoid 2–3 line helper functions—inline that logic unless it belongs in `config.py` (or similar configuration modules).
- Minimize comments; only add them for complicated or non-obvious logic.
- Prefer `Path` objects and `/` composition over `os.path.join`.
- Inject default values at interfaces (e.g., CLI options), not deep in the call stack.
- Avoid optional parameters in functions that are not interfaces when possible.
- Use click decorators to set defaults and validate inputs (e.g., ensure paths exist, numeric values > 0) before entering the main function logic.
- When invoking OpenAI, use Context7 docs to confirm the Responses API details and reference the correct endpoint.
- For structured outputs with OpenAI, check Context7 docs to understand how the `.parse` endpoint works before coding.

Run `prek run --all-files` to validate linting, typing, and formatting after any changes.
