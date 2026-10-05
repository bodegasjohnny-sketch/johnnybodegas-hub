# johnnybodegas-hub

One-screen card hub for **johnnybodegas.com** (apex). Static HTML + CSS, no build step, no secrets.
It links out to Johnny Bodegas' live properties. The client portfolio stays on its own subdomain
(`portfolio.johnnybodegas.com`, Lovable) and is **not** part of this repo.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The hub: header, one-liner, 7 cards (all open in a new tab, `rel="noopener noreferrer"`) |
| `styles.css` | Cream / charcoal theme matching the portfolio (Space Grotesk + IBM Plex), auto dark mode |
| `favicon.svg` | "JB" mark |
| `.nojekyll` | Serve files as-is on GitHub Pages |

To edit a card, change its `<a class="card">` block in `index.html`. Commit to `main`; Pages redeploys in ~1 minute.

## Preview

- Live preview (GitHub Pages): https://bodegasjohnny-sketch.github.io/johnnybodegas-hub/
- Local: open `index.html` in a browser, or `python3 -m http.server` in this folder.

## Hosting: GitHub Pages (Settings → Pages → Deploy from branch → `main` / root)

## Point johnnybodegas.com at this hub

DNS for `johnnybodegas.com` is at **GoDaddy** (nameservers `ns49/ns50.domaincontrol.com`).
Today the apex `A` record (`162.159.140.166`) and `www` (`CNAME sites.ludicrous.cloud`) serve the old trading page.

**Only change the records below. Leave every other record alone**, especially:
`portfolio` (A `185.158.133.1`, Lovable), `videoproductionengine`, `app`, `MX smtp.google.com` (email for info@),
and the `TXT` records (SPF + Google site verification).

1. GoDaddy → My Products → `johnnybodegas.com` → **DNS**.
2. Delete the apex `A @ → 162.159.140.166` record (and any other `A`/`AAAA` on `@`).
   If GoDaddy shows **Forwarding** set for the domain, remove it too.
3. Add four `A` records, Name `@`, TTL 1 hour (or 600 s):
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
4. Edit `CNAME www` → `bodegasjohnny-sketch.github.io` (replace `sites.ludicrous.cloud`).
5. GitHub → this repo → **Settings → Pages → Custom domain** → `johnnybodegas.com` → Save.
   (This commits a `CNAME` file. Do it *after* step 3 so the github.io preview doesn't redirect to the old site.)
6. Wait for the DNS check to go green (minutes to a few hours), then tick **Enforce HTTPS**.
7. Verify: `https://johnnybodegas.com` and `https://www.johnnybodegas.com` show the hub,
   and `https://portfolio.johnnybodegas.com` still shows the portfolio.

Optional: once the hub is live, cancel/disconnect the old trading-page host (ludicrous.cloud) so it stops claiming the domain.
