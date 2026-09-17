# Accessibility plan

## Implemented practices

- A skip link targets a focusable main landmark.
- Native headings, navigation, lists, forms, labels, tables, code, and warning definitions preserve
  semantics.
- Search status and answers use polite live regions; results are ordinary links and lists.
- Lifecycle state uses text plus distinct symbols, not color alone.
- Focus is visible, controls meet a 44-pixel target height, and reduced-motion preferences remove
  smooth scroll.
- Layout reflows to 320 CSS pixels without page-wide horizontal scrolling; code blocks scroll
  locally.
- Print styles remove navigation while retaining version, warning, procedure, and provenance
  content.

## Automated evidence

Playwright tests keyboard bypass navigation, mobile reflow, version-filter interaction, warning
fields, and provenance. axe scans the home page for rules tagged WCAG 2 A/AA, 2.1 AA, and 2.2 AA.
Automated scans cannot find every accessibility barrier and do not establish WCAG conformance.

## Manual checklist before release

1. Navigate every header, filter, result, citation, and on-page link using only keyboard controls.
2. Test NVDA with Firefox or Chrome for headings, labels, live status, warning structure, and link
   purpose.
3. Zoom to 400% at a 1280-pixel viewport and verify reflow without loss of content or function.
4. Apply text-spacing overrides and high-contrast/forced-color modes.
5. Verify light-theme contrast with a measurement tool and inspect focus when sticky content is
   present.
6. Confirm that status, warning level, and result order remain understandable without color.

## Known limits

The repository does not include a formal assistive-technology user study, a complete WCAG
success-criterion audit, localization, right-to-left layout, or PDF-equivalent output. Those remain
explicit release risks.
