# AGENTS.md

## Project overview

This repository is a fabric cutting management dashboard built with a React/Vite frontend and an Express/PostgreSQL API.

- Frontend entry points: [src/App.jsx](src/App.jsx), [src/main.jsx](src/main.jsx), [src/services/api.js](src/services/api.js)
- API entry point: [server/index.js](server/index.js)
- Database schema: [db/schema.sql](db/schema.sql)
- App setup and run instructions: [README.md](README.md)
- Package scripts and dependencies: [package.json](package.json)

## Working commands

Run the app from the repository root:

```sh
npm install
npm run dev
```

The frontend is expected on:

- http://localhost:5173/admin-center/login?next=inventery

Run the API separately:

```sh
cp .env.example .env
# adjust DATABASE_URL if needed
psql "$DATABASE_URL" -f db/schema.sql
npm run server
```

The API listens on:

- http://localhost:4000

Useful validation commands:

```sh
npm run build
npm run lint
```

## Important conventions

- Keep frontend and server responsibilities separate. The frontend should call the API through [src/services/api.js](src/services/api.js), not by reaching raw database logic directly.
- Treat the PostgreSQL schema in [db/schema.sql](db/schema.sql) as the source of truth for the domain model and API data shape.
- The server uses `DATABASE_URL`, `PORT`, and `CLIENT_ORIGIN` environment variables. Configure them before running the API.
- The dashboard and endpoints are organized around cutting tables, production plans, staffing, fabrics, quality issues, and daily operations. Match that domain vocabulary in new code.
- Do not assume the database is already seeded or the API is healthy without the schema applied and the environment configured.
- This project is in active development; if a feature is connected to the backend, make sure it still works when PostgreSQL is unavailable and the health endpoint is used to detect degraded state.

## Architecture notes

- The frontend is a Vite React app and renders the operational dashboard and management UIs from [src/App.jsx](src/App.jsx).
- The API is implemented in [server/index.js](server/index.js) with endpoints such as:
  - `GET /api/health`
  - `GET /api/tables`
  - `GET /api/dashboard`
  - `GET /api/workers`
  - `GET /api/fabric`
  - `GET /api/quality`
  - `POST /api/production`
- The app is designed around a cutting-room workflow, so new features should align with tables, plans, output targets, manpower, stock, and quality tracking.

## Before making changes

1. Check whether the change belongs in the frontend, the Express API, or the schema.
2. Prefer small, targeted changes that follow the existing domain naming.
3. Validate with the project’s build and lint commands when the change affects behavior or dependencies.

## Related docs

- [README.md](README.md)
- [package.json](package.json)
- [db/schema.sql](db/schema.sql)
- [server/index.js](server/index.js)
- [src/services/api.js](src/services/api.js)
