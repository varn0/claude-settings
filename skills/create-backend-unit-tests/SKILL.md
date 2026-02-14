---
name: create-backend-unit-tests
description: Create unit tests for a backend module. Detects the test framework and conventions from the project.
user-invocable: true
argument-hint: [module name or path]
---

Create a complete test suite for the backend module: $ARGUMENTS

## Project Discovery

Before writing tests, detect the project's testing setup:

1. **Identify the test framework** by checking for:
   - `pytest` / `pytest.ini` / `pyproject.toml [tool.pytest]` / `setup.cfg [tool:pytest]` -> pytest
   - `unittest` usage in existing tests -> unittest
   - `nose2` / `nosetest` configuration -> nose
   - Other framework indicators in config files

2. **Identify the test runner command** by checking:
   - `Makefile` targets (e.g., `make test`)
   - `pyproject.toml` scripts
   - `package.json` scripts (for non-Python projects)
   - Common patterns: `pytest`, `python -m pytest`, `poetry run pytest`, `npm test`

3. **Identify the test directory** — look for `tests/`, `test/`, or tests co-located with source files.

4. **Read existing tests** to understand project conventions for:
   - Test file naming (e.g., `test_*.py`, `*_test.py`)
   - Test data factories or fixtures
   - Mocking patterns
   - Assertion style (`assert` vs `self.assertEqual`)

## Conventions

- **Directory mirrors source:** place tests following the project's existing structure.
- **Filesystem isolation:** mock filesystem access and use `tempfile` for any tests touching the filesystem. Clean up after tests.
- **No external services in unit tests.** Mark tests that require running services with `@pytest.mark.integration` or equivalent.
- **Test naming:** `test_<criterion>_<expected_result>` (e.g., `test_empty_input_returns_empty_list`).
- Match the surrounding test style — don't introduce new conventions.

## Steps

1. **Identify the module under test** — locate the source file(s) matching `$ARGUMENTS`.

2. **Read the source** to understand public functions, classes, and edge cases.

3. **Read existing tests** to match the project's style and avoid duplication.

4. **Write tests** covering:
   - Happy-path behavior
   - Edge cases and boundary conditions
   - Error / exception paths
   - Any state machine transitions (must respect valid transitions only)

5. **Run the tests** to verify they pass using the detected test runner command.

6. **Report results** — show the test count and any failures.
