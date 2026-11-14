# CLAUDE.md

Hugo static site for rory.ooo. The theme lives in the repo at `themes/rory-ooo/` (a regular directory, not a submodule).

## Requirements

- Hugo extended **0.153.3** (pinned in CI). A newer local Hugo may behave differently.
- `bash`, `curl`, `jq` and a `GITHUB_TOKEN` only if you need to fetch project data locally.
- No Node, no package.json, no JavaScript. CSS goes through Hugo Pipes only.

## Commands

- `hugo server -D`: dev server at http://localhost:1313/
- `hugo --minify`: production build to `public/` (gitignored)
- `GITHUB_TOKEN=... bash scripts/fetch-projects.sh`: populate `data/projects.yaml`

## Testing

There is no test suite or linter. To check a change, run `hugo --minify` and make sure it builds without errors or warnings, then look at the result in `hugo server`.

## Where things are

- `hugo.toml`: site config and the nav menu (`[[menus.main]]`). Add nav links here, not in templates.
- `content/`: markdown with TOML front matter (`+++`).
  - `_index.md`: homepage
  - `career/_index.md`: Career page (old `/cv/` URL aliased to it). Entries are `Role, Company *dates*`; the italic date is styled as a muted line.
  - `projects/<slug>.md`: one stub per project (see below)
- `themes/rory-ooo/layouts/`: `_default/baseof.html` is the page shell; `projects/` and `career/` have their own `list.html`. `partials/row.html` renders project rows.
- `themes/rory-ooo/assets/css/main.css`: the only stylesheet.
- `themes/rory-ooo/static/`: favicon and font.
- `.github/workflows/deploy-website.yml`: on push to `main`, fetches projects, builds and deploys to GitHub Pages.

## How projects are fetched

Each `content/projects/<slug>.md` holds only a `repo` GitHub URL and a `[build]` block (`render = "never"`, `list = "always"`), so it has no page of its own. In CI, `scripts/fetch-projects.sh` reads those URLs, calls the GitHub REST API (`GET /repos/{owner}/{repo}`) for each, and writes name/description/language to `data/projects.yaml`, keyed by URL. `projects/list.html` joins the stubs against that data.

To add a project, add a stub with its `repo` URL. Never edit `data/projects.yaml` by hand; it is generated.
