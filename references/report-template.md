# Design Audit Report: HTML Template Guide

This file is a style and structure guide for HTML report generation. It is not actual HTML — it defines the exact values, specs, and CSS class names the agent uses when composing the HTML output in Step 6.

---

## Color Tokens

```
Severity colors (left-border, badge backgrounds, and text):
  Critical:  border #ef4444  |  background #fef2f2  |  text #991b1b
  Major:     border #f97316  |  background #fff7ed  |  text #9a3412
  Minor:     border #eab308  |  background #fefce8  |  text #713f12
  Cosmetic:  border #3b82f6  |  background #eff6ff  |  text #1e40af

Neutral palette:
  Page background:    #f8fafc
  Card background:    #ffffff
  Card border:        #e2e8f0
  Heading text:       #0f172a
  Body text:          #334155
  Secondary text:     #333333
  Accent (header):    #1f1f1f
  Accent light:       #ede9fe
```

---

## Typography

```
Font stack: system-ui, -apple-system, "Segoe UI", sans-serif
Font sizes:
  Page title:          28px, weight 700, color #0f172a
  Section heading:     18px, weight 600, color #0f172a
  Category heading:    18px, weight 600, color #0f172a
  Finding title:       14px, weight 600, color #0f172a
  Body / labels:       14px, weight 400, color #334155
  Secondary / meta:    12px, weight 400, color #64748b
  Table header:        12px, weight 600, color #64748b, uppercase, letter-spacing 0.05em
  Table cell:          13px, weight 400, color #334155
Line height: 1.6 for body, 1.3 for headings
```

---

## Document Shell

The generated HTML file uses this structure. All CSS is inline in `<style>` — no external stylesheets.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Design Critique Report — [Design Name]</title>
  <style>
    /* All CSS inline — use color tokens, typography, and component specs in this file */
  </style>
</head>
<body>
  <div class="header-bar">...</div>
  <div class="container">
    <div class="summary-block">...</div>
    <!-- <img> screenshot element if available — omit entirely if not -->
    <div class="severity-tally">...</div>
    <!-- .category-section divs, one per audit category -->
    <table class="priority-table">...</table>
    <div class="quick-wins">...</div>
    <div class="strengths">...</div>
    <div class="report-footer">...</div>
  </div>
</body>
</html>
```

Container (`.container`): `max-width: 900px`, `margin: 0 auto`, `padding: 40px 24px`.
Page `body`: `background: #f8fafc`, `margin: 0`.

---

## Section Order

Always output sections in this exact order:

1. Header bar — `.header-bar`
2. Summary block — `.summary-block`
3. Screenshot — `<img>` (only if available; omit entirely if not)
4. Severity tally bar — `.severity-tally`
5. Findings by Category — one `.category-section` per audit category
6. Priority Summary Table — `.priority-table`
7. Quick Wins — `.quick-wins`
8. Strengths to Preserve — `.strengths`
9. Footer — `.report-footer`

---

## Component Specs

### Header Bar — CSS class: `header-bar`

`background: #7c3aed`, `padding: 24px 40px`, `margin-bottom: 32px`.
`display: flex`, `justify-content: space-between`, `align-items: center`.

Left: "Design Critique Report" in `#ffffff`, 22px, weight 700.
Right: "Generated [YYYY-MM-DD]" in `#ede9fe`, 13px.

---

### Summary Block — CSS class: `summary-block`

`background: #ffffff`, `border: 1px solid #e2e8f0`, `border-radius: 12px`, `padding: 24px`, `margin-bottom: 24px`.

Three rows. Each row: `display: flex`, `align-items: flex-start`, `gap: 16px`, `padding: 8px 0`, `border-bottom: 1px solid #f1f5f9`. No border on the last row.

- Label: `font-size: 12px`, `font-weight: 600`, `color: #64748b`, `text-transform: uppercase`, `letter-spacing: 0.05em`, `min-width: 160px`, `flex-shrink: 0`
- Value: `font-size: 14px`, `color: #334155`

Row labels (in order): `DESIGN SUMMARY` / `CONTEXT PROFILE` / `OVERALL IMPRESSION`

The OVERALL IMPRESSION value uses `font-style: italic`.

---

### Screenshot

If a Figma screenshot is available (base64 data URI or direct URL):

```html
<img src="[data-uri-or-url]" alt="Design screenshot"
     style="max-width:100%; border-radius:8px; margin-bottom:24px; display:block;">
```

If not available, omit this element entirely — no placeholder, no empty space.

---

### Severity Tally Bar — CSS class: `severity-tally`

`display: flex`, `flex-wrap: wrap`, `gap: 12px`, `margin-bottom: 32px`.

Four pill badges. Each: `padding: 6px 16px`, `border-radius: 9999px`, `font-size: 13px`, `font-weight: 600`.
Use severity background and text colors from the Color Tokens section.

Format (left to right): `🔴 N Critical` / `🟠 N Major` / `🟡 N Minor` / `🔵 N Cosmetic`

