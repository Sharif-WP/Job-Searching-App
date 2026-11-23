# Team Startup Guide

## Fastest local start

Prerequisites: PostgreSQL must be running, and the root `.env` file must contain valid local
database credentials.

Open two PowerShell windows from the repository root.

### Window 1: API

```powershell
Set-Location backend
.\.venv\Scripts\python.exe -m uvicorn app.main:app --reload --port 8000
```

Check the API at <http://localhost:8000/docs>.

### Window 2: web app

The dependency-free runner uses the last successful frontend build and still forwards `/api` to the
backend. It is useful when `node_modules` needs to be repaired.

```powershell
Set-Location frontend
..\backend\.venv\Scripts\python.exe local_server.py
```

Open <http://localhost:5173>.

## Normal development start

After frontend dependencies are available, use Vite instead:

```powershell
Set-Location frontend
npm install
npm run dev
```

## First-time database setup

```powershell
Set-Location backend
.\.venv\Scripts\python.exe -m alembic upgrade head
.\.venv\Scripts\python.exe ..\scripts\seed_reference.py
```

The backend environment is created with:

```powershell
py -3.13 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements-dev.txt
```

Keep `.env` private. Use a database ending in `_test` for `TEST_DATABASE_URL`.