# AeroPlus Deco — Documentation

MkDocs Material site for the AeroPlus Deco dive planner.

## Local preview

```bash
pip install -r requirements.txt
mkdocs serve
```

Then open <http://127.0.0.1:8000>.

## Project layout

```
mkdocs.yml                  # site configuration
requirements.txt            # python dependencies (mkdocs-material)
.github/workflows/docs.yml  # GitHub Action: builds and publishes on push to main
docs/                       # markdown sources
├── index.md
├── getting-started.md
├── installing.md
├── license.md
├── faq.md
├── disclaimer.md
├── concepts/               # decompression theory pages
├── planning/               # workflow pages
├── ccr/                    # rebreather-specific
└── tools/                  # calculators
```

## Deployment

The GitHub Action runs `mkdocs gh-deploy` on every push to `main` that touches docs files. This builds the site and force-pushes it to the `gh-pages` branch.

### Picking a hosting URL

The app already lives at `sjjan.github.io/aeroplus-deco/` (served from the `main` branch root). Three options for the docs:

#### Option A — Separate docs repo *(recommended for clean separation)*

1. Create a new repo, e.g. `sjjan/aeroplus-deco-docs`
2. Push these files there
3. Docs publish to `sjjan.github.io/aeroplus-deco-docs/`
4. Link to it from the app's About page

App at `/aeroplus-deco/`, docs at `/aeroplus-deco-docs/`. Both work, neither breaks the other.

#### Option B — Custom subdomain

1. Push to a new repo (or use this one)
2. Configure DNS: `docs.aeroplus.nl` → GitHub Pages
3. Add `CNAME` file to `docs/` with `docs.aeroplus.nl`
4. Enable Pages with the custom domain in repo settings

App at `aeroplus.nl` (or wherever), docs at `docs.aeroplus.nl`. Cleanest user-facing setup.

#### Option C — Same repo, requires extra work

Putting docs in the same `sjjan/aeroplus-deco` repo conflicts with how GitHub Pages serves the app. You'd need to either:

- Move the app to the `gh-pages` branch root and have the action publish docs to a subfolder
- Or accept that `mkdocs gh-deploy` will overwrite the `gh-pages` branch (so the app must live elsewhere)

Skip this unless you have a specific reason. Option A or B is simpler.

### Activating the workflow

Once you've decided where the docs live:

1. Copy this entire folder (including `.github/`, `mkdocs.yml`, `requirements.txt`, `docs/`) to the root of your chosen repo
2. Commit and push to `main`
3. The Action will run; check the **Actions** tab to verify
4. In repo **Settings → Pages**, set source to the `gh-pages` branch (created by the Action)
5. Site will be live at `username.github.io/repo-name/` after a minute or two

## Editing

All content is plain Markdown in `docs/`. The Material theme supports:

- Standard Markdown (headings, lists, tables, links, images)
- Admonitions: `!!! note`, `!!! warning`, `!!! tip`, `!!! info`, `!!! danger`
- Code blocks with syntax highlighting and copy buttons
- Material icons via `:material-name:` (e.g. `:material-arrow-right:`)
- `pymdownx.tabbed` for tabbed content blocks
- Tables of contents via `[TOC]` (auto-generated in sidebar by default)

The `nav:` section in `mkdocs.yml` controls the sidebar order. Update it when you add or rename pages.

## Maintenance suggestions

- **After each app release**, scan the FAQ and version-bump any references
- **When the algorithm changes** materially (e.g. new GF behaviour), update the relevant concepts page and add a note in the Disclaimer about version stability
- **Screenshots** are not included in this initial scaffold — add them under `docs/img/` and reference with `![alt](img/filename.png){ width=400 }`. Material handles responsive sizing.
- **Search** is built-in (Lunr.js, client-side). No configuration needed.

## Custom styling (optional)

If you want to tweak colors beyond the indigo palette, create `docs/stylesheets/extra.css` and add to `mkdocs.yml`:

```yaml
extra_css:
  - stylesheets/extra.css
```

Override the Material CSS variables:

```css
:root {
  --md-primary-fg-color: #3451d1;
  --md-primary-fg-color--light: #4a66e6;
  --md-primary-fg-color--dark: #2541b3;
  --md-accent-fg-color: #3451d1;
}
```

`#3451d1` is the AeroPlus Deco brand blue from the app.

## Contact

Email: **support@aeroplus-deco.com**
Issues: **github.com/sjjan/aeroplus-deco/issues**
