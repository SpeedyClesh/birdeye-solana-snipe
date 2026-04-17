# SolanaSnipe ⚡

> Real-time onchain alert dashboard powered by Birdeye Data WebSocket APIs

Built for the **Birdeye Data 4-Week Build in Public Competition — Sprint 1**

---

## What It Does

SolanaSnipe is a production-grade Solana signal dashboard that streams three categories of onchain events in real-time:

| Alert Type | WebSocket Used | Description |
|---|---|---|
| 🐋 **Whale Moves** | `SUBSCRIBE_LARGE_TRADE_TXS` | Swaps above 5× your min threshold — likely smart money |
| ✨ **New Listings** | `SUBSCRIBE_TOKEN_NEW_LISTING` | Freshly listed tokens with configurable liquidity floor |
| ⚡ **Large Trades** | `SUBSCRIBE_LARGE_TRADE_TXS` | All swaps above your minimum volume threshold |

All data is sourced exclusively from **Birdeye Data Services** — the same infrastructure trusted by Phantom, Raydium, and Coinbase.

---

## Features

- **Live WebSocket feed** — three parallel connections to Birdeye's WebSocket API
- **Configurable thresholds** — adjust min trade size and min liquidity via sliders
- **Source filtering** — toggle pump.fun, Raydium, Meteora individually
- **Alert type filtering** — show/hide whale, new listing, and large trade alerts
- **Tabbed view** — browse all alerts or filter by category
- **Demo mode** — runs simulated data with no API key so you can explore the UI immediately
- **Alert sounds** — optional audio notification on new signal
- **Live ticker** — SOL/BTC/ETH/JUP prices across top of screen

---

## Getting Started

### 1. Get a Birdeye API Key

Sign up free at [bds.birdeye.so](https://bds.birdeye.so) and grab your API key.

### 2. Run locally

```bash
# No build step needed — pure HTML/JS
# Just open in browser or serve with any static server

npx serve .
# or
python3 -m http.server 8080
```

Then open `http://localhost:8080`

### 3. Connect

Paste your API key in the top-right input and click **CONNECT**.

The dashboard will open three WebSocket connections:
- Whale tracker: `SUBSCRIBE_LARGE_TRADE_TXS` with `min_volume = threshold × 5`
- Large trade tracker: `SUBSCRIBE_LARGE_TRADE_TXS` with `min_volume = threshold`
- New listings: `SUBSCRIBE_TOKEN_NEW_LISTING` with pump.fun + Meteora + Raydium

---

## Architecture

```
Birdeye WebSocket API (Solana)
       │
       ├── Connection 1: SUBSCRIBE_LARGE_TRADE_TXS (whale, >5× threshold)
       ├── Connection 2: SUBSCRIBE_LARGE_TRADE_TXS (large trades, 1-5× threshold)
       └── Connection 3: SUBSCRIBE_TOKEN_NEW_LISTING (new meme tokens)
                │
                ▼
         Alert Engine (JS)
         ├── Type classifier (whale vs large vs new)
         ├── Filter engine (source, type toggles)
         ├── Stats counter
         └── DOM renderer (animated alert cards)
                │
                ▼
          Live Dashboard UI
          ├── Ticker tape (static prices)
          ├── Sidebar stats + controls
          └── Alert feed (real-time, tabbed)
```

---

## Birdeye APIs Used

| API | Endpoint |
|---|---|
| WebSocket (Large Trades) | `wss://public-api.birdeye.so/socket/solana` + `SUBSCRIBE_LARGE_TRADE_TXS` |
| WebSocket (New Listings) | `wss://public-api.birdeye.so/socket/solana` + `SUBSCRIBE_TOKEN_NEW_LISTING` |

---

## Demo

No API key? The dashboard starts in **demo mode** automatically — simulated events stream in so you can explore the full UI without signing up.

---

## Built With

- Vanilla HTML/CSS/JS — zero framework dependencies
- [Birdeye Data Services](https://bds.birdeye.so) — WebSocket API
- JetBrains Mono + Syne (Google Fonts)

---

## License

MIT

---

*Built for [Birdeye Data BIP Competition Sprint 1](https://superteam.fun/earn/listing/birdeye-data-4-week-bip-competition-sprint-1) · April 2026*

*Tag [@birdeye_data](https://x.com/birdeye_data) · #BirdeyeAPI*
