# Repository Guidelines

## Project Structure & Module Organization
- `_posts/` holds dated blog entries (`YYYY-MM-DD-title.md`) with Liquid front matter; `_pages/` stores standalone pages (about, archives, etc.).
- `_layouts/`, `_includes/`, and `_sass/` define shared HTML, components, and styles; update these for cross-site design changes.
- `_data/` contains YAML data sources exposed in templates; keep schemas stable to avoid Liquid errors.
- `assets/` and `images/` host static files referenced via `/assets/...`; prefer descriptive slugs that match the post slug.
- `_config.yml` centralizes site metadata and plugin settings; `_site/` is the generated output—never edit it manually.

## Build, Test, and Development Commands
- `bundle install` installs the pinned `github-pages` and plugin dependencies.
- `bundle exec jekyll serve --livereload` builds the site locally, serves it on `http://127.0.0.1:4000`, and watches for changes.
- `bundle exec jekyll build` performs a production build into `_site/`; run it before committing structural updates.
- `JEKYLL_ENV=production bundle exec jekyll build` mimics GitHub Pages, surfacing missing assets and Liquid errors early.

## Coding Style & Naming Conventions
- Use 2-space indentation for Liquid/HTML and fenced code blocks; wrap Markdown lines at ~100 characters for readability.
- Begin post filenames with the publication date and use lowercase kebab-case slugs (`2025-01-10-deep-dive.md`).
- In front matter, keep keys in this order: `layout`, `title`, `date`, `tags`, `description`; align arrays vertically for clarity.
- Reference assets with absolute paths (`/assets/js/interactive.js`) so they resolve in both local and GitHub Pages builds.

## Testing Guidelines
- No automated test suite exists; rely on `bundle exec jekyll doctor` to flag configuration and Liquid issues.
- Validate critical posts with `bundle exec jekyll build --trace` when experimenting with new includes or plugins.
- Manually spot-check generated pages in `_site/` (links, syntax highlighting, responsive layout) before opening a PR.

## Commit & Pull Request Guidelines
- Follow the repository’s imperative-style history (`Expand CPU operation examples`, `Create [cs] ch4-1`); keep subjects under 65 characters.
- Group related content updates into single commits; separate structural or style refactors for easier review.
- Every PR should include: a concise summary, before/after screenshots for visual changes, and links to related issues or posts.
- Confirm that the PR passes a clean `bundle exec jekyll build`; mention any known build warnings in the description.
