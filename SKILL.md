---
name: design-critique-agent
description: |
  A comprehensive design review and audit agent for UI/UX designers, product teams, and developers. 
  Use this skill whenever a user wants feedback on a design, visual mockup, UI screenshot, or Figma file. 
  Triggers include: "review my design", "audit this UI", "give me design feedback", "critique this screen", 
  "what's wrong with my design", "UX review", "accessibility audit", "heuristic evaluation", or any request 
  to analyze a design file or image. Also triggers when a Figma URL or image of an interface is shared. 
  Always use this skill when the user uploads a design image or shares a Figma link and wants any kind of 
  evaluation, even if they just say "thoughts?" or "what do you think?".
compatibility: "Requires vision/image analysis capability. Optionally uses Figma MCP (https://mcp.figma.com/mcp) when a Figma file URL is provided instead of a static image."
---

# Design Critique Agent

A structured design audit tool that evaluates UI/UX designs against established design principles, 
usability heuristics, accessibility standards, and human factors research. Works with static images 
(screenshots, mockups, exports) or live Figma files via MCP.

---

## Step 0A: Collect Design Context

Before beginning the audit, determine the design's context:

- If the user's triggering message already contains a description that includes **both** a platform signal (e.g., "iOS", "Android", "mobile", "web", "website", "landing page") **and** a domain/purpose signal (e.g., "fitness", "SaaS", "e-commerce", "dashboard"), extract it directly — do not ask.
- If the description is thin — containing only one or neither of these signals (e.g., "my app", "a website", "this design") — treat it as no description and ask.
- If no description was provided, ask:
  > "Before I begin — can you briefly describe what this design is for? For example: 'iOS fitness app', 'SaaS web dashboard', 'marketing landing page', or anything else that describes its purpose and platform."
- Wait for the user's response before continuing.

---

## Step 0B: Classify Context Profile

From the description, classify into one of four profiles using the following rules:

| Profile | Classification signals |
|---------|----------------------|
| `mobile-app` | Mentions "app", "iOS", "Android", "mobile", "phone", "tablet"; design has mobile viewport proportions; contains bottom navigation, tab bars, or FABs |
| `web-app` | Mentions "dashboard", "SaaS", "admin", "tool", "portal", or "app" in a web context; design is wide-viewport; contains sidebars, toolbars, data tables, or authenticated UI |
| `marketing-site` | Mentions "landing page", "marketing", "homepage", "website", or "campaign"; design is conversion-focused with no authenticated state; contains hero sections, testimonials, or pricing |
| `other` | Does not clearly match any above; OR matches multiple equally |

**Ambiguous case resolution:**
- "e-commerce product page" → `marketing-site` (conversion-focused, no auth required)
- "e-commerce checkout" → `web-app` (authenticated flow, form-heavy, process-oriented)
- "progressive web app" → `mobile-app` if design has mobile proportions; `web-app` if desktop-wide
- "onboarding wizard" → `web-app` if SaaS context; `mobile-app` if phone proportions; `other` if unclear
- "internal admin tool" → `web-app`
- "tablet kiosk app" → `mobile-app`

When in doubt, prefer `other` over a forced match. State the classification and your reasoning at the start of the audit:
> "I'll evaluate this as a **mobile app** (iOS fitness) — applying mobile-app criteria with fitness context modifiers."

---

## Step 0C: Determine Input Type

Identify what the user has provided:

**Option A — Static Image**: The user uploaded a screenshot, mockup, or design export.
- Proceed directly to the audit using vision capabilities.

**Option B — Figma File URL**: The user provided a Figma link (figma.com/file/... or figma.com/design/...).
- Use the Figma MCP to fetch the file. Call `get_design_context` with the node URL.
- If Figma MCP is unavailable, ask the user to export the design as an image.

**Option C — No design provided**: Ask the user to share either a Figma link or an image before proceeding.

---

## Step 1: Confirm Context & Orientation

Using the context profile established in Step 0B as your starting point, visually confirm or refine your understanding of the design:

1. **Confirm interface type:** Does the visual match the classified profile (e.g., does a "mobile app" description match mobile-proportioned screens)? If the visual evidence contradicts the user's description, note the discrepancy, state which you will use as the basis for evaluation, and ask for clarification if needed.
2. **Confirm apparent purpose:** Does what you see align with the described domain (e.g., fitness, SaaS, e-commerce)?
3. **Who is the likely target user?** (infer from context: technical vs. non-technical, age range, domain expertise)
4. **What is the primary user task?** (what action is the user most likely trying to complete?)

