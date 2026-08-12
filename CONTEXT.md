# rorycaraher.com

Personal site: a homepage, a Projects listing, and a CV. Single context — the whole repo is one Hugo site with no internal sub-domains.

## Language

**Project**:
An entry on the Projects page: a card with a title, a description, and a link that opens the GitHub repo in a new tab. Backed by a headless content file (`content/projects/<slug>.md`) holding only the repo URL — title and description are resolved from GitHub by CI and stored in a generated data file, keyed by URL.
_Avoid_: Pinned repo (no longer sourced from GitHub's pinned-items feature — the project list is curated explicitly, not derived from what happens to be pinned on the GitHub profile).

**CV**:
The page listing work and education history as two flat lists. Replaces the old "Work" page, which covered work history only.
_Avoid_: Work page, resume.
