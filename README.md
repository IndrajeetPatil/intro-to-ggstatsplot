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
just install  # Install R dependencies from DESCRIPTION
just render   # Render slides to HTML
just preview  # Start a live preview with auto-reload
just open     # Alias for preview (live-reload dev server over localhost)
just clean    # Remove generated files and caches
just check    # Check the Quarto and R version setup
just          # Install dependencies and start live-reload preview
```

## Feedback

Feedback and suggestions are welcome in [the issue tracker](https://github.com/IndrajeetPatil/intro-to-ggstatsplot/issues).
