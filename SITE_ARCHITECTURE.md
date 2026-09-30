# Site Architecture — jaiproductions.com.au

## Overview

Static multi-page site. No build process. No dependencies except Google Fonts loaded from CDN. All pages share one stylesheet and link to each other with root-relative paths, so they must be served from the site root.

```
index.html                — Homepage / hub. Homepage JavaScript is inline.
styles.css                — Shared stylesheet (design tokens, all components)
animatronics/index.html   — Specialism page: animatronic commissioning
show-control/index.html   — Specialism page: show control, PLC, media networking
exhibitions/index.html    — Specialism page: immersive exhibition operations
rates/index.html          — Engagement structures (noindex, not in sitemap, linked quietly)
og-image.png              — Social preview image (1200x630px, dark/amber branded)
robots.txt                — Allows all crawlers, points to sitemap
sitemap.xml               — Homepage + three specialism pages (rates excluded on purpose)
archive/                  — Dated snapshots of previous versions
```

## Why the specialism pages exist

Each targets one keyword cluster so search engines see a page that is about that topic, rather than one page trying to cover everything:

| Page | Primary terms |
|------|---------------|
| /animatronics/ | animatronics, animatronic commissioning, hydraulic and servo systems, PID control loops |
| /show-control/ | show control, PLC, SCADA, Medialon, Alcorn McBride, Beckhoff, media networking |
| /exhibitions/ | immersive exhibition, travelling exhibition, operations management, SOPs |

Content on these pages is drawn from the homepage services and case studies; the case studies themselves live only on the homepage and are linked to, not copied.

## Shared page pattern (specialism pages)

Nav → breadcrumb + H1 + lead → "What I deliver" list → productions/track record → "Other specialisms" links → contact CTA → footer. Each page has its own title, meta description, canonical, Open Graph/Twitter tags and a JSON-LD `Service` + `BreadcrumbList` block. Page-specific CSS (`.page-hero`, `.page-section`, `.page-list`, `.spec-links`, `.crumbs`) lives at the end of styles.css.

---

## Section Map

