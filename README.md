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

The front page opens on a dotted, rotating globe (drawn on a plain canvas, no external assets): gold continents, a teal latitude/longitude cage and a glass plate beneath it. Around it, a small HUD shows live Robinhood Chain data (latest block, gas, new pools in the last hour, read straight from the chain's RPC and GeckoTerminal) and the newest launches, each one tap away from a scan; during a scan the HUD switches to the four check groups (Contract, Holders, Market, Deployer) and fills as each check finishes. During a scan every finished check leaps across it as a gold light and lands as a ring in its result colour (green clean, amber caution, red risk) with the check's name; cautions and risks stay lit on the map, and the score locks in the centre at the end, then turns into the trust score ring. Respects "reduce motion". When it locks, Lens Notes read the result back in plain words, built only from that scan's own data, with a few questions you can tap ("Why this score?", "What wasn't checked?").

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
- **Scores top out at 85.** No token gets a perfect score, because no scan sees everything. A "Ceiling" badge shows when this applies.
- **Not covered:** shared funders between holders, fresh wallets, sniper or bundled buys, and a real sell transaction test. Tools that look at *who holds* a token can reach a different conclusion than a contract-focused scan.
- For proxy tokens (clones and EIP-1967), verification and the mint / sell-restriction checks read the **implementation's** source, not the proxy's.
- Top 10 concentration counts **wallets only**. Supply held by contracts (pools, vesting, multisigs) is shown separately.
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

### Launchpad bonding curves
Tokens that haven't graduated yet (Pons-style launchpads) keep their unsold supply in a curve contract. NettoLens asks large unnamed contract holders for `graduationThreshold()` and `realQuoteReserve()`; one that answers both is labelled as the bonding curve instead of an unknown contract, and the liquidity rows show how far the curve is to graduation (for example "5.7K of 8.1K USDG raised"). Contracts that don't answer are still flagged as unidentified.
For curve tokens the scan also reads `feeBps()` and `creatorTaxBps()` and shows a **Trading fee** row (base fee plus the creator's own tax, both fixed at launch); a total of 3% or more is listed as a signal.

### Share card
When a scan finishes, NettoLens draws a 1200×675 card (token, network, score ring and the main findings, with "Checks, not advice" and nettolens.xyz in the footer). It can be posted to X (text and link prefilled), saved, copied, or shared through the phone's share sheet. Links of the form `nettolens.xyz/?ca=0x…&chain=robinhood` open straight into that scan. The card is drawn in the browser; nothing is uploaded.

### No official token yet
NettoLens has not launched a token. Copycat tokens using the NettoLens / Nettochain name and logo have appeared on Pons; the site shows a banner saying so, and scanning a token whose name or symbol uses our name shows a red "Not a NettoLens token" notice and caps its score at 20. If an official token is ever launched, its contract will be posted on nettolens.xyz first and added to the allow-list in the code.

### Same-name tokens (copycats)
Each scan searches the chain's explorer for other tokens with the same name or symbol and checks when they were created. If an older token with the same name exists, the row shows it with a link and a caution signal ("this may be a copy, check which contract the project itself posts"). If this token came first, the row says so. A failed search is shown as unavailable, never as clean. Names can coincide, so this is a caution, not a score penalty.
