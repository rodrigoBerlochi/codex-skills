# WCAG Summary

## Perceivable

- meaningful images need alt text
- decorative images should use empty alt text
- icon-only buttons need accessible names
- text and UI controls need sufficient contrast
- errors should not rely on color alone
- media should provide captions, transcripts, or descriptions as needed

## Operable

- all functionality should be keyboard accessible
- avoid keyboard traps
- provide visible focus states
- use skip links when pages have repeated navigation
- give users enough time for timed interactions
- respect `prefers-reduced-motion`

## Understandable

- declare page language
- keep navigation consistent
- associate every form field with a label
- provide clear instructions and error messages
- move focus to the first relevant error when appropriate

## Robust

- prefer valid HTML and unique IDs
- prefer native elements over ARIA re-creations
- use ARIA only when needed and correctly
- announce dynamic updates with live regions when necessary

## Common High-Impact Failures

- missing form labels
- broken keyboard navigation
- missing focus indicators
- inaccessible custom controls
- missing alt text
- poor contrast

## Manual Checks

- tab through the page
- activate controls with keyboard
- test focus order
- test at 200% zoom
- test with reduced motion enabled
- test key paths with a screen reader when feasible
