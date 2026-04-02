## Plan: Add backend FastAPI tests in a separate tests directory

TL;DR: create a `tests/` folder, add pytest-based FastAPI tests for `src/app.py`, and configure pytest so tests import the backend app from `src`.

**Steps**
1. Create a new directory `tests/` at the repository root.
2. Update `pytest.ini` to load `src` on the test import path and optionally set `testpaths = tests`.
3. Create `tests/test_app.py` with FastAPI backend tests using `fastapi.testclient.TestClient`, structured with Arrange-Act-Assert (AAA).
   - import `app` from the `src` code base via the configured python path
   - test `GET /activities`
   - test `POST /activities/{activity_name}/signup` success and duplicate signup behavior
   - test `POST /activities/{activity_name}/signup` on missing activity returns 404
   - test `DELETE /activities/{activity_name}/participants?email=...` success and missing participant returns 404
4. Update `requirements.txt` to include `pytest` so tests are easy to install and run.

**Relevant files**
- `/workspaces/github-course/pytest.ini` — configure pytest import path
- `/workspaces/github-course/requirements.txt` — add `pytest`
- `/workspaces/github-course/tests/test_app.py` — new test file

**Verification**
1. Run `pytest` from the repository root.
2. Confirm tests pass and backend routes behave as expected.
3. Confirm there are no import errors for `app` from the `src` directory.

**Decisions**
- Use `fastapi.testclient.TestClient` for backend tests.
- Keep tests in a separate `tests/` directory as requested.
- Configure `pytest` to use `src` as the import path instead of changing application structure.