### NAV (fixed, top)
- Logo: JAI.PRODUCTIONS (links to #hero)
- Links: Profile, Services, Animatronics, Show Control, Exhibitions, Case Studies, Contact (Rates is intentionally not in the nav)
- CTA button: "Engage Now" (links to #booking)

### #hero
- Availability badge (green pulsing dot)
- Hero tag: "Animatronic & Show Control Specialist"
- H1: "The technical / problem / is solved."
- Body paragraph: 35+ years positioning
- Two CTAs: "Book a consultation" (#booking) + "See case studies" (#cases)
- Credential card (right column, hidden on mobile):
  - Stats: 35+ years, 40+ productions, 20+ countries, SYD/OSA base
  - Cert list: Dante L1/L2/L3, Q-SYS, IEEE/SMPTE/AES, AICD, PLC & SCADA, LF RA

### Marquee (between hero and about)
- Scrolling ticker: production names + technology stack
- Background: #111315, text: #c8c4bc

### #about — Profile
- Section tag: "Profile"
- H2: "Nigel / Hodgson"
- Amber divider
- Three body paragraphs (opening paragraph uses translator positioning)
- IEEE/SMPTE/AES/AICD member line
- Right column: career timeline (7 entries, most recent first)

### #services — Services
- Section tag + H2: "What I / deliver"
- Intro paragraph (right column)
- 6 service cards in 3-column grid (below them, a row of three links to the specialism pages):
  1. Animatronic Show Control & Commissioning
  2. AV Network Optimisation & Troubleshooting
  3. Exhibition Technical Supervision & Operations Management
  4. IT Infrastructure & Show Network Operations
  5. Technical Documentation & Standards
  6. Remote Diagnostic & Advisory

### #cases — Case Studies
- Section tag + H2: "Problems solved. / Shows opened."
- Introductory paragraph (translator framing)
- 4 case study cards in 2-column grid:
  1. Jurassic World: The Exhibition (2019–2021)
  2. Walking With Dinosaurs (2007–2019)
  3. Metaverse of Magic (2023–2024)
  4. Titanique (2024–2025)

### Rates (moved to /rates/)
Rates are no longer a homepage section. They live on `/rates/` (`noindex, follow`, excluded from sitemap.xml), reached only through the small "Engagement structures" footer link and the "Looking for fees?" line in the contact section. Layout is unchanged: Track 01 On-Site (Technical Supervisor, All-Rounder) and Track 02 Remote (Remote Advisory, Fixed Scope). The FAQ says fees are "quoted on request" and does not list figures.

### #booking — Contact
- Section tag + H2: "Start an / engagement"
- Left column: intro text, "Looking for fees?" link to /rates/, based/available info, email/LinkedIn/response
- Right column: intake form
  - Fields: name, company, email, engagement type (dropdown), brief description
  - Submit: opens mailto: with pre-filled content
  - Note: "All enquiries treated in confidence. SOW provided before any work commences."

### #faq — Common Questions
- 5 accordion items (also mirrored in the FAQPage JSON-LD on the homepage):
  1. What animatronic systems do you have experience with?
  2. Are you available for work in Japan, Singapore, or the USA?
  3. What is the difference between on-site contract roles and remote consulting? (fees "quoted on request")
  4. What themed entertainment companies have you worked with?
  5. Do you hold Dante audio networking certification?

### Footer
- Logo: JAI.PRODUCTIONS
- Nav links: Profile, Services, Case Studies, Contact, Engagement structures (/rates/)
- Copyright: © 2025 JAI Productions · ABN registered · Sydney / Osaka

---

## CSS Architecture

All styles are in `/styles.css`, loaded by every page with `<link rel="stylesheet" href="/styles.css">`. Organised as:

```
:root              CSS variables / design tokens
*, body            Reset and base
nav                Fixed navigation
.container         Max-width wrapper (1100px)
#hero              Hero section
.hero-*            Hero child components
.hero-card         Credential card
.marquee-*         Scrolling ticker
#about             Profile section
.timeline-*        Career timeline
#services          Services section
.service-card      Individual service card
.tag               Technology tag pill
#cases             Case studies section
.case-card         Individual case study card
.case-outcome      Outcome highlight box
#rates             Rates section (used on /rates/)
.rate-card         Individual rate card
#booking           Contact section
.booking-form      Intake form
.contact-*         Contact info items
footer             Footer
.avail-badge       Green availability indicator
.fade-up           Scroll animation class (needs the homepage JS; not used on sub-pages)
@media             Mobile breakpoints (max-width: 900px)
.page-*, .crumbs,
.spec-link(s),
.quiet-link        Specialism-page and cross-link components (end of file)
```

---

## JavaScript

Homepage only (`index.html`): a single inline `<script>` block at the bottom of body. Sub-pages contain no JavaScript. Two functions:

**IntersectionObserver** — adds `.visible` class to `.fade-up` elements when they enter viewport, triggering CSS transition (opacity 0→1, translateY 24px→0).

**handleSubmit()** — validates name, email, brief fields, then constructs a mailto: URL with all form field values encoded as the email body, directed to nigelh@jaiproductions.com.au.

---

## Open Graph / SEO Head Structure

Homepage (sub-pages follow the same pattern with their own values):

```html
<title>Animatronic Commissioning & Show Control | Nigel Hodgson</title>   <!-- ~60 chars max -->
<meta name="description" ...>     <!-- ~155 chars max; lead with animatronics -->
<meta name="keywords" ...>        <!-- ~24 phrases; ignored by Google, low value -->
<meta name="author" ...>
<meta name="robots" content="index, follow">   <!-- /rates/ uses "noindex, follow" -->
<link rel="canonical" href="https://jaiproductions.com.au/">

<!-- Open Graph (Facebook/LinkedIn) -->
<meta property="og:type" content="website">
<meta property="og:url" ...>
<meta property="og:title" ...>
<meta property="og:description" ...>   <!-- Keep under 155 chars -->
<meta property="og:image" content="https://jaiproductions.com.au/og-image.png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">

<!-- Geo -->
<meta name="geo.region" content="AU-NSW">

<!-- JSON-LD Structured Data (homepage) -->
<script type="application/ld+json">
  <!-- Person schema (includes credentials and knowsAbout) -->
  <!-- ProfessionalService schema (serviceType list) -->
  <!-- FAQPage schema (mirrors FAQ section content) -->
</script>
```

Sub-pages carry a `Service` + `BreadcrumbList` JSON-LD block that points back to the homepage's `#jai-productions` organisation.

**Critical:** The FAQPage schema must always match the actual FAQ section content. If you update FAQ questions/answers, update the JSON-LD block too.

---

## Mobile Behaviour (max-width: 900px)

- Nav links hidden (hamburger not implemented — keep simple)
- Hero card hidden (single column)
- About grid: single column
- Services grid: single column
- Case grid: single column
- Specialism links row: single column
- Rates grid (on /rates/): 2-column (1fr 1fr)
- Booking grid: single column
- Footer: column layout, centered
