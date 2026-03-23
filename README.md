[README.md](https://github.com/user-attachments/files/26195796/README.md)
[README.md](https://github.com/user-attachments/files/26195796/README.md)
# MCE Field Server — Railway Deploy Guide

## Files
- `server.js` — Express server, proxies Anthropic API
- `package.json` — dependencies

## Deploy on Railway (5 minutes)

### Step 1 — Create GitHub repo
```
git init
git add .
git commit -m "MCE Field Server"
git push origin main
```

### Step 2 — Deploy on Railway
1. Go to railway.app → New Project
2. Deploy from GitHub → select your repo
3. Railway auto-detects Node.js and runs `npm start`

### Step 3 — Set Environment Variable
In Railway dashboard → Variables → Add:
```
CLAUDE_API_KEY = sk-ant-...your key here...
```

### Step 4 — Get URL
Railway gives you a URL like:
```
https://mce-field-server-production.up.railway.app
```

Send this URL to Mos — he updates one line in the React app.

## Test (after deploy)
```bash
curl https://YOUR-URL.railway.app/

curl -X POST https://YOUR-URL.railway.app/chat \
  -H "Content-Type: application/json" \
  -d '{"messages":[{"role":"user","content":"hello"}],"system":"You are Claude."}'
```

Expected response:
```json
{
  "text": "Hello! How can I help you?",
  "phase": "HYDROGEN",
  "model": "claude-sonnet-4-20250514"
}
```

## Local test (before Railway)
```bash
npm install
export CLAUDE_API_KEY=sk-ant-...
npm start
# Server runs on http://localhost:3000
```
