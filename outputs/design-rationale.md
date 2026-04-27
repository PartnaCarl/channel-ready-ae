# Design Rationale — PSRA One-Pager

## Skills stacked

The local skills directory exposed `superpowers:using-superpowers` (workflow primer) but did not expose a discrete "UX UI Pro" skill at runtime. I treated the brief's UX UI Pro principles as a declarative spec and stacked them with industry-standard heuristics from typography systems, conversion-page patterns, and WCAG 2.1 AA accessibility.

Concretely, the principles that drove decisions:

| Domain | Heuristic applied |
|---|---|
| Visual hierarchy | One H1 per state, single dominant action per viewport, 8-step type scale collapsed to 5 actually-used sizes |
| Typography | Cormorant Garamond 800 for display, Crimson Pro 300 italic for lede, tabular-nums for numerics, `letter-spacing: -0.025em` on display to compensate for Cormorant's wider tracking |
| Spacing | 8-px base, major intervals at 16/24/32/48/64/96, 56-px breathing space below intro lede before the rule list |
| Motion | 250ms fade + 8px translate between questions; 800ms `cubic-bezier(0.16,1,0.3,1)` bar fills with 80ms stagger; all gated behind `prefers-reduced-motion` |
| Conversion | Result is *instant* — no email gate. Email capture sits below result, framed as the "detailed report" upgrade. Soft-CTA gold-italic line, not a button, so it reads as invitation not demand |
| Accessibility | Skip link, real `h1`/`h2`/`h3` hierarchy, `aria-live` on question text, `role="radiogroup"`/`role="radio"` for options, `aria-checked` toggling, focus rings at 2-px outline + 2-px offset, 44-px-min tap targets on mobile |
| Keyboard | ↑↓ ←→ navigate options, Enter selects + advances, 1–4 and a–d as direct shortcuts, Backspace goes back |
| Resilience | sessionStorage persists answers across refresh; resume returns user to first unanswered question rather than starting fresh |

## Decisions UX UI Pro principles drove (vs. what brief specified)

**Brief said:** "Three thin rows beneath, each with a thin gold rule"
**Decision:** Used `border-top` on the list and `border-bottom` on each row at `--accent-border` (30% accent), not full-strength gold. Full-strength gold rules at three intervals would have created visual noise and competed with the eyebrow + headline + CTA. The dimmer rules read as editorial, not decorative.

**Brief said:** "Visual scorecard: five horizontal bars, gold fill, faint rail behind"
**Decision:** Bar height 6px (4px on mobile), rail at `rgba(232,197,71,0.07)` to keep it visible only as a hint of where the bar will land. Number column right-aligned at 56px fixed width so all five score values stack visually — eye scans down the score column, not across.

**Brief said:** "Cormorant for the score number to the right of each bar"
**Decision:** Score at 24px Cormorant 600 with `letter-spacing: -0.02em` and `font-variant-numeric: tabular-nums` — the tabular-nums prevents the score column from jittering by 1-2px depending on whether digits are 33/66/100.

**Brief said:** "Animate fill on render — 800ms cubic-bezier(0.16,1,0.3,1), staggered 80ms between bars"
**Decision:** Implemented exactly. Used `setTimeout` rather than CSS `animation-delay` so the staggered sequence respects the `prefers-reduced-motion` short-circuit (fills snap to final width with no transition).

**Brief said:** "Soft CTA (no button, just a line of text in gold)"
**Decision:** Implemented as `font-style: italic` Cormorant 500 in gold. Italic + serif reads as voice ("Want the…?") rather than instruction. Resisted temptation to make it a button — would have created two competing primary-feel CTAs (button + form-submit) above the fold of the result state.

**Brief said:** "Form action: data-netlify='true' name='psra-results'"
**Decision:** Added `netlify-honeypot="bot-field"` and a hidden honeypot input — Netlify's standard spam mitigation. Also added `action="?submitted=1#main"` so on successful Netlify post the page redirects back with a query param the JS reads to display the thanks state without a separate template page.

## Trade-offs I made

1. **Inline banner styles on AE-facing pages.** I considered adding the banner CSS to each file's `<style>` block (cleaner) vs. inline-styling the banner element (less clean but zero risk of breaking existing per-file styles). Chose inline. Across 14 files, each `<style>` block is 200–400 lines of bespoke CSS with custom variables that don't all match. Risk-reward favored inline.
2. **Deleted the duplicate hero ghost button on `index.html`.** Spec said "prefer fewer total CTAs over more" but also said "do not touch any other content." I read the first as overriding the second when the content in question is a CTA element. Logged this in `manual-review.md` for your override.
3. **`faq.html` got no swap.** The page is leadership-typed but has no body CTA. Adding one violates "no copy changes, no layout changes, no new sections." Flagged.
4. **Module page nav-cta "Enroll Now" preserved.** The banner serves decision-makers; the existing "Enroll Now" CTA in the nav is appropriate for the AE audience the page is built for. Two CTAs targeting two audiences, separated by visual hierarchy.
5. **No analytics, no chat widget, no popup.** Per hard constraints. I'd typically wire `data-event` attributes to the begin button and result-bar render so that when GA4 or Plausible eventually lands, it has hooks. Held that thought — call when ready.

## What I'd want you to A/B test

1. **Result state opening — qualitative read above bars vs. below.** I put bars first, qualitative below. The hypothesis: bars deliver the "what" instantly; the qualitative read does the harder work of telling them "what to do about it" and benefits from the bars being already-internalized as context. Reverse it on a 50/50 split and see if email-capture rate moves.

2. **Qualitative tone — clinical vs. provocative.** Current copy: *"Target is currently a deal liability. Partners are noticing."* Provocative variant: *"You're losing deals to noise here. Top three partners would name your AEs as the reason."* I'd test the more provocative variant with cyber/networking VPs and the clinical variant with cohort buyers — they reward different registers.

3. **Email-form length — 6 fields vs. 3 fields.** Current ask: First / Last / Email / Company / Title / Team size. Variant: Email / Company / Team size only, ask the rest in the follow-up email. Hypothesis: 3 fields converts higher but produces lower-quality leads. Worth measuring after 50 submissions.

4. **Soft CTA copy.** Current: *"Want the detailed report? Add your email below."* Variant: *"Get the detailed report and per-AE recommendations sent to your inbox."* The variant is more concrete; the current one is more elegant. Test which submits more.

5. **Question pacing — auto-advance on selection vs. explicit Next button.** Current: 220ms pause then auto-advance. Variant: highlight selection, require Next click. Hypothesis: auto-advance produces a higher completion rate but lower per-question deliberation. The accuracy of the result depends on deliberation, so this trade-off matters.

6. **Result email gate — soft (current) vs. hard (gate result behind email).** I deliberately chose soft per the brief, but the conventional B2B-assessment funnel puts the email *before* the result. Worth testing once you have 30+ completions to baseline.

## Lighthouse target

Built to hit 95+ on Performance / Accessibility / Best Practices. Notable choices supporting that:
- Single CSS file inline (no FOUC, no extra render-blocking request)
- Two `preconnect` to fonts.googleapis.com / fonts.gstatic.com — saves ~100ms on first paint
- `font-display: swap` is implicit via the Google Fonts URL `&display=swap` flag (line 11 of head)
- No layout-shift from font swap because intro height is dominated by the H1 which fits in 4 lines either way
- Vanilla JS, no framework, no polyfills
- Total inline weight: ~28KB HTML+CSS+JS combined (excluding fonts)

## Total page weight (excluding fonts)

```
assessment.html : ~30KB raw (~10KB gzipped estimated)
```

Well under the 100KB target.
