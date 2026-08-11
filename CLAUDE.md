# CLAUDE.md — Context for Claude Code

This file gives Claude Code everything it needs to work on this repository without re-briefing. Read this first before making any changes.

---

## Who This Site Is For

**Nigel Hodgson** — animatronic and show control specialist, 35+ years experience.

Core positioning: *"The person who translates artistic intent into technical scope, and technical constraint back into creative options, across every department."*

This is both a consulting services site and a visibility platform targeting specific companies in the themed entertainment and live production industries.

---

## Target Audience (Who Will Visit This Site)

Primary targets — these specific companies and their staff:
- **Creature Technology Company** (Melbourne) — warm CEO/engineering relationships
- **NEON / ANIMAX / Victory Hill** (Singapore/Nashville/Las Vegas) — known, staff turnover strategy
- **Global Creatures** (Melbourne) — HR relationship warm
- **A Blanc Canvas** (Melbourne) — owner Joe Blanck, personal relationship
- **Universal Creative** (Singapore/Osaka/Beijing) — indirect via supplier relationships
- **Smart Monkeys** (global) — fresh relationship
- **TAIT / Thinkwell** (LA/Abu Dhabi/Montreal) — TAIT Navigator training credential
- **Unify Productions Global** (UK) — Harry Potter Forbidden Forest Experience producers

Secondary targets:
- Theatre production companies using LED/video
- Exhibition operators and venues across Asia Pacific
- Recruiters in the themed entertainment space

---

## Site Architecture

The site is a **single HTML file** (index.html) with all CSS and JavaScript inline. There is no build process, no framework, no package.json. Sections are identified by anchor IDs:

| Anchor | Section | Purpose |
|--------|---------|---------|
| `#hero` | Hero | Name, tagline, credential card, availability badge |
| `#about` | Profile | About text, career timeline |
| `#services` | Services | Six service cards |
| `#cases` | Case Studies | Four case study cards |
| `#rates` | Rates | Two-track rate structure |
| `#booking` | Contact | Intake form + contact details |
| `#faq` | FAQ | Five Q&A accordion items |

**Footer** contains copyright and nav links.

---

## Design System

All design tokens are CSS variables in `:root`. Never hardcode colours — always use variables or the established hex values below.

```css
--bg: #0d0e0f          /* Page background */
--bg2: #141618         /* Card/elevated background */
--bg3: #1c1f22         /* Deeper card background */
--amber: #e8960a       /* Primary accent — amber/gold */
--amber-dim: #a06a06   /* Dimmer amber for borders */
--amber-pale: #2a1f08  /* Very dark amber for tag backgrounds */
--text: #e8e4dc        /* Primary text */
--text-dim: #8a8580    /* Secondary text */
--text-faint: #4a4845  /* Tertiary/disabled text */
--border: #2a2d30      /* Border colour */
```

**Established bright text colours (use these, not the dim variables):**
- Body text on dark backgrounds: `#9a9690` or `#b0aca4`
- Labels and secondary mono text: `#c8c4bc` or `#b8b4ac`
- Dimmer supporting text: `#a0a0a0`
- Contact section "Based/Available" text: `#a8a4a0`

**Fonts:**
- Headings: `'Bebas Neue', sans-serif` — all caps, tracking
- Mono labels/tags/nav: `'DM Mono', monospace`
- Body: `'DM Sans', sans-serif`

**Tag style:**
```css
color: #e8a020; border: 1px solid #6b4e10; background: #2e2008;
```

---

## Content Rules

### What to preserve exactly
- The hero tagline: *"The technical problem is solved."*
- The positioning line in #about: *"translating artistic intent into technical scope... translating technical constraint back into creative options"*
- All four case studies — do not rewrite without explicit instruction
- The two-track rates structure (Track 01 On-Site / Track 02 Remote)
- The FAQ section — feeds JSON-LD schema, do not remove

