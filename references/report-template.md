# Design Audit Report: HTML Template Guide

This file is a style and structure guide for HTML report generation. It is not actual HTML — it defines the exact values, specs, and CSS class names the agent uses when composing the HTML output in Step 6.

The **canonical scaffold** is `references/report-template.html`. When generating a report, copy that file as the starting point and fill in the placeholder content.

---

## Font

Google Inter via `<link>` in `<head>`:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
```

Font stack: `'Inter', system-ui, -apple-system, "Segoe UI", sans-serif`

---

## Color Tokens

```
Severity colors (badge backgrounds and text):
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
  Finding body text:  #475569
  Secondary text:     #64748b
  Tertiary text:      #94a3b8
  Accent (header):    #1f1f1f
  Accent light:       #ede9fe
  Divider light:      #f1f5f9
```

---

## Typography

```
Font: Inter
Base body size: 16px

Scale:
  Header title:              22px, weight 700, color #ffffff
  Category heading:          22px, weight 700, color #0f172a, letter-spacing -0.02em
  Section heading:           22px, weight 700, color #0f172a, letter-spacing -0.02em
  Finding title:             17px, weight 600, color #0f172a, letter-spacing -0.01em
  Quick wins/strengths head: 18px, weight 700
  Summary value:             15px, weight 400, color #334155
  Finding body:              15px, weight 400, color #475569
  Table cell:                14px, weight 400, color #334155
  Tally pill:                14px, weight 600
  Summary label:             11px, weight 700, color #94a3b8, uppercase, letter-spacing 0.08em
  Table header:              11px, weight 700, color #94a3b8, uppercase, letter-spacing 0.06em
  Finding label:             12px, weight 700, color #64748b, uppercase, letter-spacing 0.05em
  Severity badge:            12px, weight 700
  Date / footer:             13px, weight 500

Line height: 1.6 body, 1.65 summary/finding text, 1.2 headings
```

---

## Document Shell

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Design Audit Report — [Design Name]</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  <style>
    /* All CSS inline — see component specs in this file and report-template.html */
  </style>
</head>
<body>
  <div class="header-bar">...</div>
  <div class="container">
    <div class="summary-block">...</div>
    <!-- <img> screenshot element if available — omit entirely if not -->
    <div class="severity-tally">...</div>
    <!-- .category-section divs, one per audit category -->
    <h2 class="section-heading">Priority Summary</h2>
    <hr class="section-divider">
    <table class="priority-table">...</table>
    <div class="quick-wins">...</div>
    <div class="strengths">...</div>
    <div class="report-footer">...</div>
  </div>
</body>
</html>
```

Container (`.container`): `max-width: 900px`, `margin: 0 auto`, `padding: 48px 40px`.
Page `body`: `background: #f8fafc`, `margin: 0`, `font-size: 16px`.

---

## Section Order

Always output sections in this exact order:

1. Header bar — `.header-bar`
2. Summary block — `.summary-block`
3. Screenshot — `<img>` (only if available; omit entirely if not)
4. Severity tally bar — `.severity-tally`
5. Findings by Category — one `.category-section` per audit category
6. Priority Summary heading + table — `.section-heading` + `.priority-table`
7. Quick Wins — `.quick-wins`
8. Strengths to Preserve — `.strengths`
9. Footer — `.report-footer`

---

## Component Specs

### Header Bar — CSS class: `header-bar`

`background: #1f1f1f`, `padding: 24px 40px`.
`display: flex`, `justify-content: space-between`, `align-items: center`.

