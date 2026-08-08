# Projects page is sourced from an explicit repo list, not GitHub's pinned items

Previously, `scripts/fetch-projects.sh` queried the GitHub GraphQL API for the account's *pinned* repositories, including topics/tags, and wrote the result to `data/projects.yaml`. We're replacing this with explicit per-project content stubs (`content/projects/<slug>.md`, headless, holding only the repo URL); CI resolves title and description for each listed URL via the GitHub REST API and writes them to a generated data file keyed by URL, dropping tags/topics/homepage entirely.

We made this change because pinning on the GitHub profile is a different decision than "what should this site show" — the profile's pinned set can drift independently of site intent — and because the card design was simplified to title/description/link only, so topics/tags data is no longer needed. The trade-off is one extra step (adding a content stub per repo) in exchange for explicit control over exactly which repos appear.
