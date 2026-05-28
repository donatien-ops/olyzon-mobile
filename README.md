# olyzon-mobile

Static deployment target for the **Olyzon mobile companion** — the agent-first phone surface for CTV operators.

The source app lives in
[`olyzon-tv/saas-design-workspace`](https://github.com/olyzon-tv/saas-design-workspace)
at `src/proto-v2/mobile/`. This repo holds the built static output
(`dist-mobile/`) so a dedicated Vercel project can serve it without
running a build itself.

## Sync workflow

After each PR merge on the upstream app:

```bash
cd /Users/do/code/olyzon-tv/saas-mobile-wt
git pull origin mobile-work-…
npm run build:mobile
cp -r dist-mobile/. /path/to/olyzon-mobile/
cd /path/to/olyzon-mobile
git add -A && git commit -m "sync: build <sha>" && git push
```

Vercel rebuilds automatically on every push to `main`.

## Vercel project

- Framework preset: **Other** (static)
- Build command: leave empty (artifacts are already built)
- Output directory: `.`
- Install command: leave empty

`vercel.json` ships SPA fallback (`/(.*) → /index.html`) and long-cache
headers for hashed assets in `/assets/`.
