# Off-Season Training Block

A single-page app for a 23-week off-season speed and fitness block (28 Sep 2026 - 7 Mar 2027), built around GAA squad training on Tuesday and Friday nights.
Today's session, the full week, gym loads in kilos, running paces calculated from a 1 km time,
and the January strength test.

Everything is in `index.html`: no build step, no dependencies, no backend. Open the file and it runs.

## Put it online with GitHub Pages

1. Create a new repository on github.com (public, no README).
2. Upload these files to the root of it: `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png`.
   Or, from a terminal:

   ```bash
   git init
   git add .
   git commit -m "Off-season training block"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo>.git
   git push -u origin main
   ```

3. In the repo: Settings > Pages > Source: "Deploy from a branch", branch `main`, folder `/ (root)`. Save.
4. Wait a minute, then open `https://<your-username>.github.io/<repo>/`.

## Install it on your phone

Open that address in Safari, tap share, then **Add to Home Screen**. Because this version ships a manifest
and a service worker, it installs with its own icon and name, opens without browser chrome, and works
offline after the first visit.

On Android, Chrome offers "Install app" from the menu.

## Updating an existing deployment

Replace `index.html` and `sw.js`, commit and push. `sw.js` carries a `CACHE` version string; it is bumped on every
content change so installed phones fetch the new version instead of serving the cached one. If a phone still shows the
old plan, close the app fully and reopen it once.

## Changing the plan

The whole 23 weeks live in the `DATA` object at the top of the `<script>` block in `index.html`:
one entry per week, seven days each, with `r` (running), `g` (gym), `i` (isometrics), `t` (times) and
`s` (study). Edit, commit, push; Pages redeploys in about a minute. The service worker cache is versioned
by the `CACHE` string in `sw.js` - bump it (`offseason-v2`) when you change the app so phones pick the new
version up rather than serving the cached one.

## Notes

- The 1 km time and max heart rate you enter are stored in that browser's localStorage. They are per-device
  and never leave it.
- No analytics, no network calls, no accounts.
