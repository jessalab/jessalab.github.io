# Jessa Lab website

Built with Jekyll. Content is specified in plain markdown/YAML files — no code changes needed for routine updates.

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
