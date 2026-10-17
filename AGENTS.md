# Repository Guidelines

## Project Structure & Module Organization

`FlaskRecap.py` is the entire Flask application. It defines the in-memory greeting data and the `GET /greeting`, `GET /greeting/<lang>`, and `POST /greeting` routes. `requirements.txt` pins Python dependencies. `udacity-fsnd-flaskrecap.postman_collection.json` contains example API requests; `README.md` has setup instructions. There are no templates, static assets, or automated test directories in this checkout.

## Build, Test, and Development Commands

Create and activate a virtual environment, then run `python -m pip install -r requirements.txt` to install dependencies. If the pinned versions conflict, report the resolver error instead of bypassing dependency checks. Run `flask --app FlaskRecap.py run --reload` to start the local development server on port 5000. There is no build step. Use `python -m py_compile FlaskRecap.py` for a basic syntax check.

## Coding Style & Naming Conventions

Use four spaces for Python indentation and follow PEP 8 for new code. Keep route handlers and variables in `snake_case`; use clear names for language codes and JSON fields. Keep responses JSON-based and use Flask status errors consistently. No formatter or linter is configured, so review formatting manually and keep changes focused on this small app.

## Testing Guidelines

There is no automated test framework or coverage target. Import the Postman collection and exercise all three requests against `http://127.0.0.1:5000`. For route changes, also check invalid language codes (`404`) and missing POST fields (`422`). If you add automated tests, place them under `tests/`, name files `test_*.py`, and document the test command in the README.

## Commit & Pull Request Guidelines

Git history is mostly dependency updates titled `Bump <package> from <old> to <new>`; it does not establish a broader commit convention. Use a short, specific subject for other changes. In pull requests, describe the changed routes or dependencies, include the commands and manual requests you ran, and link a related issue when one exists. Include example request and response bodies when API behavior changes.
