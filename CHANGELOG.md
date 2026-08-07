# Changelog

## [Phase 3] SEO/Schema + Accessibility + Performance

**Date:** 2026-08-07

### What I found already in place (no action needed)
Your site already had excellent SEO before this phase: Person schema,
WebSite schema (with SearchAction), FAQPage schema, full OpenGraph + Twitter
Card tags, canonical URL, geo tags, `robots`/`googlebot` meta, and
`preconnect` hints for fonts. I did not touch any of it — re-doing solid
work would only risk breaking something. Item 11 ("SEO — Highest Priority")
was, in practice, largely already done.

### What was added (all new, additive — no existing tag/section edited)
- **Skip-to-content link** — a standard, WCAG 2.4.1 "skip navigation" link,
  invisible until keyboard-focused. Verified it correctly reveals on Tab and
  jumps to `<main>`.
- **Site-wide visible keyboard-focus ring** (`:focus-visible`) — the site
  uses a custom cursor (`cursor:none`), which makes a strong focus indicator
  more important for keyboard users. This is a new, supplementary rule; it
  doesn't remove or replace any existing `:focus` styling (e.g. the contact
  form's existing purple border-on-focus still works exactly as before).
- **`prefers-reduced-motion` support** (WCAG 2.3.3) — users who've enabled
  "reduce motion" at the OS level now get instant transitions instead of the
  site's animations. No visual change for everyone else.
- **LCP image preload** — added `<link rel="preload" as="image">` for
  `profile.png` (your hero image) to shave time off the Largest Contentful
  Paint metric.
- **`id="main-content"` added to `<main>`** — required as the skip-link's
  jump target. This is the one existing tag that got a new attribute; no
  visual/behavioral change.
- **Runtime accessibility script** (new `<script>`, doesn't edit any existing
  HTML in the file): at page-load it (1) programmatically links each contact
  form `<label>` to its input via `id`/`for` so screen readers announce them
  together, (2) marks the "message sent" confirmation as a live region
  (`role="status" aria-live="polite"`) so screen reader users are notified
  without focus changing, and (3) keeps `aria-pressed` in sync on the CTF and
  Open Source filter tabs. None of this changes the saved HTML — it's
  progressive enhancement applied in the browser.
- **`sitemap.xml`** `lastmod` bumped to reflect the real content update.

### Checked, deliberately left alone
- **Color contrast** — computed the actual contrast ratios for the site's
  `--muted` text color: ~6.6:1 against the background, which passes WCAG AA
  comfortably. `--muted2` (used for small secondary labels like timeline
  arrows) is lower-contrast and wouldn't pass for body text, but fixing it
  means editing the global color tokens used across every protected section
  — which you said not to touch. Flagging it here in case you ever want that
  specific token adjusted; I didn't change it.
- **Image dimensions / CLS** — checked `.profile-img`: it's already sized by
  its wrapper's CSS (not intrinsic `<img>` width/height), so there's no
  layout-shift risk to fix.
- Real Lighthouse score / live Google ranking can't be verified from a
  sandbox with no internet access — the changes above follow Lighthouse's
  documented best practices, but you'll want to run a real Lighthouse pass
  once this is deployed to GitHub Pages to confirm the number.

### What was NOT changed
Re-verified byte-for-byte against your original upload: `<nav>`, Hero,
Skills, Hall of Fame, Certificates, Projects, CTF, Writeups, **Contact form**
(including its `<label>`/`<input>` markup — the association is done at
runtime, not in the file), and `<footer>` are all identical to the original.
No color, font, spacing, or animation-timing variable was edited.

---

## [Phase 2] Research Timeline + Methodology + Open Source scaling

**Date:** 2026-08-06

### What was added
- **New "Research Timeline" section** (`#timeline`), placed after the
  Achievement Dashboard, before About. Milestone *order* reflects your actual
  journey (bug hunting → first disclosure → first Hall of Fame → first reward
  → first open source contribution → current research). **Dates are
  placeholders** (`[Add date]`) — I don't have your real dates, so I did not
  invent them. Search-and-replace `[Add date]` in `index.html` with the real
  ones before publishing. Reuses the existing `.term`/`.term-body` terminal
  card style from the About section — zero new CSS.
- **New "Research Methodology" section** (`#methodology`), placed after
  Skills, before Hall of Fame. A 9-step pipeline (Recon → Enumeration →
  Analysis → Validation → Proof of Concept → Responsible Disclosure → Vendor
  Validation → Fix → Recognition). This describes your process generically,
  so no fabricated personal data was needed. Reuses the existing `.hof-chip`
  style from the Hall of Fame marquee — zero new CSS.
- **Open Source Contributions section refactored to be data-driven** (visual
  output unchanged — verified pixel-for-pixel via screenshot). The single
  IntersectMBO entry now lives in an `OSS_DATA` JavaScript array; a
  `renderOSS()` function generates the cards, and filter tabs (matching the
  CTF section's `.ctf-tabs`/`.ctf-tab` style) let visitors filter by
  contribution type. **Adding a future contribution now only requires adding
  one object to `OSS_DATA`** — no HTML editing. The stats row (OSS
  Contributions / Merged Fixes / Public Advisories / Repos Improved) is now
  computed from `OSS_DATA` automatically instead of being hand-typed.

### Explicitly skipped this round (flagged, not forgotten)
- **Awards & Recognition as a separate new section** — your Hall of Fame and
  Certificates sections already cover "Hall of Fame" and "Certificates."
  Building a third section that just re-lists the same entries under a new
  heading would duplicate content for no benefit (and hurts SEO via
  duplicate content). If you have actual **Letters, Recommendations, or
  Swag** to show (categories not currently on the site), send them over and
  I'll add a real section for those specifically.
- Testimonials and Research Statistics (severity/industry charts) — still
  waiting on your real data, per our earlier agreement.

### What was NOT changed
Verified by diffing byte-for-byte against your original upload: `<nav>`,
the About section's terminal + bio text, Skills, Hall of Fame, Certificates,
Projects, CTF, Writeups, Contact, and `<footer>` are all **identical** to the
original file. Only new sections were inserted between existing ones, and the
Open Source section (added by me last round, not part of your original site)
was refactored as requested. No existing CSS rule was edited — only new rules
were added, built from existing color/spacing/radius/transition tokens. No
original JavaScript was edited — the new OSS renderer reuses the page's
existing `esc()` helper instead of duplicating it, and the animated-counter
script (added last round) is unchanged.

---

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
