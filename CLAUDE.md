# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

See `AGENTS.md` for the repository's contributor guidelines (style, testing, commit/PR conventions); the essentials are repeated below.

## Overview

A minimal Flask teaching demo (Udacity FSND "Flask Recap"). The whole app is `FlaskRecap.py`: a module-level `greetings` dict (language code → greeting) and three JSON routes:

- `GET /greeting` → `{"greetings": {...}}`
- `GET /greeting/<lang>` → `{"greeting": "..."}`, or `abort(404)` for an unknown code
- `POST /greeting` with JSON `{"lang", "greeting"}` → adds/overwrites the entry and returns the full dict; `abort(422)` if either field is missing

State is in-memory only. POSTed greetings disappear when the server restarts, and with `--reload` that includes every code edit. There's no database, no templates, no static files, and no custom error handlers, so `abort()` returns Flask's default HTML error pages, not JSON.

## Commands

```bash
python -m pip install -r requirements.txt   # inside a virtualenv
flask --app FlaskRecap.py run --reload      # dev server on http://127.0.0.1:5000
python -m py_compile FlaskRecap.py          # only automated check available
```

The README's `export FLASK_APP=FlaskRecap.py` + `flask run` form is older but equivalent.

`requirements.txt` pins every direct and transitive dependency, including `blinker`, which Flask 3 requires. When you bump one package, check that the others still satisfy its requirements (`python -m pip check`). If the pins conflict, report the resolver error; don't bypass dependency checks (e.g. `--no-deps`).

On macOS, the AirPlay Receiver usually holds port 5000 and answers with `403` (`Server: AirTunes`). If you see 403s, run with `--port 5050` (or another free port) and use that port in your requests.

## Testing

There's no test framework, linter, or formatter. To verify changes by hand, use the Postman collection `udacity-fsnd-flaskrecap.postman_collection.json` (or equivalent `curl` calls) against `http://127.0.0.1:5000`. It has three requests: GET all, GET `es`, and POST `{"lang": "fr", "greeting": "bonjour"}`. For route changes, also check an unknown language code (404) and a POST missing a field (422). If you add automated tests, put them in `tests/test_*.py` and document the command in the README.

## Conventions

- PEP 8, four-space indentation, `snake_case` handlers; keep responses JSON and use `abort(<status>)` for errors.
- Keep changes small; this is a single-file teaching app.
- Commits: dependency bumps use `Bump <package> from <old> to <new>`; anything else gets a short, specific subject. PRs should list the changed routes or dependencies and the commands and requests you ran, plus example request/response bodies if API behavior changes.
