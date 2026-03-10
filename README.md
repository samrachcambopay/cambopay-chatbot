# CamboPay API Assistant — Deployment Guide

A secure AI chatbot for CamboPay TOPUP Service SOAP API V2.
The Anthropic API key is stored **server-side only** and never exposed to the browser.

---

## Deploy to Render.com (Free — Recommended)

### Step 1 — Push to GitHub
1. Go to https://github.com/new and create a **new public repository** (e.g. `cambopay-chatbot`)
2. Upload all files from this folder to the repository root:
   - `server.js`
   - `package.json`
   - `systemPrompt.js`
   - `.gitignore`
   - `public/index.html`

### Step 2 — Create a Render Web Service
1. Go to https://render.com and sign up (free)
2. Click **"New +"** → **"Web Service"**
3. Connect your GitHub account and select the `cambopay-chatbot` repo
4. Fill in the settings:
   - **Name:** `cambopay-chatbot` (or any name)
   - **Runtime:** `Node`
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
   - **Instance Type:** `Free`

### Step 3 — Set the API Key (Secret)
1. In the Render dashboard, go to your service → **"Environment"**
2. Click **"Add Environment Variable"**
3. Set:
   - **Key:** `ANTHROPIC_API_KEY`
   - **Value:** your Anthropic API key (starts with `sk-ant-...`)
4. Click **Save** — Render will restart the service automatically

### Step 4 — Done!
Your chatbot will be live at:
`https://your-service-name.onrender.com`

---

## Local Development

```bash
# 1. Install dependencies
npm install

# 2. Create your .env file
cp .env.example .env
# Edit .env and add your ANTHROPIC_API_KEY

# 3. Run locally
npm start
# Open http://localhost:3000
```

---

## Project Structure

```
cambopay-chatbot/
├── server.js          # Express backend (holds API key securely)
├── systemPrompt.js    # CamboPay knowledge base (server-side only)
├── package.json
├── .gitignore
├── .env.example
└── public/
    └── index.html     # Frontend chatbot UI
```

## Security

- The `ANTHROPIC_API_KEY` is stored as a Render environment variable — never in code
- The frontend calls `/api/chat` (your own server), not Anthropic directly
- The system prompt with CamboPay documentation lives on the server, not in the browser
