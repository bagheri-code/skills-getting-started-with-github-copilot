## Plan: Add backend FastAPI tests

Create a dedicated `tests/` directory for FastAPI backend tests and verify the activity signup and removal flows.

**Steps**
1. Add a new `tests/` directory at the repository root.
2. Create `tests/test_app.py` with FastAPI `TestClient` tests.
3. In `tests/test_app.py`, import `app` from `src.app` and reset the in-memory `activities` data between tests to keep tests isolated.
4. Write tests for key backend behaviors:
   - GET `/activities` returns the activities list successfully.
   - POST `/activities/{activity_name}/signup` registers a participant and updates activity participants.
   - POST duplicate signup returns HTTP 400.
   - DELETE `/activities/{activity_name}/participants?email=...` unregisters a participant.
   - DELETE for a non-signed-up participant returns HTTP 400.
5. Ensure test execution is configured via `pytest.ini` and optionally add `pytest` to `requirements.txt` if not already present.

**Relevant files**
- `/workspaces/skills-getting-started-with-github-copilot/src/app.py` — backend app under test
- `/workspaces/skills-getting-started-with-github-copilot/pytest.ini` — pytest configuration
- `/workspaces/skills-getting-started-with-github-copilot/requirements.txt` — add `pytest` if needed
- `/workspaces/skills-getting-started-with-github-copilot/tests/test_app.py` — new test file

**Verification**
1. Run `pytest` from the repo root and confirm all tests pass.
2. Confirm tests exercise both signup and participant removal endpoints and detect duplicate signup.
3. Confirm tests do not depend on manual page reload or separate frontend behavior.

**Decisions**
- Use FastAPI `TestClient` to exercise the backend directly.
- Use the AAA (Arrange-Act-Assert) pattern within each test.
- Use a fixture to restore `activities` to initial state before each test.
- Keep tests focused on API behavior rather than frontend rendering.
