# AGENTS.md

A single-page [Quarto](https://quarto.org/) presentation rendered to
[RevealJS](https://revealjs.com/) slides and deployed as a static site via
GitHub Pages.

## Repository layout

```text
index.qmd            # All slide content (the only file you usually need to edit)
_quarto.yml          # Quarto project config (output dir, resources list)
_quarto-a11y.yml     # Opt-in profile enabling the axe accessibility checker (`just axe`)
accessibility.html   # Compatibility fixes supplementing the a11y extension
style.css            # Custom RevealJS theme (fonts, colours, component classes)
meta-tags.html       # OpenGraph, Twitter Card, JSON-LD, and analytics tags
justfile             # Command runner
media/               # Images: evidence screenshots, illustrations, social card
llms.txt, llms-full.txt   # Machine-readable summaries (mirrored in .well-known/)
robots.txt, sitemap.xml   # Static crawl files; rarely change
DESCRIPTION          # R dependencies and minimum R version (installed with pak)
LICENSE              # CC0 dedication
```

`_site/`, `_extensions/`, `.quarto/` and `index.html` are gitignored; never
commit them.

## Commands

```bash
just install   # Install R dependencies with pak and the latest a11y extension
just update    # Upgrade R dependencies
just render    # Render index.qmd to _site/ (run after every change)
just preview   # Live-reload dev server
just clean     # Remove build artefacts
just check     # Verify Quarto setup and the minimum R version
just axe       # Preview with the axe accessibility checker enabled
```

## Key conventions

- **Single-file deck.** All slides live in `index.qmd`; do not split it. Slides
  are separated by `##` headings. Use Quarto's RevealJS dialect: fenced divs
  (`:::`), columns (`.columns` / `.column`), raw HTML blocks (`{=html}`), and
  the `{.smaller}` class for dense slides. Follow the layout patterns of
  neighbouring slides.
- **Theme and colours.** Keep the theme `simple` and the format `revealjs`;
  restyle through `style.css`. Inline `style` backgrounds on fenced divs reuse
  colours already in `index.qmd`; do not invent new ones. New widgets follow the
  naming patterns already in `style.css`.
- **Scroll-view image sizing.** Slides with top-level images that otherwise
  collapse in native `?view=scroll` use `.nostretch` and an explicit image
  `height`. Check image visibility in both views when editing them.
- **Sources.** Every factual claim has a source citation at the bottom of its
  slide in a small-font centred div. Keep this pattern.
- **Spelling and punctuation.** Use British spelling in prose (colour, licence,
  catalogue, artefact) and the Oxford comma in lists of three or more. Leave
  code, identifiers, file names, URLs, quotations, and proper names (`license`
  in YAML, `.well-known/api-catalog`) as they are.
- **Accessibility.** Images must have `fig-alt` text; raw HTML widgets use
  `role="img"` and `aria-label`. Load the `check-accessibility` skill before
  changing markup, styles, widgets or the a11y setup.
- **Icons.** Icons are HTML spans backed by only the required SVG path data in
  `style.css`; no icon font or Quarto icon extension. When adding one, add only
  its mask data, preserve the source licence attribution, and keep an
  accessible label where the icon conveys meaning.
- **Mermaid.** Keep diagrams as Mermaid source; do not replace them with
  pre-rendered SVGs to shrink the bundle.
- **Code execution is on.** The front matter sets `execute: eval: true`: R
  chunks produce the plots and usage statistics. Preserve the setup chunk,
  the executed examples, and the existing execution settings.
- **R dependencies.** Quarto picks the knitr engine from the R chunks; there is
  no `engine:` key. `DESCRIPTION` declares the R packages and minimum R
  version; `just install` installs them with `pak` and CI with
  `r-lib/actions/setup-r-dependencies`.
- **Discoverability files.** Update `meta-tags.html` when the title,
  description, or social card changes, and `llms.txt` / `llms-full.txt` (and
  their `.well-known/` mirrors) when the content changes significantly.
- **No new top-level files** without a clear reason; the structure is flat.

## CI/CD

- `.github/workflows/build-presentation.yaml` calls a reusable workflow from
  `IndrajeetPatil/workflows`: pushes to `main` build and deploy to GitHub
  Pages, pull requests build without deploying. Do not inline or modify that
  workflow here.
- Reference reusable workflows as `@main`, never a commit SHA: they are
  first-party, and a pinned SHA once went five months stale.
- Dependabot updates GitHub Actions weekly; it does not cover R packages.

## Agent skills

Skills live in `.agents/skills/<name>/SKILL.md`. Load one before its task:

| Skill | Load before |
| --- | --- |
| `check-accessibility` | Changing slide markup, styles, widgets, menus or the a11y setup; any accessibility audit |
