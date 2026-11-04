# Accessibility Review — My IT Portfolio

**Project:** [Live portfolio](https://angelakoska.github.io/my-it-portfolio/)  
**Repository:** [angelakoska/my-it-portfolio](https://github.com/angelakoska/my-it-portfolio/)

## WAVE results

A WAVE screenshot of the Home page showed **0 errors, 0 contrast errors, and 0 alerts**. WAVE screenshots were also captured for the Projects and About pages. These screenshots are evidence of the automated checks, **not** evidence that every keyboard, screen-reader, or zoom interaction is accessible.

Because WAVE did not flag three issues in the original test, the following findings came from code review and narrow-viewport analysis beyond WAVE's automated warnings. These are **not claimed as WAVE-reported errors**.

## Three accessibility issues and fixes

### 1. Skip link did not have an explicitly focusable main target

- **Pages/element:** All pages; `<a class="skip-link" href="#main-content">` and `<main id="main-content">`.
- **How identified:** Keyboard-navigation-oriented code review. WAVE recognized a skip link as a positive feature, but did not verify focus movement.
- **Issue/impact:** The main target lacked `tabindex="-1"`, so the destination had no explicit programmatic focus target. This can make the result of skipping the navigation harder to perceive and less predictable for keyboard users.
- **Fix:** Added `tabindex="-1"` to each `<main>` and a visible `.page-grid:focus-visible` outline.

### 2. Navigation links were squeezed at very narrow zoomed widths

- **Pages/element:** All pages; `.site-nav` and its three links.
- **How identified:** Responsive CSS review and browser-width reproduction at narrow CSS viewport sizes.
- **Issue/impact:** The original navigation stayed in three columns even at extremely narrow viewports. Enlarging a page or using a very small effective viewport could squeeze text into narrow link boxes. This makes navigation harder for people who magnify their screens.
- **Fix:** Added an `@media (max-width: 359px)` rule to stack the links vertically, ensure a minimum 44px height, and allow wrapping. This preserves readable, reachable links when the viewport narrows.

### 3. Content sections lacked accessible region names

- **Pages/elements:** All pages; the `<section class="panel">` elements.
- **How identified:** Semantic HTML / screen-reader-navigation-oriented code review. WAVE did not report an error for these sections.
- **Issue/impact:** Each section had a visible heading, but the section itself lacked an accessible name. Some screen-reader users navigate by named regions, so those sections were less useful as navigational landmarks.
- **Fix:** Assigned unique IDs to each section's `<h2>` and connected the section to its visible heading with `aria-labelledby`, creating meaningful named regions.

## Follow-up checks

- Rerun **WAVE** for Home, Projects, and About **after** the updates, and save the current screenshots or report links.
- Use the **Tab** key, activate **Skip to main content**, and check that focus and navigation work on all pages.
- Test each page at **200% zoom** and a narrow viewport; confirm that navigation text does not overlap and no horizontal scrolling is required.
- Remember: zero WAVE errors is a good outcome, but manual checks are still necessary.
