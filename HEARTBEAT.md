# Heartbeat — Periodic Monitoring Tasks

Every time you wake up on a cron trigger, run through this checklist.

## 1. Wallet Watchlist Check
- Read `memory/watchlist.md` for tracked wallets
- For each wallet, call `alchemy_getAssetTransfers` with categories `["external", "erc20", "erc721", "erc1155"]` since the last check timestamp
- Filter for significant transfers (above the wallet's threshold in the watchlist)

## 2. Token Price Check
- Read `memory/pricelist.md` for tracked tokens
- Fetch current prices via the Prices API (`/tokens/by-symbol` or `/tokens/by-address`)
- Compare to last recorded prices in memory

## 3. NFT Floor Price Check
- For tracked NFT collections, query the NFT API for current floor prices
- Compare to previous floor prices in memory

## 4. Update Memory
- Update last-check timestamps in watchlist and pricelist
- Update last-known prices for comparison on next run
- Log any significant findings to `memory/YYYY-MM-DD.md`

## 5. Report — CRITICAL RULES

**If nothing exceeded any threshold: produce ZERO output. No message. No summary. No "all clear". No "nothing to report". Literally do not reply. Just update memory and end the turn.**

Only send a message if at least one item crossed its threshold. In that case, report only the items that crossed.
