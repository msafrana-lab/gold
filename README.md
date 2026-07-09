# Gold Price Dashboard

A single-file, static HTML dashboard showing the **real-time gold spot price** with a built-in **gold-bar value calculator**.

![Static site](https://img.shields.io/badge/type-static%20site-informational)

## Features

- **Live spot price** (USD per troy ounce) from [gold-api.com](https://gold-api.com) — free, no API key required.
- Auto-refreshes every 60 seconds, plus a manual **Refresh** button.
- Derived prices: per gram, per kilogram, per troy ounce.
- **Bar calculator**: for each standard bar type (1 g → 1 kg and a 400 oz Good Delivery bar) it shows the value of one bar, lets you enter how many you hold, and sums a grand total.
- **Graceful fallback**: if the live feed can't be reached, you can type in the current price manually and the calculator keeps working.
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
