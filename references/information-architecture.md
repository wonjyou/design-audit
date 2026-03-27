# Information Architecture Reference

## Core IA Components (Rosenfeld, Morville & Arango)
1. **Organization systems**: How content is categorized and structured
2. **Labeling systems**: How content is represented and named
3. **Navigation systems**: How users move through the content
4. **Search systems**: How users look for content

Reference: Rosenfeld, L., Morville, P. & Arango, J. (2015). *Information Architecture: For the Web and Beyond* (4th ed.). O'Reilly.

---

## Wayfinding
Users need to always know:
1. **Where am I?** — Current location clearly indicated (active nav state, breadcrumb, page title, URL)
2. **Where have I been?** — Visited link styling, breadcrumb trail, step indicators in flows
3. **Where can I go?** — Clear navigation options, visible affordances for exploration

Evaluate:
- Is the current page/section clearly labeled?
- Is there a page title or section header?
- Are breadcrumbs present for deep hierarchies?
- Do step indicators show progress in multi-step flows?

---

## Navigation Structure
**Types of navigation systems**:
- **Global/Primary**: Always present, represents top-level categories
- **Local/Secondary**: Sub-navigation within a section
- **Contextual**: In-page links, related content links
- **Supplemental**: Footer links, sitemap, index

**Evaluation criteria**:
- Are top-level categories mutually exclusive? (items don't fit in multiple places)
- Are top-level categories exhaustive? (all content has a home)
- Is the depth appropriate? (3–4 levels max before users get lost)
- Does the navigation reflect user mental models, not org structure?

**Card Sorting**: If IA seems off, recommend user card sorting exercise to validate categories.
Reference: [Card Sorting — NNg](https://www.nngroup.com/articles/card-sorting-definition/)

---

## Labeling Systems
- Labels should use language from the user's vocabulary, not the organization's internal terminology
- Consistent: same concept = same label throughout (don't say "Clients" in nav and "Customers" in the page)
- Specific: "Financial Reports" > "Reports"
- Brief: ideally 1–3 words for navigation labels

**Common labeling anti-patterns**:
- Marketing-speak in navigation ("Solutions", "Our Story", "Platform" without context)
- Jargon-heavy labels for non-technical audiences
- Inconsistent terminology across different sections

---

## Content Organization Patterns

**Hierarchical**: Parent-child relationships, tree structure. Best for: broad content sets, clear taxonomy.

**Sequential**: Step 1 → Step 2 → Step 3. Best for: onboarding, checkout, setup wizards.

**Matrix/Grid**: Equal-weight items in a grid. Best for: product catalogs, dashboards.

**Faceted**: Filter-based navigation. Best for: e-commerce, search results.

**Tag-based**: Non-hierarchical, many-to-many relationships. Best for: blogs, wikis, knowledge bases.

---

## Progressive Disclosure
**Principle**: Show only the information needed at each step. Reveal complexity only when the user needs it.

Apply when:
- Forms have advanced vs. basic options
- Settings have simple vs. expert modes  
- Content can be expanded with "Read more" / "Show details"
- Multi-step flows can hide later steps until earlier ones are complete

Reference: [Progressive Disclosure — NNg](https://www.nngroup.com/articles/progressive-disclosure/)

---

## Search
When to include search:
- Site has 200+ pages, OR
- Users arrive with a specific known item in mind, OR
- Content doesn't fit into clean categories

Evaluation criteria (if present):
- Is the search bar visible without scrolling?
- Are search results relevant and ranked well?
- Does it handle typos/synonyms?
- Are zero-result states handled gracefully?

---

## User Mental Models
IA should match how users think about the domain — not how the company is structured.
- Example: Users look for "Billing" not "Revenue Operations"
- Example: Users look for "Help" not "Knowledge Base"
- Test with: tree testing, first-click testing

Reference: [Mental Models — NNg](https://www.nngroup.com/articles/mental-models/)