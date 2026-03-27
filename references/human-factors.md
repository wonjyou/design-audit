# Human Factors Reference

## Fitts's Law
**Principle**: The time to acquire a target is a function of the distance to and size of the target.
**Formula**: T = a + b × log₂(2D/W) — larger and closer = faster to hit.
**Implications for UI**:
- Primary CTAs should be large (generous padding) and in predictable locations
- Destructive actions (delete, cancel) should be smaller and/or further from primary actions
- On mobile, key actions should be in the thumb zone (bottom 60% of screen)
- Avoid placing critical actions at screen corners or edges (except on touch where edges are easy)
- Corner targets on desktop are actually easy due to infinite size (cursor stops at edge)

**Reference**: Fitts, P.M. (1954). The information capacity of the human motor system in controlling the amplitude of movement. *Journal of Experimental Psychology*, 47(6), 381–391. https://doi.org/10.1037/h0055392

---

## Hick's Law (Hick-Hyman Law)
**Principle**: The time it takes to make a decision increases with the number and complexity of choices.
**Formula**: RT = a + b × log₂(n + 1)
**Implications for UI**:
- Limit primary navigation items to 5–7 options
- Use progressive disclosure to hide advanced options
- Group related options to reduce perceived complexity
- Avoid presenting all features simultaneously on a dashboard
- Wizards and stepped flows reduce decision paralysis

**Reference**: Hick, W.E. (1952). On the rate of gain of information. *Quarterly Journal of Experimental Psychology*, 4(1), 11–26.

---

## Miller's Law
**Principle**: The average person can hold 7 (±2) items in working memory at once.
**Implications for UI**:
- Navigation menus: ideally 5–7 items
- Wizards: break long forms into 3–5 step chunks
- Group related form fields under section headers
- Paginate long lists rather than infinite scroll where memorization matters
- Use progressive disclosure for complex settings

**Reference**: Miller, G.A. (1956). The magical number seven, plus or minus two. *Psychological Review*, 63(2), 81–97.

---

## Jakob's Law
**Principle**: Users spend most of their time on other sites, so they prefer your site to work like all the other sites they already know.
**Implications for UI**:
- Logo top-left → links to home page
- Shopping cart icon in top-right
- Search bar in header
- Login/account in top-right
- Footer = less important links, legal, social
- Hamburger menu = hidden navigation (mobile)
- Deviating from conventions requires a compelling reason AND clear signposting

**Reference**: https://www.nngroup.com/videos/jakobs-law-internet-ux/

---

## Serial Position Effect
**Principle**: People tend to remember the first (primacy) and last (recency) items in a list better than middle items.
**Implications for UI**:
- Place most important navigation items first or last
- Key CTAs at the end of a flow benefit from recency
- Don't bury the most critical option in the middle of a list
- Consider this when ordering dropdown options

---

## Gestalt Principles
**Proximity**: Elements close together are perceived as related.
**Similarity**: Elements that look alike are perceived as related.
**Continuity**: The eye follows paths and lines.
**Closure**: The mind fills in missing information to complete shapes.
**Figure/Ground**: Elements are perceived as either objects (figure) or background.

**Implications for UI**:
- Use spacing to group form fields with their labels
- Use consistent styling for all clickable elements
- Use visual lines/dividers sparingly — proximity usually suffices
- Avoid orphaned labels or buttons that appear disconnected from their context

---

## Cognitive Load Theory
**Principle**: Working memory has limited capacity. Extraneous cognitive load should be minimized.

**Three types**:
- **Intrinsic**: Complexity inherent to the content (can't eliminate, but can scaffold)
- **Extraneous**: Unnecessary complexity from poor design (ELIMINATE THIS)
- **Germane**: Cognitive effort that leads to learning/understanding (keep and support this)

**Implications for UI**:
- Reduce visual noise (extraneous load)
- Use familiar patterns so users don't have to learn new interactions
- Show only the information needed at each step
- Use defaults intelligently to reduce required decisions
- Inline validation reduces the mental effort of remembering error rules

**Reference**: Sweller, J. (1988). Cognitive load during problem solving. *Cognitive Science*, 12(2), 257–285.

---

## Tesler's Law (Law of Conservation of Complexity)
**Principle**: Every application has an inherent amount of complexity that cannot be removed — it can only be shifted (from user to system, or vice versa).
**Implication**: If a feature is complex, the complexity should be handled by the system (smart defaults, automation, validation) — not pushed onto the user.

---

## Peak-End Rule
**Principle**: People judge an experience largely based on how they felt at its most intense point and at the end.
**Implications for UI**:
- Design confirmation screens / success states with care — they're the "end" of a flow
- Minimize the pain of the hardest step in a flow (often: long forms, payment, account creation)
- A delightful end state can redeem a difficult journey