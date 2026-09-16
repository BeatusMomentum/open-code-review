# Viewer redesign: Session detail — Files Reviewed, Session Tasks & Conversations

> Part of the viewer UI redesign (see main tracking issue). Depends on #01, #02.

## Summary

Restyle the lower portion of the session detail page: the Files Reviewed list, the Session
Tasks cards, and the Conversations transcript (per-request tool calls).

## Design reference

![Session detail — light](https://raw.githubusercontent.com/alibaba/open-code-review/docs/viewer-redesign-assets/docs/design/viewer-redesign/assets/session-detail-light.png)
![Session detail — dark](https://raw.githubusercontent.com/alibaba/open-code-review/docs/viewer-redesign-assets/docs/design/viewer-redesign/assets/session-detail-dark.png)

**Files Reviewed** (flat list of paths), **Session Tasks** (grouped
task cards — e.g. `GROUPING_TASK` with request/model/token badges), and **Conversations**
(collapsible per-file groups; each `PLAN_TASK` / `MAIN_TASK` request shows model + token
badges and expandable TOOL CALLS with arguments/results).

## Current state

- Template: `internal/viewer/templates/session.html` — Files Reviewed list, task cards, and
  conversation blocks.
- Helpers in `server.go`: `orderedTasks`, `taskTypeClass`, `sessionTaskLabel`,
  `groupingView`, `cardCount` (task ordering: Plan → Main → ReLocation → MemoryCompression →
  Grouping).
- Script: `internal/viewer/static/session.js` for collapsibles.

## Scope

- [ ] Restyle the Files Reviewed list to the mockup.
- [ ] Restyle task cards (type label, request #, model badge, token/latency badges) using
      the new tokens; keep the existing task ordering and `taskTypeClass` mapping.
- [ ] Restyle the Conversations transcript: collapsible file groups, per-request headers,
      and the TOOL CALLS arguments/results blocks (monospace, subtle surface).
- [ ] Preserve all collapse/expand behavior and CSP safety.

## Out of scope

- Coverage/token cards (#06), comments (#07).

## Acceptance criteria

- All three regions match the mockup in light and dark; collapsibles still work.
- `make check` and `make test` pass.

**AI disclosure:** The scope, decisions and issue breakdown are my own. An AI assistant (Claude Code) was used only to polish the English wording.
