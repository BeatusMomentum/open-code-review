# Viewer redesign: Session detail — header / meta bar

> Part of the viewer UI redesign (see main tracking issue). Depends on #01, #02.

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
- [ ] Apply status styling (complete/partial/failed) consistent with tokens from #01.

## Out of scope

- Coverage/Token cards (#06), comments (#07), tasks/conversations (#08).

## Acceptance criteria

- Header + meta bar match the mockup in light and dark.
- `make check` and `make test` pass.

<!-- AI disclosure: fill in before posting. -->
