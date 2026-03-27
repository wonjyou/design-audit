# Mobile App Audit Criteria

Apply these criteria in addition to the six baseline audit categories whenever the context profile is `mobile-app`.

---

## Touch Targets

- iOS HIG minimum: 44×44pt [Apple Human Interface Guidelines — Layout]
- Material Design minimum: 48×48dp [Material Design 3 — Accessibility]
- Flag any interactive element that appears below these thresholds; estimate size from visual proportions relative to the screen
- Minimum spacing between adjacent interactive elements: 8pt to prevent accidental activation

## Thumb Zone Analysis

[Steven Hoober, "How Do Users Really Hold Mobile Devices?", UXMatters 2013]

- **Comfortable zone:** bottom third of screen — primary thumb reach for average hand size
- **Stretch zone:** middle of screen — reachable but requires repositioning
- **Hard-to-reach zone:** top corners — avoid placing primary actions here
- Primary CTAs and navigation should be in the comfortable zone
- Destructive actions (delete, sign out, clear all) should be placed in harder-to-reach positions

## Font Size Minimums

- Body text: 16sp / 17pt minimum for comfortable reading [WCAG 2.1 — 1.4.4 Resize Text]
- Secondary/caption text: 12sp / 11pt absolute minimum
- Flag any text that appears smaller than these thresholds
- Look for signals that Dynamic Type (iOS) or scalable text (Android) is supported

## Platform Conventions

Apply general mobile standards first. Then, if the platform is identifiable from visual signals, apply platform-specific checks:

### iOS Signals & Checks

Visual signals: navigation bar at top, tab bar at bottom, swipe-from-left-edge back gesture, SF Symbols iconography, rounded rectangles, blur/transparency effects.

iOS HIG violations to flag:
- Custom back buttons that obscure or override the system back gesture area
- Bottom sheets presented without a drag handle
- Destructive actions placed in a prominent primary CTA position
- Tab bar icons used without labels (acceptable in some cases, flag if ambiguous)

### Android Signals & Checks

Visual signals: bottom navigation bar, FAB (floating action button) at bottom-right, edge-to-edge layout, Material You color roles.

Material Design violations to flag:
- Navigation drawer used in contexts where bottom navigation is more appropriate
- FAB not positioned at bottom-right
- Interactive elements missing state layer / ripple feedback signals
- Non-standard back navigation handling

## Safe Areas & Notch

- Content must not be obscured by the status bar, notch, Dynamic Island, or home indicator
- Buttons placed near the bottom edge must respect the home indicator safe area (approximately 34pt on iPhone X and later)
- Assess whether content extends edge-to-edge appropriately or is being clipped

## Gesture Navigation

- Check for potential conflicts between custom swipe gestures and system navigation gestures
- Horizontal swipes near the left or right screen edges risk conflicting with the system back gesture (iOS and Android gesture nav)
- Full-screen horizontal carousels or drawers should be evaluated for this conflict

## Density & Spacing

- List items: minimum 44pt tall for a comfortable tap target
- Form input fields: minimum 44pt tall
- Inline icon buttons: minimum 44×44pt tap area even if the visual icon is smaller — use invisible padding around the icon

---

## Context-Enriched Modifiers (runtime inference)

When the user's description includes domain-specific detail beyond the platform type (e.g., "iOS **fitness** app"), infer and apply relevant modifiers across all six audit categories at runtime. Apply these in addition to the criteria above. Examples:

- **Fitness app** → glanceability (can key data be read at a glance mid-workout?), oversized tap targets for sweaty or moving hands, progress and streak visualization clarity, high-contrast legibility for outdoor/bright light use
- **Banking / fintech app** → trust and security signals, confirmation dialogs before destructive financial actions, clear amount/currency formatting, biometric authentication placement
- **Children's app** → very large touch targets for small fingers, simple vocabulary, no dark patterns, parental gate placement
- **Navigation / maps app** → large tap targets for in-motion use, minimal text on primary screens, clear wayfinding hierarchy, voice prompt compatibility signals
