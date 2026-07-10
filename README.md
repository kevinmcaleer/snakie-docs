# Snakie documentation

The source for the [Snakie](https://github.com/kevinmcaleer/Snakie) documentation
site, published at **[docs.snakie.org](https://docs.snakie.org)**.

Built with [MkDocs](https://www.mkdocs.org/) and the
[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) theme, and
organised with the [Diátaxis](https://diataxis.fr/) framework (tutorials, how-to
guides, reference, explanation).

## Write / preview locally

```bash
python3 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
mkdocs serve                     # live preview at http://127.0.0.1:8000
```

Edit the Markdown in `docs/` and the browser reloads automatically. Add new pages
to the `nav:` in [`mkdocs.yml`](mkdocs.yml).

```bash
mkdocs build --strict            # build the site into site/ and fail on warnings
```

## Structure

```
docs/
  index.md              Home
  get-started/          Download, install, first steps
  tutorials/            Learn by doing (start here)
  guides/               How-to recipes for a single task
  reference/            Facts: shortcuts, file formats, APIs
  explanation/          How things work and why
  images/              Screenshots (add as features land)
```

## Publishing

Every push to `main` triggers
[`.github/workflows/deploy.yml`](.github/workflows/deploy.yml), which builds the
site and publishes it to the `gh-pages` branch via `mkdocs gh-deploy`. The custom
domain is set by [`docs/CNAME`](docs/CNAME) (`docs.snakie.org`).

To finish the first-time setup:

1. In the repo's **Settings → Pages**, set the source to the `gh-pages` branch.
2. Add a DNS `CNAME` record for `docs` → `kevinmcaleer.github.io`.
3. Tick **Enforce HTTPS** once the certificate is issued.

## Screenshots

Pages mark where a screenshot belongs with a `📸 Screenshot` admonition. Capture
these from the app and drop them into `docs/images/`, then replace the placeholder
with `![Alt text](../images/name.png)`.
