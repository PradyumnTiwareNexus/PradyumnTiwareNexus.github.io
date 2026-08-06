# Changelog

## [Phase 1] Identity rewrite + Premium badges + Achievement Dashboard

**Date:** 2026-08-06

### What was added
- **Identity section (`#who-is-pradyumntiwarenexus`) — content rewrite only.**
  Layout, card (`.gc`/`.gc-inner`), inline-style conventions, and structure are
  unchanged; only the three paragraphs were rewritten to more clearly answer who
  Pradyumn Tiwari / PradyumnTiwareNexus is, his specialization, the organizations
  that have recognized him, and what differentiates his research — written
  factually, no keyword stuffing, all claims consistent with content already on
  the page.
- **Premium Research Snapshot badge row** (`.id-badges`/`.id-badge`) added below
  the Identity paragraphs: Hall of Fame Researcher, Responsible Disclosure, Open
  Source Contributor, GitHub Security Advisories, Recon Automation, Security
  Research — each with a gradient-glow hover/lift animation built from the
  site's existing `--purple`/`--cyan` color tokens and transition timing.
- **New "Research Dashboard" section** (`#achievements`) with 6 animated
  count-up stats: Hall of Fame (11), Responsible Disclosures (14), Certificates
  (3), Open Source Contributions (1), GitHub Advisories (1), Organizations
  Engaged (13). **Every number is counted directly from real entries already
  on this page** (Hall of Fame cards, Devsly certificates, the IntersectMBO
  open-source contribution) — nothing was invented. Reuses the existing
  `.stats-bar`/`.sc`/`.si`/`.sn`/`.sl` classes from the hero section.

### Explicitly skipped this round (by design, not by mistake)
- **Trusted Recognition / logo wall** — your Hall of Fame section already has
  an animated, data-driven scrolling logo/company strip (`.hof-strip` /
  `.hof-marquee`) containing every company you listed (NASA, Microsoft, Toyota,
  BMW, Quick Heal, ISRO, Whir, TrekMail, BT, Aeterna) plus BSNL. Rebuilding it
  as a separate section would duplicate content and risk touching the Hall of
  Fame section, which is off-limits. Flagging this so you can decide if you
  want per-logo hover detail (recognition type / date / link) added to the
  *existing* strip in a future round — that would need real dates/links for
  each entry that aren't currently on the page.
- **Testimonials & Research Statistics (severity/industry charts)** — not built
  yet. You confirmed you'll provide the real data later; building these now
  would mean either fabricating names/quotes/numbers or shipping empty shells,
  neither of which is right for a page representing real credentials.
- Timeline, Awards & Recognition (as a distinct new section), Open Source card
  scaling/filtering, Research Methodology pipeline, full SEO/schema overhaul,
  accessibility pass, and performance work are Phase 2/3 — not started yet.

### What was NOT changed
- No existing section was modified, removed, reordered, or renamed. Hero,
  Navigation, About, Skills, Hall of Fame, Certificates, Projects, Open Source
  Contributions (added last round), CTF, Writeups, Contact, and Footer are
  untouched.
- No existing CSS rule was edited — only new rules were added (`.id-badges`,
  `.id-badge`, and a mobile override for the new dashboard's grid), all built
  from existing color/spacing/radius/transition tokens.
- No existing JavaScript was edited. The animated-counter script from the
  previous round was generalized in place (still a script *I* added, not part
  of your original site) to also drive the new dashboard, avoiding duplicate
  counter logic — your original inline `<script>` block is untouched.

---

## [Added] Open Source Security Contributions section

**Date:** 2026-08-06

### What was added
- A new `<section id="opensource">` — **"🚀 Open Source Security Contributions"** —
  inserted in `index.html` immediately after the Hall of Fame / Appreciation &
  Certificates ("Achievements") section and before the Projects / Contact sections.
- One contribution card for **IntersectMBO / plutus-script-evaluation**, including:
  - Status badges (Issue Reproduced, Root Cause Confirmed, Fix Implemented, Merged into Main Branch)
  - Description of the finding
  - Technology tags (Haskell, GitHub, Open Source, Concurrency, Thread Management)
  - A terminal-styled timeline (Security Advisory Published → Merged into Main Branch)
  - "View Security Advisory" and "View Pull Request" links
- A 4-stat animated counter row (OSS Contributions, Merged Fixes, Public Advisories,
  Repos Improved), reusing the existing hero stats-bar styling, with a small
  standalone `IntersectionObserver`-based count-up script.

### What was NOT changed
- No existing section was modified, removed, reordered, or renamed:
  Hero, Navigation, Colors, Theme, Typography, Animations, Background, Cards,
  Timeline, Skills, Experience, Hall of Fame, Certificates/Rewards, Projects,
  CTF, Writeups, Contact, and Footer are all byte-for-byte identical to the
  original upload.
- No existing CSS rules were edited, and **no new CSS was written at all** —
  the new section is built entirely from classes that already exist in the
  site's stylesheet (`.sh`, `.st`, `.hof-intro`, `.stats-bar`, `.sc`, `.hof-grid`,
  `.hof-card`, `.hof-badge`, `.ptags`/`.ptag`, `.hof-btn`, `.term`/`.term-body`),
  so spacing, colors, fonts, card style, shadows, radius, and transitions all
  match the rest of the site automatically.
- No existing JavaScript was edited. The counter animation lives in a brand-new,
  self-contained `<script>` block placed after the existing script, scoped only
  to `#oss-stats`, and does not interact with or override any existing logic
  (typing effect, cursor, vuln bars, reveal-on-scroll, cert tabs, CTF filter, form).
- The existing scroll-reveal system (`.sec.rev` + the page's `IntersectionObserver`)
  was reused as-is for the new section — no new animation library was introduced.
- No `nav` link was added, per the instruction not to touch Navigation.
- All other files (assets, LICENSE, README.md, robots.txt, sitemap.xml,
  `.nojekyll`, verification HTML) are unchanged.

### A note on the project's actual tech stack
This portfolio is a **static single-file site** (`index.html` with inline
`<style>`/`<script>`, no React/TypeScript/build tooling, no npm packages).
The new section was built to match that: plain HTML + the site's existing CSS
classes + a small vanilla-JS enhancement, so it runs immediately with no
install/build step — exactly like the rest of the site.