Count N by tallying all findings across all categories from the Step 4 report.

---

### Category Section — CSS class: `category-section`

One wrapper `<div class="category-section">` per audit category.

Category heading inside: `font-size: 18px`, `font-weight: 600`, `color: #0f172a`, `margin-top: 40px`, `margin-bottom: 8px`. For the first `.category-section` only, use `margin-top: 8px` to avoid stacking with the `margin-bottom: 32px` already on `.severity-tally`.
Followed by `<hr style="border: none; border-bottom: 2px solid #e2e8f0; margin-bottom: 16px;">`.

Each finding within the category: CSS class `finding-card`.

```html
<div class="finding-card">
  <div class="finding-header">
    <span class="severity-badge">[emoji + label]</span>
    <span class="finding-title">[Finding Title]</span>
  </div>
  <div class="finding-body">
    <p><span class="finding-label">What:</span> [description]</p>
    <p><span class="finding-label">Why it matters:</span> [rationale]</p>
    <p><span class="finding-label">Suggestion:</span> <em>[fix]</em></p>
  </div>
</div>
```

Finding card styles:
- `background: [severity background color]`
- `border-left: 4px solid [severity border color]`
- `border-radius: 8px`
- `padding: 16px 20px`
- `margin-bottom: 12px`

`.finding-header`: `display: flex`, `align-items: center`, `gap: 10px`, `margin-bottom: 10px`.
`.finding-title`: `font-size: 14px`, `font-weight: 600`, `color: #0f172a`.
`.finding-label`: `font-weight: 600`, `color: #64748b`, `font-size: 13px`.
`.severity-badge`: severity background + text colors from tokens, `padding: 2px 10px`, `border-radius: 9999px`, `font-size: 12px`, `font-weight: 600`, `white-space: nowrap`.

---

### Priority Summary Table — CSS class: `priority-table` (on `<table>`)

`width: 100%`, `border-collapse: collapse`, `margin-bottom: 40px`.

`<thead>` row: `background: #f1f5f9`.
`<th>` cells: `font-size: 12px`, `font-weight: 600`, `color: #64748b`, `text-transform: uppercase`, `letter-spacing: 0.05em`, `padding: 12px 16px`, `text-align: left`.
Columns: `#` | `Severity` | `Category` | `Finding` | `Suggested Fix`

`<tbody>` rows: alternating `background: #ffffff` (odd) / `#f8fafc` (even).
`<td>` cells: `padding: 12px 16px`, `font-size: 13px`, `color: #334155`, `border-bottom: 1px solid #e2e8f0`.

Severity column: use severity text color from tokens (no background in table cells — text color only).

---

### Quick Wins Box — CSS class: `quick-wins`

`background: #f0fdf4`, `border: 1px solid #bbf7d0`, `border-radius: 12px`, `padding: 24px`, `margin-bottom: 24px`.

Heading: "Quick Wins", `color: #166534`, `font-size: 16px`, `font-weight: 600`, `margin-bottom: 12px`.
Numbered list (`<ol>`): `font-size: 14px`, `color: #334155`, `line-height: 1.6`, `padding-left: 20px`.

**Empty state:** If no Quick Wins were identified, render instead of the list:
```html
<p style="color:#64748b; font-style:italic;">No quick wins were identified in this audit.</p>
```
Do not omit the section box.

---

### Strengths to Preserve Box — CSS class: `strengths`

`background: #eff6ff`, `border: 1px solid #bfdbfe`, `border-radius: 12px`, `padding: 24px`, `margin-bottom: 40px`.

Heading: "Strengths to Preserve", `color: #1e40af`, `font-size: 16px`, `font-weight: 600`, `margin-bottom: 12px`.
Bulleted list (`<ul>`): `font-size: 14px`, `color: #334155`, `line-height: 1.6`, `padding-left: 20px`.

**Empty state:** If no Strengths were identified, render instead of the list:
```html
<p style="color:#64748b; font-style:italic;">No standout strengths were identified in this audit.</p>
```
Do not omit the section box.

---

### Footer — CSS class: `report-footer`

`border-top: 1px solid #e2e8f0`, `padding-top: 16px`, `margin-top: 40px`, `text-align: center`.
Text: "Design Critique by WJY Studios", `font-size: 12px`, `color: #333`.

---

## Print Rules

```css
@media print {
  body { background: white; }

  .header-bar {
    background: white !important;
    color: #0f172a !important;
    border-bottom: 2px solid #e2e8f0;
  }

  .header-bar * {
    color: #0f172a !important;
  }

  .finding-card {
    break-inside: avoid;
  }

  .category-section {
    break-before: auto;
  }

  .priority-table tbody tr {
    break-inside: avoid;
  }

  .priority-table thead {
    display: table-header-group;
  }

  .quick-wins,
  .strengths {
    break-inside: avoid;
  }
}

@page {
  margin: 1.5cm;
  size: A4;
}
```
