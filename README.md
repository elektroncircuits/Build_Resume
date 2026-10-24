# Build Your Resume — Live Gemini edition

A GitHub Pages resume builder with real Google Gemini-powered resume improvements, job tailoring, and cover-letter generation. The Gemini API key stays on a Cloudflare Worker, never in the public website code.

## Files
- `index.html` — the website; publish this to GitHub Pages.
- `worker.js` — backend proxy for Gemini; deploy this as a Cloudflare Worker.

## 1. Create a Gemini API key
1. Open [Google AI Studio](https://aistudio.google.com/app/apikey).
2. Create an API key for Gemini API. Check Google's current pricing and free-tier availability for your account/model before use.
3. Do not paste the key into `index.html`, GitHub, or a public repository.

The Worker uses `gemini-3.5-flash-lite`. If your Google AI Studio account doesn't offer that model, change the `MODEL` constant in `worker.js` to a currently available Gemini API model in your account.

## 2. Deploy the backend on Cloudflare Workers
1. Sign in at [Cloudflare Dashboard](https://dash.cloudflare.com/) and open **Workers & Pages**.
2. Create a Worker, for example `resumecraft-ai-api`.
3. Choose **Edit code** and replace the starter code with the full contents of `worker.js`, then deploy.
4. Open the Worker **Settings → Variables and Secrets** (wording may vary).
5. Add a secret named `GEMINI_API_KEY` and paste your Gemini key as the value. Save/deploy.
6. Add a text variable named `ALLOWED_ORIGIN` with the exact public website origin, for example `https://YOUR-GITHUB-USERNAME.github.io`. If using a project site, the origin is still `https://YOUR-GITHUB-USERNAME.github.io` (not the repository path). For a custom domain, use its origin such as `https://resume.example.com`. Save/deploy.
7. Copy the Worker URL, such as `https://resumecraft-ai-api.YOUR-SUBDOMAIN.workers.dev`.

`ALLOWED_ORIGIN` is a browser-origin check, not full authentication or rate limiting. For a public app, add Cloudflare rate limiting / abuse protection before promoting it widely; otherwise someone could call the endpoint outside your page and consume your API quota.

## 3. Publish the website on GitHub Pages
1. Create a GitHub repository, such as `resumecraft-ai`.
2. Upload `index.html` to the repository root and commit.
3. Go to **Settings → Pages**. Select **Deploy from a branch**, branch `main`, folder `/(root)`, then save.
4. Wait for GitHub Pages to publish the site.

## 4. Connect the site to your AI backend
1. Open your published website.
2. Paste the Worker URL into **Your Cloudflare Worker URL**.
3. Click **Save connection**.
4. Fill in resume details and a target job description, then try **Improve summary with AI**, **Improve experience bullets**, **Tailor to job**, or **Generate cover letter**.

## What each button does
- **Improve summary with AI** — improves the summary and work bullets, then updates the resume fields.
- **Improve experience bullets** — rewrites work bullets and keeps role/company/dates.
- **Tailor to job** — uses the job description to prioritize relevant facts already in your resume; review all output before applying.
- **Generate cover letter** — shows a draft in the app for review/copying.

## Privacy and safety
- AI actions send the resume fields and job description to your Cloudflare Worker and Google Gemini. Do not submit sensitive personal information you don't need in a resume.
- The website stores draft data and the Worker URL in browser local storage. On shared devices, clear local data after use.
- AI can make mistakes. Verify every statement, skill, date, and achievement before sending a resume.
- This app does not guarantee ATS scores, job interviews, or employment.
- The AI features require a working Worker URL and valid Gemini API key. The static site cannot call Gemini securely on its own.
