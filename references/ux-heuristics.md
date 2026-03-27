# UX Heuristics Reference

## Nielsen's 10 Usability Heuristics (1994)
Source: https://www.nngroup.com/articles/ten-usability-heuristics/

### 1. Visibility of System Status
The system should always keep users informed about what is going on.
- Look for: loading indicators, progress bars, active/selected states, confirmation feedback
- Red flags: actions with no visible response, unclear whether something is loading

### 2. Match Between System and the Real World
Use words, phrases, and concepts familiar to the user — not system-oriented language.
- Look for: plain language labels, familiar metaphors, logical ordering of information
- Red flags: technical jargon, internal system terminology, numeric error codes

### 3. User Control and Freedom
Users often choose functions by mistake and need a clearly marked "emergency exit."
- Look for: undo/redo, cancel buttons, back navigation, confirmation dialogs before destructive actions
- Red flags: no way to undo a delete, modals without close buttons, forced linear flows

### 4. Consistency and Standards
Users should not have to wonder whether different words, situations, or actions mean the same thing.
- Look for: consistent terminology, consistent UI patterns, platform conventions followed
- Red flags: "Submit" in one place, "Send" in another for the same action; different button styles for same function

### 5. Error Prevention
Even better than good error messages is a careful design which prevents a problem from occurring.
- Look for: input constraints, confirmation steps, smart defaults, warnings before irreversible actions
- Red flags: easy-to-accidentally-trigger destructive actions, no validation feedback

### 6. Recognition Rather than Recall
Minimize the user's memory load by making objects, actions, and options visible.
- Look for: visible options (not hidden in menus), contextual help, autocomplete, breadcrumbs
- Red flags: users must remember info from one step to another, hidden affordances

### 7. Flexibility and Efficiency of Use
Accelerators — unseen by novice users — may speed up the interaction for experts.
- Look for: keyboard shortcuts, saved searches, quick actions, customization options
- Red flags: every task requires the same number of steps regardless of user expertise

### 8. Aesthetic and Minimalist Design
Dialogues should not contain irrelevant or rarely needed information.
- Look for: focused layouts, removal of decorative clutter, progressive disclosure
- Red flags: too much information on one screen, competing visual elements, modal overload

### 9. Help Users Recognize, Diagnose, and Recover from Errors
Error messages should be expressed in plain language, precisely indicate the problem, and constructively suggest a solution.
- Look for: inline validation, clear error messages with solutions, error state styling (not just red)
- Red flags: generic "Something went wrong", errors that don't indicate which field failed

### 10. Help and Documentation
Even though it is better if the system can be used without documentation, it may be necessary to provide help.
- Look for: contextual tooltips, onboarding flows, empty state guidance, FAQs accessible in context
- Red flags: complex flows with no in-context help

---

## Affordance
Does the visual design signal how to interact with elements?
- Buttons should look pressable (elevation, border, background fill)
- Links should look clickable (underline or distinct color)
- Draggable elements should have grab handles or visual cues
- Input fields should look editable (border, background differentiation)
- Reference: [Don Norman, *The Design of Everyday Things*](https://www.nngroup.com/books/design-everyday-things-revised/)

---

## WCAG 2.1 Accessibility (AA Standard)
Source: https://www.w3.org/TR/WCAG21/

### Perceivable
- Text contrast: ≥4.5:1 (normal), ≥3:1 (large text 18px+ or 14px bold+)
- UI component contrast: ≥3:1 against adjacent colors
- No information conveyed by color alone
- Text can resize to 200% without loss of content

### Operable
- All functionality accessible via keyboard
- Touch targets: minimum 44×44px (iOS HIG), 48×48dp (Material)
- No seizure-inducing animations (3+ flashes per second)
- Focus indicators visible

### Understandable
- Language of page identifiable
- Labels for all form inputs
- Error identification: if input error detected, item described and error described in text

### Robust
- Sufficient for assistive technologies to interpret

### Quick Reference
| Element | Minimum Size | Preferred |
|---------|-------------|-----------|
| Touch targets | 44×44px | 48×48px |
| Body text contrast | 4.5:1 | 7:1 |
| Large text contrast | 3:1 | 4.5:1 |
| UI component contrast | 3:1 | — |

Tools: [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/), [axe DevTools](https://www.deque.com/axe/)