[README.md](https://github.com/user-attachments/files/31201181/README.md)

# Oyster Farm Tracker

A shared, live layout of your farm — 5 longlines, 450 baskets each — with
click-to-label baskets, bulk selection, CSV export, and data that's shared
across everyone who opens the site.

## Project structure

```
public/index.html   → the whole frontend (grid, panel, all logic)
api/baskets.js       → serverless function: GET loads data, POST saves it
package.json          → declares the @vercel/kv dependency
```

No build step, no framework — Vercel serves `public/` as static files and
`api/` as serverless functions automatically.

## Deploy

1. **Push this folder to a GitHub repo.**
   ```
   git init
   git add .
   git commit -m "Oyster farm tracker"
   git remote add origin <your-repo-url>
   git push -u origin main
   ```

2. **Import the repo into Vercel.**
   Go to [vercel.com/new](https://vercel.com/new), pick your repo, leave the
   framework preset as "Other" — no build settings needed — and deploy.

3. **Create a KV database and connect it.**
   In your Vercel project → **Storage** tab → **Create Database** → choose
   **KV**. When you connect it to this project, Vercel automatically adds
   the required environment variables (`KV_REST_API_URL`,
   `KV_REST_API_TOKEN`, etc.) — you don't need to set anything by hand.

4. **Redeploy.**
   After connecting KV, trigger a redeploy (Vercel usually prompts you to)
   so the new environment variables are picked up.

That's it — the URL Vercel gives you is now a live, shared farm map. Anyone
with the link sees the same baskets and labels, and changes save
automatically as people label baskets.

## Notes

- There's no login — anyone with the link can view and edit. Fine for a
  small crew, worth knowing if you plan to share the link more widely.
- If two people label the same basket at nearly the same moment, the last
  save wins (no conflict merging).
- Local dev: `npm install`, then `vercel dev` (requires the [Vercel
  CLI](https://vercel.com/docs/cli) and a KV database linked via `vercel
  link` + `vercel env pull`).