State your confirmed assumptions at the top of your report. These frame the entire critique and ensure feedback is contextually appropriate.

---

## Step 2: Run the Six-Category Audit

Evaluate the design across all six categories below. For each finding, apply the **ASK Framework** and **Severity Scoring** (see Step 3).

Read the full reference files for detailed criteria:
- Visual design criteria → `references/visual-design.md`
- UX heuristics criteria → `references/ux-heuristics.md`
- UI patterns criteria → `references/ui-patterns.md`
- Human factors criteria → `references/human-factors.md`
- UX copy criteria → `references/ux-copy.md`
- Information architecture criteria → `references/information-architecture.md`
- Context-specific criteria → `references/[profile].md` (loaded based on Step 0B classification — `mobile-app`, `web-app`, or `marketing-site`; for `other` context, apply the inferred focus areas stated in Step 0B instead)

### Category 1: Visual Design

> **Context modifiers active:** For `mobile-app`, `web-app`, or `marketing-site` — apply relevant visual criteria from `references/[profile].md` in addition to the baseline below. For `other` — no profile file loaded; apply the inferred focus areas stated in Step 0B.

Evaluate: hierarchy, spacing, alignment, typography, color, consistency, aesthetics, brand cohesion, visual weight, use of white space, contrast ratios.

Key questions:
- Is there a clear visual hierarchy that guides the eye?
- Is spacing consistent and using a grid or spacing scale?
- Is typography legible, with appropriate size/weight hierarchy?
- Are colors used purposefully and consistently?
- Does the design feel cohesive and polished?

### Category 2: UX Design — Usability Heuristics

> **Context modifiers active:** For `mobile-app`, `web-app`, or `marketing-site` — apply relevant UX criteria from `references/[profile].md` in addition to the baseline below. For `other` — no profile file loaded; apply the inferred focus areas stated in Step 0B.

Apply **Jakob Nielsen's 10 Usability Heuristics** (1994):
1. Visibility of system status
2. Match between system and real world
3. User control and freedom
4. Consistency and standards
5. Error prevention
6. Recognition rather than recall
7. Flexibility and efficiency of use
8. Aesthetic and minimalist design
9. Help users recognize, diagnose, and recover from errors
10. Help and documentation

Additionally evaluate:
- **Affordance**: Do interactive elements look interactable?
- **Accessibility / WCAG 2.1**: Check AA compliance for color contrast (4.5:1 text, 3:1 UI), touch target sizes (min 44×44px), keyboard navigability signals, alt text signals
- **Error handling**: Are there visible error states, confirmation dialogs, undo mechanisms?

### Category 3: UI Design — Patterns

> **Context modifiers active:** For `mobile-app`, `web-app`, or `marketing-site` — apply relevant UI pattern criteria from `references/[profile].md` in addition to the baseline below. For `other` — no profile file loaded; apply the inferred focus areas stated in Step 0B.

Evaluate the use of established UI design patterns:
- **Buttons**: Primary/secondary/tertiary hierarchy clear? CTAs prominent? Disabled states handled?
- **Forms & Input Fields**: Labels visible? Placeholder text not replacing labels? Validation states present?
- **Navigation / Menus**: Consistent positioning? Active states indicated? Overflow handled (hamburger, etc.)?
- **Cards & Lists**: Consistent structure? Tappable areas clear?
- **Modals & Overlays**: Dismissible? Focus trapped appropriately?
- **Empty States**: Designed? Helpful guidance present?
- **Loading States**: Skeleton screens or spinners present where needed?

