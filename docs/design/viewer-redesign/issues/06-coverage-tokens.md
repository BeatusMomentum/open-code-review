# Viewer redesign: Session detail — Coverage & Token Usage

> Part of the viewer UI redesign (see #1319). Depends on #1320, #1321.

## Summary

Restyle the Coverage and Token Usage cards, including the per-file token breakdown table.

## Design reference

![Session detail — light](https://raw.githubusercontent.com/alibaba/open-code-review/docs/viewer-redesign-assets/docs/design/viewer-redesign/assets/session-detail-light.png)
![Session detail — dark](https://raw.githubusercontent.com/alibaba/open-code-review/docs/viewer-redesign-assets/docs/design/viewer-redesign/assets/session-detail-dark.png)

A **Coverage** card (Selected / Completed / Reused / Failed / Waived)
and a **Token Usage** card (Prompt / Completion / Total / LLM Requests / Cache Read / Cache
Write / LLM Failures) with a collapsible **File breakdown** table.

## Current state

- Template: `internal/viewer/templates/session.html` — `.token-summary`, `.token-stats`,
  `.token-item`, `.token-breakdown` / `.token-table` (~lines 37–110).
- Number formatting helpers (`formatNumber`) already exist in `server.go`.

## Scope

- [ ] Restyle the stat cards (grid of value + label) to match the mockup spacing/typography.
- [ ] Keep the `Failed`/`LLM Failures` error accent (`badge-error`) but align it with the
      new severity/error color tokens.
- [ ] Restyle the collapsible per-file breakdown table (`<details>`), preserving current
      columns (Prompt / Completion / Cache Read / Cache Write / Total).
- [ ] Preserve the numeric `title` tooltips (full values).

## Out of scope

- Review comments (#1326), tasks/conversations (#1327).

## Acceptance criteria

- Cards + breakdown table match the mockup in light and dark; collapse/expand still works.
- `make check` and `make test` pass.

## Parallelization & conflicts

Depends on #1320/#1321. **Conflict hotspot:** #1325 (this one — Coverage & Token Usage), #1324,
#1326 and #1327 all edit `session.html`. Coordinate with the other three — ideally one owner
for `session.html`, or serialize these four — and rebase frequently. `static/style.css` is
shared with all screens too.

**AI disclosure:** The scope, decisions and issue breakdown are my own. An AI assistant (Claude Code) was used only to polish the English wording.
