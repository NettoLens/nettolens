# NettoLens 🔍

**See the chain clearly.** Live tokens and safety scans for Robinhood Chain.

🌐 **Live site:** [nettolens.xyz](https://nettolens.xyz) · 🐦 **X:** [@nettolens](https://x.com/nettolens)

Free · No wallet needed · No sign-up

---

## What it does

Paste a token contract address and NettoLens runs a set of on-chain checks, then gives you a **Trust Score (0–100)** with a plain-English list of what it found.

| Area | What we check |
|---|---|
| **Contract** | Verified source, ownership / renounce status, contract age, mint authority, upgradeable (proxy) logic |
| **Sell restrictions** | Blacklists, trading on/off switches, sell taxes, pausable transfers, and whether anyone can still use them |
| **Admin & privileges** | Owner, AccessControl roles (admin, minter, pauser, upgrader, blacklister) |
| **Holders** | Top 10 concentration (DEX pools and burned supply excluded), holder tiers, supply held in contracts |
| **Liquidity** | Total USD liquidity across pools, main pool, LP burn status |
| **Market** | Market cap, 24h change and volume, drop from peak |
| **Deployer** | Launchpad detection, the real launching wallet, previous launches, creator-funded wallet clusters |

Other tools on the site: trending / new / top pairs, a watchlist, and a trade calculator.

**Supported chains:** Robinhood Chain (main focus), Base, Arbitrum, Arc, Ethereum.

## How it works

Everything runs **in your browser**. The page calls public APIs directly:

- [Blockscout](https://www.blockscout.com/) explorers (contract, holders, roles)
- [DEX Screener](https://dexscreener.com/) and [GeckoTerminal](https://www.geckoterminal.com/) (pools, liquidity, prices)
- The selected chain's public RPC (owner, proxy slots, privileged addresses)

No backend, no database, no tracking of what you scan. The watchlist is stored only in your own browser.

## Honest limits

We'd rather tell you what we *can't* see than show a false green light:

- **A scan is not financial advice** and not a guarantee that a token is safe.
- Sell-restriction checks read the **source code**. We don't simulate a real sell transaction yet, so this is not a full honeypot test.
- "LP burned" only counts liquidity sent to a burn address. Liquidity in locker contracts isn't recognised yet.
- Holder tiers are based on the **top 50 holders** returned by the explorer. Smaller wallets are grouped as "Others".
- If a check can't run, the result says so. **A missing result is not a pass.**

## Run it locally

It's a single HTML file, so there's nothing to install:

```bash
git clone https://github.com/NettoLens/nettolens.git
cd nettolens
# open index.html in your browser
```

## Roadmap

- Shareable scan result cards
- 24h buy/sell pressure
- "Ticker Twins": spot copycat tokens sharing the same name or symbol
- Telegram bot (send a contract address, get a scan)

Follow [@nettolens](https://x.com/nettolens) for weekly updates.

## Feedback

Found a wrong result or a bug? Open an [issue](../../issues) or reach out on X.

---

*NettoLens is an independent project and is not affiliated with Robinhood.*
