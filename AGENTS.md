# AGENTS.md

Project-level instructions for AI coding agents working on this repository —
Codex, GitHub Copilot (code review and coding agent), and other
`AGENTS.md`-aware tools read this file directly.

## What this is

A single-page [Quarto](https://quarto.org/) presentation rendered to [RevealJS](https://revealjs.com/) slides and deployed as a static site via GitHub Pages.

## Repository layout

```
index.qmd           # All slide content (the only file you usually need to edit)
_quarto.yml          # Quarto project config (output dir, resources list)
_quarto-a11y.yml     # Opt-in profile enabling the axe accessibility checker (`just axe`)
styles.css           # Custom RevealJS theme (fonts, colours, component classes)
meta-tags.html       # OpenGraph, Twitter Card, JSON-LD, and analytics tags
justfile             # Command runner (install, render, preview, clean, etc.)
media/               # Images: evidence screenshots, illustrations, social card
llms.txt             # Short machine-readable summary for LLM discovery
llms-full.txt        # Extended machine-readable summary
.well-known/         # Mirrors of llms.txt and llms-full.txt
robots.txt           # Crawl rules
sitemap.xml          # Sitemap for search engines
.github/             # CI workflow (reusable, from IndrajeetPatil/workflows) and Dependabot
_extensions/         # Optional Quarto extensions (gitignored; currently unused)
_site/               # Build output (gitignored)
```

### Language-specific files

Python-based decks also have:

```
pyproject.toml       # Project metadata and dependencies (managed by uv)
uv.lock              # Locked Python dependencies
.python-version      # Python version pin
.venv/               # Python virtualenv (gitignored)
```

R-based decks have instead:

```
DESCRIPTION          # R dependencies and minimum supported R version
```

Check which set is present to know which language context applies.

## Key conventions

- **Single-file deck.** All slides live in `index.qmd`. There are no partial includes or multi-file splits.
- **Slide syntax.** Slides are separated by `##` headings. Use Quarto's RevealJS dialect: fenced divs (`:::`), columns (`.columns` / `.column`), raw HTML blocks (`{=html}`), and the `{.smaller}` class for dense slides.
- **Inline styling.** Visual design uses inline `style` attributes on fenced divs with a small palette of background colours (e.g. `#e3f2fd`, `#e8f5e9`, `#fff3e0`, `#ffebee`, `#FFFBC1`, `#f8f9fa`). The CSS maps these to the custom theme. Do not change these colour values without updating `styles.css`.
- **Scroll-view image sizing.** Slides with top-level images that otherwise collapse in native `?view=scroll` use `.nostretch` and an explicit image `height` to preserve their live-slide dimensions. Check image visibility in both views when editing them.
- **Image classes.** Images may use semantic classes (e.g. `.hero`, `.artifact`, `.illustration`) that control border, shadow, and rounding in `styles.css`. Check the existing CSS before adding new image classes.
- **Sources.** Every factual claim has a source citation at the bottom of its slide in a small-font centered div. Keep this pattern.
- **Accessibility.** Images must have `fig-alt` text. Raw HTML widgets use `role="img"` and `aria-label`. Keep these.
  Verify with `just axe`, which appends an "Accessibility Report" slide listing axe-core violations. Keep `axe` in
  `_quarto-a11y.yml`, not `index.qmd`, so normal renders never ship the axe-core payload. The explicit `format:`
  block in `index.qmd` takes precedence over CLI metadata such as `-M axe:true`.
  Links inside muted text need a non-colour cue (e.g. `text-decoration: underline`) to satisfy WCAG 1.4.1.
- **Icons.** Icons use lightweight HTML spans backed by only the required SVG path data in the custom stylesheet; no icon-font or Quarto icon extension is needed.
  When adding an icon, add only its mask data, preserve the source licence attribution, keep an accessible label where the icon conveys meaning, and render the deck to verify it.
- **Mermaid performance boundary.** Keep Mermaid diagrams as Mermaid source. Do not replace them with pre-rendered SVGs solely to reduce the website bundle.
- **Code execution.** This deck sets `execute: eval: true` and executes R chunks to produce plots and usage statistics. Preserve its setup chunk and existing execution settings.
- **Compute engine.** Quarto discovers the knitr engine from the R chunks. R dependencies and the minimum supported R version are declared in `DESCRIPTION`.

## Commands

All commands use [just](https://github.com/casey/just). The recipes are the same across decks; only the dependency backend differs:

```bash
just install   # Install language dependencies
just render    # Render index.qmd to _site/
just preview   # Live-reload dev server
just open      # Alias for preview (live-reload dev server over localhost)
just clean     # Remove build artifacts
just check     # Verify Quarto setup
just axe       # Preview with the axe accessibility checker enabled
```

Python decks wrap Quarto in `uv run` (e.g. `uv run quarto render index.qmd`), which syncs the locked environment and puts the project interpreter on `PATH` so Quarto discovers it automatically. R decks call `quarto render` directly (R is discovered automatically). See the `justfile` for exact commands.

## Editing slides

When modifying `index.qmd`:

1. Follow the existing card/column layout patterns visible in neighbouring slides.
2. Preserve the source-citation div at the bottom of each slide.
3. Use the established background-colour palette for info cards rather than inventing new colours.
4. Keep `fig-alt` on every image and `aria-label` on HTML widgets.
5. Run `just render` (or `just preview`) to verify changes compile without errors.

## Editing styles

`styles.css` defines CSS custom properties under `:root` and component classes for complex HTML widgets. The variable names and widget classes vary per deck. When adding a new widget, follow the naming and structure patterns already present in the file.

## SEO and discoverability files

- `meta-tags.html` contains OpenGraph, Twitter Card, JSON-LD structured data, and Google Analytics. Update it when the title, description, or social card image changes.
- `llms.txt` and `llms-full.txt` are machine-readable summaries following the llms.txt convention. Update them when the deck content changes significantly.
- `sitemap.xml` and `robots.txt` are static and rarely need changes.

## CI/CD

- The GitHub Actions workflow in `.github/workflows/` renders the deck and deploys to GitHub Pages on push to `main`. It calls a reusable workflow from `IndrajeetPatil/workflows` (Python and R decks use different workflow files). Do not inline the workflow.
- **Reference the first-party reusable workflow as `@main`, not a commit SHA.** Tracking `main` intentionally brings upstream fixes immediately, including stable Quarto and removal of the unused FontAwesome extension install.
- Dependabot keeps GitHub Actions dependencies up to date weekly. Python decks also have Dependabot configured for `uv`; R decks do not use Dependabot for R packages.

## What not to do

- Do not add new top-level files without a clear reason; the project intentionally has a flat structure.
- Do not split `index.qmd` into multiple files.
- Do not change the Quarto theme from `simple` or the output format from `revealjs`.
- Preserve the existing executed R examples; this presentation needs their computed output.
- Do not commit `_site/`, `_extensions/`, or `.quarto/` (all gitignored). For Python decks, `.venv/` is also gitignored; for R decks, `renv/library/` and `renv/staging/` are gitignored.
- Do not modify the reusable CI workflow inline; it lives in a separate repository.
- Do not pin the first-party reusable workflow to a commit SHA; use `@main` (see CI/CD).
