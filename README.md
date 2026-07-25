# Coil — an agent-native trading system · [coil.trade](https://coil.trade)

> **Read this first.** This repository is **documentation only** — no product code is
> distributed from GitHub. The runnable open-source harness is
> **[coil-agent](https://github.com/joeyfife/coil-agent)**; the paid product lives at
> **[coil.trade](https://coil.trade)**.

## What Coil is

[Coil](https://coil.trade) (v4) is an agent-native, **long-only** trading system you buy once and run yourself. One purchase is three things: a **scanner** that scores every name across the S&P 500, the Nasdaq-100, and a Macro book (bonds / income / gold & metals / commodities); a **dashboard** that shows the whole board; and an **engine** that trades the scanner's published scores by rule. Its identity is leadership rotation — it hunts the market's relative-strength leaders and buys them when they're coiled at real support: structural stops (4–14%), volume-profile and Fibonacci support/resistance, and an intraday-thrust guard so it doesn't chase the open. It is long-only by design: in downturns it raises cash and rotates defensively into the Macro book, and it never touches inverse ETFs. It runs on your machine, inside your own AI agent, against your own brokerage — your credentials never leave your machine.

## For agents and developers — the board is readable without buying anything

The scanner's published board is available as a hosted API and a hosted **MCP server**. This
is separate from the downloadable product: you are reading Coil's scores, not running its
engine.

| | |
|---|---|
| **Free MCP server** | `claude mcp add --transport http coil https://coil.trade/mcp` — 7 tools, full board one market day delayed. No key, no wallet, no account. |
| **Free API key** | `POST https://coil.trade/api/key` with an email — 25 live calls/day on the cheap slices. |
| **Pay per read (x402)** | 15 endpoints, $0.001–$0.25 in USDC on Base or Algorand. No account. |
| **Live subscription** | [$12/mo Coil Scanner](https://coil.trade/scanner) — the live intraday board. |
| **Open-source harness** | [coil-agent](https://github.com/joeyfife/coil-agent) — reads the board, paper-trades it through Alpaca. MIT. |

**Check the record before trusting any of it — both of these are free and unauthenticated:**

- [`/api/perf`](https://coil.trade/api/perf) — the engine's return vs SPY and QQQ, funding-adjusted, published with its sample size. Omitted rather than estimated when unavailable.
- [`/api/board/proof`](https://coil.trade/api/board/proof) — an append-only sha256 commitment over every archived day, written at publish time *before* the outcome was known, with a verification recipe that reproduces byte-identically in Python and JavaScript.

Each scored name carries `opp_pct` (opportunity 0–100), `entry_q` (buyable now vs extended), `hold_q` (trend durability) and a `state` (`firing` / `ready` / `setup` / `wait` / `chase` / `falling`). Scores and states only — **never stop prices, never target prices, never individualized advice.**

## What this repository is

The public docs and pointer repo. Machine-readable sources are on the site:
[`llms.txt`](https://coil.trade/llms.txt) · [`llms-full.txt`](https://coil.trade/llms-full.txt) ·
[`.well-known/coil.json`](https://coil.trade/.well-known/coil.json) ·
[`openapi.json`](https://coil.trade/openapi.json). Treat **coil.trade** as the source of truth.

## How the product works

1. **Scanner** — scores every name on independent, readable factors: opportunity, entry-window, hold-conviction, leadership, sector-rotation phase, market posture. It publishes those scores.
2. **Dashboard** — a local view of the whole board: every score, every position, every rule the engine is following, on your machine.
3. **Engine** — reads the scanner's *published* scores (it never re-ranks them) and trades by rule: buys leaders coiled at real support, sizes by conviction, exits on a ladder with trailing stops, holds cash when the pool is thin — all behind a hard safety core. It may use a leveraged ETF long-side only, at reduced size, and never uses inverse ETFs.

**Where it runs.** Inside your own AI agent — built for **Claude Code**, adaptable to equivalents that run code on a schedule. Orders go through your **broker's MCP connector** (built for Robinhood's agentic accounts; any broker with an equivalent MCP works). The scan and the dry-run need no broker connection at all. See the [Robinhood pairing recipe](https://coil.trade/agents/robinhood).

**What the downloadable product is not:** not a managed account, not a signal service, not SaaS. Nothing phones home. It ships **disarmed** (`LIVE_TRADING=False`); going live is a separate, deliberately gated flow (your own account allowlisted, an integrity re-pin, the self-test suite green, and a typed total-loss acknowledgment).

## Requirements

- **macOS or Windows**, Python 3.9+ (agent-led onboarding detects your OS and branches the install).
- **An AI agent that can run code on a schedule** — built for Claude Code; adaptable to equivalents.

## Results — the claim next to its benchmark, as it always should be

- **Backtest, 2017–2026 H1: +638% cumulative, vs. +282% for buy-and-hold SPY** over the same window.
- Survivorship-free: point-in-time S&P 500 membership including delisted names, next-open fills, trading costs modeled.
- **Where the edge lives:** the outperformance concentrates in leadership regimes. Through the end of 2025 the strategy ran roughly *even* with SPY — at about one-third less maximum drawdown. The cumulative gap was earned when market leadership was strong and rotating, not spread evenly across the decade.

Caveats — none of these are optional reading:

- These are **backtested research figures that validate the ranking model**. They are **not client returns** and not a live track record.
- The live record is thin and published honestly at [`/api/perf`](https://coil.trade/api/perf) — read it rather than the backtest.
- Backtested is not live. Fills, costs, and behavior in regimes the backtest never saw can be worse.
- Long-only does not mean safe. Markets can lose money, and where the engine uses leveraged ETFs a position can lose value rapidly — up to and including its entire value.
- Nothing here or on [coil.trade](https://coil.trade) is investment advice. Coil is self-operated software: you decide to run it, and you bear the results.

## Pricing

**$29, one-time** (launch price; regular $39) for the downloadable system — no subscription, no tiers. Checkout is a hosted **Gumroad** flow; Gumroad is the merchant of record. All sales are final (instant digital download). The hosted board is separate: free tiers as above, or **$12/mo** for the live intraday board.

→ [Get Coil — $29 (Gumroad checkout)](https://6634161787305.gumroad.com/l/rtdctu)

## Links

| | |
|---|---|
| Site | [coil.trade](https://coil.trade) |
| For agents | [coil.trade/agents](https://coil.trade/agents) · [Robinhood pairing](https://coil.trade/agents/robinhood) |
| Open-source harness | [joeyfife/coil-agent](https://github.com/joeyfife/coil-agent) |
| How it works · FAQ · Use cases | [how-it-works](https://coil.trade/how-it-works) · [faq](https://coil.trade/faq) · [use-cases](https://coil.trade/use-cases) |
| Buy ($29 one-time, Gumroad) | [6634161787305.gumroad.com/l/rtdctu](https://6634161787305.gumroad.com/l/rtdctu) |
| Live board subscription | [coil.trade/scanner](https://coil.trade/scanner) |
| Agent manifest · OpenAPI | [coil.json](https://coil.trade/.well-known/coil.json) · [openapi.json](https://coil.trade/openapi.json) |
| X | [@coil_trade](https://x.com/coil_trade) — an autonomous agent posting the engine's own trades from its ledger |
| Terms · Privacy · Refunds | [terms](https://coil.trade/terms) · [privacy](https://coil.trade/privacy) · [refund](https://coil.trade/refund) |

Built by Joey Fife (solo).

## History

This repository previously documented **Coil Sync**, an MCP server that shipped alongside an earlier, retired product: a $9.99 SOXL/SOXS semiconductor pair engine sold through Lemon Squeezy. That product line is dead, and Coil Sync was shelved with the old Pro tier. **Coil v4** replaced it — long-only, market-wide, sold once at [coil.trade](https://coil.trade). In July 2026 a *new*, unrelated hosted MCP server went live at `coil.trade/mcp` serving the scanner's published board (read-only, free tier); it is not Coil Sync and does not run the engine. Rather than delete this repo and break inbound links, it remains the public docs repo.

---

*Not investment advice. Coil is self-operated software; it is not a managed account, a signal service, or a guarantee of profit. Markets can lose money, and leveraged ETFs can lose value rapidly, including total loss. Backtested results are not live results and are not client returns.*
