# PRD: Dark Theme for Memory Game

## 1. Overview

This product requirements document defines the work needed to add a dark theme to the existing Memory Game web app while preserving the current gameplay, accessibility, responsiveness, and score-saving behavior.

The current app is a single-file HTML/CSS/JavaScript implementation with a light theme and functional game mechanics. The objective is to add a theme toggle that enables a dark visual mode without causing regressions in gameplay, layout, accessibility, or browser compatibility.

## 2. Goal

Add a dark theme option to the Memory Game so users can switch between light and dark modes while maintaining the following:

- no loss of gameplay functionality
- no UI breakage in card layout or controls
- no regression in score persistence or timer logic
- no negative effect on keyboard accessibility
- smooth visual experience across common desktop and mobile browsers

## 3. Problem Statement

The current game is visually optimized for a light background and uses a limited color palette. Users may want a dark theme for comfort, low-light environments, or aesthetic preference. However, the app must remain stable and fully functional after theme changes.

## 4. Product Scope

### In Scope

- Implement a light/dark theme toggle
- Apply dark colors to background, cards, panel surfaces, and text
- Ensure card flip states remain visible and readable
- Maintain responsive layout for 4x4 and 6x6 grids
- Preserve accessibility contrast and keyboard focus styles
- Keep localStorage-based score tracking unchanged
- Ensure win modal and scoreboard remain readable in dark mode

### Out of Scope

- Full theme customization with multiple palettes
- User account or cloud sync for preferences
- Sound effects or animations beyond existing design
- Redesign of the game rules or mechanics

## 5. User Personas

### Casual player

Wants a comfortable visual experience with minimal friction. They expect a quick theme switch and a clean, readable layout.

### Accessibility-focused user

Needs strong contrast and clear focus states while using the keyboard or playing in dark environments.

### Returning player

Wants the app behavior to stay exactly the same after enabling the dark theme, including scores, timers, and grid switching.

## 6. Requirements

### Functional Requirements

1. The app must provide a visible theme toggle, such as a button labeled “Dark Mode” / “Light Mode”.
2. The theme switch must immediately update the visual design without reloading the page.
3. The dark mode must apply to all major UI regions:
   - page background
   - game container and panels
   - cards and card faces
   - controls and buttons
   - modal dialog
   - score display
4. The selected theme must persist for the user across refreshes if possible using localStorage.
5. Game logic must remain identical in both themes.
6. Card matching, timer counting, and move tracking must not be affected by the theme toggle.

### Non-Functional Requirements

1. No breakage of gameplay logic or DOM structure
2. No external libraries required
3. Theme implementation must be compatible with modern browsers
4. Color contrast must meet accessible readability standards
5. Theme changes must not interfere with keyboard navigation or focus ring visibility
6. Existing app behavior must remain stable in the default light theme

## 7. User Experience Requirements

- Theme toggle should be obvious and visible near the controls area
- Dark mode should feel polished, not just inverted colors
- Card symbols and emoji must remain clear and readable
- Buttons and modal content must keep proper contrast and spacing
- The app should feel consistent between light and dark modes

## 8. Acceptance Criteria

### AC-1: Theme toggle exists
The user can see and use a toggle to switch themes.

### AC-2: Dark mode is visually applied
When toggled, the page, panels, cards, buttons, modal, and scoreboard update to dark styling.

### AC-3: No gameplay regression
All existing functions continue to work:
- card flips
- matching logic
- move counter
- timer
- grid switching
- win detection
- local score saving

### AC-4: Accessibility preserved
Text remains legible, focus states are visible, and contrast is sufficient for keyboard users.

### AC-5: Theme persists
If implemented using localStorage, the selected mode remains across page refreshes.

### AC-6: Light mode remains intact
The default theme remains functional and visually correct when the dark mode is toggled off.

## 9. Technical Constraints

- The app is currently implemented in a single HTML file with embedded CSS and JavaScript.
- Features must be updated in a way that does not disturb the current script structure.
- Any changes should be surgical and minimally invasive.
- New CSS variables or classes should be introduced carefully to avoid conflicts with existing styles.
- Existing state logic should not be rewritten unless necessary.

## 10. Proposed Solution

### Theme model

Use CSS custom properties for both themes so the game styling can be switched by toggling a class on the root element or body.

Example approach:

- default variables define light theme values
- dark theme variables override the same tokens with dark colors
- JavaScript toggles a class such as `dark-theme`

### Minimal implementation strategy

1. Add a theme toggle button in the control area
2. Define CSS variables for colors used throughout the UI
3. Add a dark theme variable set and apply it via a root class
4. Adjust only affected selectors for contrast and readability
5. Validate all card states, modal content, and scoreboard elements under dark mode
6. Confirm score persistence still works after toggling

## 11. Risk Assessment

### Risk 1: Card readability in dark mode
If contrast is poor, card symbols and button text may be hard to read.

Mitigation: use carefully chosen dark background and high-contrast text colors.

### Risk 2: Theme class interference with state styling
If classes are applied incorrectly, card flip states may not display properly.

Mitigation: keep existing card classes and add theme values only through CSS custom properties.

### Risk 3: Local storage or app logic breakage
A rushed theme implementation may accidentally alter the script or DOM logic.

Mitigation: keep gameplay code intact and scope changes to UI styling and toggle behavior.

### Risk 4: Accessibility issues
Dark themes can reduce focus visibility or contrast if not tested.

Mitigation: explicitly test button focus, keyboard controls, and card visibility.

## 12. Testing Plan

### Manual checks

- Launch the app in browser
- Confirm light theme loads by default
- Toggle to dark mode and verify colors update across all sections
- Flip cards and confirm matching logic still works
- Switch board sizes (4x4 and 6x6) and ensure layout remains correct
- Start a game and verify timer and moves behave normally
- Win a game and verify modal and score save remain correct
- Refresh page and verify theme persistence if implemented
- Use keyboard navigation to confirm focus remains visible and usable

### Regression checks

- Score list still loads and updates correctly
- Timer resets appropriately on a new game
- Buttons remain clickable and aligned
- Card flip animation remains smooth
- No console errors appear during interaction

## 13. Definition of Done

The dark theme feature is complete when:

- a working dark mode toggle is added
- all major app areas render correctly in dark mode
- no gameplay functionality is broken
- all existing tests/manual checks pass
- UI remains responsive and accessible
- the default light mode still works as before

## 14. Implementation Notes for Future Developers

- Prefer CSS variables over hardcoded colors for easy theme switching
- Do not modify the game logic unless required for theme integration
- Keep changes scoped to the HTML/CSS/JS file already in use
- Use browser testing to confirm no layout drift across card sizes and screen widths

## 15. Summary

This feature adds a dark theme to the existing Memory Game with minimal risk, preserving the core game mechanics and expected behavior. The main emphasis is on safe UI enhancement, accessibility, and regression prevention. The final result should feel polished and consistent in both light and dark modes without altering how the game works.
