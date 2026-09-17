# Viewer UI icons — source & licensing

These SVGs are the UI glyphs the redesign mockups use. They are taken from
**[Ant Design Icons](https://github.com/ant-design/ant-design-icons)**, which is
distributed under the **MIT License** — the same set the reference implementation renders
(the reference loaded them via a repackaged iconfont; here they are the upstream SVGs so we
can ship them offline, CSP-safe, with a clear license).

Each file was normalized for embedding: the XML prolog and `class` attribute were dropped,
and `fill="currentColor"` was added so a single asset adapts to both light and dark themes.
The path data is unchanged from upstream.

| File | Ant Design glyph | Used for |
|------|------------------|----------|
| `chevron-left.svg` | `left` (outlined) | back navigation; pagination "previous" |
| `chevron-right.svg` | `right` (outlined) | collapsed section toggle; pagination "next" |
| `chevron-down.svg` | `down` (outlined) | expanded section toggle |
| `search.svg` | `search` (outlined) | repositories search box |
| `settings.svg` | `setting` (outlined) | settings / theme control |

## Attribution to keep when integrating into `internal/viewer/static/icons/`

Ship an MIT attribution alongside the icons (a short `NOTICE`/`README` in that directory is
enough). Do **not** add the project's Apache SPDX header to these third-party SVGs, and do
**not** reintroduce the remote iconfont `<script>` or the `antd` runtime — only these static
SVGs are needed.

```
Ant Design Icons
Copyright (c) 2015-present Ant UED, https://xtech.antfin.com/
Licensed under the MIT License: https://github.com/ant-design/ant-design-icons/blob/master/LICENSE
```
