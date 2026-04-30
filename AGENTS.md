# AGENTS.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project overview

Opensource Sunday is a Hugo static site that publishes free Sunday School curriculum (Middle School, High School, Confirmation). Content is plain Markdown; there are no JavaScript build steps. The theme is [Hextra](https://imfing.github.io/hextra/), pulled in as a Hugo module — there is currently nothing in `layouts/`, `assets/`, `data/`, or `i18n/`, so styling and templates come entirely from the Hextra module.

## Common commands

Local preview (drafts visible, no fast-render caching weirdness):

```bash
hugo server --buildDrafts --disableFastRender
```

Refresh Hugo modules after editing `hugo.yaml` or pulling theme updates:

```bash
hugo mod tidy
```

Update the Hextra theme:

```bash
hugo mod get -u github.com/imfing/hextra
hugo mod tidy
```

Production build (mirrors what `git deploy` runs):

```bash
hugo --minify --cleanDestinationDir
```

## Repository layout (non-obvious bits)

- `content/<grade-level>/<series>/<N-slug>.md` — lessons. `weight` in frontmatter controls sidebar order within a series; `linkTitle` is the (shorter) sidebar label. Lessons with `draft: true` only appear when `--buildDrafts` is passed.
- `content/<grade-level>/<series>/_index.md` — series overview / landing page for that arc.
- `public/` — **intentionally checked into git.** See deployment section below before touching it.
- `hugo.yaml` — single source of truth for nav, theme params, edit-on-GitHub URL, and module imports.
- `archetypes/default.md` — template applied by `hugo new`.
- `layouts/`, `assets/`, `data/`, `i18n/` — empty on purpose; everything is inherited from the Hextra module. Add files here only when overriding the theme.

## Lesson authoring contract

Every lesson under `content/` follows the same four canonical H2 sections, in order:

```markdown
## Behind the Curtain
## Center Stage
## Prop Department
## Directing the Scene
```

Under *Directing the Scene*, use H3s for each segment (Start with Prayer, Catch Their Attention, Read and Interpret, Ponder the Possibilities, Turn Toward Action). The sidebar prev/next pagination relies on `weight`, so keep weights sequential within a series.

Frontmatter skeleton (see README "Contributing a lesson" for the full version):

```yaml
---
title: "Lesson 1 · Up the Mountain"
linkTitle: "1 · Up the Mountain"
weight: 1
description: "..."
tags: [Middle School, Beatitudes, Matthew 5]
scripture: "Matthew 5:1–12"
---
```

Writing conventions enforced by review (not tooling): address the teacher as "you", scripture refs in parentheses like `(Matt. 5:3)`, teacher-spoken lines as blockquotes, no decorative em-dashes.

## Deployment model — read before pushing

This repo has two remotes and an unusual deploy flow:

- **`got.fugu.farm`** (`ssh://git.itm.works/opensourcesunday`) — authoritative, served by [Game of Trees](https://gameoftrees.org) `gotwebd` on an OpenBSD box. **`gotwebd` serves `public/` directly out of the repo at the tip of `master`.** There is no CI, no build step on the server, no deploy hook. **Pushing to `got.fugu.farm` *is* deploying.**
- **`github`** ([github.com/meerleo/opensourcesunday](https://github.com/meerleo/opensourcesunday)) — public mirror that also receives PRs, so it is a *source* of commits, not just a passive mirror.

Consequences:

1. `public/` must be rebuilt locally and committed before every deploy. Never edit files inside `public/` by hand.
2. Always `git pull github master` before starting work so merged PRs are integrated. `pull.rebase = true` is set globally to keep history linear.
3. The deploy is a single alias:

   ```bash
   git deploy
   # equivalent to:
   hugo --minify --cleanDestinationDir \
     && git add public/ \
     && git commit -m "build: deploy" \
     && git pushall
   ```

   `git pushall` pushes to `got.fugu.farm` then `github`. Manual fallback: `git push got.fugu.farm master && git push github master`.
4. After a local rebase, `got.fugu.farm` will reject a non-fast-forward push. Use `git push --force-with-lease got.fugu.farm master` (never plain `--force`), then `git push github master`.

## Licensing split (relevant when adding files)

- Markdown under `content/` — CC BY-SA 4.0 (`LICENSE-CONTENT`).
- Everything else (Hugo config, any future layouts/CSS) — MIT (`LICENSE`).
