# avolens-site

The public website for the **AvoLens** mobile app (`app.avolens.mobile`) — landing page plus
the legal pages both app stores require.

Live at **https://sahelummm-cpu.github.io/avolens-site/**

Static HTML served by GitHub Pages. No build step, no framework, no external network
requests of any kind (no CDN, no web font, no analytics) — which is consistent with what the
privacy policy claims about the app.

## Pages

| URL | File | Why it exists |
| --- | --- | --- |
| `/` | `index.html` | Marketing page. Play Console "Website" field. |
| `/privacy/` | `privacy/index.html` | **Required** by Play and the App Store. Play's Data safety form will not submit without it. |
| `/terms/` | `terms/index.html` | Linked from the paywall and onboarding consent line. Required for auto-renewing subscriptions. |
| `/delete-account/` | `delete-account/index.html` | **Required** by Play — a *web* account-deletion path, in addition to the in-app one. Easy to miss; it blocks the release. |
| `/support/` | `support/index.html` | Play Console "Support" contact surface. |

`robots.txt` and `sitemap.xml` are at the root. `404.html` uses absolute paths (GitHub Pages
serves it from any depth) and is the only file that hardcodes the `/avolens-site/` base path.



## Moving to a custom domain

If you buy `avolens.app` (or any domain) and want to serve from it instead:

1. Add a `CNAME` file at the repo root containing just the bare domain, e.g. `avolens.app`
2. At your registrar, point the apex at GitHub Pages
   (`185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`), or a
   `www` CNAME to `sahelummm-cpu.github.io`
3. Repo → Settings → Pages → set the custom domain, and tick **Enforce HTTPS**
4. Search-and-replace `https://sahelummm-cpu.github.io/avolens-site` → `https://avolens.app`
   across `*.html`, `robots.txt` and `sitemap.xml` (canonical, OG and JSON-LD URLs)
5. Fix the five absolute `/avolens-site/...` paths in `404.html`
6. In the **app** repo, update `src/lib/links.ts` — it is the single source of truth for
   every legal and support URL the app opens — then ship a build

## Editing

Open any `.html` file directly in a browser; there is nothing to compile. Keep the legal
pages and the app in agreement: if the app starts collecting something new, the privacy
policy and the Play Data safety form both have to change with it.

The content here is derived from `store/listing/04-COMPLIANCE.md` in the app repo, which was
itself verified against the code. That document is the reference for anything ambiguous.
