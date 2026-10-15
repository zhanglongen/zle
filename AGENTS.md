# AGENTS.md

## What this repo is
A student's "高级网页设计" (Advanced Web Design) course archive: **static HTML + CSS pages, no build system, no package manager, no tests, no git**. Each file is a standalone, self-contained page (styles inline in a `<style>` tag). Content is Chinese (UTF-8), author 张珑恩.

## Ignore these directories
`CodeBuddy/` and `Steam++/` are bundled third-party Windows applications (an Electron editor and a Steam tool), **not part of the website**. Never search, edit, or scan them — they add tens of thousands of irrelevant files.

## Layout
- Repo root `10-1.html` … `10-4.html` — newest assignments (CSS animation, image slideshow, responsive viewport/grid demos). Not yet linked from the site index.
- `netlify/` — the deployable site. `netlify/index.html` is the navigation hub; it links assignment pages `1.html` … `9-1.html` via `.link-card` entries.
- `netlify/img/` — the only image assets (`1.jpeg`, `2.jpeg`, `3.jpeg`).

## Conventions (follow these)
- **Pure/native HTML + CSS only; no CDN, no external frameworks or scripts.** This is an explicit requirement recorded in the prompt box inside `netlify/index.html`. Keep pages self-contained.
- Keep the `<style>`-in-head pattern; do not introduce separate build steps or dependencies.
- Responsive style: `@media` breakpoints at `40rem` / `64rem`, fluid `clamp()`/`rem` type, and a `@media (prefers-reduced-motion: reduce)` fallback for any animation. Semantic landmarks with `aria-label`/`aria-labelledby`.
- `netlify/index.html` uses CSS custom properties (`:root`) for its theme — reuse them if editing it.
- **Naming:** every CSS class name, `id`, and JS variable name must be prefixed with `zhang` (e.g. `.zhang-card`, `id="zhang-box"`, `zhangCount`).

## Workflow rule: log every prompt first
Before executing any user request, **append** it to `zhang prompt.md` at the repo root — never overwrite existing entries. Each entry records the timestamp, the model used, and the prompt text. Only then perform the task.

## Gotchas
- Images live **only** in `netlify/img/`. Root-level pages must reference them as `netlify/img/N.jpeg`; pages inside `netlify/` use `img/N.jpeg`.
- `netlify/5-1.html` links `css.css`, which **does not exist** (known broken reference — don't "fix" by inventing a file unless asked).
- `netlify/6-1 flex.html` has a space in its filename; quote paths in shell commands.
- To publish a new page: add it under `netlify/` and add a matching `.link-card` block to `netlify/index.html` following the existing pattern.
- No lint/typecheck/test commands exist; verify by opening the HTML in a browser (e.g. `Start-Process netlify\index.html`).
