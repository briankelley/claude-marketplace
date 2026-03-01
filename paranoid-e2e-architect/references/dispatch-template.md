# Paranoid E2E Architect — Dispatch Template

Use this template when dispatching the paranoid-e2e-architect agent against a specific application. Fill in the bracketed sections. Delete this header and all comments before dispatching.

---

## Application

- **Name**: [project name]
- **Framework**: [e.g., FastAPI + Jinja2, Express + React, Django + HTMX]
- **Source**: [absolute path to project root]
- **Entry point**: [path to app factory or main module]

## Write Endpoints

[List every endpoint/action that modifies state. The agent will build the registry from this, but giving it a head start avoids redundant discovery. Include HTTP method, path, what it writes to, and what payload it expects.]

```
POST /api/config/env     → writes .env file (API keys)
POST /api/config         → writes models.yaml (full config)
POST /api/config/model-timeout → writes models.yaml (single field)
...
```

## Pre-existing State to Protect

[Describe the files, database tables, or state that must survive paranoid testing. The agent needs to know what "existing good data" looks like so it can seed fixtures and verify survival.]

```
~/.config/[app]/.env           — contains API keys, must not be wiped
~/.config/[app]/config.yaml    — contains model configuration, must not be corrupted
~/.local/share/[app]/reviews/  — contains review artifacts, must not be deleted
```

## Existing Test Infrastructure

- **Test framework**: [pytest, jest, etc.]
- **Test directory**: [path]
- **E2E framework**: [Playwright, Cypress, etc., or "none yet"]
- **Existing test count**: [approximate]
- **How to run**: [command]
- **Fixtures/conftest**: [path to shared fixtures, note any patterns to follow]

## Frontend Behavior

[Describe how forms submit — this is critical for identifying the delta-vs-full-state gap.]

```
Forms submit via fetch() with JSON body.
CSRF token passed in X-Custom-Token header from meta tag.
API key inputs are password fields; .value is empty string when untouched (placeholder text).
The frontend sends ALL field values on save, not just changed ones.
```

## Known Concerns

[If you already know about specific footguns, list them. The agent will still discover independently, but this seeds the registry with confirmed issues.]

```
- Save API Keys button sends empty strings for untouched fields → backend interprets as "delete"
- Config save with models: {} passes YAML parse but may not be caught by validation
```

## Scope Constraints

- **Test files to create**: [list target paths, e.g., tests/e2e/test_paranoid_*.py]
- **Files NOT to modify**: [e.g., tests/conftest.py, any existing test files]
- **LLM available for Approach 3?**: [yes/no, and how to reach it — e.g., http://localhost:8080/v1]
- **Markers to use**: [e.g., @pytest.mark.paranoid]
- **How to validate**: [command to run tests after writing them]
