# Web App Audit Criteria

Apply these criteria in addition to the six baseline audit categories whenever the context profile is `web-app`.

---

## Interactive States

[WCAG 2.1 — 1.4.11 Non-text Contrast; 2.4.7 Focus Visible]

- All interactive elements must have visible hover states (cursor pointer change + visual feedback such as color shift or underline)
- Focus indicators must be clearly visible for keyboard navigation: minimum 3:1 contrast ratio for the focus ring against adjacent colors
- Active/pressed states must be designed for buttons and links
- Disabled states must be visually distinct from enabled states and must not rely on color alone

## Pointer Target Sizes

- Minimum recommended target size: 24×24px [WCAG 2.5.8 — Target Size (Minimum)]
- AAA target size: 44×44px [WCAG 2.5.5 — Target Size (Enhanced)]
- Smaller targets are acceptable only when spacing ensures no adjacent target falls within 24px
- Icon buttons without visible text labels: minimum 32×32px with a clear affordance indicating interactivity

## Keyboard Navigation

[WCAG 2.1 — 2.1.1 Keyboard; 2.4.3 Focus Order]

- Tab order must follow logical reading order (left-to-right, top-to-bottom)
- All interactive elements must be reachable by keyboard
- Modal dialogs must trap focus within the dialog — focus must not escape to background content
- Complex layouts (multiple navigation regions, data tables) should include skip navigation links

## Dense Information Layouts

[Nielsen Norman Group — Data Tables UX]

- **Tables:** Are sortable column indicators visible? Row hover states designed? Sticky column or row headers for long content? Overflow handling for narrow viewports?
- **Toolbars:** Are actions grouped logically? Is overflow/ellipsis behavior designed for narrower viewports?
- **Sidebars:** Is the sidebar collapsible? Is the active/current section visually indicated? Is a resize handle provided if the sidebar width is variable?
- **Data grids:** Are row selection states designed? Are bulk action patterns accounted for?

## Responsive Signals

- Assess whether fixed-width layouts will break at common breakpoints: 768px (tablet), 1024px (small desktop), 1440px (standard desktop)
- Horizontal scroll at any common breakpoint is a red flag in web apps
- At tablet breakpoints (768px–1024px), pointer targets should approach mobile minimums (44×44px) to accommodate touch input

## Dashboard-Specific Criteria (apply if applicable)

[Few, S. "Show Me the Numbers", 2012; Nielsen Norman Group]

- **Data hierarchy:** Most important KPIs prominent, secondary data clearly subordinate
- **Scannable layout:** F-pattern or Z-pattern reading flow honored; avoid placing critical data in the middle of long rows
- **Progressive disclosure:** Drill-down details available on demand without cluttering the primary view
- **Empty states:** All widgets, charts, and data tables must have designed empty states (what appears before data loads or when no data exists?)
- **Loading states:** Skeleton screens or spinners designed for all async data regions

---

## Context-Enriched Modifiers (runtime inference)

When the user's description includes domain-specific detail beyond the web app type (e.g., "**B2B SaaS** dashboard"), infer and apply relevant modifiers across all six audit categories at runtime. Apply these in addition to the criteria above. Examples:

- **B2B SaaS dashboard** → power-user density is acceptable, keyboard shortcut discoverability, data export and share workflows, role-based UI signals, onboarding empty states
- **Internal admin tool** → efficiency over aesthetics, bulk action patterns, confirmation dialogs on all destructive operations, audit trail visibility
- **E-commerce checkout** → progress indicator showing checkout steps, form field optimization (autofill, inline validation), trust signals near payment entry, clear error recovery
- **Project management tool** → drag-and-drop interaction signals, multi-select patterns, date picker UX, notification/alert placement
