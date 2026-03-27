# Marketing Site Audit Criteria

Apply these criteria in addition to the six baseline audit categories whenever the context profile is `marketing-site`.

---

## Above-the-Fold Effectiveness

["5-second test" — Nielsen Norman Group; Fogg, B.J. "Persuasive Technology", 2003]

- The value proposition must be clear within 5 seconds of viewing without scrolling
- The hero section must answer three questions: What is this? Who is it for? What do I do next?
- The primary CTA must be visible above the fold at a 1024px+ viewport width without scrolling

## CTA Strategy

[Eisenberg, B. "Call to Action", 2006]

- The primary CTA must be visually dominant: differentiated by size, color contrast, and surrounding whitespace
- CTA copy must be action-oriented and outcome-specific: "Start Free Trial" outperforms "Get Started" which outperforms "Submit"
- The CTA should repeat at logical scroll milestones: hero section, mid-page feature or proof section, and bottom of page
- Avoid CTA competition: one primary action per section — multiple competing CTAs in the same viewport reduce conversion

## Trust Signals

[Cialdini, R. "Influence", 1984 — Social Proof and Authority principles]

- **Social proof:** Testimonials, case studies, customer logos, review counts, user count statistics ("Join 10,000+ teams")
- **Authority signals:** Press mention logos, analyst recognition, awards, certifications
- **Risk reducers:** Free trial offer, "no credit card required", money-back guarantee, visible cancellation terms
- **Placement:** Trust signals should appear adjacent to CTAs and at high-friction decision points in the scroll journey

## Scroll Journey & Visual Storytelling

[Nielsen Norman Group — Scrolling and Attention research]

- The page narrative should follow a logical arc: Problem → Solution → Proof → CTA
- Visual flow: the eye should move naturally down the page without dead ends, orphaned content, or confusing jumps
- Section transitions: clear visual breaks between content sections (whitespace, dividers, or background color changes)
- The page should build momentum toward a primary conversion moment — content that meanders or loops back creates friction

## Friction Reduction

[Fogg, B.J. — Behavior Model; Nielsen Norman Group — Form Design Best Practices]

- Forms: minimize required fields; use inline validation; ensure autofill-compatible field names (name, email, etc.)
- Signup or checkout flows: progress indicators, clear error states, no surprise required fields
- Objection handling: FAQs, comparison tables, and "Who is this for?" / "Who is this not for?" sections placed near conversion points

## SEO & Performance Signals

[Google Search Central — Page Titles and Descriptions]

- H1 is present, above the fold, and descriptive of the page's primary purpose
- Images: are alt text placeholders or annotations visible in the design?
- Performance signals: excessive full-bleed video backgrounds, autoplay media, complex parallax animations, or very large image files may degrade Core Web Vitals (LCP, CLS) — flag these for engineering review

---

## Context-Enriched Modifiers (runtime inference)

When the user's description includes domain-specific detail beyond the marketing site type (e.g., "**SaaS** marketing site"), infer and apply relevant modifiers across all six audit categories at runtime. Apply these in addition to the criteria above. Examples:

- **SaaS marketing site** → feature comparison tables, pricing page patterns, free trial vs. demo request CTA strategy, integration partner logos, security/compliance trust badges
- **E-commerce landing page** → product imagery prominence, scarcity or urgency signals (stock count, countdown timer), customer reviews near the add-to-cart action, return policy visibility
- **Lead generation page** → form above the fold, minimal navigation to reduce exits, clear value exchange statement (what does the user get for submitting their email?), social proof quantity over quality
- **Event or launch page** → countdown timer as primary urgency driver, speaker or feature highlights, single focused CTA (register / waitlist / buy), no competing navigation
