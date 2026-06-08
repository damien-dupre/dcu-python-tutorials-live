# DCU Python Tutorials (browser version)

Interactive Python tutorials that run entirely in the browser, with no install, no
login, and no server. The Python interpreter (Pyodide) is compiled to WebAssembly
and runs on the reader's own machine, so the published page is just static HTML
that can be served anywhere, including GitHub Pages.

This is a [Quarto](https://quarto.org) website built with the
[quarto-live](https://r-wasm.github.io/quarto-live/) extension. It is a browser
based version of the server based
[DCU Python Tutorials](https://damien-dupre.github.io/dcu-python-tutorials/).

## A note on Polars and pandas

The classroom course teaches Polars. Polars is written in Rust and has no
WebAssembly build, so it cannot run inside Pyodide. This browser based edition
therefore uses pandas, which Pyodide ships out of the box, for the data wrangling,
and keeps plotnine for the grammar of graphics plots. The concepts are the same.

## What is in here

- `index.qmd` is the tutorial itself, with editable, runnable exercise blocks that
  move from the basics to pandas and then plotnine.
- `_quarto.yml` holds the website and live-html configuration, including the list
  of Pyodide packages to preload.
- `custom.scss` is some light theming.
- `_extensions/r-wasm/live/` is a vendored copy of the quarto-live extension, so
  the project is self-contained. To update it later, run
  `quarto add r-wasm/quarto-live`.

## Preview locally

You need [Quarto](https://quarto.org/docs/get-started/) and R, with the `knitr` and
`rmarkdown` packages installed. Yes, R, see the note below. The Python packages
(`pandas`, `plotnine`) are not needed locally, because they are downloaded by the
reader's browser at runtime.

```bash
quarto preview      # live-reloading local server
quarto render       # build the static site into _site/
```

## Deploy to GitHub Pages

A workflow is included at `.github/workflows/publish.yml`. Once this folder is
pushed to a GitHub repository:

1. Push to the `main` branch. The action renders the site and publishes it to the
   `gh-pages` branch.
2. In Settings, then Pages, set the source to the `gh-pages` branch.

You can also publish from your own machine:

```bash
quarto publish gh-pages
```

Rendering uses the knitr engine, so it needs R and `knitr` rather than a Python
install. The `pyodide` code cells are passed through to the browser and only run
there, never when the site is built.
