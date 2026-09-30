# Deployment Guide — jaiproductions.com.au

## Infrastructure

| Component | Detail |
|-----------|--------|
| Domain registrar | Webcentral (theconsole.webcentral.au) |
| Hosting | Webcentral Enhance panel |
| Server | e4976.syd1.stableserver.net |
| Server IP | 198.38.93.43 |
| Staging URL | https://jaiproductions-com-au-fdfe.syd1.mystaging.site/ |
| Live URL | https://jaiproductions.com.au |
| Email | nigelh@jaiproductions.com.au (Office 365) |
| DNS | Nameservers: ns1–ns4.stableserver.net |

## Files That Live on the Server (public_html/)

```
index.html              ← Homepage
styles.css              ← Shared stylesheet (all pages load /styles.css)
animatronics/index.html ← Specialism page
show-control/index.html ← Specialism page
exhibitions/index.html  ← Specialism page
rates/index.html        ← Unlisted rates page (noindex)
og-image.png            ← Social preview image
robots.txt              ← Search engine instructions
sitemap.xml             ← Search engine sitemap
```

The folders must keep their names and sit directly inside `public_html/`, because the pages link to each other and to `/styles.css` with root-relative paths.

---

## Standard Deployment Process

### 1. Make changes locally
Edit the relevant page (`index.html`, or the `index.html` inside a page folder) or `styles.css` using Claude Code or any text editor. A change to `styles.css` affects every page.

### 2. Test locally
Pages use root-relative links (`/styles.css`, `/animatronics/`), so opening files directly (File → Open) will show unstyled pages. Serve the folder instead: `python3 -m http.server 8000` from the repo root, then open http://localhost:8000. The Google Fonts CDN link requires an internet connection for correct font rendering.

### 3. Commit and push to GitHub
```bash
git add -A
git commit -m "Brief description of what changed"
git push origin main
```

### 4. Upload to Webcentral
1. Go to theconsole.webcentral.au → log in
2. Click Websites → jaiproductions.com.au → Files
3. Navigate to public_html/
4. Upload every changed file, keeping the folder structure (upload the whole folder for a page you changed, e.g. animatronics/)
5. Overwrite existing files when prompted
6. Confirm the full list above is present: index.html, styles.css, the four page folders, og-image.png, robots.txt, sitemap.xml

### 5. Verify
Open an incognito/private browser window and go to jaiproductions.com.au. Check the changed page, and click through to /animatronics/, /show-control/, /exhibitions/ and /rates/ to confirm they load with styling. If the browser shows a cached version (including a cached styles.css), hard refresh with Ctrl+Shift+R.

---

## When to Redeploy og-image.png

Only redeploy og-image.png if the branded preview image has been regenerated. It rarely changes. The current og-image.png is at the correct 1200x630px dimensions.

After updating og-image.png on the server, force LinkedIn to re-crawl:
- Go to linkedin.com/post-inspector
- Enter https://jaiproductions.com.au and click Inspect

---

## Checking SEO After Changes

Use **OpenGraph.xyz** to verify meta tags and preview image:
- Go to https://www.opengraph.xyz
- Enter https://www.jaiproductions.com.au
- Click Rescan after any deployment
- Target: 0 errors, warnings only for title/description length (acceptable)

Use **Google Search Console** to submit updated sitemap:
- Go to search.google.com/search-console
- Submit https://jaiproductions.com.au/sitemap.xml after major content changes
- Use URL Inspection → Request indexing for any new or substantially changed page (the three specialism pages in particular)
- /rates/ is deliberately left out of the sitemap and marked noindex; do not request indexing for it

---

## Troubleshooting

**Site not updating after upload**
Browser cache. Always check in incognito window. Webcentral sometimes has a short CDN cache — wait 5–10 minutes if incognito still shows old version.

**Site shows old version everywhere**
Check that the files were uploaded to public_html/ not the parent directory. File manager shows both levels — double-click public_html to enter it before uploading.

**Pages show unstyled text**
styles.css is missing from public_html/ or was uploaded into a sub-folder. It must sit next to index.html.

**A page returns 404**
Check the folder name matches exactly (animatronics, show-control, exhibitions, rates) and contains index.html.

**og:image not appearing on LinkedIn**
1. Confirm og-image.png is in public_html/
2. Confirm the og:image tag in each page points to https://jaiproductions.com.au/og-image.png
3. Use linkedin.com/post-inspector to force re-crawl
4. SSL certificate must be valid — LinkedIn won't crawl http:// links

**SSL showing as expired or invalid**
Log into Enhance hosting panel → Websites → jaiproductions.com.au → SSL. AutoSSL (Let's Encrypt) should renew automatically. If not, contact Webcentral support.

**DNS not resolving**
Check nameservers at dnschecker.org. Should show ns1–ns4.stableserver.net. If showing netregistry.net nameservers, the change hasn't propagated yet — wait up to 4 hours.
