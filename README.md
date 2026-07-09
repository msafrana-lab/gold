# Capital Y — Gold Price Dashboard

A single-file, static HTML dashboard showing the **real-time gold spot price** with a built-in **gold-bar value calculator**, styled in the **Capital Y** visual identity (warm rose→coral→orange gradient, sage-green footer, Playfair Display headings over Montserrat body).

![Static site](https://img.shields.io/badge/type-static%20site-informational)

## Features

- **Live spot price** (per troy ounce) from [gold-api.com](https://gold-api.com) — free, no API key required.
- Auto-refreshes every 60 seconds (keeps showing the last good price if a fetch fails), plus a manual **Refresh** button and an up/down change flash.
- **Currency conversion**: pick USD, CHF, EUR, GBP, JPY, CNY, CAD, AUD, HKD, SGD or INR — every figure converts using an FX rate fetched from a resilient chain of free sources ([frankfurter.dev](https://frankfurter.dev) ECB → exchangerate-api → currency-api), with the rate's "as of" date shown. Falls back to USD only if every source is unreachable.
- **CHF (and any) price is a proper cross**: the 1 kg bar's CHF price is `live gold (USD/oz) × USD/CHF` — the same cross as Bloomberg's XAUCHF (there is no separate CHF gold market). The page states whether the FX leg is live or end-of-day.
- **Live quote on demand** (`METALS_API_KEY`, [metals.dev](https://metals.dev)): the free tier allows only ~100 requests/month, so it is **never polled on a timer**. Instead, clicking **Refresh price** spends one request to pull an authoritative **live** gold + live-FX snapshot (a true live CHF cross) — ideal for checking a broker quote. Auto-refresh always stays on the free feed; a double-click guard prevents accidental double-spend, and it falls back cleanly with a notice if the quota is exhausted.
- **Optional continuous live FX** (`FX_API_KEY`, [Twelve Data](https://twelvedata.com), free 800/day): makes the FX leg intraday on a ~3 min cadence (paused when the tab is hidden) so the auto-refreshed CHF cross is live too.
- Keys in a static page are visible in the source — both providers let you rotate/restrict them.
- **Clean spot reference**: the headline is the raw **USD per troy ounce** international benchmark — no conversion baked in.
- **Gold value table** (1 troy ounce + 1 kg bar): each unit shows its **reference price in its native currency** (the ounce in USD, the 1 kg bar in CHF as Swiss desks quote it) *and* a separate **account-currency** column driven by the top selector — so the conversion is explicit, not hidden. Enter quantities to get subtotals and a total in the account currency.
- **Broker Quote Analyzer**: cross-checks a dealer's quote and compares two execution paths — selling directly in the local currency (e.g. CHF) vs. selling in USD and converting separately via a treasury FX desk. It computes the all-in cost of each in basis points, recommends the cheaper path, and **reverse-engineers the spread**: the metal bid-ask vs spot, the USD/CHF rate embedded in the dealer's local-currency quote, and the hidden FX markup (in pips and bps). Settlement currency and bar size are selectable; defaults to the 30 × 1 kg USD-vs-CHF case.
- **Mobile-first**: on phones the calculator reflows into stacked cards (no sideways scroll) with large, touch-friendly inputs.
- **Graceful fallback**: if the price feed can't be reached, you can type in the current price manually and the calculator keeps working.
- No build step, no dependencies, no tracking — just one `index.html`.

## Run locally

Open `index.html` in any browser, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Publish with GitHub Pages

1. Push this repository to GitHub (already done for this branch).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Select the branch (e.g. `main` after merging) and the `/ (root)` folder, then **Save**.
5. After a minute the site is live at:
   `https://<your-username>.github.io/<repo-name>/`

## Notes

- The gold price is per **troy ounce** (31.1034768 g), the standard unit for precious metals.
- Values reflect the pure-gold spot price; physical bars are typically sold with a dealer premium.
- For information only — not investment advice.
