# ⛽ GasFinder — Live Gas Prices Near You

A live, auto-refreshing gas price finder for any US city. Search any location and instantly find the cheapest gas stations nearby — powered by real US government price data.

🌐 **Live Site:** https://rahulreddyutd.github.io/gasfinder

---

## 📊 How It Works

1. **Search** any US city, ZIP code, or use GPS
2. **Worker fetches** the latest weekly price from the US EIA (Energy Information Administration)
3. **Claude AI** generates real local station names and addresses with prices based on the EIA baseline
4. **Prices auto-refresh** every 5 minutes

```
Browser (GitHub Pages)
       │
       ▼
Cloudflare Worker
       │
       ├──▶ EIA.gov API  →  real weekly regional gas price
       │
       └──▶ Anthropic Claude  →  real local stations + addresses
```

---

## ✨ Features

- 🔍 Search any US city, state, or ZIP code
- 🛰️ GPS detection with one click
- 🏛️ Real prices from US Energy Information Administration (EIA.gov)
- 📡 Correct regional pricing (East Coast, Midwest, Gulf Coast, West Coast, Rockies)
- ⏱️ Auto-refreshes every 5 minutes with countdown ring
- 🏆 Best Deal card highlighting the cheapest station
- 📊 Summary stats — cheapest, average, highest, station count
- ⛽ Regular, Midgrade, Premium, Diesel
- 🔵 2, 5, 10, 15 mile radius
- 🔐 API key secured via GitHub Secrets — never in source code

---

## 📁 File Structure

```
gasfinder/
├── index.html                 ← full frontend app
├── worker.js                  ← Cloudflare Worker (EIA + Claude proxy)
├── README.md                  ← this file
└── .github/
    └── workflows/
        └── deploy.yml         ← GitHub Actions auto-deploy
```

---

## 🔧 Customization

**Change auto-refresh interval** in `index.html`:
```js
var REFRESH = 300; // seconds (300 = 5 minutes)
```

**Change default radius** in `index.html`:
```js
var radius = 5; // miles
```

---

## 🔐 Security

- Claude API key stored as **GitHub Secret** — never committed to code
- GitHub Actions replaces `__ANTHROPIC_API_KEY__` placeholder at build time
- Cloudflare Worker stores key as **encrypted environment secret**

---

## 🏛️ Data Sources

| Data | Source | Updates |
|---|---|---|
| Regional gas prices | [US EIA](https://www.eia.gov) — official US government | Weekly (every Monday) |
| Station names & addresses | Claude AI based on real local knowledge | Every refresh |
| Location search & GPS | OpenStreetMap Nominatim | Real-time |

---

## 🛠️ Built With

- Vanilla HTML / CSS / JavaScript
- [Cloudflare Workers](https://workers.cloudflare.com) — serverless proxy
- [US EIA Open Data API](https://www.eia.gov/opendata/) — free government gas prices
- [Anthropic Claude](https://anthropic.com) — AI for local station data
- [OpenStreetMap Nominatim](https://nominatim.org) — free geocoding
- [GitHub Pages](https://pages.github.com) — free hosting
- [GitHub Actions](https://github.com/features/actions) — CI/CD deploy
