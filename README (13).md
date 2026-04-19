# ⛽ GasFinder — Live Gas Prices Near UMD College Park

Live auto-refreshing gas price finder powered by Claude AI. Single HTML file, deploys free to GitHub Pages.

---

## 🚀 Setup Guide (~5 minutes)

### Step 1 — Create GitHub repo
1. Go to https://github.com/new
2. Name it `gasfinder`, set **Public**, click **Create repository**

### Step 2 — Upload files
Upload `index.html` and `README.md` to the repo root (drag & drop on GitHub works).

### Step 3 — Add your API secret
1. Repo → **Settings → Secrets and variables → Actions**
2. Click **New repository secret**
3. Name: `ANTHROPIC_API_KEY`
4. Value: your Claude API key from https://console.anthropic.com
5. Click **Add secret**

### Step 4 — Enable GitHub Pages
1. Repo → **Settings → Pages**
2. Source → **GitHub Actions** → Save

### Step 5 — Deploy
Go to **Actions → Build & Deploy GasFinder → Run workflow**
(Or just push any commit — auto-deploys every time)

### Step 6 — Visit your site
```
https://YOUR_USERNAME.github.io/gasfinder
```

---

## How secret injection works

The `deploy.yml` workflow replaces `__ANTHROPIC_API_KEY__` in `index.html` with your secret at build time — your key is never stored in source code.
