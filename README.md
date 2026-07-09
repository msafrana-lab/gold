# Capital Y — Gold Price Dashboard

A single-file, static HTML dashboard showing the **real-time gold spot price** with a built-in **gold-bar value calculator**, styled in the **Capital Y** visual identity (warm rose→coral→orange gradient, sage-green footer, Playfair Display headings over Montserrat body).

![Static site](https://img.shields.io/badge/type-static%20site-informational)

## Features

- **Live spot price** (per troy ounce) from [gold-api.com](https://gold-api.com) — free, no API key required.
- Auto-refreshes every 60 seconds (keeps showing the last good price if a fetch fails), plus a manual **Refresh** button and an up/down change flash.
- **Live currency conversion**: pick USD, CHF, EUR, GBP, JPY, CNY, CAD, AUD, HKD, SGD or INR — every figure converts using a live FX rate from [frankfurter.app](https://www.frankfurter.app) (ECB reference rates). Falls back to USD if the FX feed is unavailable.
- Derived prices: per troy ounce, per kilogram, per gram.
- **Bar calculator**: bar types ordered by most common use (1 oz, 1 kg, 100 g, …). For each it shows the value of one bar, lets you enter how many you hold, and sums a grand total.
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
