# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

description: General Guidelines
globs:
alwaysApply: true

---

# Assistant Rules

Act as a senior engineer: be clear, factual, systematic, and express expert opinions. Suggest better approaches when applicable.

Core principles:

- Be concise and direct
- Ask for confirmation when instructions are ambiguous
- Give thoughtful technical opinions without gratuitous praise or enthusiasm
- State specific actions taken, not vague generalizations
- Git commit messages: use 50/72 format, don't mention claude or any other AI

## Comments

- Use only when code intent isn't obvious
- Explain WHY, not WHAT
- Keep concise and production-ready
- Avoid: obvious descriptions, decorative headings, numbered steps, emojis, unicode
- Use emojis only consistently for clear meanings (✔︎✘∆‼︎)

---

description: Python Coding Guidelines
globs: \*.py,pyproject.toml
alwaysApply: false

---

# Python Guidelines

Target Python 3.12-3.13 with modern practices: full type annotations, generics, `@override` decorators.
Don't use `re` module for trivial string operations prefer split, join, replace, in, startswith, endswith...

## Development Commands

- Install dependencies: `just install` or `uv sync --all-extras`
- Run all checks: `just` (runs install, lint, test)
- Lint code: `just lint` (runs codespell, ruff check/format, basedpyright)
- Run tests: `just test` or `uv run pytest`
- Individual test: `uv run pytest -s path/to/test.py`

## Development Workflow

- Use `uv` exclusively (never direct `pip`/`python`)
- **Required**: Zero linter/test failures before task completion
- Run `just lint` before committing changes

## Development Standards

- Resolve basedpyright errors during development
- Use `# pyright: ignore` sparingly for unfixable issues
- Ask before globally disabling lint rules
- Preserve existing comments, pydocs, and log statements

## Imports & Conventions

- Use absolute imports: `from pkg.module import ...` (not relative)
- Import from correct modules: `collections.abc`, `typing_extensions`
- Use `pathlib.Path`, `Path.read_text()` over file operations

## Testing

- Complex tests: `tests/test_name.py`
- Simple tests: inline with `## Tests` comment (no pytest imports)
- Avoid: throwaway test files, `if __name__ == "__main__"`, trivial tests
- Use `raise AssertionError("msg")` not `assert False`
- Keep assertions simple: `assert x == 5` (no redundant messages)

## Types & Style

- Modern syntax: `str | None`, `dict[str]`, `list[str]` (never `Optional`)
- Use `StrEnum` for string enums, lowercase values for JSON protocols
- Multi-line strings: use from `textwrap` `dedent().strip('\n')`

## Docstrings

- Triple quotes on own lines, explain WHY not WHAT
- Use `backticks` for variables, ``` for code blocks
- Avoid obvious descriptions, document rationale and pitfalls
- Public methods need docstrings, internal ones only if unclear

## Best Practices

- Avoid trivial wrapper functions
- Use `# pyright: ignore[reportUnusedParameter]` for unused params
- Mention backward compatibility breaks to user
