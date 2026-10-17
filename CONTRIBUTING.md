# Contributing

Additions and corrections are welcome. This list is a curated catalog, in the style of [awesome-selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted).

## What belongs in the README

- Reusable Gas City packs (a `pack.toml` with a `[pack]` table and Gas City tables such as agents, formulas, orders, or imports).
- Official docs, guides, and the registry.
- Workshops, tutorials, and talks that are specifically about Gas City.
- Tools whose purpose is to run, inspect, or extend a city.

## What belongs in other.md

- A factory or tool shaped around one product, workshop, or lab, when it is still useful to read.

Leave out search misses, test fixtures, superseded schema 1 packs, and anything that is not a Gas City project.

## Entry format

One entry per line, in the section it fits best:

```markdown
- [Name](https://example.com) - One sentence on what it is and when to use it. ([Source Code](https://github.com/owner/name)) `License`
```

- If the project page is the GitHub repository, link the name there and drop the separate source link.
- End with the SPDX license in backticks. If the repository has no `LICENSE` file, write `` `No license file` ``.
- Descriptions are one sentence, specific, and free of marketing.
- Keep entries alphabetical within a section, except the official build methodologies, which stay in the order the official packs README recommends.

## Pull requests

- One addition or correction per pull request.
- Confirm the repository still contains a Gas City `pack.toml` on the default branch, or that the link is a doc, talk, or tool from the categories above.
- Say which section the entry belongs in, and why it is reusable.
