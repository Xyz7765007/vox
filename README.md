# Voxelised Command Center

Single-screen ops dashboard for Voxelised. Static HTML, zero build step. Hosted on Vercel.

Live: _add your deployed URL here after first deploy_

---

## Stack

Pure HTML + CSS + vanilla JS in one file. No framework, no build. Google Fonts loaded via CDN. That's it.

If you ever want to move to Next.js / React, see `voxelised-dashboard-brief.md` in your docs folder for the full spec.

---

## Local dev

Open `index.html` in a browser. Done.

Or, if you want a proper local server (fonts can behave oddly when opened as `file://`):

```bash
npx serve .
```

---

## Deploy: option A — CLI (fastest, ~2 minutes)

Assumes you have Git, GitHub CLI (`gh`), and Vercel CLI (`vercel`) installed.

```bash
# from the project folder
git init
git add .
git commit -m "initial: voxelised command center"

# create github repo and push
gh repo create voxelised-command-center --public --source=. --remote=origin --push

# deploy to vercel (first time: will prompt for project setup, accept defaults)
vercel --prod
```

Vercel auto-detects this as a static site. No config needed.

Subsequent deploys:

```bash
git add .
git commit -m "your message"
git push
# vercel auto-deploys on push once the github repo is linked in the vercel dashboard
```

To link the GitHub repo for auto-deploy on push: go to vercel dashboard → project → Settings → Git → Connect Git Repository.

---

## Deploy: option B — GitHub web + Vercel web (no CLI)

1. Go to https://github.com/new and create a new repository called `voxelised-command-center` (public or private, your call).
2. On the empty repo page, click "uploading an existing file". Drag in `index.html`, `README.md`, and `.gitignore`.
3. Commit directly to main.
4. Go to https://vercel.com/new.
5. Import your `voxelised-command-center` repo.
6. Framework Preset: leave as "Other" (Vercel auto-detects static).
7. Root directory: leave blank.
8. Build command: leave blank.
9. Output directory: leave blank.
10. Click Deploy.

Done in about 30 seconds. Every push to main from then on auto-deploys.

---

## Custom domain

In the Vercel project dashboard:

1. Settings → Domains
2. Add your domain (e.g., `dashboard.voxelised.com`)
3. Vercel shows DNS records to add at your registrar
4. Add the CNAME or A record and wait for propagation (usually minutes)

---

## File structure

```
voxelised-command-center/
├── index.html        # the entire dashboard, self-contained
├── README.md
└── .gitignore
```

---

## Notes

- The viewport is fixed at 1440px (`<meta name="viewport" content="width=1440">`). This is a desktop-only dashboard. If you want responsive, the full brief in `voxelised-dashboard-brief.md` covers grid collapse behavior.
- Data is all dummy. When you wire up real data sources (Smartlead, LinkedIn automation, GA4, HubSpot, ClickUp), you'll need to move to a Next.js setup with API routes. The static HTML is a design prototype, not a data-fed production dashboard.
- The cursor spotlight and ECG animation are both running on `requestAnimationFrame` / `setInterval`. They pause cleanly when the browser tab is backgrounded.
