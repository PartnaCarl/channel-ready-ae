# CTA Changes — Diff Summary

Local-only. No git commit yet.

## Files Modified

### Leadership pages (CTA swaps)

**`index.html`**
- Hero primary CTA (line 892):
  - `"Enroll Your Team"` → `"Take the Readiness Assessment →"`
  - `href="#apply"` → `href="./assessment.html"`
- Hero ghost CTA (was line 893): **deleted** — duplicated the new primary (both pointed to assessment.html)
- All other CTAs preserved (nav-cta "Member Login", 4 pricing-tier cards, footer links)

**`business_plan.html`**
- Nav-cta (line 354):
  - `"Enroll Now"` → `"Take the Assessment →"`
  - `href="index.html#apply"` → `href="./assessment.html"`
- All other content untouched

**`faq.html`**
- No changes — page has no buyer CTA to swap (only utility "Member Login"). Nav-link already exposes `Assessment` to readers.

### AE-facing pages (banner only)

**`curriculum.html`**, **`module_01.html` – `module_12.html`** (12 files), **`trace-playbook.html`**
- Inserted a single thin top banner directly after `<body>`:
  ```html
  <div role="region" aria-label="Audience notice" style="background:#0f0f0f;border-bottom:1px solid #242424;padding:10px 24px;text-align:center;font-family:'Crimson Pro',serif;font-size:12px;color:#a8a8a8;letter-spacing:0.02em;line-height:1.5;">For your AE team. Decision-makers: <a href="assessment.html" style="color:#e8c547;text-decoration:none;font-weight:500;">Take the Readiness Assessment →</a></div>
  ```
- Marker comment `<!--ae-banner-marker-->` placed above the banner so future automation can find/replace.
- Inline styles used (not stylesheet edits) to avoid touching the per-file `<style>` blocks across 14 files. Trade-off documented in `design-rationale.md`.

### Configuration

**`netlify.toml`**
- Updated redirect: `/assessment` → was `/channel_readiness.html`, now `/assessment.html`
- Added redirect: `/psra` → `/assessment.html` (vanity URL for outbound)

### New file

**`assessment.html`** — created (~30KB, single self-contained file)

---

## Files Untouched

- `login.html` — utility, no swap
- `assessment.html` was already touched earlier in session and is now fully rewritten as the PSRA destination
- All 4 pricing-tier card CTAs in `index.html` (Workshop / Cohort / Starter Kit / PSRA) — engagement ladder preserved
- All footer links across all pages
- All sidebar navigation in module files
- `/multiplier-vet/` and `/multiplier-landscaper/` — not in this repo

## Verification commands

```bash
cd "/Users/carl/Desktop/Channel Ready AE/website"

# confirm hero primary on index points to assessment
grep "btn-primary" index.html | grep "assessment"

# confirm business_plan nav-cta points to assessment
grep "nav-cta" business_plan.html

# confirm banner present on all 14 AE pages
grep -l "ae-banner-marker" *.html | wc -l   # expect 14
```
