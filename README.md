# pareapps.com

The Pare Apps website: a home page for every app, a page per app, support, and
a privacy policy per app. Plain HTML and CSS — no build step.

Hosted on GitHub Pages from the `main` branch: each push publishes the site.

- `index.html` — home
- `myday/`, `weatherpare/`, `savepare/` — app pages, each with a `privacy/` policy
- `privacy/` — lists every app's policy
- `support/` — contact and FAQ
- `assets/css/site.css` — every page's styles
- `assets/img/` — icons and screenshots

Preview locally with `python3 -m http.server 8787` and open http://localhost:8787.

**How to make changes** — App Store links, new apps, privacy policies,
screenshots, DNS — is in [CLAUDE.md](CLAUDE.md).
