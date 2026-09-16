# Viewer redesign: Session detail — Review Comments

> Part of the viewer UI redesign (see main tracking issue). Depends on #01, #02.

## Summary

Restyle the Review Comments section: severity/category filter chips, the marked/hidden
controls, per-file grouping, and each comment's EXISTING CODE / SUGGESTED CHANGE blocks and
Fixed / Ignored / Clear actions.

## Design reference

![Session detail — light](https://raw.githubusercontent.com/alibaba/open-code-review/docs/viewer-redesign-assets/docs/design/viewer-redesign/assets/session-detail-light.png)
![Session detail — dark](https://raw.githubusercontent.com/alibaba/open-code-review/docs/viewer-redesign-assets/docs/design/viewer-redesign/assets/session-detail-dark.png)

"Review Comments (N findings)" with Severity chips (All / Medium /
Low …), Category chips (Maintainability / Documentation …), a right-aligned
"Hide marked" toggle + "clear all marked" and an "N marked, N hidden" counter. Each finding
groups under its file path, shows a category+severity badge, an EXISTING CODE block (with
line numbers) and a green SUGGESTED CHANGE block, plus Fixed / Ignored / Clear buttons.

## Current state

- Template: `internal/viewer/templates/session.html` — `.comments-section`,
  `.comment-filter-bar`, `.comment-filter-chip`, severity/category chips (~line 113+),
  EXISTING/SUGGESTED code blocks, mark buttons.
- Script: `internal/viewer/static/session.js` (filtering + marked/hidden state; CSP-safe).
- Template helpers: `severityClass`, `categoryClass`, `groupCommentsByFile`,
  `numberedCodeLines`, severity/category counts in `server.go`.

## Scope

- [ ] Restyle filter chips (active/inactive, counts) for severity and category to match the
      mockup; keep `aria-pressed` semantics.
- [ ] Restyle the marked/hidden toggle + "clear all marked" + counter.
- [ ] Restyle per-file comment groups, the category/severity badges, and the EXISTING CODE
      (numbered) vs SUGGESTED CHANGE (accent-green) blocks.
- [ ] Restyle the Fixed / Ignored / Clear action buttons and their marked state.
- [ ] Preserve all existing JS behavior (filtering, marking, hide-marked) and CSP safety.

## Out of scope

- Coverage/token cards (#06), tasks/conversations (#08).

## Acceptance criteria

- Section matches the mockup in light and dark; filters, marking and hide-marked still work.
- No CSP console errors; `make check` and `make test` pass.

<!-- AI disclosure: fill in before posting. -->
