# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

Source-of-truth content repo for the Tidy3D FAQ. Authors edit Markdown files in `_faqs/`; two CI pipelines compile that content into (a) Sphinx-flavored Markdown under `docs/faq/` for the Tidy3D documentation site and (b) Jekyll-style frontmatter + Algolia search index for the marketing site (`flexcompute/flex`).

There is no application to build or test — this repo is a content + transformation pipeline.

## Authoring workflow

1. Add or edit a file in `_faqs/<slug>.md`. Filenames are slugified titles.
2. Frontmatter required (YAML between `---` fences):
   - `title` — human-readable question
   - `date` — `YYYY-MM-DD HH:MM:SS`
   - `enabled` — `true` to publish, `false` to hide. **An FAQ with `enabled: false` is dropped from both pipelines** (it won't appear in `docs/faq/` or sync to the marketing site).
   - `category` — must match a `category` string in `faq_categories.json`
   - `version` — optional; rendered into the docs site header table when present
3. Add the new file's relative path (e.g. `_faqs/how-can-i-foo.md`) to the matching category's `faqs` array in `faq_categories.json`. Order in this array controls display order.
4. Images go in `_faqs/img/`. Reference them with relative Markdown (`![alt](img/foo.png)`) — the marketing-site pipeline rewrites these paths to `/assets/tidy3d/faqs/<filename>` automatically.
5. Push to `develop`. Both GitHub Actions fire on changes under `_faqs/**` or to `faq_categories.json`.

## The two pipelines

Same source files, two destinations, two scripts:

### `docs/compile_rst_categories.py` → in-repo Sphinx docs

Triggered by `.github/workflows/compile_docs.yaml` on push to `develop`. The bot commits results back to `develop` (recent commits like `Compile FAQ to documentation markdown :robot:` are these auto-commits — do **not** hand-edit files under `docs/faq/` or the per-category `.rst` files; they will be overwritten).

What it does:
- Copies each `_faqs/*.md` into `docs/faq/`, stripping frontmatter and replacing it with a Markdown title + a metadata table (Date / Category / optional Version).
- Strips Jekyll-isms: `{: ... }` attribute blocks, `{% highlight python %} ... {% endhighlight %}` → fenced ```python blocks, `&nbsp;` → space, residual `<p>`/`<div>`/`<span>` tags.
- Generates one `docs/<category-id>.rst` toctree per category from `faq_categories.json`, plus the top-level `docs/index.rst` listing every category `.rst`.

### `script/convert-and-sync.py` → marketing site (`flexcompute/flex`)

Triggered by `.github/workflows/sync.yml` on push to `develop`. Runs in CI only (touches Algolia and pushes to another repo). Steps:
- Walks `_faqs/**/*.md`, parses frontmatter, **skips entries where `enabled` is falsy**.
- Uploads FAQ titles as Algolia search suggestions to index `faq-titles` (app `7HAKFDYBT6`). Uses `replace_all_objects` — every run is a full replacement of the index.
- For each enabled FAQ: rewrites image URLs from local paths to `/assets/tidy3d/faqs/<file>`, writes the rewritten file to `temp/`.
- Regenerates `faq_categories.yml` from `faq_categories.json` (including auto-adding any new category found in frontmatter that isn't already in the JSON).
- The workflow then `rsync`s `temp/`, `_faqs/img/`, and `faq_categories.yml` into a checkout of `flexcompute/flex` and commits.

`temp/` and `faq_categories.yml` are CI build artifacts — both are gitignored and should not be committed.

## Local dev commands

Run the docs pipeline locally (safe — no network):

```bash
pip install PyYAML
python docs/compile_rst_categories.py
```

Run the sync pipeline locally — **caveat: this calls Algolia and replaces the live `faq-titles` index** with the credentials in `script/config.ini`. Use only if you mean to:

```bash
pip install -r script/requirements.txt
python script/convert-and-sync.py
```

To dry-run the sync transformations without touching Algolia, comment out the `Sync()` call at the bottom of `script/convert-and-sync.py` and inspect `temp/` + `faq_categories.yml`.

There are no tests, no linter config, and no build. `script/crawler.py` is an empty stub.

## Things to know before editing

- **Two slug spaces.** The on-disk filename slug (e.g. `how-can-i-define-graphene.md`) is independent of the `id` injected into Jekyll frontmatter by `convert-and-sync.py` (which is `slugify(title)`). They usually agree but don't have to. The category `id` in `faq_categories.json` is similarly derived from the category name.
- **`faq_categories.json` is the ordering source of truth.** A file existing in `_faqs/` is not enough — if it's not listed under a category's `faqs` array, the docs pipeline won't include it. The sync pipeline will still pick it up via frontmatter and append it to the matching category (creating a new category entry if needed).
- **Date format matters.** `extract_content_between_dashed` parses YAML, then re-serializes datetimes as `%Y-%m-%d %H:%M:%S`. Bare dates (no time) work but get normalized.
- **`develop` is the working branch** for both workflows; PRs are merged into `develop`, not `main`.
- **Algolia credentials are checked in** at `script/config.ini` (writable key). Treat any change there as security-sensitive.
