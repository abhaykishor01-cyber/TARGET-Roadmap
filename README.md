# Waypoint — Deploy to Vercel

This folder is a ready-to-deploy Vercel project:
- `index.html` — the site
- `api/analyze.js` — serverless function that securely calls the Anthropic API (keeps your key off the browser)
- `package.json` — lets Vercel detect this as a Node project

## 1. Get an Anthropic API key (~2 minutes)

1. Go to https://console.anthropic.com
2. Sign up / log in
3. Go to **Settings → API Keys → Create Key**
4. Copy the key (starts with `sk-ant-...`) — you won't be able to see it again, so save it somewhere safe
5. Note: you'll need a small amount of credit on the account (a few dollars covers a lot of roadmap generations) — add billing under **Settings → Billing**

## 2. Deploy to Vercel

**Easiest path — no command line, using the Vercel dashboard:**

1. Go to https://vercel.com and sign up / log in (GitHub login is easiest)
2. Put this folder in a GitHub repo:
   - Create a new repo on GitHub
   - Upload these three items (`index.html`, `api/analyze.js`, `package.json`) keeping the same folder structure
3. In Vercel, click **Add New → Project**, and import that GitHub repo
4. Before deploying, expand **Environment Variables** and add:
   - Name: `ANTHROPIC_API_KEY`
   - Value: *(paste your key from step 1)*
5. Click **Deploy**

That's it — Vercel will give you a live URL like `https://waypoint-yourname.vercel.app`.

**Alternative — using the Vercel CLI:**

```bash
npm install -g vercel
cd waypoint-deploy
vercel
# follow the prompts, accept defaults

# then add your key:
vercel env add ANTHROPIC_API_KEY
# paste your key when prompted, select "Production"

# redeploy so the env var takes effect:
vercel --prod
```

## 3. Custom domain (optional)

In the Vercel dashboard → your project → **Settings → Domains**, add your own domain and follow the DNS instructions shown.

## Notes

- The serverless function (`api/analyze.js`) is what keeps your API key private — never put the key directly in `index.html`.
- Vercel's free tier is plenty for personal/small-scale use.
- If you ever see "Server is missing ANTHROPIC_API_KEY" on the live site, it means the environment variable wasn't set (or you need to redeploy after adding it).