Reference: [UI Patterns Library](https://ui-patterns.com/), [Nielsen Norman Group](https://www.nngroup.com/articles/)

### Category 4: Human Factors

> **Context modifiers active:** For `mobile-app`, `web-app`, or `marketing-site` — apply relevant human factors criteria from `references/[profile].md` in addition to the baseline below. For `other` — no profile file loaded; apply the inferred focus areas stated in Step 0B.

Evaluate using established human factors principles:
- **Fitts's Law**: Are touch/click targets large enough and placed where users expect them? Primary actions should be large and easy to reach. [Fitts 1954, doi:10.1037/h0055392]
- **Hick's Law**: Is the number of choices appropriate? Too many options increases decision time. Aim for 7±2 items in navigation. [Hick 1952]
- **Miller's Law**: Is information chunked into groups of ~7±2? Are long lists or flows broken into digestible steps?
- **Jakob's Law**: Does the design follow conventions users know from other products? (e.g., logo top-left = home)
- **Serial Position Effect**: Are the most important items placed first or last in lists/nav? (primacy/recency)
- **Gestalt Principles**: Are proximity, similarity, continuity, and closure used to organize information?
- **Cognitive Load**: Is the interface demanding too much working memory? Are labels, icons, and actions self-explanatory?

### Category 5: UX Copy

> **Context modifiers active:** For `mobile-app`, `web-app`, or `marketing-site` — apply relevant copy criteria from `references/[profile].md` in addition to the baseline below. For `other` — no profile file loaded; apply the inferred focus areas stated in Step 0B.

Evaluate all text in the interface:
- **Clarity**: Is the language plain and unambiguous? Avoid jargon unless the audience demands it.
- **Helpfulness**: Does microcopy guide users, reassure them, or explain what's happening?
- **Call-to-Actions (CTAs)**: Are CTAs action-oriented, specific, and outcome-focused? ("Save Changes" > "OK"; "Start Free Trial" > "Submit")
- **Labeling**: Are form labels, nav items, and section headers descriptive and consistent in voice/tense?
- **Error Messages**: Do errors explain what went wrong AND how to fix it? Avoid "Error 404" without context.
- **Onboarding / Empty State Copy**: Does it explain value and guide the next step?
- **Tone consistency**: Is the brand voice consistent throughout?

Reference: [Mailchimp Content Style Guide](https://styleguide.mailchimp.com/), [Writing for UX — NNg](https://www.nngroup.com/articles/writing-for-ux/)

### Category 6: Information Architecture

> **Context modifiers active:** For `mobile-app`, `web-app`, or `marketing-site` — apply relevant IA criteria from `references/[profile].md` in addition to the baseline below. For `other` — no profile file loaded; apply the inferred focus areas stated in Step 0B.

Evaluate structure, navigation, and wayfinding:
- **Wayfinding**: Can users always tell where they are? Are breadcrumbs, active states, or page titles present?
- **Navigation Structure**: Is the hierarchy logical? Are categories mutually exclusive and exhaustive?
- **Labeling Systems**: Are menu/section labels clear and predictable?
- **Search**: If present, is it visible and functional? If absent, should it be?
- **Content Organization**: Is related content grouped? Is progressive disclosure used where appropriate?
- **User Mental Models**: Does the IA match how users think about the domain?

Reference: [IA Institute](https://www.iainstitute.org/), Rosenfeld et al. *Information Architecture* (4th ed.)

---

## Step 3: ASK Framework + Severity Scoring

### The ASK Framework
Every piece of feedback must be:
- **Actionable**: Tell the designer exactly what to change. Not "this is confusing" but "change the CTA label from 'Go' to 'Continue to Payment'."
- **Specific**: Reference the exact element (e.g., "the blue button in the top-right corner", "the 12px body text in the card description").
- **Kind**: Frame critique constructively. Acknowledge intent, explain the principle, then offer the fix. Avoid "this is wrong" — prefer "this could be even stronger by..."

### Severity Scoring
Assign one of four severity levels to each finding:

| Level | Label | Description |
|-------|-------|-------------|
| 🔴 | **Critical** | Blocks task completion, causes data loss, or fails accessibility in a way that excludes users. Fix before launch. |
| 🟠 | **Major** | Significantly impairs usability or comprehension. Strong likelihood of user confusion or abandonment. High priority. |
| 🟡 | **Minor** | Noticeable friction or inconsistency. Users can work around it, but the experience suffers. Address in next iteration. |
| 🔵 | **Cosmetic / Low** | Polish-level improvements. Minimal user impact. Nice-to-have in backlog. |

---

## Step 4: Structure the Output Report

Deliver the critique in this format:

---

### 🎨 Design Critique Report

**Design Summary**
> Brief description of the interface type, apparent purpose, and assumed user context.

**Context Profile**
> The context profile applied in this audit. Example: "Mobile App (iOS fitness) — mobile-app profile + fitness context modifiers" or "Other — inferred focus: progressive disclosure, cognitive load, error prevention."

**Overall Impression**
> 2–3 sentences on the design's strengths and the most pressing area for improvement.

---

**Findings by Category**

For each category, list findings in descending severity order.

#### [Category Name]
**[Severity Emoji + Label] — [Short Finding Title]**
- **What**: Describe the specific issue and where it appears.
- **Why it matters**: Reference the principle or standard (link when possible).
- **Suggestion**: The specific, actionable fix.

---

**Priority Summary Table**
| # | Severity | Category | Finding | Suggested Fix |
|---|----------|----------|---------|---------------|
| 1 | 🔴 Critical | ... | ... | ... |
| 2 | 🟠 Major | ... | ... | ... |
| ... | | | | |

---

**Quick Wins** (3–5 high-impact, low-effort improvements)
1. ...
2. ...

**Strengths to Preserve**
- List 1–5 things the design does well that should not be changed.

---

## Step 5: Offer Follow-Up

After delivering the report, offer:
1. A deeper dive into any single category
2. A revised version of specific copy (UX copy improvements)
3. A checklist version of findings for dev handoff
4. Re-evaluation after revisions are made
5. Export as a visual HTML report — open in your browser and use File → Print → Save as PDF

---

## Step 6: Export as HTML Report

**Trigger:** User selects option 5 from Step 5, or uses language like "export", "PDF", "generate report", "HTML report". If the user uses ambiguous save language (e.g., "save that", "save this") without clearly indicating they want an HTML file, ask: "Did you want to export this as a visual HTML report for PDF printing?"

Do not run this step unless the Step 4 audit report has already been delivered in this session.

**Instructions:**

1. Read `references/report-template.md` for exact color values, component specs, section order, CSS class names, and print rules. Follow it precisely.
2. Compose the full HTML document using the audit report content delivered in Step 4. Do not re-run the audit — reuse the findings already produced.
3. **Screenshot handling** (self-containment is the goal):
   - If a Figma screenshot URL was returned by the Figma MCP during this audit session:
     - Attempt to fetch and base64-encode the image using the Bash tool:
       - macOS: `curl -s "[url]" | base64`
       - Linux: `curl -s "[url]" | base64 -w 0`
       - Windows/Git Bash: `curl -s "[url]" | base64 -w 0`
     - Detect the image MIME type from the URL (look for `.jpg`/`.jpeg` → `image/jpeg`, `.webp` → `image/webp`, otherwise assume `image/png`). Embed as `<img src="data:[mime-type];base64,[encoded]" alt="Design screenshot" style="max-width:100%; border-radius:8px; margin-bottom:24px; display:block;">` immediately after the Summary block.
     - If the Bash tool is unavailable or the `curl` fetch fails, fall back to embedding the URL directly: `<img src="[url]" alt="Design screenshot" style="max-width:100%; border-radius:8px; margin-bottom:24px; display:block;">`. Add an HTML comment above it: `<!-- Note: image URL expires in ~7 days -->`.
   - If the audit was performed on a static uploaded image (no Figma URL), omit the screenshot element entirely.
4. Write the HTML file to the current working directory using the Write tool. Filename: `design-audit-report-YYYY-MM-DD.html` (today's date in ISO 8601 format, e.g. `design-audit-report-2026-03-27.html`).
5. Confirm to the user:
   > "Report saved to `design-audit-report-YYYY-MM-DD.html`. Open it in your browser, then File → Print → Save as PDF."
6. If the Write tool is unavailable, inform the user and offer to display the full HTML in a code block so they can copy-paste it manually.

---

## Notes for the Agent

- **Be specific about location**: Always describe where on the screen the issue appears. Use annotations (top-left, bottom-right), section names, or element descriptions.
- **Don't over-critique cosmetics on early-stage work**: If the design appears to be a wireframe or low-fidelity mockup, focus on structure/UX over visual polish.
- **Adjust depth to context**: A quick "any thoughts?" deserves a shorter summary + top 5 findings. A formal audit request deserves the full report.
- **When Figma data is available**: You may also reference component names, layer names, and design token usage in your critique.
- **WCAG checking**: When checking color contrast, note that you're making a visual estimate — recommend the designer verify with a contrast checker tool such as [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/).