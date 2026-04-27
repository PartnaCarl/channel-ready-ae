# CTA Audit — Channel Ready AE Site

Audit performed at the start of the PSRA build. Each tracked HTML file in repo root.

## index.html
Page type: leadership
Existing primary CTA: "Enroll Your Team" → `#apply`
Existing secondary CTAs: "Take the Free PSRA →" → `assessment.html` (hero ghost); "Take the Free PSRA →" → `assessment.html` (pricing card 1); "Book a Workshop" → `#apply` (pricing card 2); "Enroll Your Team" → `#apply` (pricing card 3); "Buy the Starter Kit" → `#apply` (pricing card 4); "Member Login" → `login.html` (nav-cta)
Recommended action: **swap to PSRA** — replace hero primary text + href, delete duplicate hero ghost. Leave pricing-tier card CTAs intact (they form the engagement ladder).

## business_plan.html
Page type: leadership
Existing primary CTA: "Enroll Now" → `index.html#apply` (nav-cta — only top-fold CTA on the page)
Existing secondary CTAs: none
Recommended action: **swap to PSRA**

## faq.html
Page type: leadership
Existing primary CTA: "Member Login" → `login.html` (nav-cta only — page has no body-level CTA)
Existing secondary CTAs: none
Recommended action: **leave** — Member Login is utility, not a buyer CTA. Nav already exposes `Assessment` link to leadership.

## curriculum.html
Page type: AE-facing
Existing primary CTA: "Member Login" → `login.html` (nav-cta)
Existing secondary CTAs: "Open the Playbook →" → `trace-playbook.html`
Recommended action: **banner-only** — add thin top banner directing decision-makers to PSRA.

## module_01.html — module_12.html (12 files)
Page type: AE-facing
Existing primary CTA: "Enroll Now" → `index.html#apply` (nav-cta)
Existing secondary CTAs: previous/next module navigation, sidebar tab nav (intra-module)
Recommended action: **banner-only** — add thin top banner across all 12 module pages.

## trace-playbook.html
Page type: AE-facing
Existing primary CTA: "Member Login" → `login.html` (nav-cta); "Go to Curriculum" → `curriculum.html`
Existing secondary CTAs: none
Recommended action: **banner-only** — playbook is paid-student reference material, AE-facing.

## login.html
Page type: utility
Existing primary CTA: "Access the Curriculum" (login button — gate auth)
Recommended action: **leave** — utility page, no swap.

## assessment.html
Page type: utility (this is the destination — the new PSRA page itself)
Recommended action: **N/A** — this is the build target, not a swap target.

---

## Page-type counts

| Type | Count | Files |
|---|---|---|
| Leadership | 3 | index.html, business_plan.html, faq.html |
| AE-facing | 14 | curriculum.html, module_01.html–module_12.html, trace-playbook.html |
| Utility | 2 | login.html, assessment.html |
| Vertical-proof | 0 | (none in this repo — `/multiplier-vet/` and `/multiplier-landscaper/` live elsewhere) |
| Unclear | 0 | none |
