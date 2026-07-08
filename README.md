# Coil — an agent-native trading system · [coil.trade](https://coil.trade)

> **Read this first.** This repository is **documentation only**. Coil is **not an MCP server**, and no product code is distributed from GitHub. The "Coil Sync" MCP server this repo originally described was **shelved** and is no longer offered — see [History](#history). The product lives at **[coil.trade](https://coil.trade)**.

## What Coil is

[Coil](https://coil.trade) (v4) is an agent-native, **long-only** trading system you buy once and run yourself. One purchase is three things: a **scanner** that scores every name across the S&P 500, the Nasdaq-100, and a Macro book (bonds / income / gold & metals / commodities); a **dashboard** that shows the whole board; and an **engine** that trades the scanner's published scores by rule. Its identity is leadership rotation — it hunts the market's relative-strength leaders and buys them when they're coiled at real support: structural stops (4–14%), volume-profile and Fibonacci support/resistance, and an intraday-thrust guard so it doesn't chase the open. It is long-only by design: in downturns it raises cash and rotates defensively into the Macro book, and it never touches inverse ETFs. It runs on your machine, inside your own AI agent, against your own brokerage — your credentials never leave your machine. Full detail: [coil.trade](https://coil.trade).

## What this repository is

This is the public docs and pointer repo for Coil ([coil.trade](https://coil.trade)). No product code lives here — Coil is a paid download you run locally. What's here:

- **This README** — a plain-language, current description of what Coil is and is not.
- **Agent-readable pointers.** If you are an AI agent evaluating this project, the canonical machine-readable sources are on the site:
  - [`coil.trade/llms.txt`](https://coil.trade/llms.txt) — condensed agent-readable summary
  - [`coil.trade/llms-full.txt`](https://coil.trade/llms-full.txt) — full agent-readable documentation
  - [`coil.trade/.well-known/coil.json`](https://coil.trade/.well-known/coil.json) — machine-readable product manifest (what Coil is and how an agent sets it up)

Treat **coil.trade** as the source of truth. This repository exists so that old links to it keep resolving to accurate information.

## How it works

One pipeline, three parts:

1. **Scanner** — scores every name in the S&P 500, the Nasdaq-100, and the Macro book on independent, readable factors: opportunity, entry-window, hold-conviction, leadership, sector-rotation phase, and market posture. It publishes those scores.
2. **Dashboard** — a local view of the whole board: every score, every position, every rule the engine is following, on your machine.
3. **Engine** — reads the scanner's *published* scores (it never re-ranks them) and trades by rule: buys leaders coiled at real support, sizes by conviction, exits on a ladder with trailing stops, and holds cash when the pool is thin — all behind a hard safety core. It may use a leveraged ETF (e.g. SOXL) to accelerate a semiconductor leader — long side only, at reduced size — and never uses inverse ETFs.

**Where it runs.** Inside your own AI agent: it's built for **Claude Code** (a scheduled Claude Code session is the operator) and is adaptable to other agents that can run code on a schedule. Orders are placed through your **broker's MCP connector** — built for Robinhood, which supports agentic trading through dedicated agentic accounts; any broker with an equivalent MCP works. The scan and the dry-run need no broker connection at all.

**What Coil is not — worth being precise about, given this repo's name:**

- Coil is **not an MCP server**. It exposes no MCP tools. It is Python software your agent runs, and that software *drives* your broker's MCP server to place orders.
- The former **Coil Sync MCP** — the product this repository was created for — was shelved along with the old Pro tier. It is not part of v4, and nothing here installs an MCP server.
- It is not a signal service, not a managed account, and not SaaS. Nothing phones home. It ships **disarmed** (`LIVE_TRADING=False`); going live is a separate, deliberately gated flow (your own account allowlisted, an integrity re-pin, the self-test suite green, and a typed total-loss acknowledgment).

## Requirements

- **macOS or Windows**, Python 3.9+ (the agent-led onboarding detects your OS and branches the install).
- **An AI agent that can run code on a schedule** — built for Claude Code; adaptable to equivalents.
- **A brokerage connector** — built for Robinhood via its MCP; any broker with an equivalent MCP works. Not needed for scanning or dry-run.
- **A free Alpaca account** for market data (onboarding wires the key for you).
- Your broker account id and keys stay on your machine — nothing is sent anywhere else.
- Ships with a self-test suite (100+ assertions) and interactive, agent-led onboarding; about an hour to a scheduled dry-run.

## Performance & risk

The headline claim, stated next to its benchmark, as it always should be:

- **Backtest, 2017–2026 H1: +638% cumulative, vs. +282% for buy-and-hold SPY** over the same window.
- The backtest is survivorship-free: point-in-time S&P 500 membership including delisted names, next-open fills, and trading costs modeled.
- **Where the edge lives:** the outperformance concentrates in leadership regimes. Through the end of 2025 the strategy ran roughly *even* with SPY — at about one-third less maximum drawdown. The cumulative gap over SPY was earned in the periods when market leadership was strong and rotating, not spread evenly across the decade.

Caveats — none of these are optional reading:

- These are **backtested research figures that validate the ranking model**. They are **not client returns** and not a live track record. The engine is **newly live**.
- Backtested is not live. Live results will differ; fills, costs, and behavior in regimes the backtest never saw can be worse.
- Long-only does not mean safe. Markets can lose money, and where the engine uses leveraged ETFs a position can lose value rapidly — up to and including its entire value.
- Nothing in this repository or on [coil.trade](https://coil.trade) is investment advice. Coil is self-operated software: you decide to run it, and you bear the results.

## Pricing

**$29, one-time** (launch price; regular $39). No subscription, no tiers, no recurring anything — you own the current version and keep it. Checkout is a hosted **Gumroad** flow; Gumroad is the merchant of record and handles receipts and license keys. All sales are final (instant digital download).

→ [Get Coil — $29 (Gumroad checkout)](https://6634161787305.gumroad.com/l/rtdctu)

## Links

| | |
|---|---|
| Site | [coil.trade](https://coil.trade) |
| How it works | [coil.trade/how-it-works](https://coil.trade/how-it-works) |
| FAQ | [coil.trade/faq](https://coil.trade/faq) |
| Use cases | [coil.trade/use-cases](https://coil.trade/use-cases) |
| Buy ($29 one-time, Gumroad) | [6634161787305.gumroad.com/l/rtdctu](https://6634161787305.gumroad.com/l/rtdctu) |
| Agent manifest | [coil.trade/.well-known/coil.json](https://coil.trade/.well-known/coil.json) |
| llms.txt / llms-full.txt | [coil.trade/llms.txt](https://coil.trade/llms.txt) · [coil.trade/llms-full.txt](https://coil.trade/llms-full.txt) |
| X | [@coil_trade](https://x.com/coil_trade) — an autonomous agent posting the engine's own trades from its ledger |
| Terms · Privacy · Refunds | [terms](https://coil.trade/terms) · [privacy](https://coil.trade/privacy) · [refund](https://coil.trade/refund) |

Built by Joey Fife (solo).

## History

This repository previously documented **Coil Sync**, an MCP server that shipped alongside an earlier, retired product: a $9.99 SOXL/SOXS semiconductor pair engine sold through Lemon Squeezy. That product line is dead. **Coil v4** replaced it — long-only, market-wide (S&P 500 / Nasdaq-100 / Macro), sold once at [coil.trade](https://coil.trade) — and the Coil Sync MCP was shelved with the old Pro tier. Rather than delete the repo and break inbound links, it was repurposed as the public docs repo you're reading, so anything that still points here lands on accurate information.

---

*Not investment advice. Coil is self-operated software; it is not a managed account, a signal service, or a guarantee of profit. Markets can lose money, and leveraged ETFs can lose value rapidly, including total loss. Backtested results are not live results and are not client returns; the engine is newly live.*
