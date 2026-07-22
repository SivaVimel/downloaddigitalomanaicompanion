# download.digitaloman.ai — AI Companion share pages

Per-character share/redirect pages for the DigitalOman.ai **AI Companion** feature.
Same pattern as the OmanJobs `/j/{id}` pages: each link carries a character's name +
image for the Facebook/social preview, then bounces the visitor to the right app store.

## How it works

- `c/{name}-{n}.html` — one page per character (e.g. `/c/layla-1`). Carries Open Graph
  tags (title, description, image) so a shared link shows that character, then
  auto-redirects to `/download`.
- `download.html` (served at `/download`) — detects the device and forwards to
  Google Play on Android, or the App Store on iPhone/iPad/Mac. Desktop shows both.
- `index.html` — gallery homepage linking every character.
- `characters/*.jpg` — Open Graph images (≤1200px). `characters/thumb/*.jpg` — gallery thumbs.
- `assets/logo.png` — app icon / favicon.

App store IDs (same app as the rest of DigitalOman.ai):
- Google Play `com.digitaloman.ai`
- App Store `id6760588911`

## Deploy (GitHub Pages)

1. Push the **contents of this `site/` folder** to the repo root (or set Pages
   → Source to this folder).
2. `CNAME` is already set to `download.digitaloman.ai`. Point that host at GitHub
   Pages in your DNS (CNAME → `<user>.github.io`), then enable **Enforce HTTPS**.
3. `.nojekyll` keeps Pages from touching the files. Extensionless URLs like
   `/c/layla-1` resolve to `c/layla-1.html` automatically.

## Rebuilding

These files are generated. To regenerate after editing names/captions or adding
images, run the builder one directory up:

```bash
python3 build_site.py     # reads roster_raw.json + clean/*.png → site/ + posts.txt
```

Edit `roster_raw.json` (names, captions) and rerun; the script re-diversifies any
duplicate first names and rewrites every page, image, and caption to match.
