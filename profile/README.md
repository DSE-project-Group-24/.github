# DSE-project-Group-24

This repository contains two primary applications used by the Data Science & Engineering (DSE) group: 24

- Frontend — React + Vite application providing role-based UIs for hospital staff, patients, accidents and prediction features.
- Core-Backend — FastAPI service exposing authenticated REST endpoints, persisting data in Supabase, and serving ML prediction endpoints.

This profile README gives a concise developer-oriented overview and quick start pointers for getting both apps running locally.

---

## Frontend (folder: `Frontend/`)

- Main entry: `src/main.jsx` and top-level routing in `src/App.jsx`.
- Pages & components: `src/pages/` and `src/components/`.

Run locally:

# from Frontend/

npm install
npm run dev

- Cypress E2E tests are under `cypress/e2e`. Run with `npx cypress open` or `npx cypress run`.

---

## Core-Backend (folder: `Core-Backend/`)

- Framework: FastAPI
- Entrypoint: `app/main.py`
- DB / Supabase setup: `app/db.py` (reads `SUPABASE_URL` and `SUPABASE_KEY` from `.env`)
- Models: `app/models/` (Pydantic models)
- Routes: `app/routes/` (e.g. `auth_routes.py` for authentication)
- Utilities & auth helpers: `app/utils/` and `app/auth/`
  Important auth endpoints:

- POST `/auth/login` — exchange credentials for a JWT
  Run locally (PowerShell example):

````powershell
pip install -r requirements.txt
# DSE-project-Group-24

This repository contains two primary applications used by the Data Science & Engineering (DSE) group:

- Frontend — React + Vite application providing role-based UIs for hospital staff, patients, accidents and prediction features.
- Core-Backend — FastAPI service exposing authenticated REST endpoints, persisting data in Supabase, and serving ML prediction endpoints.

This profile README gives a concise developer-oriented overview and quick start pointers for getting both apps running locally.

---

## Frontend (folder: `Frontend/`)

- Main entry: `src/main.jsx` and top-level routing in `src/App.jsx`.
- Pages & components: `src/pages/` and `src/components/`.
- Central API client: `src/utils/api.js` — change `baseURL` here to point the frontend at the backend. The client reads the JWT from `localStorage` (key: `access_token`) and attaches it to requests.
- Login: single login page posts to the backend auth endpoint; after successful login the user is redirected to a role-specific dashboard.
```bash
npm install
npm run dev
````

- Cypress E2E tests are under `cypress/e2e`. Run with `npx cypress open` or `npx cypress run`.

---

## Core-Backend (folder: `Core-Backend/`)

- Framework: FastAPI
- Entrypoint: `app/main.py`
- DB / Supabase setup: `app/db.py` (reads `SUPABASE_URL` and `SUPABASE_KEY` from `.env`)
- Models: `app/models/` (Pydantic models)
- Routes: `app/routes/` (e.g. `auth_routes.py` for authentication)
- Services/business logic: `app/services/` (auth, patients, hospital, predictions)
- Utilities & auth helpers: `app/utils/` and `app/auth/`

Important auth endpoints:

- POST `/auth/login` — exchange credentials for a JWT
- POST `/auth/register` — user registration (usually restricted)
- GET `/auth/me` — get current user info

Other resources: `/hospital`, `/nurse`, `/doctor`, `/patients`, `/accidents`, `/medical`

Predictions endpoints are available under `/predictions/*` (discharge outcome, hospital stay prediction, SARIMA forecasts, etc.).

Run locally (PowerShell example):

```powershell
# from Core-Backend/
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
# run the app (adjust port as needed)
uvicorn app.main:app --reload --port 8080
```

Notes:

- Create a `.env` in `Core-Backend/` containing `SUPABASE_URL`, `SUPABASE_KEY`, and JWT settings such as `SECRET_KEY`, `ALGORITHM`, and `ACCESS_TOKEN_EXPIRE_MINUTES`.
- If you change the backend host/port, update `Frontend/src/utils/api.js` `baseURL` accordingly.
- API docs (Swagger / ReDoc) are available when the server is running (e.g. `http://127.0.0.1:8080/docs`).

---

## Quick contributor pointers

- To test frontend <-> backend flow: start the backend, then run the frontend dev server and point `baseURL` to the backend.
- Authentication flow: check `Core-Backend/app/routes/auth_routes.py` and `Core-Backend/app/services/auth_service.py` for login/refresh logic.
- If you want, I can add a short `developer-checklist.md` with exact commands and environment templates.

---
