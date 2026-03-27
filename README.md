# Design Critique Agent

A structured design audit skill for Claude Code that evaluates UI/UX designs against established design principles, usability heuristics, accessibility standards, and human factors research.

## What It Does

When invoked, this skill guides Claude through a systematic 5-step design critique:

1. **Determines input type** — static image (screenshot/mockup) or live Figma file via MCP
2. **Orients to context** — identifies interface type, purpose, target user, and primary task
3. **Runs a six-category audit** across Visual Design, UX Heuristics, UI Patterns, Human Factors, UX Copy, and Information Architecture
4. **Scores findings** using the ASK Framework (Actionable, Specific, Kind) with four severity levels
5. **Delivers a structured report** with a priority table, quick wins, and strengths to preserve

## Trigger Phrases

This skill activates on requests like:
- "Review my design"
- "Audit this UI"
- "Give me design feedback"
- "Critique this screen"
- "What's wrong with my design?"
- "UX review" / "accessibility audit" / "heuristic evaluation"
- Sharing a Figma URL or design image with "thoughts?" or "what do you think?"

## Inputs

| Input | How to Provide |
|-------|---------------|
| Static image | Upload a screenshot, mockup, or exported design file |
| Figma file | Share a `figma.com/design/...` or `figma.com/file/...` URL |

> Requires vision/image analysis capability. Figma MCP (`https://mcp.figma.com/mcp`) is used automatically when a Figma URL is provided.

## Design Context Input

Before the audit begins, the skill asks for a brief description of what the design is for. You can provide this upfront in your request or answer when prompted.

**Providing context upfront:**
> "Review my iOS fitness app design"  ← context extracted automatically

**Answering when prompted:**
> "Before I begin — can you briefly describe what this design is for?"
> "It's a SaaS dashboard for project management"  ← you answer here

The skill classifies your description into one of four context profiles:

| Profile | When used | Reference file |
|---------|-----------|---------------|
| `mobile-app` | iOS/Android/mobile app designs | `references/mobile-app.md` |
| `web-app` | SaaS tools, dashboards, admin portals | `references/web-app.md` |
| `marketing-site` | Landing pages, marketing homepages | `references/marketing-site.md` |
| `other` | Everything else — criteria inferred from your description | _(runtime inference)_ |

Context-enriched modifiers are also applied when your description includes domain detail beyond the platform (e.g., "fitness" or "B2B" on top of "mobile app").

## Audit Categories

| # | Category | Key Criteria |
|---|----------|-------------|
| 1 | **Visual Design** | Hierarchy, spacing, typography, color, consistency |
| 2 | **UX Heuristics** | Nielsen's 10 heuristics, affordance, WCAG 2.1 accessibility |
| 3 | **UI Patterns** | Buttons, forms, navigation, modals, empty/loading states |
| 4 | **Human Factors** | Fitts's Law, Hick's Law, Miller's Law, Gestalt, cognitive load |
| 5 | **UX Copy** | Clarity, CTAs, labels, error messages, tone consistency |
| 6 | **Information Architecture** | Wayfinding, nav structure, labeling, content organization |

> Context-specific criteria from the loaded profile are applied as modifiers within each category — in addition to, not instead of, the baseline criteria above.

## Severity Levels

| Level | Label | When to Apply |
|-------|-------|---------------|
| 🔴 | **Critical** | Blocks task completion or fails accessibility — fix before launch |
| 🟠 | **Major** | Significant usability impairment — high priority |
| 🟡 | **Minor** | Noticeable friction — address in next iteration |
| 🔵 | **Cosmetic** | Polish-level — nice-to-have in backlog |

## Report Format

The output includes:
- **Design Summary** — interface type, purpose, assumed user context
- **Context Profile** — the context profile applied and any active modifiers
- **Overall Impression** — strengths and top area for improvement
- **Findings by Category** — each finding with What / Why it matters / Suggestion
- **Priority Summary Table** — all findings ranked by severity
- **Quick Wins** — 3–5 high-impact, low-effort improvements
- **Strengths to Preserve** — what's working well and should stay

## Follow-Up Options

After the report, Claude can offer:
- Deeper dive into any single category
- Revised UX copy suggestions
- Dev-handoff checklist version
- Re-evaluation after revisions

## Installation

Place `SKILL.md` in your Claude Code skills directory. The skill is invoked automatically via the `Skill` tool when relevant triggers are detected.
