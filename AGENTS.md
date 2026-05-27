# Repository Guidelines

## Project Structure & Module Organization

The Python package lives in `confluence_markdown_exporter/`. `main.py` defines the Typer CLI, `confluence.py` holds core export behavior, `api_clients.py` contains Atlassian integrations, and shared helpers are in `utils/`. Tests are split between `tests/unit/` and `tests/integration/`, with fixtures in `tests/conftest.py`. Documentation is a Docusaurus site: Markdown in `docs/`, React/CSS in `src/`, assets in `static/`, and config in `docusaurus.config.ts` and `sidebars.ts`.

## Build, Test, and Development Commands

- `uv sync --all-groups`: create/update the local virtual environment with runtime and dev dependencies.
- `uv run cme --help` or `uv run confluence-markdown-exporter --help`: verify and run the CLI.
- `uv run pytest`: run the full Python test suite.
- `uv run ruff check`: run linting with the repository Ruff configuration.
- `uv build --no-sources`: test the publishable Python package build.
- `npm ci`: install documentation site dependencies from `package-lock.json`.
- `npm start`: run the Docusaurus docs site locally.
- `npm run build:versioned`: build docs with versions generated from git tags.

## Coding Style & Naming Conventions

Python targets 3.10+, uses 4-space indentation, double quotes, LF line endings, and a 100-character line limit. Ruff enforces linting, import ordering, Google-style docstrings, and type annotations for new code. Keep imports one per line as configured. Use `snake_case` for modules, functions, variables, and tests; use `PascalCase` for classes. Keep CLI option names clear and stable.

## Testing Guidelines

Use `pytest`. Name files `test_*.py` and functions `test_*`. Put isolated logic tests in `tests/unit/`; reserve `tests/integration/` for CLI or cross-module behavior. Add regression tests for bug fixes and new converters, config paths, or API-client behavior. Before opening a PR, run `uv run ruff check`, `uv run pytest`, and `uv build --no-sources`.

## Commit & Pull Request Guidelines

History uses short imperative summaries, with optional conventional prefixes for scoped work, for example `docs: square favicon and navbar logo`, `build(deps): bump the actions group`, or `Add per-instance certificate support for Atlassian clients`. Keep commits focused.

Pull requests should follow `.github/PULL_REQUEST_TEMPLATE.md`: include a descriptive title, summary, related issues when applicable, and a test plan. Update documentation for user-facing CLI, configuration, Docker, or compatibility changes. Add screenshots for docs-site UI changes.

## Security & Configuration Tips

Do not commit Confluence credentials, API tokens, generated exports with private content, or local `.env` files. Treat `confluence-lock.json` and exported content as environment-specific unless intentionally used as fixtures. Prefer documented paths in `docs/configuration/` when changing authentication, target systems, or CI behavior.
