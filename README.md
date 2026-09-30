# JAI Productions — jaiproductions.com.au

Personal website and consulting/contract services platform for Nigel Hodgson, animatronic and show control specialist.

## Repository Structure

```
jaiproductions-website/
├── index.html          # Homepage / hub (homepage JS inline)
├── styles.css          # Shared stylesheet for every page
├── animatronics/       # Specialism page: animatronic commissioning
├── show-control/       # Specialism page: show control, PLC, media networking
├── exhibitions/        # Specialism page: immersive exhibition operations
├── rates/              # Unlisted engagement structures page (noindex, not in sitemap)
├── og-image.png        # Open Graph social preview image (1200x630px)
├── robots.txt          # Search engine crawl instructions
├── sitemap.xml         # Search engine sitemap (homepage + three specialism pages)
├── CLAUDE.md           # Claude Code instructions and context
├── SITE_ARCHITECTURE.md # Full site structure and section reference
├── DEPLOYMENT.md       # How to deploy changes to live server
└── CONTENT_GUIDE.md    # Content, tone, and keyword guidelines
```

## Quick Reference

**Live site:** https://jaiproductions.com.au  
**Host:** Webcentral (Enhance panel) — Sydney server  
**Server IP:** 198.38.93.43  
**Stack:** Static HTML pages + one shared stylesheet — no build process, no framework, no dependencies except Google Fonts CDN  
**Deploy method:** Manual upload via Webcentral file manager → public_html/

## The Site in One Line

Dark industrial aesthetic, amber (#e8960a) accents. A homepage with anchor navigation plus three keyword-focused specialism pages and an unlisted rates page. All CSS is in styles.css; homepage JavaScript is inline in index.html. No backend, no CMS, no database.

## Owner

Nigel Hodgson  
nigelh@jaiproductions.com.au  
+61 414 997 448  
Sydney, Australia / Osaka, Japan  
LinkedIn: linkedin.com/in/nigelhodgson  
GitHub: github.com/njhod1