### Tone
Direct, specific, confident without being boastful. No fluff. No generic consulting language. Every claim should be backed by a specific production or technology. Kraken-style warmth is appropriate in the contact section but not in services or case studies.

### Never do
- Change rates without explicit instruction from Nigel
- Remove or rewrite the FAQ section (it feeds structured data for AI search)
- Change the og:image path (it must point to /og-image.png)
- Add external JavaScript libraries or frameworks
- Add a backend or server-side code — this is a static site
- Remove the JSON-LD structured data block in the `<head>`

---

## SEO Configuration

The site has comprehensive SEO already implemented:

**Meta tags:** title, description, keywords, author, robots, canonical  
**Open Graph:** og:title, og:description, og:image (1200x630), og:url, og:locale  
**Twitter Card:** summary_large_image  
**Structured Data:** JSON-LD with Person, ProfessionalService, and FAQPage schemas  
**Geo targeting:** AU-NSW, Sydney  

**Primary keyword clusters:**
- Animatronic commissioning technician
- Show control technician / show creation specialist
- Travelling exhibition technical supervisor
- Themed entertainment technical consultant
- Dante network exhibition / Dante L3 certified
- PLC SCADA show control
- TAIT Navigator certified / Thinkwell themed entertainment
- Exhibition operations manager

When adding new content, ensure relevant keywords appear naturally in body text. Do not keyword-stuff.

---

## Contact and Form Behaviour

The intake form uses a `mailto:` handler — no backend required. On submit, it opens the user's email client with a pre-filled message to `nigelh@jaiproductions.com.au`.

LinkedIn URL in the contact section: `https://linkedin.com/in/nigelhodgson`

---

## Rates (Current — Do Not Change Without Instruction)

**Track 01 — On-Site Contract & Crew (USD)**
- Technical Supervisor: $4,500–$5,500/week + travel/accommodation
- All-Rounder / Show Technician: $550–$750/day or $2,500–$3,500/week

**Track 02 — Remote Consulting (USD)**
- Remote Advisory: $100–$150/hr, 2hr minimum
- Fixed Scope Documentation/Audit: $1,200–$2,500

All fees are in USD. Nigel receives via Charles Schwab (US account) or Qantas Business USD account.

---

## Deployment

See DEPLOYMENT.md for full instructions. Short version:
1. Edit index.html locally
2. Commit and push to GitHub
3. Download index.html from GitHub
4. Upload to public_html via Webcentral Enhance file manager
5. Verify at jaiproductions.com.au in incognito window

---

## Key Credentials to Mention in Content

- Audinate Dante Certification Levels 1, 2 & 3 (2024)
- Q-SYS Audio Systems Certification (2021)
- PLC & SCADA Systems Certificate — Engineering Institute of Technology (2011)
- TAIT Navigator Automation Platform (2019)
- AICD Governance Essentials (2020)
- SMPTE ST 2110 IP Media Transport (2020)
- IEEE / SMPTE / AES / AICD member
- High Risk Work Licence — LF RA

## Work Eligibility

- Australia: Full work rights
- Japan: Spousal visa / Osaka base (Asia Pacific positioning advantage)
- USA: SSN + postal address (1099 contractor eligible)

---

## Productions to Reference (in order of impact)

1. Jurassic World: The Exhibition — Technical Supervisor Worldwide (Victory Hill/Cityneon, 2019–2021)
2. Walking With Dinosaurs — Head of Creatures/Head of Controls (Global Creatures, 2007–2019)
3. King Kong Live — Head of Creatures (Global Creatures, 2013–2014)
4. How To Train Your Dragon — Head of Show Control / Head of Creatures (DreamWorks/Global Creatures, 2011–2014)
5. Cirque du Soleil — EMC/IT Lead (2017)
6. Titanique — Head of Sound, Australian Premiere (JPJ Audio/Michael Cassel, 2024–2025)
7. Metaverse of Magic — Show Networking Engineer (Jones, 2023–2024)
8. Phantom of the Opera, Les Misérables, Sound of Music, Oliver — System Sound (1993–2005)
