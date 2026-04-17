# Opensource Sunday

Free, open-source Sunday School & youth ministry curriculum for **Middle School**, **High School**, and **Confirmation** — because great lessons shouldn't live behind a $299 paywall.

🌐 **Live site:** [opensourcesunday.com](https://opensourcesunday.com)

## Why this exists

Every weekend, tens of thousands of volunteer Sunday School teachers walk into a room of kids holding a lesson plan they skimmed in the church parking lot. Most published curricula are either locked behind expensive licenses, tied to a particular denomination's marketing funnel, or so watered down they could be taught at a secular summer camp.

Opensource Sunday is the opposite of all of that:

- **Free forever.** MIT-licensed content. Fork it, print it, remix it, teach it.
- **Scripture at the center.** Every lesson starts and ends with the Bible. No moralizing.
- **One consistent template.** *Behind the Curtain → Center Stage → Prop Department → Directing the Scene.* Volunteers learn the shape once, then every lesson feels familiar.
- **Written for real rooms.** Real middle schoolers. Real attention spans. Real snack-based metaphors.

## What's in the box

The site is organized around three grade levels, each containing **series** (multi-week arcs) which contain **lessons**:

```
content/
├── _index.md                          # Landing page (Hextra hero)
├── middle-school/                     # Grades 6–8
│   ├── _index.md
│   └── sermon-on-the-mount/           # A series
│       ├── _index.md                  # Series overview
│       ├── 1-up-the-mountain.md       # Lesson 1 · The Beatitudes (published)
│       ├── 2-salt-and-light.md        # Lesson 2 · Matt 5:13–16 (published)
│       ├── 3-but-i-say.md             # Lesson 3 · Matt 5:17–48 (draft)
│       ├── 4-when-you-pray.md         # Lesson 4 · Matt 6:5–15 (draft)
│       ├── 5-treasures-and-two-masters.md  # Lesson 5 · Matt 6:19–24 (draft)
│       ├── 6-do-not-worry.md          # Lesson 6 · Matt 6:25–34 (draft)
│       ├── 7-judge-not.md             # Lesson 7 · Matt 7:1–6 (draft)
│       ├── 8-ask-seek-knock.md        # Lesson 8 · Matt 7:7–12 (draft)
│       └── 9-house-on-the-rock.md     # Lesson 9 · Matt 7:24–29 (draft)
├── high-school/                       # Grades 9–12 (coming soon)
│   └── _index.md
└── confirmation/                      # 9th grade confirmation (coming soon)
    └── _index.md
```

### The lesson template

Every lesson follows the same four-section format:

| Section | Purpose |
| --- | --- |
| **Behind the Curtain** | What the teacher needs to know before walking in — context, theology, the *why* |
| **Center Stage** | The ONE thing you want students to walk out with |
| **Prop Department** | The shopping list — Bibles, index cards, snacks, etc. |
| **Directing the Scene** | The actual plan: prayer, a hook, Scripture reading + discussion, deeper reflection, and a tangible "turn toward action" response |

## Tech stack

- **[Hugo](https://gohugo.io/)** — static site generator
- **[Hextra](https://imfing.github.io/hextra/)** — documentation theme (installed as a Hugo module)
- Plain Markdown — no JavaScript frameworks, no build-time magic, no Node

## Running locally

### Prerequisites

- [Hugo](https://gohugo.io/installation/) (extended version)
- [Go](https://go.dev/) (for Hugo modules)
- [Git](https://git-scm.com/)

### Quick start

```bash
git clone https://github.com/meerleo/opensourcesunday.git
cd opensourcesunday
hugo mod tidy
hugo server --buildDrafts --disableFastRender
```

The site will be live at <http://localhost:1313>.

### Updating the theme

```bash
hugo mod get -u github.com/imfing/hextra
hugo mod tidy
```

## Contributing a lesson

Pull requests warmly welcomed. Heresy gently declined.

### 1. Pick a home for it

Decide which grade level and series the lesson belongs to. If you're starting a new series, create a folder with an `_index.md` that describes the arc (see `content/middle-school/sermon-on-the-mount/_index.md` for an example).

### 2. Create the lesson file

Lessons are single Markdown files named like `1-up-the-mountain.md`. Use this frontmatter skeleton:

```yaml
---
title: "Lesson 1 · Up the Mountain"
linkTitle: "1 · Up the Mountain"
weight: 1
description: "The Beatitudes. Who gets called 'blessed'? Jesus flips the scoreboard."
tags:
  - Middle School
  - Beatitudes
  - Matthew 5
scripture: "Matthew 5:1–12"
---
```

- `weight` controls sidebar order within a series.
- `linkTitle` is what shows in the sidebar (shorter than the full title).
- `tags` auto-generate taxonomy pages under `/tags/`.

### 3. Follow the template

Use the four canonical H2 sections in order:

```markdown
## Behind the Curtain
## Center Stage
## Prop Department
## Directing the Scene
```

Under *Directing the Scene*, use H3s for each segment (Start with Prayer, Catch Their Attention, Read and Interpret, Ponder the Possibilities, Turn Toward Action).

### 4. Preview it

```bash
hugo server
```

Make sure the sidebar looks right and the prev/next pagination flows chronologically.

### 5. Open a PR

Include a sentence or two about:
- Where you've taught it (or plan to)
- Age range it's written for
- Anything a teacher absolutely needs to know before using it

## Writing conventions

A few things that keep lessons consistent across contributors:

- **Address the teacher directly.** Use "you" for the teacher, "students" for students.
- **Scripture references in parentheses.** `(Matt. 5:3)`, `(John 4:34)`.
- **Quotes for the teacher to say aloud use blockquotes.** Makes them visually scannable mid-lesson.
- **No em-dashes for decoration.** Use them to join thoughts, not to pad sentences.
- **Humor is allowed.** Sentimentality is not.

## License

The **content** (all Markdown files under `content/`) is licensed under [Creative Commons BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) — use it, adapt it, share it, with attribution. See [LICENSE-CONTENT](LICENSE-CONTENT).

The **site code** (Hugo config, layouts, CSS) is [MIT licensed](LICENSE).

## Credits

- A mission of **Crossroads**, the youth ministry of [Allentown Presbyterian Church](https://allentownpresbyterian.org) in Allentown, NJ
- Lesson template & structure adapted from Allentown Presbyterian Church's Sunday School curriculum
- Site theme: [Hextra](https://imfing.github.io/hextra/) by [Xin](https://github.com/imfing)
- Fueled by the conviction that every kid deserves an adult who knows their name and points them to Jesus
## Maintainer note · mirroring to GitHub

This repo lives in two places:

- **`got.fugu.farm`** — the authoritative remote on my personal server (`ssh://git.itm.works/opensourcesunday`)
- **`github`** — the public mirror at [github.com/meerleo/opensourcesunday](https://github.com/meerleo/opensourcesunday), where pull requests come in

Because GitHub can receive PRs, it is a *source* of commits — not just a passive mirror — so the workflow has to fetch from it before pushing.
### One-time setup (already done, kept here for reference)

```bash
# Rename the original server remote
git remote rename origin got.fugu.farm

# Add the GitHub mirror
git remote add github git@github.com:meerleo/opensourcesunday.git

# Fetch GitHub's refs
git fetch github

# Handy alias that pushes to both in one shot
git config --global alias.pushall '!git push got.fugu.farm master && git push github master'
```
### Day-to-day workflow

**Before starting work**, pull any PRs that were merged on GitHub so both remotes stay in sync:

```bash
git fetch github
git merge github/master   # or: git rebase github/master
```

**After committing**, push to both remotes at once:

```bash
git pushall
```

If `pushall` ever misbehaves, the manual equivalent is:

```bash
git push got.fugu.farm master && git push github master
```
