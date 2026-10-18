# CLAUDE.md

How to work on **pareapps.com**, the Pare Apps website: a home page for every app, a page per app, support, and a privacy policy per app.

## Basics

- **Plain HTML and CSS, no build step and no framework.** Every page is a finished `index.html` in its own folder, so `/myday/` is `myday/index.html`.
- **Hosting:** GitHub Pages serves the `main` branch of `github.com/pareappsdev/pareapps.site` at the domain root. **Every push to `main` goes live** within a minute or two; there is no staging.
- **Pushing:** use SSH as `bishopdnate`, a collaborator on the `pareappsdev` repo. The remote is `git@github.com:pareappsdev/pareapps.site.git`.

## Rules for the content

- **There is no company logo or icon yet.** The header shows "Pare Apps" as text, the site has no favicon, and My Day's pages use its app icon as theirs. Don't reuse an app's icon as the company's.
- **The company is always "Pare Apps"** (two words) in visible text: titles, headings, copy, the copyright line and legal pages. **Never use a personal name anywhere on the site.** The domain and URLs stay `pareapps.com`.
- Contact address: **developer@pareapps.com**.
- **Don't publish prices.** Pricing lives in the App Store.
- **Don't claim features an app doesn't ship.** Check the app's code first. For example, My Day's Watch app only went on the site once its watch target built and shipped inside the iPhone app.

## Layout

| Path | What it is |
|---|---|
| `index.html` | Home: a card for each app |
| `myday/` | One page per app (only My Day for now) |
| `<app>/privacy/` | That app's privacy policy |
| `privacy/` | Lists every app's policy (keeps the old `/privacy/` link working) |
| `support/` | Contact and FAQ |
| `home/`, `my-day/`, `privacy-policy/` | Redirect pages for old or short links (GitHub Pages ignores `_redirects` files) |
| `404.html` | Not-found page |
| `assets/css/site.css` | Every page's styles: colours, phone frames and section layouts |
| `assets/img/` | Icons and screenshots; My Day's are in `assets/img/myday/` |
| `sitemap.xml`, `robots.txt` | For search engines |
| `CNAME` | The custom domain. **Don't delete it**, or GitHub drops pareapps.com |
| `.nojekyll` | Tells GitHub to serve files as they are |

**The header and footer are copied into every page; there are no includes.** A change to the nav or footer has to be made in every `index.html` (find them with `grep -rl site-footer`). Footer rules:
- On an app's page and that app's policy page, the footer's Privacy Policy link goes to that app's policy.
- Everywhere else, it goes to `/privacy/`.

## Common changes

### An app reaches the App Store
On the home page card and on the app's page, replace the "Coming soon…" badge with a button:
```html
<a class="btn light" href="https://apps.apple.com/…">Download on the App Store</a>
```
- Use `btn light` on the purple hero, and `btn` on white.
- `myday/index.html` has a comment marking the spot, and its closing section ("coming soon") needs the button too.
- Current status:
  - **My Day:** coming soon.
  - **WeatherPare and SavePare** were taken off the site on 2026-10-17 (they are off the App Store). Their pages are in git history if they come back.

### Adding a new app
1. Make `<app>/index.html` from `myday/`. The home page's "More coming soon" card makes way for, or sits after, the new app's card.
2. Add `<app>/privacy/index.html`, written from what that app actually collects. Check its code: frameworks such as Firebase and RevenueCat, iCloud, and the system permissions it asks for.
3. Add a card to `index.html`, a link in **every** page's header nav, and a line in `privacy/index.html`.
4. Add both new URLs to `sitemap.xml`.
5. Put its icon (512px) and screenshots (about 786px wide for phones, 1600px for iPad) in `assets/img/`.

### Changing a privacy policy
- Edit `<app>/privacy/index.html` and change its "Last updated" date.
- My Day's policy must match the iOS app. If the app adds a framework that collects data, or a new permission, update the policy in the same change.
- The app links to `https://pareapps.com/myday/privacy/` from its paywall (`ProPaywallViewController.privacyURL`) and from Settings → About. **Don't move that URL**, or those links break.

### Screenshots
- **My Day's** screenshots are real, taken from the iOS Simulator in demo mode. iPhone shots are in `assets/img/myday/iphone/` (786px wide), iPad shots in `assets/img/myday/ipad/` (1600px wide), all JPEG at quality 85.
- How to retake them is in the iOS repo: `Marketing/pareapps-myday/sim/README.md` (a showcase day for demo mode, photos dated to that day, and favourites seeded into the app group).

## Checking before a push
- **Preview:** run `python3 -m http.server 8787` in this folder and open http://localhost:8787. Links like `/myday/` only work from the site root, so don't open the files directly.
- **Check desktop and phone widths.** Use the browser pane's mobile size (375pt); headless Chrome won't go narrower than about 500px. Make sure nothing runs off the side.
- After pushing, confirm it's live, e.g. `curl -s https://pareapps.com/<page>/ | grep "<new text>"`.

## Domain and DNS (registered at Wix)
- Wix won't let you change the nameservers on a domain bought through Wix, so the DNS stays at Wix.
  - `pareapps.com`: A records to `185.199.108.153`, `.109.153`, `.110.153` and `.111.153`
  - `www`: CNAME to `pareappsdev.github.io`
- **Never touch the MX or TXT records.** They carry Google Workspace email for developer@pareapps.com.
- HTTPS is GitHub's automatic certificate; "Enforce HTTPS" is set in the repo's Settings → Pages.
- To move to Cloudflare Pages one day, the domain would first have to be transferred from Wix to Cloudflare.
