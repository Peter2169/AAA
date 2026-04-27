# AnyPromo AI Chat Assistant

Powered by Claude — deployed on Vercel with a secure serverless proxy.

## Project Structure

```
anypromo-ai/
├── api/
│   └── chat.js          ← Serverless function (API key lives here, server-side)
├── public/
│   └── index.html       ← Frontend widget (no API key exposed)
├── vercel.json          ← Vercel routing config
├── package.json
└── README.md
```

## Deploy to Vercel (5 minutes)

### Step 1 — Push to GitHub
1. Create a new GitHub repo (can be private)
2. Upload all files maintaining the folder structure above
3. Push to main branch

### Step 2 — Connect to Vercel
1. Go to https://vercel.com and sign in (free account)
2. Click **"Add New Project"**
3. Import your GitHub repo
4. Click **Deploy** (don't change any settings)

### Step 3 — Add your API Key
1. In Vercel dashboard → your project → **Settings → Environment Variables**
2. Add:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** your key from https://console.anthropic.com
   - **Environment:** Production, Preview, Development (check all three)
3. Click **Save**
4. Go to **Deployments** → click **Redeploy** (so the new env var takes effect)

### Step 4 — Done!
Your site will be live at `https://your-project.vercel.app`

## Embed on AnyPromo.com

To embed the chat widget on your existing site instead of as a standalone page,
add this iframe anywhere in your HTML:

```html
<iframe
  src="https://your-project.vercel.app"
  style="position:fixed; bottom:0; right:0; width:420px; height:680px; border:none; z-index:9999;"
  allow="clipboard-write"
></iframe>
```

## Updating the AI's Knowledge

The system prompt (product knowledge, ASI research, swag guides) lives in:
`api/chat.js` — at the top in the `SYSTEM_PROMPT` constant.

Edit it there, push to GitHub, and Vercel auto-deploys within ~30 seconds.

## Costs

- **Vercel hosting:** Free (Hobby plan is sufficient)
- **Anthropic API:** ~$0.003 per 1K tokens
  - Each conversation exchange ≈ $0.002–0.005
  - 1,000 conversations/month ≈ $3–5

## Security

- The API key is stored as a Vercel environment variable — never in the browser
- Users cannot see or extract the key from the frontend
- To restrict access to your domain only, change `'*'` in `api/chat.js` to:
  `'https://www.anypromo.com'`
