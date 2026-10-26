# AGENTS.md

## What this repo is
A student's "高级网页设计" (Advanced Web Design) course archive: **static HTML + CSS pages, no build system, no package manager, no tests, no git**. Each file is a standalone, self-contained page (styles inline in a `<style>` tag). Content is Chinese (UTF-8), author 张珑恩.

## Ignore these directories
`CodeBuddy/` and `Steam++/` are bundled third-party Windows applications (an Electron editor and a Steam tool), **not part of the website**. Never search, edit, or scan them — they add tens of thousands of irrelevant files.

## Layout
- `netlify/` — the deployable site. `netlify/index.html` is the navigation hub; it links **all** assignment pages (`1.html` … `15-1.html`) via `.link-card` entries.
- All assignment pages live under `netlify/` (including the formerly root-level `10-1.html` … `15-1.html`). Do not create new assignment pages at the repo root.
- `netlify/img/` — the only image assets (`1.jpeg`, `2.jpeg`, `3.jpeg`).

## Conventions (follow these)
- **Native HTML + CSS + JavaScript only; no third-party libraries, frameworks, CDN, or external scripts.** This is an explicit requirement recorded in the prompt box inside `netlify/index.html`. Keep pages self-contained.
- **Icons:** all icons must come from the local iconfont in the `font/` directory (`font/iconfont.css` plus its font files, downloaded from iconfont.cn). Never load a CDN icon library (Font Awesome, iconfont CDN, etc.) or substitute emoji/SVG icon packs. The `font/` directory does not exist yet — add it when an icon is first needed.
- **Data fetching:** get server-side data with the native `fetch()` API (`async`/`await`); never use AJAX libraries (jQuery, axios, etc.).
- Keep the `<style>`-in-head pattern; do not introduce separate build steps or dependencies.
- Responsive style: `@media` breakpoints at `40rem` / `64rem`, fluid `clamp()`/`rem` type, and a `@media (prefers-reduced-motion: reduce)` fallback for any animation. Semantic landmarks with `aria-label`/`aria-labelledby`.
- `netlify/index.html` uses CSS custom properties (`:root`) for its theme — reuse them if editing it.
- **Naming:** every CSS class name, `id`, and JS variable name must be prefixed with `zle_` (e.g. `.zle_card`, `id="zle_box"`, `zleCount`). This supersedes the older `zhang` prefix used by existing pages.
- **Header comment:** every newly created HTML file must include a comment as the first thing inside `<head>`. The comment records the author, the creation date, the AI model that built the page, and the page's purpose, in this exact shape:
  ```html
  <!-- 张珑恩 | 建立时间：2026-10-26 13:40 | 使用大模型：GLM-5.3-Flash | 功能名称：页面功能简述 -->
  ```
  Fill 建立时间 with the actual creation moment (`Get-Date`) and 使用大模型 with the model actually used for that session.

## Workflow rule: log every prompt first
Before executing any user request, **append** it to `zhang prompt.md` at the repo root — never overwrite existing entries. Each entry records the timestamp, the model used, and the prompt text. Only then perform the task.

## Gotchas
- Images live **only** in `netlify/img/`. Root-level pages must reference them as `netlify/img/N.jpeg`; pages inside `netlify/` use `img/N.jpeg`.
- `netlify/5-1.html` links `css.css`, which **does not exist** (known broken reference — don't "fix" by inventing a file unless asked).
- `netlify/6-1 flex.html` has a space in its filename; quote paths in shell commands.
- To publish a new page: add it under `netlify/` and add a matching `.link-card` block to `netlify/index.html` following the existing pattern.
- No lint/typecheck/test commands exist; verify by opening the HTML in a browser (e.g. `Start-Process netlify\index.html`).
