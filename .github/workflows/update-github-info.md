---
name: update-github-info
description: Keep Mona's GitHub Info website current with practical, sourced updates from the GitHub Blog and Changelog.
intent: Help developers learn GitHub faster by keeping Mona's GitHub Info website current with practical, sourced updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
strict: true
network:
  allowed:
    - github.blog
    - github.com
engine:
  id: copilot
  copilot-sdk: true
tools:
  edit: true
  web-fetch:
safe-outputs:
  create-pull-request:
    max: 1
    title-prefix: "[mona] "
    base-branch: main
    branch-prefix: update-github-info/
    draft: true
    fallback-as-issue: false
    reviewers:
      - mona
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and the current `site/content/github-info.md`. Web-fetch
both `https://github.blog/latest/` and `https://github.blog/changelog/`. Use recent
items from those sources to identify practical, developer-focused updates that
fit the site's existing editorial angle.

Update only `site/content/github-info.md`. Keep the page concise, preserve useful
existing content, and include a clear source link for every new fact drawn from
the GitHub Blog or Changelog. Do not add claims that the fetched sources do not
support. If neither source yields a relevant update, or the page needs no
material change, make no edits and call `noop` with a brief reason.

Open a pull request for Mona to review. 
Use a pull request title that mentions Mona or GitHub Info. 
Do not write directly to `main`;
rely on `safe-outputs` with `create-pull-request`.
