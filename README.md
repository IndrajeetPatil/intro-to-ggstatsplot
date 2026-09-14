# Statistical Visualizations with {ggstatsplot}: A Biography

<img src="media/logo.webp" align="right" width="240" alt="ggstatsplot logo" />

This is a repository for presentation about the `{ggstatsplot}`.

## Links

- 📊 [Presentation slides](https://www.indrapatil.com/intro-to-ggstatsplot/)
- 🌐 [Package website](https://www.indrapatil.com/ggstatsplot/)

## Setup

The package can be installed from CRAN:

```r
install.packages("ggstatsplot")
```

## Development

This project uses R 4.6.0 or later (declared in `DESCRIPTION`), [Quarto](https://quarto.org/) for rendering slides, and [just](https://github.com/casey/just) as a command runner.

### Prerequisites

```bash
# Install just (macOS)
brew install just
```

### Setup

```bash
just install
```

### Just Commands

```bash
just help     # Show all available commands
just install  # Install R dependencies and the a11y extension
just render   # Render slides to HTML
just preview  # Start a live preview with auto-reload
just open     # Alias for preview (live-reload dev server over localhost)
just clean    # Remove generated files and caches
just check    # Check the Quarto and R version setup
just axe      # Preview with an accessibility report slide
just          # Install dependencies and start live-reload preview
```

`just axe` opts into the `_quarto-a11y.yml` profile for local accessibility audits.
Normal renders and deployments do not include the axe checker or report slide.
Preview options can be forwarded, for example `just axe --no-browser --port 4200`.
All Quarto recipes use the native R engine and the dependencies in `DESCRIPTION`.

### Accessibility

`just install` and the shared CI workflow install the latest
[`quarto-revealjs-a11y`](https://github.com/mcanouil/quarto-revealjs-a11y) directly
from upstream with `quarto add mcanouil/quarto-revealjs-a11y --no-prompt`.
The extension handles browser zoom, slide isolation, focus indicators, link
underlines, reduced motion, and screen-reader announcements.

The `accessibility.html` helper still handles scrollable code, slide-menu focus,
and vertical-slide semantics. Unused tabset handling has been removed.
The extension's slide-menu patch and accessibility settings panel are disabled
as in the reference deck: version 0.2.3 introduces ARIA and contrast failures in
those components.

Use `just axe` to inspect slides, fragments, and menu panels in presentation and
scroll views. Normal builds omit the axe checker.

## Feedback

Feedback and suggestions are welcome in [the issue tracker](https://github.com/IndrajeetPatil/intro-to-ggstatsplot/issues).