Left: "Design Audit Report" in `#ffffff`, 22px, weight 700, `letter-spacing: -0.01em`.
Right: `[MM/DD/YYYY]` (today's date formatted as month/day/year) in `#94a3b8`, 13px, weight 500.

---

### Summary Block — CSS class: `summary-block`

`background: #ffffff`, `border: 1px solid #e2e8f0`, `border-radius: 12px`, `padding: 0 32px`, `margin-bottom: 32px`.

Three rows. Each row: `display: flex`, `align-items: flex-start`, `gap: 32px`, `padding: 20px 0`, `border-bottom: 1px solid #f1f5f9`. No border on the last row.

- Label: `font-size: 11px`, `font-weight: 700`, `color: #94a3b8`, `text-transform: uppercase`, `letter-spacing: 0.08em`, `min-width: 148px`, `flex-shrink: 0`, `padding-top: 4px`
- Value: `font-size: 15px`, `color: #334155`, `line-height: 1.65`

Row labels (in order): `DESIGN SUMMARY` / `CONTEXT PROFILE` / `OVERALL IMPRESSION`

The OVERALL IMPRESSION value uses `font-style: italic`, `color: #475569`.

---

### Screenshot

If a Figma screenshot URL or base64 data URI is available:

```html
<img src="[data-uri-or-url]" alt="Design screenshot"
     style="max-width:100%; border-radius:8px; margin-bottom:32px; display:block; border:1px solid #e2e8f0;">
```

If not available, omit this element entirely — no placeholder, no empty space.

---

### Severity Tally Bar — CSS class: `severity-tally`

`display: flex`, `flex-wrap: wrap`, `gap: 10px`, `margin-bottom: 48px`.

Four pill badges. Each: `padding: 7px 20px`, `border-radius: 9999px`, `font-size: 14px`, `font-weight: 600`, `letter-spacing: -0.01em`.
Use severity background and text colors from the Color Tokens section.

Format (left to right): `🔴 N Critical` / `🟠 N Major` / `🟡 N Minor` / `🔵 N Cosmetic`

Count N by tallying all findings across all categories.

---

### Category Section — CSS class: `category-section`

One wrapper `<div class="category-section">` per audit category. `margin-bottom: 56px`.

Category heading: `font-size: 22px`, `font-weight: 700`, `color: #0f172a`, `letter-spacing: -0.02em`, `margin-bottom: 6px`.
Followed by `<hr class="category-divider">`: `border-bottom: 2px solid #e2e8f0`, `margin-bottom: 28px`.

Each finding within the category: CSS class `finding-item`.

```html
<div class="finding-item">
  <div class="finding-header">
    <span class="severity-badge badge-[level]">[emoji + label]</span>
    <span class="finding-title">[Finding Title]</span>
  </div>
  <ul class="finding-bullets">
    <li><span class="finding-label">What</span> [description]</li>
    <li><span class="finding-label">Why it matters</span> [rationale]</li>
    <li><span class="finding-label">Suggestion</span> <em>[fix]</em></li>
  </ul>
</div>
```

Finding item styles:
- `margin-bottom: 32px`, `padding-bottom: 32px`, `border-bottom: 1px solid #f1f5f9`
- Last `.finding-item` in a section: `border-bottom: none`, `margin-bottom: 0`, `padding-bottom: 0`

`.finding-header`: `display: flex`, `align-items: center`, `gap: 12px`, `margin-bottom: 14px`.
`.finding-title`: `font-size: 17px`, `font-weight: 600`, `color: #0f172a`, `letter-spacing: -0.01em`.

`.finding-bullets`: `list-style: none`, `padding: 0`, `display: flex`, `flex-direction: column`, `gap: 10px`, `padding-left: 4px`.
`.finding-bullets li`: `font-size: 15px`, `color: #475569`, `line-height: 1.65`, `padding-left: 20px`, `position: relative`.
`.finding-bullets li::before`: `content: "–"`, `position: absolute`, `left: 0`, `color: #cbd5e1`, `font-weight: 600`.

`.finding-label`: `font-weight: 700`, `color: #64748b`, `font-size: 12px`, `text-transform: uppercase`, `letter-spacing: 0.05em`, `margin-right: 6px`.

`.severity-badge`: severity background + text colors from tokens, `padding: 3px 12px`, `border-radius: 9999px`, `font-size: 12px`, `font-weight: 700`, `white-space: nowrap`, `display: inline-flex`, `align-items: center`, `flex-shrink: 0`.

---

### Priority Summary Table

Precede with `<h2 class="section-heading">Priority Summary</h2>` and `<hr class="section-divider">`.

`.section-heading`: `font-size: 22px`, `font-weight: 700`, `color: #0f172a`, `letter-spacing: -0.02em`, `margin-bottom: 6px`.
`.section-divider`: `border-bottom: 2px solid #e2e8f0`, `margin-bottom: 24px`.

CSS class: `priority-table` (on `<table>`)

`width: 100%`, `border-collapse: collapse`, `margin-bottom: 56px`.

`<thead>` row: `background: #f8fafc`, `border-bottom: 2px solid #e2e8f0`.
`<th>` cells: `font-size: 11px`, `font-weight: 700`, `color: #94a3b8`, `text-transform: uppercase`, `letter-spacing: 0.06em`, `padding: 12px 16px`, `text-align: left`.
Columns: `#` | `Severity` | `Category` | `Finding` | `Suggested Fix`

`<tbody>` rows: alternating `background: #ffffff` (odd) / `#f8fafc` (even).
`<td>` cells: `padding: 13px 16px`, `font-size: 14px`, `color: #334155`, `border-bottom: 1px solid #e2e8f0`, `vertical-align: top`, `line-height: 1.5`.

Severity column: use severity text color from tokens, `font-weight: 600`. No background in table cells.

---

### Quick Wins Box — CSS class: `quick-wins`

`background: #f0fdf4`, `border: 1px solid #bbf7d0`, `border-radius: 12px`, `padding: 28px 32px`, `margin-bottom: 24px`.

Heading: "Quick Wins", `color: #166534`, `font-size: 18px`, `font-weight: 700`, `letter-spacing: -0.02em`, `margin-bottom: 16px`.
Numbered list (`<ol>`): `font-size: 15px`, `color: #334155`, `line-height: 1.7`, `padding-left: 22px`, items with `gap: 8px` via flex column.

**Empty state:** If no Quick Wins were identified:
```html
<p style="color:#64748b; font-style:italic;">No quick wins were identified in this audit.</p>
```
Do not omit the section box.

---

### Strengths to Preserve Box — CSS class: `strengths`

`background: #eff6ff`, `border: 1px solid #bfdbfe`, `border-radius: 12px`, `padding: 28px 32px`, `margin-bottom: 56px`.

Heading: "Strengths to Preserve", `color: #1e40af`, `font-size: 18px`, `font-weight: 700`, `letter-spacing: -0.02em`, `margin-bottom: 16px`.
Bulleted list (`<ul>`): `font-size: 15px`, `color: #334155`, `line-height: 1.7`, `padding-left: 22px`, items with `gap: 8px`.

**Empty state:** If no Strengths were identified:
```html
<p style="color:#64748b; font-style:italic;">No standout strengths were identified in this audit.</p>
```
Do not omit the section box.

---

### Footer — CSS class: `report-footer`

`border-top: 1px solid #e2e8f0`, `padding-top: 20px`, `text-align: center`.
Text: "Design Report Skill created by WJY Studios", `font-size: 13px`, `color: #94a3b8`, `font-weight: 500`.

---

## Print Rules

```css
@media print {
  body { background: white; font-size: 14px; }

  .header-bar {
    background: white !important;
    border-bottom: 2px solid #e2e8f0;
    -webkit-print-color-adjust: exact;
    print-color-adjust: exact;
  }
  .header-bar .title { color: #0f172a !important; }
  .header-bar .date  { color: #64748b  !important; }

  .container { padding: 24px 0; }

  .finding-item     { break-inside: avoid; }
  .category-section { break-before: auto; }

  .priority-table tbody tr { break-inside: avoid; }
  .priority-table thead    { display: table-header-group; }

  .quick-wins,
  .strengths { break-inside: avoid; }

  /* Preserve severity colors in print */
  .tally-pill, .severity-badge,
  .sev-critical, .sev-major, .sev-minor, .sev-cosmetic,
  .tally-critical, .tally-major, .tally-minor, .tally-cosmetic,
  .badge-critical, .badge-major, .badge-minor, .badge-cosmetic,
  .quick-wins, .strengths {
    -webkit-print-color-adjust: exact;
    print-color-adjust: exact;
  }
}

@page {
  margin: 1.5cm;
  size: A4;
}
```
