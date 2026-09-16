# Viewer UI Redesign — issue drafts & design assets

Draft issues and mockups for redesigning the `ocr viewer` web UI (`internal/viewer/`) to
match a new design system. This branch (`docs/viewer-redesign-assets`) exists to **host the
design assets** so the GitHub issues can reference them by stable raw URL — it is not meant
to merge into `main`.

## Layout

```
docs/design/viewer-redesign/
├── README.md            # this file
├── issues/              # one Markdown draft per issue (00 = main tracking, 01–10 = sub-issues)
└── assets/              # mockups (PNG) + exported icons (SVG) referenced by the issues
```

## Issues

| File | Becomes | Kind |
|------|---------|------|
| `issues/00-main-tracking.md` | Main tracking issue | epic / meta |
| `issues/01-design-tokens.md` | design tokens & app header | foundation |
| `issues/02-icon-set.md` | shared SVG icon set | foundation |
| `issues/03-repositories-page.md` | Repositories page | screen |
| `issues/04-sessions-page.md` | Sessions list page | screen |
| `issues/05-session-header.md` | Session detail — header/meta bar | screen |
| `issues/06-coverage-tokens.md` | Session detail — Coverage & Token Usage | screen |
| `issues/07-review-comments.md` | Session detail — Review Comments | screen |
| `issues/08-tasks-conversations.md` | Session detail — Files/Tasks/Conversations | screen |
| `issues/09-compare-page.md` | Compare page | screen |
| `issues/10-responsive-a11y-tests.md` | responsive, a11y & tests | polish |

## Dependency order

```
01 design tokens ─┐
02 icon set ──────┤→ 03, 04, 05, 06, 07, 08, 09 (screens, parallelizable) → 10 (polish)
```

`01` and `02` are foundational and should land first; the per-screen issues can then be
picked up in parallel by different contributors.

## How the images work

Each issue draft embeds its mockup with an absolute raw URL pointing at this branch, e.g.
`https://raw.githubusercontent.com/alibaba/open-code-review/docs/viewer-redesign-assets/docs/design/viewer-redesign/assets/<file>`.
Once the branch is pushed, those URLs render inline in issue bodies — just paste the draft.

> Caveat: the URLs are tied to this branch. If the branch is renamed or deleted, the images
> in the issues break. Keep the branch, or move the assets to `main` and update the URLs.

## How to create on GitHub

1. Create the main tracking issue from `issues/00-main-tracking.md`.
2. Create each sub-issue by pasting its draft (images render via the raw URLs).
3. Link them as native sub-issues (GitHub "Sub-issues" panel) **or** keep the checklist in
   the main issue and reference each sub-issue number.
4. Suggested labels: `enhancement`, `viewer`, `frontend`, plus `good first issue` on the
   per-screen issues.
5. Fill in the `AI disclosure` line at the bottom of each issue before posting.

## Contributor rules (from AGENTS.md — keep in every issue/PR)

- Each issue/PR **must disclose AI/LLM usage** and which tools/models were used.
- All GitHub-facing text is **English**.
- Source files need an SPDX header (`make license-add`); run `make check` and `make test`;
  90% coverage threshold applies (`make coverage`).
- The viewer is **read-only** and **CSP-constrained**: no inline `<script>`/`onclick`,
  scripts are externalized (see PR #758) and served from `static/`. Assets are embedded via
  `//go:embed` in `internal/viewer/server.go`.
