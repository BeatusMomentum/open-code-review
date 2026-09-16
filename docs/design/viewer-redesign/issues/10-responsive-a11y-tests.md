# Viewer redesign: responsive, accessibility & tests

> Part of the viewer UI redesign (see #1319). **Land last**, after the screens.

## Summary

Cross-cutting polish once the screens are restyled: responsive behavior, accessibility, and
test coverage for the new markup/styles.

## Scope

- [ ] Responsive: verify tables and cards degrade gracefully on narrow widths (horizontal
      scroll or stacked layout) across all four screens.
- [ ] Accessibility: visible focus states, sufficient contrast (WCAG AA), correct
      `aria-pressed`/`aria-label` on chips/toggles, keyboard operability of collapsibles and
      pagination.
- [ ] Reduced motion: respect `prefers-reduced-motion` for any transitions introduced.
- [ ] Tests: update/extend the viewer template + handler tests (`internal/viewer/*_test.go`)
      for any changed markup hooks; keep the read-only route contract test
      (`TestMux_HasNoWriteRoutes`) green.
- [ ] Confirm the CSP/security-header and host-guard tests still pass unchanged.

## Acceptance criteria

- No regressions across screens in light and dark, desktop and narrow widths.
- `make check`, `make test` and `make coverage` (90% threshold) pass.

## Notes

- Optional follow-up (separate issue if desired): a JS light/dark theme toggle with
  `localStorage` persistence, building on the `prefers-color-scheme` default from #1320.

## Parallelization & conflicts

**Land last**, after the screens (#1322–#1328) are restyled. This is cross-cutting polish and
test coverage over the final markup, so starting early means reworking against moving targets.

**AI disclosure:** The scope, decisions and issue breakdown are my own. An AI assistant (Claude Code) was used only to polish the English wording.
