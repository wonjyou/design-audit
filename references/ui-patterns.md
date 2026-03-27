# UI Patterns Reference

## Buttons
- **Hierarchy**: Visual weight should match importance: Primary > Secondary > Tertiary/Ghost/Link
- Only ONE primary button per view (unless it's a repeated pattern like a list)
- Disabled state: visually distinct AND explains why disabled (tooltip or inline text) when non-obvious
- Loading state: button should show spinner + disable during async action to prevent double-submission
- Destructive actions: use danger/red styling to signal consequence
- Touch target: minimum 44×44px
- Reference: [Button Design — NNg](https://www.nngroup.com/articles/ok-cancel-or-cancel-ok/)

## Forms & Input Fields
- **Always visible labels**: Placeholder text disappears on focus — it cannot replace labels
- **Label position**: Above the field (not beside) for better mobile experience and resize behavior
- **Field width**: Should communicate expected input length (postal code = narrow, message = wide/tall)
- **Required vs optional**: Mark the minority. If most fields are required, mark optional ones. If most are optional, mark required ones.
- **Inline validation**: Validate on blur (after leaving field), not on keystroke (too aggressive)
- **Grouping**: Related fields should be visually grouped (address: street + city + state + zip)
- **Autocomplete**: Enable browser autocomplete for standard fields (name, email, address, payment)
- **Input masking**: For structured inputs (phone, card numbers, dates) — guide the format
- Reference: [Form Design Patterns — Structural](https://adamsilver.io/articles/form-design-from-zero-to-hero-all-in-one-blog-post/)

## Navigation
- **Primary nav**: Persistent, consistent across all pages, reflects top-level IA
- **Active states**: Clear indicator of current location
- **Mobile nav**: Hamburger acceptable only when space is the constraint; consider tab bars for 3–5 items
- **Overflow**: Handle navigation items that don't fit gracefully (overflow menu, "More" item)
- **Breadcrumbs**: Appropriate for deep hierarchies (3+ levels); not needed for flat structures
- **Skip navigation**: For keyboard accessibility, include "skip to main content" link

## Modals & Dialogs
- Should be used sparingly — for critical confirmations, not for additional info that could be inline
- Always dismissible: ESC key, click outside (unless action required), visible X button
- One primary action per modal
- Avoid nested modals
- For mobile: consider bottom sheets as alternative
- Reference: [Modal vs Non-Modal Dialogs — NNg](https://www.nngroup.com/articles/modal-nonmodal-dialog/)

## Cards
- Consistent internal padding
- Clear delineation of what is clickable (the whole card, or just a link within it?)
- Elevation/shadow used consistently to indicate interactivity
- Avoid truncating critical information without visible indication (show "..." or "Read more")

## Empty States
Every empty state needs: illustration or icon (optional), explanation, call to action
- First-use empty state: welcoming, explain value, guide first action
- User-emptied state: confirm the action, offer to undo or restart
- Error empty state: explain what went wrong, offer a recovery path
- Reference: [Empty State Design — NNg](https://www.nngroup.com/articles/empty-state-interface-design/)

## Loading & Skeleton Screens
- Use skeleton screens (content placeholders) for pages/sections loading for >1s
- Use spinner for isolated component loading
- Use progress bar for multi-step operations with known duration
- Never leave a blank white screen without feedback
- Optimistic UI: show the result immediately for high-confidence async actions (like liking a post)

## Notifications & Toasts
- Toasts: for confirmations of non-critical actions (auto-dismiss in 3–5s)
- Alerts/Banners: for persistent system-level messages (errors, warnings, feature announcements)
- Position: top-right or top-center (consistent)
- Don't stack more than 3 toasts
- Always include a dismiss option

## Tables & Data Grids
- Column headers should be sortable when data order matters
- Fixed header when table scrolls vertically
- Pagination or virtualization for large datasets (50+ rows)
- Row actions: show on hover for desktop; always visible on mobile
- Empty cells: show "—" not blank space