# Viewer redesign: Compare page

> Part of the viewer UI redesign (see main tracking issue). Depends on #01, #02.

## Summary

Restyle the session compare page (`GET /r/{repo}/compare`) to the redesigned system.

## Design reference

No dedicated mockup was provided for this screen — apply the same tokens, header, tables and
badges established by #01/#02 and the session-detail issues so Compare stays visually
consistent. Confirm layout details with a maintainer if ambiguous.

## Current state

- Template: `internal/viewer/templates/compare.html`
- Handler: `handleCompare` in `internal/viewer/handler.go` (added in PR #1175)

## Scope

- [ ] Apply the shared header, tokens and table/badge styles to the compare layout.
- [ ] Ensure the side-by-side / diff presentation reads clearly in light and dark.
- [ ] Keep the existing compare data and semantics unchanged.

## Out of scope

- Compare logic / data selection.

## Acceptance criteria

- Visually consistent with the redesigned screens in light and dark.
- `make check` and `make test` pass.

<!-- AI disclosure: fill in before posting. -->
