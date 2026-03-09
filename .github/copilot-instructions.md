## Quick context

This repository is a Hugo site that uses the Ananke theme as a Hugo module (see `go.mod` and `hugo.toml`). Content is multilingual and stored under `content/en` and `content/fr`. The generated site lives in `public/` (do not edit generated files).

## Big picture architecture (what's important)

- Site core: Hugo static site generator. Theme is a module at `github.com/theNewDynamic/gohugo-theme-ananke/v2` (vendored under `_vendor/`).
- Content: `content/<lang>/...` (example: `content/en/about/index.md`). Front matter uses typical Hugo keys (title, menu, featured_image, etc.). Example: `content/en/about/index.md` uses the `figure` shortcode: `{{< figure src="/images/me.jpeg">}}`.
- Templates: theme-provided templates are used by default. Overrides live in `layouts/` and `layouts/partials/` (see `layouts/partials/page-header.html`). Edit or add templates here to override theme behavior.
- Static assets: `static/` for static files (images, etc.). `assets/` is available for Hugo Pipes (SCSS/JS) when using the Hugo Extended binary.
- Resources: `resourceDir` is set in `config.toml` (currently `"../resources"`); be mindful when running Hugo from a different working directory.

## Key files to inspect first

- `config.toml` — site config and language blocks (DefaultContentLanguage, Paginate=3, resourceDir).
- `hugo.toml` & `go.mod` — module imports and theme version (theme imported as a module). Use these to understand theme/versioning.
- `content/` — markdown content (front matter conventions). Example: `content/en/post/chapter-*.md`.
- `layouts/partials/` and `assets/` — where local theme overrides and asset pipeline inputs live.
- `_vendor/` — vendored modules (the theme is present here).

## Development & build commands (practical)

- Preview locally (dev server, shows drafts):

  hugo server -D

  Visit http://localhost:1313 to preview pages. Use `--disableFastRender` if you see stale templates.

- Build production output (minified):

  hugo --minify

- If you modify SCSS/JS assets or rely on Hugo Pipes, use a Hugo Extended binary. If you edit theme modules, run:

  hugo mod get
  hugo mod vendor

  (the repo already includes `_vendor/` for the theme—only re-run if you change module imports)

## Project-specific conventions and patterns

- Multilingual layout: content is split by language under `content/en` and `content/fr`. When adding content, follow the same directory structure to have Hugo generate language-specific routes (see `config.toml` language blocks).
- Front matter keys used commonly in repo: `title`, `featured_image`, `menu.main.weight`, and `description` (sometimes commented out). Keep image references as `/images/<name>` which maps to `static/images/`.
- The repository keeps a small `Paginate = 3` for demo content. Expect list pages and paginated paths under `public/en/page/1/` etc.
- Theme overrides: Prefer copying small partials into `layouts/partials/` instead of editing vendored theme files. Example override file: `layouts/partials/page-header.html`.

## Integration points & external dependencies

- Theme module: `github.com/theNewDynamic/gohugo-theme-ananke/v2` tracked in `go.mod` and `hugo.toml`.
- Static hosting: generated output is in `public/`. CI/CD or hosting platforms (Netlify, GitHub Pages) should run `hugo --minify` to produce `public/`.
- If you need to change behavior inside the theme, override templates in `layouts/` rather than editing `_vendor/` or `themes/` directly unless you intend to maintain a fork.

## Debugging tips (project-specific)

- If content isn't appearing, check language-specific `content/<lang>` directories and `config.toml` language blocks.
- If CSS/SCSS changes don't apply, ensure you're running Hugo Extended and that `assets/` pipeline files are correctly referenced by templates.
- `nohup.out` in the repo suggests a background process was run locally—inspect it for server logs if present.

## Examples to reference when changing code

- Add a new localized page: copy `content/en/about/index.md` and adjust front matter and translations into `content/fr/...`.
- Override a header partial: create `layouts/partials/page-header.html` (this project already contains an override you can iterate on).

## What NOT to edit

- Do not edit files in `public/`—they are generated output. Prefer editing `content/`, `layouts/`, `assets/`, and `config.toml`.

---
If anything in this file is unclear or you'd like more detail (deployment commands, Hugo version requirements, or CI examples), tell me which area to expand and I'll iterate.
