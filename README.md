# pareapps.com

The PareApps website: a home page for every app, a page per app, support and
the privacy policy. Plain HTML and CSS — no build step.

Hosted on GitHub Pages from the `main` branch: each push publishes the site.
`CNAME` names the custom domain; `.nojekyll` serves the files as they are.
`home/`, `my-day/` and `privacy-policy/` redirect old or short links.

- `index.html` — home
- `myday/`, `weatherpare/`, `savepare/` — app pages
- `support/`, `privacy/` — support and privacy policy
- `assets/css/site.css` — every page's styles
- `assets/img/` — icons and screenshots

When My Day is on the App Store, replace the "Coming soon" badges on the home
page and `myday/index.html` with the App Store link (the spot is marked).

Preview locally with `python3 -m http.server` and open http://localhost:8000.
