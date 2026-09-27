# muhighmin.github.io

# muhighmin.github.io

Personal portfolio and blog by **Ahmed Muhaimin Choudhury**, built with Quarto and hosted at [muhighmin.github.io](https://muhighmin.github.io).

The site is a small Quarto website with computational blog posts written in Python, R, and one that uses both languages together via `reticulate`. This README explains how to rebuild the site from scratch on a fresh machine.

## What's inside

- **Home** — short intro with photo
- **About** — longer background
- **Blog** — one post about starting MDS and three computational posts:
  - *Can Flipper Length be used to identify Penguin Species?* — Python (pandas + matplotlib) on Palmer Penguins
  - *Do Manual Cars Really Pack More Horsepower?* — R (dplyr + ggplot2) on `mtcars`
  - *Which Penguin Species Has the Biggest Bill?* — Python and R together via `reticulate`

## Prerequisites

Install these once, in any order:

- [Quarto](https://quarto.org/docs/get-started/) (tested with 1.10.18)
- [uv](https://docs.astral.sh/uv/getting-started/installation/) for Python environments (tested with 0.4+)
- [R](https://cran.r-project.org/) (tested with 4.6.1)

`renv` bootstraps itself when R first starts inside this repo — no separate install needed.

## Build steps

Run these from the repository root:

```bash
# 1. Clone the repo
git clone git@github.com:muhighmin/muhighmin.github.io.git
cd muhighmin.github.io

# 2. Install the Python environment (reads pyproject.toml + uv.lock)
uv sync

# 3. Install the R environment (reads renv.lock)
R -e 'renv::restore()'

# 4. Render the full site
uv run quarto render
```

The built site lands in `docs/`. Open `docs/index.html` in a browser to view locally, or push to GitHub — Pages serves from the `docs/` folder on `main`.

## Data

- **Palmer Penguins** (Python + reticulate posts) — bundled with the `palmerpenguins` R and Python packages. No network fetch during render. Released under CC0.
- **mtcars** (R post) — bundled with base R. Public domain.

## Repository structure

```
├── _quarto.yml           Site config
├── index.qmd             Home page
├── about.qmd             About page
├── blog.qmd              Blog listing page
├── styles.css            Site styles
├── posts/                Blog posts
│   ├── first-weeks/
│   ├── python-analysis-post-palmerpenguins/
│   ├── r-analysis-post-mtcars/
│   └── python-r-analysis-together/
├── images/               Static images
├── docs/                 Rendered site (published by GitHub Pages)
├── pyproject.toml        Python dependencies
├── uv.lock               Python lockfile
├── .python-version       Python version pin
├── renv.lock             R lockfile
├── .Rprofile             Auto-activates renv
└── renv/                 renv scaffolding
```

## Troubleshooting

- **`uv sync` fails on Python 3.14+** — this project uses Python 3.12 for `reticulate` compatibility. `uv sync` reads `.python-version` and installs 3.12 automatically. If you have issues, run `uv python pin 3.12` first.
- **`renv::restore()` prompts about lockfile mismatch** — accept the prompt to install the recorded versions.
- **`quarto render` errors on the reticulate post** — confirm `.venv/` exists (created by `uv sync`) and that R can find it. The post uses `use_virtualenv(here::here(".venv"))` to locate it.

## License

Code: MIT. Written content: CC BY 4.0.