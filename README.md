# Jessa Lab website

Built with Jekyll. Content is specified in plain markdown/YAML files — no code changes needed for routine updates.

## Editing via GitHub web

For simple content edits (team entries, news items, publications, research text), no need for a local setup at all — edit files directly in the GitHub web UI.

Editing on `main` publishes immediately once committed (GitHub Pages auto-builds `main` — see "Deployment" below), and the web editor has no live preview of the rendered site, so double-check YAML/front matter syntax before committing since a malformed file can break the build. For anything you want to preview first, use GitHub's "Create a new branch for this commit and start a pull request" option instead of committing straight to `main`.

To preview a branch/PR, since this repo has no CI or PR-preview deploy, and GitHub Pages only serves `main`, a branch doesn't get its own live URL automatically. Pull it locally and serve:

```
git fetch origin
git checkout <branch-name>
bundle exec jekyll serve
```

then visit http://127.0.0.1:4000 as described below (requires the same prerequisites).

## Prerequisites

- **Ruby** (3.x) — macOS's built-in system Ruby is old and not recommended; install a current version via [rbenv](https://github.com/rbenv/rbenv) or Homebrew (`brew install rbenv ruby-build`).
- **Xcode Command Line Tools** — needed to compile native extensions for some gems. Install with `xcode-select --install` if not already present.
- **Bundler** — install with `gem install bundler` if `bundle -v` doesn't work.

## Running locally

```
bundle install
bundle exec jekyll serve
```

Visit http://127.0.0.1:4000. Pages rebuild automatically while `jekyll serve` is running (except changes to `_config.yml`, which require a restart).

## Where to edit each page

### Homepage
- **`index.md`** — tagline, and the two square "drawing" images + captions (`drawings:` front matter).
- **`_news/`** — one markdown file per news item (e.g. `2026-07-28-welcome.md`), each with a `date:` in the front matter and the item text as the file body. Add a new file to add a new news item.

### Team
- **`_data/team.yml`** — one entry per lab member: `name`, `role`, `photo`, `bio`, `email`, and optional links `scholar`, `orcid`, `github`, `bluesky`, `linkedin`. Add/remove entries to add/remove people; order in the file is the display order.

### Research
- **`research.md`** — free-form markdown: page intro, section headings (`##`), images (use a leading `/` in image paths, e.g. `![](/assets/img/foo.png)`), and "Representative publications" lists linking to entries on the Publications page (`/publications/#slug`).

### Publications
- **`_publications/`** — one markdown file per paper (filename doesn't matter, but by convention `lastname-year-xx.md`). Front matter fields:
  - `slug` — used for anchor links (`/publications/#slug`)
  - `title`, `authors` (comma-separated, `*` marks co-first authors, `^` marks co-corresponding), `year`, `venue`
  - `doi`, `link`, `pdf`, `code`, `commentary` — optional, each renders as a small link badge
  - `description` — optional blurb shown under the entry
  - `selected: true` — shows the paper in the "Selected publications" section
  - `contributing: true` — shows the paper in the "Contributions to collaborative work" section
  - Lab member names in the author list are auto-detected (matched against `_data/team.yml`) and bolded/highlighted.
- **`publications.md`** — just the page title/permalink; don't need to touch this for adding papers.

## Deployment

Pushing to `main` publishes automatically — GitHub Pages builds and deploys Jekyll sites on every push, no separate build/CI step needed. The `CNAME` file points the custom domain (`www.jessalab.org`) at the site; DNS is configured separately with the domain registrar and doesn't need to change here.
