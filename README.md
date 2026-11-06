# Stockman

Paper-trading web application for practicing stock trading without real money. Spot-only and Islamic-compliant, covering the Egyptian Exchange (EGX) and crypto, with an audited virtual wallet and no admin balance overrides.

## Structure

| Directory   | Description                                                                 |
| ----------- | --------------------------------------------------------------------------- |
| `backend/`  | Django 5.2 + Django REST Framework API — see [backend/README.md](backend/README.md) |
| `frontend/` | Next.js 16 client — see [frontend/README.md](frontend/README.md)            |

The two directories are tracked as **git submodules** (references to their own repositories), not as inline copies.

## Cloning

```bash
git clone --recurse-submodules <repo-url>
```

If you already cloned without submodules:

```bash
git submodule update --init --recursive
```

## Quick start

1. Start the backend — migrate, bootstrap, then run the API server and the background worker (see [backend/README.md](backend/README.md)).
2. Start the frontend — `npm install && npm run dev`, then open http://localhost:3000 (see [frontend/README.md](frontend/README.md)).

## Notes

- Paper trading only — no real money.
- Each project owns its own `.env`, `.gitignore`, and `AGENTS.md`; secrets never go into `NEXT_PUBLIC_*` or the Postman collection.
