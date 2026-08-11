# Site Architecture — jaiproductions.com.au

## Overview

Single HTML file. All CSS, JavaScript, and content are inline. No build process. No dependencies except Google Fonts loaded from CDN.

```
index.html      — Everything. The entire site.
og-image.png    — Social preview image (1200x630px, dark/amber branded)
robots.txt      — Allows all crawlers, points to sitemap
sitemap.xml     — Single URL entry for homepage
```

---

## Section Map

### NAV (fixed, top)
- Logo: JAI.PRODUCTIONS (links to #hero)
- Links: Profile, Services, Case Studies, Rates, Contact
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
- 6 service cards in 3-column grid:
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

### #rates — Rates
- Section tag + H2: "Engagement / structures"
- Intro paragraph
- Track header bar (Track 01 / Track 02)
- 4-column rate grid:
  - Track 01: Technical Supervisor ($4,500–$5,500/wk) + All-Rounder ($550–$750/day)
  - Divider
  - Track 02: Remote Advisory ($100–$150/hr) + Fixed Scope ($1,200–$2,500)

### #booking — Contact
- Section tag + H2: "Start an / engagement"
- Left column: intro text, based/available info, email/LinkedIn/response
- Right column: intake form
  - Fields: name, company, email, engagement type (dropdown), brief description
  - Submit: opens mailto: with pre-filled content
  - Note: "All enquiries treated in confidence. SOW provided before any work commences."

### #faq — Common Questions
- 5 accordion items (HTML details/summary):
  1. What animatronic systems do you have experience with?
  2. Are you available for work in Japan, Singapore, or the USA?
  3. What is the difference between on-site contract roles and remote consulting?
  4. What themed entertainment companies have you worked with?
  5. Do you hold Dante audio networking certification?

### Footer
- Logo: JAI.PRODUCTIONS
- Nav links: Profile, Services, Case Studies, Contact
- Copyright: © 2025 JAI Productions · ABN registered · Sydney / Osaka

---

## CSS Architecture

All styles are in a single `<style>` block in `<head>`. Organised as:

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
#rates             Rates section
.rate-card         Individual rate card
#booking           Contact section
.booking-form      Intake form
.contact-*         Contact info items
footer             Footer
.avail-badge       Green availability indicator
.fade-up           Scroll animation class
@media             Mobile breakpoints (max-width: 900px)
```

---

## JavaScript

Single inline `<script>` block at bottom of body. Two functions:

**IntersectionObserver** — adds `.visible` class to `.fade-up` elements when they enter viewport, triggering CSS transition (opacity 0→1, translateY 24px→0).

**handleSubmit()** — validates name, email, brief fields, then constructs a mailto: URL with all form field values encoded as the email body, directed to nigelh@jaiproductions.com.au.

---

## Open Graph / SEO Head Structure

```html
<title>Nigel Hodgson | Animatronic & Show Control Specialist | JAI Productions</title>
<meta name="description" ...>
<meta name="keywords" ...>        <!-- ~25 targeted keyword phrases -->
<meta name="author" ...>
<meta name="robots" content="index, follow">
<link rel="canonical" href="https://jaiproductions.com.au/">

<!-- Open Graph (Facebook/LinkedIn) -->
<meta property="og:type" content="website">
<meta property="og:url" ...>
<meta property="og:title" ...>
<meta property="og:description" ...>   <!-- Keep under 125 chars -->
<meta property="og:image" content="https://jaiproductions.com.au/og-image.png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">

<!-- Geo -->
<meta name="geo.region" content="AU-NSW">

<!-- JSON-LD Structured Data -->
<script type="application/ld+json">
  <!-- Person schema -->
  <!-- ProfessionalService schema -->
  <!-- FAQPage schema (mirrors FAQ section content) -->
</script>
```

**Critical:** The FAQPage schema must always match the actual FAQ section content. If you update FAQ questions/answers, update the JSON-LD block too.

---

## Mobile Behaviour (max-width: 900px)

- Nav links hidden (hamburger not implemented — keep simple)
- Hero card hidden (single column)
- About grid: single column
- Services grid: single column
- Case grid: single column
- Rates grid: 2-column (1fr 1fr)
- Booking grid: single column
- Footer: column layout, centered
