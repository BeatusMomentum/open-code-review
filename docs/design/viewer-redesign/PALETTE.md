# Viewer palette — authoritative token values (light + dark)

Single source of truth for the viewer's color tokens, derived from the design mockups (as
captured by the reference implementation's `global.less`).

Rules this table encodes:
- **Keep the existing CSS variable names** established in #1338 — do not introduce the
  reference's names (`--accent-green`, `--bg-page`, …).
- **Keep ocr's theming model**: light is the default (`:root`); dark is served via
  `@media (prefers-color-scheme: dark)`. No `data-theme` attribute, no JS theme toggle.
  So the reference's *light* values go in `:root` and its *dark* values go in the media block
  (the reference is dark-default; we invert that mapping).
- Only **values** change. Structure and names stay.

## Core palette — update these `:root` / dark values

| Variable (keep name) | Light (`:root`) | Dark (`prefers-color-scheme: dark`) | Reference role |
|----------------------|-----------------|--------------------------------------|----------------|
| `--bg`             | `#ffffff`             | `#000000`               | bg-page |
| `--surface`        | `#fafafa`             | `#0a0a0a`               | card fill over page |
| `--surface-alt`    | `#f5f5f5`             | `#141414`               | alt/bar fill |
| `--surface-inset`  | `#f0f0f0`             | `#111111`               | tool-item / inset |
| `--text`           | `rgba(0,0,0,0.77)`    | `rgba(255,255,255,0.80)`| text-primary |
| `--text-strong`    | `rgba(0,0,0,0.87)`    | `rgba(255,255,255,0.90)`| text-strong |
| `--text-secondary` | `rgba(0,0,0,0.55)`    | `rgba(255,255,255,0.60)`| text-secondary |
| `--text-muted`     | `rgba(0,0,0,0.39)`    | `rgba(255,255,255,0.40)`| text-tertiary |
| `--border`         | `rgba(0,0,0,0.08)`    | `rgba(255,255,255,0.16)`| border-card |
| `--border-subtle`  | `rgba(0,0,0,0.06)`    | `rgba(255,255,255,0.08)`| border-inner |
| `--accent`         | `#17CB4B`             | `#2BDE5E`               | accent-green |
| `--accent-hover`   | `#14A83E`             | `#60E686`               | derived (darker light / lighter dark) |
| `--accent-soft`    | `rgba(23,203,75,0.10)`| `rgba(43,222,94,0.10)`  | accent-green-soft |
| `--accent-glow`    | `rgba(23,203,75,0.16)`| `rgba(43,222,94,0.12)`  | accent-green-hover tint |
| `--link`           | `#177d35`             | `var(--accent)`         | AA-safe text/link green |

**Accessibility note on `--link`:** the mockup accent `#17CB4B` is only ~2.2:1 on white, so
it fails WCAG AA as text. `--accent` keeps `#17CB4B` for fills, borders and active states, but
**`--link` (and green text) uses a darker `#177d35`** (~5.3:1) in light mode. On dark surfaces
the bright accent already clears AA, so `--link` reverts to `var(--accent)` there.

`--response-bg`, `--code-bg`, `--inline-code-bg`, `--text-faint` remain aliases of other
variables and inherit the new values automatically.

## Interactive tokens — add these (used by the per-screen work; not present in #1338 yet)

| New variable | Light (`:root`) | Dark | Reference role |
|--------------|-----------------|------|----------------|
| `--row-border`               | `#ebebeb`            | `#292929`               | border-row |
| `--btn-border`               | `rgba(0,0,0,0.16)`   | `#3d3d3d`               | btn-border |
| `--input-bg`                 | `rgba(0,0,0,0.04)`   | `rgba(255,255,255,0.08)`| input-bg |
| `--input-hover`              | `rgba(0,0,0,0.08)`   | `rgba(255,255,255,0.12)`| input-hover |
| `--tag-bg`                   | `rgba(0,0,0,0.05)`   | `rgba(255,255,255,0.06)`| tag-bg |
| `--tag-hover`                | `rgba(0,0,0,0.08)`   | `rgba(255,255,255,0.10)`| tag-hover |
| `--hover-row`                | `rgba(0,0,0,0.03)`   | `rgba(255,255,255,0.03)`| hover-row |
| `--marked-text`              | `rgba(0,0,0,0.55)`   | `#9e9e9e`               | marked-text |
| `--pagination-active-border` | `rgba(0,0,0,0.24)`   | `#3d3d3d`               | pagination-active-border |
| `--pagination-active-text`   | `rgba(0,0,0,0.87)`   | `#ffffff`               | pagination-active-text |
| `--scroll-thumb`             | `rgba(0,0,0,0.16)`   | `rgba(255,255,255,0.16)`| scroll-thumb |
| `--code-red-bg`              | `rgba(227,61,73,0.08)`| `rgba(227,61,73,0.12)` | code-red-bg (SUGGESTED CHANGE removed lines) |
| `--code-green-bg`            | `rgba(23,203,75,0.08)`| `rgba(43,222,94,0.08)` | code-green-bg (SUGGESTED CHANGE added lines) |

## Leave unchanged (out of scope for the palette alignment)

`--font`, `--mono`, spacing (`--space-*`), `--shadow-*`, `--radius*`, `--transition`, and the
role-specific accents that the reference does not define: `--task-*`, `--tool-name`,
`--danger`, `--badge-*`, and `--severity-*`.

## Notes

- The two derived `--accent-hover` values are the only hand-picked entries (the reference
  expresses accent hover as an rgba tint, not a solid); everything else is taken from the
  reference palette.
- This corrects the interim accent shipped in #1338 (`--accent: #177d35` in light), which was
  darker than the mockup, and the mismatched `--accent-soft/glow` that used the bright-green
  rgba against the dark base.
