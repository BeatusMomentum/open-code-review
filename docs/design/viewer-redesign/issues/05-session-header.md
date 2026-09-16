# Viewer redesign: Session detail — header / meta bar

> Part of the viewer UI redesign (see #1319). Depends on #1320, #1321.

## Summary

Restyle the top of the session detail page (`GET /r/{repo}/{sessionID}`): the title and the
metadata bar.

## Design reference

![Session detail — light](https://raw.githubusercontent.com/alibaba/open-code-review/docs/viewer-redesign-assets/docs/design/viewer-redesign/assets/session-detail-light.png)
![Session detail — dark](https://raw.githubusercontent.com/alibaba/open-code-review/docs/viewer-redesign-assets/docs/design/viewer-redesign/assets/session-detail-dark.png)

Header shows `Session: <id>` with a back chevron, then
a compact meta row: **CWD · BRANCH · MODE · FROM · TO · MODEL · DURATION · FILES · STATUS**.

## Current state

- Template: `internal/viewer/templates/session.html` (title at ~line 16; meta fields follow)
- Handler: `handleSession` in `internal/viewer/handler.go`

## Scope

- [ ] Restyle the title row with the back chevron.
- [ ] Lay out the meta fields as a compact, labeled row/grid matching the mockup, including
      truncation for long CWD/branch values.
- [ ] Apply status styling (complete/partial/failed) consistent with tokens from #1320.

## Out of scope

- Coverage/Token cards (#1325), comments (#1326), tasks/conversations (#1327).

## Acceptance criteria

- Header + meta bar match the mockup in light and dark.
- `make check` and `make test` pass.

## Parallelization & conflicts

Depends on #1320/#1321. **Conflict hotspot:** #1324 (this one — header/meta), #1325, #1326 and
#1327 all edit `session.html`. Coordinate with the other three — ideally one owner for
`session.html`, or serialize these four — and rebase frequently. `static/style.css` is shared
with all screens too.

**AI disclosure:** The scope, decisions and issue breakdown are my own. An AI assistant (Claude Code) was used only to polish the English wording.
