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
index.html      ← Main site file
og-image.png    ← Social preview image
robots.txt      ← Search engine instructions
sitemap.xml     ← Search engine sitemap
```

---

## Standard Deployment Process

### 1. Make changes locally
Edit `index.html` using Claude Code or any text editor.

### 2. Test locally
Open `index.html` directly in a browser (File → Open). Check the changed section looks correct. Note: the Google Fonts CDN link requires internet connection for correct font rendering.

### 3. Commit and push to GitHub
```bash
git add index.html
git commit -m "Brief description of what changed"
git push origin main
```

### 4. Upload to Webcentral
1. Go to theconsole.webcentral.au → log in
2. Click Websites → jaiproductions.com.au → Files
3. Navigate to public_html/
4. Delete the existing index.html
5. Upload the new index.html
6. Confirm all four files are present: index.html, og-image.png, robots.txt, sitemap.xml

### 5. Verify
Open an incognito/private browser window and go to jaiproductions.com.au. Check the changed section. If browser shows cached version, hard refresh with Ctrl+Shift+R.

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

---

## Troubleshooting

**Site not updating after upload**
Browser cache. Always check in incognito window. Webcentral sometimes has a short CDN cache — wait 5–10 minutes if incognito still shows old version.

**Site shows old version everywhere**
Check that index.html was uploaded to public_html/ not the parent directory. File manager shows both levels — double-click public_html to enter it before uploading.

**og:image not appearing on LinkedIn**
1. Confirm og-image.png is in public_html/
2. Confirm og:image tag in index.html points to https://jaiproductions.com.au/og-image.png
3. Use linkedin.com/post-inspector to force re-crawl
4. SSL certificate must be valid — LinkedIn won't crawl http:// links

**SSL showing as expired or invalid**
Log into Enhance hosting panel → Websites → jaiproductions.com.au → SSL. AutoSSL (Let's Encrypt) should renew automatically. If not, contact Webcentral support.

**DNS not resolving**
Check nameservers at dnschecker.org. Should show ns1–ns4.stableserver.net. If showing netregistry.net nameservers, the change hasn't propagated yet — wait up to 4 hours.
