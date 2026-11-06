# Stockman

**Stockman** is a paper-trading web application for practicing stock and crypto trading without risking real money. It simulates a real brokerage — funded virtual wallets, live market prices, order placement, profit/loss tracking, alerts, and notifications — so you can learn how markets behave and how trading decisions play out, safely.

## The idea

Most people learn trading by losing money. Stockman inverts that: it gives you a **realistic market environment and a virtual wallet** so you can place real-feeling orders against live prices and watch the outcome in a portfolio and ledger — with zero financial risk.

The platform is intentionally scoped to be **spot-only and Islamic-compliant**: no shorting, no margin/leverage, no derivatives, no interest or fees, and no FX conversion. Funding comes only through audited top-up/withdrawal requests — there is no "edit your balance" shortcut, so your practice results stay honest and reproducible.

## Who it's for

- **Beginners** learning how orders, fills, and P&L work before touching a real broker.
- **Traders practicing** a strategy against live market data without capital at risk.
- **Egyptian investors** — the Egyptian Exchange (EGX) is a first-class market alongside crypto.
- **Educators and teams** who want an audited, role-based environment (admin, analyst, user) for teaching or demos.
- **Anyone who wants Islamic-compliant trading mechanics** (spot-only, no riba).

## What you can practice

- Fund a virtual wallet (EGP and USDT) through audited top-ups.
- Browse markets, inspect price history, and maintain a watchlist.
- Place **market** and **limit** orders; watch them match against live prices with FIFO cost-lot accounting.
- Track realized and unrealized profit/loss per currency in a portfolio.
- Set **price and percent-change alerts** and receive live **notifications** over SSE.
- Read an immutable **audit trail** of every account, order, and access change.
- Manage **roles and permissions** through a policy-based administration console.

## Architecture at a glance

| Component | Stack | Purpose |
| --- | --- | --- |
| [`backend/`](backend/README.md) | Django 5.2 + DRF, SQLite, uv | Single source of truth for authorization, money math, and market data. |
| [`frontend/`](frontend/README.md) | Next.js 16 + React 19, Tailwind, shadcn/ui | Thin client rendering what the backend authorizes and computes. |

The two directories are tracked as **git submodules** (references to their own repositories: `stockman-backend` and `stockman-frontend`), not as inline copies. Each project owns its own `.env`, `.gitignore`, and `AGENTS.md`.

## Cloning

```bash
git clone --recurse-submodules <repo-url>
```

If you already cloned without submodules:

```bash
git submodule update --init --recursive
```

## How to use

1. **Start the backend** — see [backend/README.md](backend/README.md): set up `.env`, `uv sync`, migrate, `bootstrap`, then run the API server and the background worker.
2. **Start the frontend** — see [frontend/README.md](frontend/README.md): `cp .env.example .env && npm install && npm run dev`, then open http://localhost:3000.
3. **Register**, top up practice funds, and start trading paper positions.

## Notes

- Paper trading only — no real money, no orders are sent to any real exchange.
- Spot-only and Islamic-compliant: no shorting, margin, interest, or fees.
- Secrets never go into `NEXT_PUBLIC_*`, source files, or the Postman collection.
- EGX data is gated behind `EGX_ACCESS_VERIFIED` until free entitlement and permitted usage are confirmed; crypto (Binance public data) works out of the box.
