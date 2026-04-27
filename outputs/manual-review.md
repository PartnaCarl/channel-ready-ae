# Manual Review — Pages Flagged

No pages were flagged as unclear. All HTML files in repo root classified cleanly into leadership / AE-facing / utility.

## Edge cases worth a second pair of eyes

These were classified and processed, but flagging them in case the call differs from yours:

### `faq.html` — classified leadership, no change applied
- Page addresses VPs/CROs evaluating the program (Q1 about licensing, Q4 about PSRA pricing, Q7 about employer-sponsored cohort) — that's leadership.
- But the page has no body-level CTA — only a nav-cta "Member Login" which is utility.
- **Action taken:** none. The nav-link `Assessment` (already present in nav) gives readers a path. Adding a CTA would require a layout change which the constraints prohibit.
- **Override option:** if you want me to insert a single line at the bottom of the page like *"Decision-maker? Take the Readiness Assessment →"*, say the word.

### `trace-playbook.html` — classified AE-facing, banner applied
- Page is the deep field-playbook reference material for paid students of the Multiplier Method. AE-facing by purpose.
- But VP-level readers may legitimately land here (e.g., evaluating curriculum depth). Banner correctly serves both audiences.

### `index.html` hero — duplicate CTAs collapsed
- Pre-swap state: hero had `"Enroll Your Team"` (primary, → `#apply`) AND `"Take the Free PSRA"` (ghost, → `assessment.html`).
- Post-swap state: only `"Take the Readiness Assessment →"` (primary, → `./assessment.html`).
- I deleted the ghost rather than swap-and-keep, per the spec line *"prefer fewer total CTAs over more."* If you want a secondary back, the natural one is `"See the curriculum →"` → `curriculum.html`.

### Pricing-tier cards on `index.html` — left untouched
- Lines 1061, 1075, 1089: "Book a Workshop", "Enroll Your Team", "Buy the Starter Kit" all pointing to `#apply`.
- These match the spec's *"Schedule a call / Book a demo / Get in touch"* pattern superficially, but they're the engagement ladder — distinct commercial actions per tier, not generic contact CTAs.
- Replacing all three with "Take the Assessment" would destroy the pricing-card structure. The PSRA tier card (#1) is already the assessment entry point.
- **Action taken:** leave. If you'd rather route Workshop/Cohort/Starter Kit cards to the PSRA as a soft entry, that's a 3-line change — flag and I'll do it.

### `module_01.html–module_12.html` "Enroll Now" nav-cta — left untouched
- Module pages are AE-facing per spec (banner-only treatment), but the nav-cta on every module says "Enroll Now" → `index.html#apply`.
- The banner above the nav now redirects decision-makers to the PSRA. The "Enroll Now" nav-cta below it is appropriate for the AE-trained audience.
- **Action taken:** leave. Both audiences have a path.

## Things outside scope, surfaced anyway

- The nav-logo on every page still says "The Multiplier Method™" rather than "Channel Ready AE™". Per CLAUDE.md brand hierarchy, the public-facing brand is Channel Ready AE; the methodology name belongs on methodology pages only. Not part of this task — flag for future site-wide rebrand pass.
- `business_plan.html` line 354's CTA was "Enroll Now" pre-swap — implying enrollment is the buyer's primary action. Post-swap, it's "Take the Assessment". The page body still has "Enroll" language elsewhere — those weren't touched per the no-content-rewrite constraint.
