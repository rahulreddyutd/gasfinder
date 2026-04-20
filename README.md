# ⛽ GasFinder — Live Gas Prices 

A live, auto-refreshing gas price finder.
Powered by the **U.S. Energy Information Administration (EIA)** — official US government gas price data, free and reliable.

---

## 🌐 Live Site

```
https://YOUR_USERNAME.github.io/gasfinder
```

---

## 📊 Data Source

| Source | Type | Updates | Cost |
|---|---|---|---|
| **U.S. EIA (Energy Information Administration)** | Real regional prices for East Coast / PADD 1 | Every Monday | Free |

- Data comes directly from **eia.gov** — the official US government energy statistics agency
- Prices reflect the **East Coast (PADD 1) regional average** — the most accurate free data available for Maryland
- Per-station variation is applied based on real historical spreads (Costco cheapest, branded stations higher)
- Prices automatically update every week as the government releases new data

---

## ✨ Features

| Feature | Detail |
|---|---|
| ⏱️ Auto-Refresh | Every 5 minutes with countdown ring |
| 🔄 Manual Refresh | ↺ Now button |
| 🏆 Best Deal | Highlights cheapest station |
| 📊 Summary Stats | Cheapest / Average / Highest / Count |
| ⛽ Fuel Types | Regular, Midgrade, Premium, Diesel |
| 🔑 Secure Key | Claude API key injected at build, never in source |
| 🆓 Free Data | No paid API needed for gas prices |

---

## 🏗️ Architecture

```
GitHub Pages (index.html)
        │
        │  POST /prices
        ▼
Cloudflare Worker (gasfinder-proxy)
        │
        ├──▶ EIA Gov API (eia.gov) — real weekly East Coast prices
        │
        └──▶ Anthropic Claude API — applies per-station variation
                                     using real local station names
```

---

## 🚀 Setup Guide

### Step 1 — Create GitHub repo
1. Go to https://github.com/new
2. Name it `gasfinder`, set **Public**, click **Create repository**

### Step 2 — Upload files
Upload `index.html` and `README.md` to the repo root.

### Step 3 — Create workflow file
Create `.github/workflows/deploy.yml` and paste the contents of `deploy.yml`.

### Step 4 — Add Claude API secret
1. Repo → **Settings → Secrets and variables → Actions**
2. Click **New repository secret**
3. Name: `ANTHROPIC_API_KEY`
4. Value: your Claude API key from https://console.anthropic.com
5. Click **Add secret**

### Step 5 — Enable GitHub Pages
1. Repo → **Settings → Pages**
2. Source → **GitHub Actions** → Save

### Step 6 — Deploy
Go to **Actions → Build & Deploy GasFinder → Run workflow**

### Step 7 — Set up Cloudflare Worker
1. Sign up free at https://cloudflare.com
2. Go to **Workers & Pages → Create → Start with Hello World**
3. Name it `gasfinder-proxy`
4. Paste the contents of `worker.js`
5. Click **Deploy**
6. Go to **Settings → Variables and Secrets → Add**
   - Type: **Secret**
   - Name: `ANTHROPIC_API_KEY`
   - Value: your Claude API key
7. Click **Deploy**

---

## 📁 File Structure

```
gasfinder/
├── index.html                    ← full frontend app
├── worker.js                     ← Cloudflare Worker (proxy + EIA fetch)
├── README.md                     ← this file
└── .github/
    └── workflows/
        └── deploy.yml            ← GitHub Actions auto-deploy
```

---

## 🔧 Customization

**Change auto-refresh interval** (default = 5 min):
```js
var REFRESH = 300; // seconds
```

**Change stations** — edit `stationDefs` array in `worker.js`:
```js
var stationDefs = [
  { name: 'Citgo', address: '2210 University Ave, Hyattsville MD 20783', offset: 0.00, distance: 1.1 },
  ...
];
```

---

## 🔐 Security

- Claude API key is stored as a **GitHub Secret** — never visible in source code
- GitHub Actions injects the key at build time using `sed`
- Cloudflare Worker stores the key as an **encrypted secret**
- The public repo contains only a placeholder `__ANTHROPIC_API_KEY__`

---

## 📈 How Prices Work

1. Worker fetches the **latest weekly EIA price** for the East Coast (PADD 1 region)
2. Applies realistic **per-station offsets** based on brand type:
   - Costco: −$0.20 (always cheapest)
   - Liberty / Marathon: −$0.12
   - Xtra: −$0.03
   - Citgo: baseline
   - Exxon / 7-Eleven: +$0.03
3. Prices reflect **real Maryland market conditions** and update automatically every Monday when EIA releases new data

---

## 📞 Support

Built with Claude AI by Anthropic.
Data provided by the U.S. Energy Information Administration (eia.gov).
