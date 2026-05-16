# Zoomlion Tractor Advisor 🚜
**Bilingual (EN / 中文) AI-powered model recommendation system**

No Claude account required for end users. The API key stays on the server.

---

## Quick Start (Local)

### 1. Install Node.js
Download from https://nodejs.org (v18 or newer recommended)

### 2. Install dependencies
```bash
npm install
```

### 3. Set your API key
```bash
cp .env.example .env
```
Open `.env` and replace the placeholder with your real key from https://console.anthropic.com

### 4. Run the server
```bash
npm start
```

Open http://localhost:3000 — works without any Claude account.

---

## Deployment Options

### Option A — VPS / Cloud Server (recommended)
Any Linux server (Ubuntu, Debian, etc.):

```bash
# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# Upload files, then:
npm install
cp .env.example .env
nano .env   # add your API key

# Run with PM2 (keeps it alive after reboot)
npm install -g pm2
pm2 start server.js --name zoomlion-advisor
pm2 save
pm2 startup
```

### Option B — Railway.app (easiest, free tier available)
1. Create account at https://railway.app
2. New Project → Deploy from GitHub (or upload zip)
3. Add environment variable: `ANTHROPIC_API_KEY=sk-ant-...`
4. Deploy — Railway gives you a public URL automatically

### Option C — Render.com (free tier available)
1. Create account at https://render.com
2. New → Web Service → connect your repo
3. Build command: `npm install`
4. Start command: `node server.js`
5. Add `ANTHROPIC_API_KEY` in Environment Variables
6. Deploy

### Option D — Heroku
```bash
heroku create zoomlion-advisor
heroku config:set ANTHROPIC_API_KEY=sk-ant-...
git push heroku main
```

---

## File Structure
```
zoomlion-advisor/
├── server.js          ← Express server + API proxy (API key stays here)
├── public/
│   └── index.html     ← Full frontend UI (no framework needed)
├── package.json
├── .env               ← Your API key (never commit this!)
├── .env.example       ← Template
└── README.md
```

---

## Security Notes
- The `ANTHROPIC_API_KEY` is **only used server-side** — never exposed to the browser
- Add rate limiting for production use (e.g. `express-rate-limit` package)
- Optionally add basic auth if you want to restrict access

---

## Costs
Each conversation turn uses ~1,000–1,500 tokens (input + output).
With `claude-sonnet-4-20250514`, this is approximately $0.003–0.005 per message.
