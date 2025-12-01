# Agent Workflow

Guidelines:
- Do **not** add `from __future__ import annotations` to agent code.
- This is a uv-managed project; prefix CLI commands with `uv run` when executing tools locally, and add dependencies with `uv add`.
- If you need external library docs (e.g., pydantic ai), use the Context7 MCP docs tool to search before coding.
- Coding style: do not code defensively—this is a research project, and certain failures (imports, dependency versions, etc.) are expected.
- Place imports at the top of the file unless there is an absolute need to defer them.
- Testing: write end-to-end tests only; do not use mocking.
- Avoid casting unless it is absolutely necessary.
- Always run `python` via `uv run python`; do not invoke `python` directly.
- Keep shared constants in `config.py`.
- Prefer `Path` objects and `/` composition over `os.path.join`.
- Inject default values at interfaces (e.g., CLI options), not deep in the call stack.
- Avoid optional parameters in functions that are not interfaces when possible.
- Use click decorators to set defaults and validate inputs (e.g., ensure paths exist, numeric values > 0) before entering the main function logic.
- When invoking OpenAI, use Context7 docs to confirm the Responses API details and reference the correct endpoint.
- For structured outputs with OpenAI, check Context7 docs to understand how the `.parse` endpoint works before coding.

Run these commands to validate changes. Do not ask permission to run these commands. Chain them to save time. 

```bash
UV_NO_SYNC=1 uv run mypy src ; UV_NO_SYNC=1 uv run basedpyright src ; UV_NO_SYNC=1 uv run ruff format src ; UV_NO_SYNC=1 uv run ruff check --fix src
```
Ensure your `MODEL` and prompt files are set before running the agent CLIs.
