# Exchange fee data

What instant crypto exchanges actually deliver, measured on their own public websites and published as raw rows.

Every figure Cambio publishes about another exchange comes from this data. It is here so anyone can check the arithmetic, disagree with it, or use it for their own work.

## What is in here

```
data/<YYYY-MM>-<route>/
  website-checks.csv   one row per check of an exchange's own website
  cambio-quotes.csv    one row per Cambio quote on the same route
```

Each dated folder is written once and never edited. A later correction arrives as a new folder, not as a change to an old one.

### `website-checks.csv`

| column | meaning |
|---|---|
| `exchange` | the exchange checked |
| `band_usd` | the size asked for, in US dollars: 200, 1000 or 5000 |
| `sent_btc` | the amount of the source coin used for that check |
| `received_usdt` | what the exchange's own website said it would deliver |
| `market_usdt` | the market price at the same moment (Binance), for the same amount |
| `pct_below_market` | how far `received_usdt` sits below `market_usdt`, in percent |
| `checked_at_utc` | when the check was made, UTC, ISO 8601 |

### `cambio-quotes.csv`

| column | meaning |
|---|---|
| `exchange` | always `Cambio` |
| `sent_btc` | the amount quoted |
| `received_usdt` | what Cambio's quote said it would deliver |
| `stated_network_fee_usdt` | the network fee stated on that quote, already taken out of `received_usdt` |
| `quoted_at_utc` | when the quote was made, UTC, ISO 8601 |

## How the checks are made

- A small server, separate from Cambio's site, asks each exchange's own public website for a floating-rate quote, once an hour, at three sizes.
- The market price is read from Binance at the same moment as the check.
- `received_usdt` is what the exchange said would arrive, so its margin and its withdrawal fee are already inside the number. That is the point: the cost of a swap is what lands in your wallet.

## What this data cannot tell you

- **These are quotes, not completed swaps.** A floating rate can move between the quote and the payout, in either direction.
- **A quote is not a promise.** Minimums, verification checks and network conditions can change what an exchange actually pays.
- **The sample is small and dated.** Each folder covers a few days on one route. Read it as observations with timestamps, not as a league table of exchanges.
- **Cambio is one of the parties measured here.** The Cambio rows come from its own quotes, recorded the same way. Check them against the exchanges' rows yourself; that is why both files are published.

## Publications using this data

- *What $200 and $1,000 of BTC → USDT on Tron really cost: 716 checks of five exchanges* (16–18 Sep 2026) — https://cambio.one/blog/btc-to-usdt-real-cost-at-five-exchanges-september-2026?utm_source=github&utm_medium=dataset&utm_campaign=exchange-fee-data-2026-09
- *What $200 and $1,000 of BTC → USDT really cost: 546 checks of three exchanges* (13–15 Sep 2026, superseded by the five-exchange measurement above; the folder stays as published) — https://cambio.one/blog/btc-to-usdt-real-cost-at-five-exchanges-september-2026?utm_source=github&utm_medium=dataset&utm_campaign=exchange-fee-data-2026-09

## Corrections

Found a mistake? Open an issue, or write to support@cambio.one. Corrections are published, including when they are ours.

## Licence

CC BY 4.0 — use it, including commercially, with credit to Cambio (https://cambio.one/?utm_source=github&utm_medium=dataset&utm_campaign=exchange-fee-data-2026-09). See [LICENSE](LICENSE).
