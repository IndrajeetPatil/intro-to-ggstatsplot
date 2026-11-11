---
version: alpha
name: Statistical Visualizations with {ggstatsplot}
description: >-
  Scientific statistical visualization presentation design: crisp white canvas,
  signature slate-navy inline code accents, warm peach and apricot overview
  cards, and categorical pastel panels.
colors:
  primary: "#354478"
  secondary: "#0758a8"
  bg-canvas: "#ffffff"
  text: "#222222"
  muted: "#666666"
  code-text: "#354478"
  code-highlight-bg: "#f4f7fb"
  code-highlight-border: "#315e86"
  fragment-blue: "#0758a8"
  card-peach: "#ffdca9"
  card-apricot: "#fde7bb"
  card-green: "#d0e8c5"
  card-blue: "#d4f6ff"
  card-pink: "#f0c1e1"
  card-yellow: "#ffe31a"
typography:
  display:
    fontFamily: News Cycle, Impact, sans-serif
    fontSize: 2.1em
    fontWeight: 700
  heading:
    fontFamily: News Cycle, Impact, sans-serif
    fontSize: 1.4em
    fontWeight: 700
  body:
    fontFamily: News Cycle, sans-serif
    fontSize: 32px
    fontWeight: 400
  mono:
    fontFamily: monospace
rounded:
  sm: 4px
  pill: 25px
components:
  page:
    backgroundColor: "{colors.bg-canvas}"
    textColor: "{colors.text}"
  code-inline:
    color: "{colors.code-text}"
  code-highlight:
    backgroundColor: "{colors.code-highlight-bg}"
    borderColor: "{colors.code-highlight-border}"
  card-philosophy:
    backgroundColor: "{colors.card-apricot}"
    rounded: "{rounded.pill}"
    padding: 20px
  card-feature:
    backgroundColor: "{colors.card-peach}"
    rounded: "{rounded.pill}"
    padding: 20px
---

# DESIGN.md

The visual design specification of the Statistical Visualizations with {ggstatsplot} presentation deck.

## Overview

The visual design is tailored for statistical communication and rich graphical output on a clean white canvas. It uses the RevealJS `simple` theme, customized with high-contrast slate-navy inline code styling (`#354478`), soft code highlight blocks (`#f4f7fb` with `#315e86` inset border), warm apricot and peach card containers (`#fde7bb` and `#ffdca9`), and soft pastel backings for statistical taxonomy.

The presentation format is Quarto RevealJS (`theme: simple`). Custom styles are defined in `style.css` and mirrored in the front matter above.

## Colours

- **Canvas & Typography:**
  - `bg-canvas` (`#ffffff`): Crisp white presentation canvas.
  - `text` (`#222222`): Deep charcoal text for primary readability.
  - `muted` (`#666666`): Slide footer text, metadata, and citation references.
- **Code & Syntax Accents:**
  - `code-text` (`#354478`): Distinctive slate-navy tone for inline code elements.
  - `code-highlight-bg` (`#f4f7fb`): Soft cool background for highlighted code lines.
  - `code-highlight-border` (`#315e86`): Inset 3px solid indicator for active lines.
  - `fragment-blue` (`#0758a8`): High-contrast blue for active step fragments.
- **Card Containers:**
  - `card-apricot` (`#fde7bb`) / `card-peach` (`#ffdca9`): Signature warm card panels for philosophy, API design, and package summaries (25px border radius).
  - `card-green` (`#d0e8c5`): Parametric and robust statistical mode cards.
  - `card-blue` (`#d4f6ff`): Non-parametric statistical mode cards.
  - `card-pink` (`#f0c1e1`): Bayesian statistical mode cards.
  - `card-yellow` (`#ffe31a`): Highlighted takeaway card.

## Typography

- **Headings & Body:** Default clean sans-serif stack from RevealJS `simple` (`News Cycle`, `Impact`, sans-serif).
- **Code:** Monospace stack for R function calls, arguments, and statistical output formulas.

## Layout & Components

- **Statistical Graphics:** Executed ggplot2 figures render at high resolution (`fig-dpi: 300`) and are centered on slide canvases (`fig-align: center`).
- **Cards:** Rounded pill containers (`border-radius: 25px; padding: 20px;`) with warm apricot/peach backings.
- **Title & Overview Images:** Use `.nostretch` and explicit dimensions to maintain stable proportions in both linear and vertical scroll views.
- **Icons:** SVG mask icons (`.deck-icon`) using Font Awesome Free paths rendered in `currentColor`.

## Do's and Don'ts

- **Do** retain `theme: simple` in `index.qmd` front matter.
- **Do** preserve `#354478` for inline code to maintain contrast against card backgrounds.
- **Do** reuse the established apricot (`#fde7bb`) and peach (`#ffdca9`) card containers.
- **Don't** introduce dark presentation canvases that clash with generated ggplot2 light themes.
