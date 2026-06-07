# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project purpose

A single-page static **personal introduction / about-me website** (개인 소개 페이지)
built entirely in `index.html`. There is no build system, framework, or package manager —
it is plain HTML/CSS served as a static file. The intent is to present one person's
profile: hero (name/role/tagline), about, experience, education, skills, projects, and
contact.

`mycareer.md` is the **content source of truth**: the page's text (name, role, career
history, education, etc.) should mirror what is in `mycareer.md`. When `mycareer.md`
changes, update the corresponding markup in `index.html`. Where `mycareer.md` does not
provide a value (e.g. contact email, exact dates), `index.html` uses placeholders that
are safe to fill in — do not invent facts that aren't in `mycareer.md`.

## Running / previewing

There is no build step. Open the file directly or serve the folder over a local HTTP
server:

```powershell
# Option 1: open directly
start index.html

# Option 2: local server (Python)
python -m http.server 8000   # then visit http://localhost:8000
```

There are no tests, linters, or CI configured.

## Architecture

Everything lives in `index.html`: semantic markup plus an inline `<style>` block (no JS
needed for the current page). Structure to understand before editing:

- **Content is the markup** — each profile section is a `<section>` with an `id` matching
  a sticky `<nav>` anchor (`#about`, `#experience`, `#projects`, `#contact`). Treat the
  document structure as the data model; there is no separate data array.
- **Experience/education entries** use a shared `.entry` two-column layout
  (`.when` date column + `.what` details). Skills are `.skills > span` pills; projects are
  `.project` cards in a responsive `.cards` grid.
- **Theming is driven entirely by `:root` CSS custom properties** (`--accent`, `--bg`,
  `--surface`, `--text`, `--muted`, `--line`). A `@media (prefers-color-scheme: dark)`
  block overrides those variables — change colors there, not at individual rules.

## Conventions

Keep the site self-contained and dependency-free unless the user asks otherwise:

- Prefer the **single `index.html`** with inline CSS; avoid introducing a framework,
  build tooling, or a separate data file for what is a static document.
- **Apple-inspired design language**: SF/`-apple-system` font stack, generous whitespace,
  tight negative letter-spacing on large headings, `#0071e3` blue accent, pill buttons
  (`border-radius: 980px`), `backdrop-filter` blur on the nav. Keep new UI consistent
  with this aesthetic and the existing `:root` variables.
- Keep it **responsive** (uses `clamp()`, a grid that collapses to one column, and a
  `max-width: 600px` media query) and support **dark mode** via the existing block.
- UI copy is in Korean (`<html lang="ko">`); keep new user-facing strings consistent.
