# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

A minimal Express REST API used as a course project for setting up Claude Code on a real codebase.

## Commands

```bash
npm install        # install dependencies
npm run dev        # start API with file-watching on http://localhost:3000
npm test           # run all tests (Node built-in test runner)
npm run lint       # check code style with ESLint
```

To run a single test file: `node --test tests/users.test.js`

## Architecture

- `server.js` — entry point; mounts route modules and exports `app` (no live port) for test imports
- `routes/` — one file per resource (`users.js`, `health.js`); each file creates an `express.Router` and exports it
- `db/store.js` — in-memory data layer; all data access goes through its exported functions (`getAllUsers`, `getUserById`, `createUser`); data resets on restart

## Conventions

- Use CommonJS (`require`/`module.exports`), not ES modules — `"sourceType": "script"` is set in ESLint
- Route parameters that should be numbers must be explicitly cast: `Number(req.params.id)`
- New routes go in a new file under `routes/` and are mounted in `server.js`; do not add routes directly to the server file
