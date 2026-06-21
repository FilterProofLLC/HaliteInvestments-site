# haliteinvestments-site

Static website for **Halite Investments LLC**, featuring the **HaliteHomes** app.
Plain HTML/CSS — no backend, no build step, no JavaScript dependencies, no
analytics/cookies/tracking. Intended to live at **https://haliteinvestments.com**
and to satisfy Google Play organization website verification, Google Search
Console ownership, and the HaliteHomes privacy/support URLs.

## Pages

| Path | Purpose |
| --- | --- |
| `/` | Company landing page |
| `/halitehomes/` | HaliteHomes product page |
| `/privacy/` | Privacy policy (Google Play privacy URL) |
| `/support/` | Support page (Google Play support URL) |
| `/terms/` | Terms / disclaimer |
| `/404.html` | Branded not-found page |

Support files: `CNAME`, `robots.txt`, `sitemap.xml`, `favicon.ico` +
`/assets/*` (logo, emblem, favicon, apple-touch-icon, OG image), `.nojekyll`.

## Local preview

No build needed. From the repo root:

```bash
python3 -m http.server 8080
# open http://localhost:8080/
```

## Deployment method: GitHub Pages from the `main` branch (root)

This site is **plain static files**, so it deploys most simply via **Settings →
Pages → Build and deployment → Source: “Deploy from a branch” → Branch: `main` /
root**. No GitHub Actions workflow is required (fewer moving parts, easiest
long-term maintenance — the stated goal). `.nojekyll` is included so GitHub
serves the files as-is.

> A GitHub Actions Pages workflow is an alternative if a build step is ever
> added, but it is unnecessary for static HTML and would also require extra
> token permissions to commit, so it was intentionally not used.

### One-time repository setup
1. Push this repo to GitHub (see below).
2. Repo **Settings → Pages**:
   - **Source:** Deploy from a branch
   - **Branch:** `main`, folder `/ (root)` → **Save**
3. Under **Custom domain**, enter `haliteinvestments.com` → **Save**. (The
   `CNAME` file already pins this; GitHub will read it.)
4. After DNS is configured and verified, tick **Enforce HTTPS**.

## Custom domain & DNS

We use the apex domain `haliteinvestments.com` plus `www`. The `CNAME` file in
this repo tells GitHub Pages the canonical custom domain — keep it as
`haliteinvestments.com`.

At your domain registrar / DNS provider, add these records (values are GitHub’s
published Pages addresses; confirm against GitHub’s docs at deploy time):

**Apex `haliteinvestments.com` → four A records:**
```
A   @   185.199.108.153
A   @   185.199.109.153
A   @   185.199.110.153
A   @   185.199.111.153
```
**Optional IPv6 (AAAA):**
```
AAAA  @  2606:50c0:8000::153
AAAA  @  2606:50c0:8001::153
AAAA  @  2606:50c0:8002::153
AAAA  @  2606:50c0:8003::153
```
**`www` subdomain → CNAME to the GitHub Pages host:**
```
CNAME   www   <your-github-owner>.github.io.
```
(For owner `FilterProofLLC`, that is `filterproofllc.github.io.`)

DNS changes can take from minutes to ~48 hours to propagate. GitHub Pages will
provision a TLS certificate automatically once the domain resolves; then enable
**Enforce HTTPS**.

> **Owner note:** the repo currently lives under the **FilterProofLLC** GitHub
> account (the only owner available). This does **not** affect the public
> address — with the custom domain configured, the site still serves at
> **https://haliteinvestments.com**.

## Google Search Console verification
1. Go to **Google Search Console** → **Add property** → **Domain** →
   `haliteinvestments.com`.
2. Copy the **TXT** verification record Google shows.
3. Add that TXT record at your registrar/DNS provider (host `@`).
4. Wait for DNS propagation.
5. Click **Verify** in Search Console.

## Google Play Console — organization website verification
1. Complete Search Console domain verification above.
2. In **Google Play Console**, open the organization/website settings.
3. Enter `https://haliteinvestments.com` as the organization website.
4. Submit verification. (Google may cross-check Search Console ownership and/or
   ask for an additional DNS/file check — follow the on-screen prompt.)

### URLs to paste into Play Console (live after deployment)
- Privacy policy: `https://haliteinvestments.com/privacy/`
- Support / contact: `https://haliteinvestments.com/support/`
- Website: `https://haliteinvestments.com/`

## Placeholders to confirm
- **`support@haliteinvestments.com`** — used on the Privacy and Support pages.
  Configure this mailbox (or replace with the real support address) before
  submitting to Google Play.

## Editing
Every page is a standalone HTML file sharing `/styles.css`. Update the year or
copy directly; commit to `main` and GitHub Pages redeploys automatically.
