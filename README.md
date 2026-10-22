# BAM computational & systems biology lab

Source repository for the [BAM computational & systems biology lab website](https://ghjuvangrimaud.github.io/) at Lund University, led by Ghjuvan Micaelu Grimaud. The site presents the group's research, people, publications, software and contact information.

The BAM redesign was merged on **7 September 2026** in [PR #1](https://github.com/GhjuvanGrimaud/ghjuvangrimaud.github.io/pull/1). The site uses **Jekyll**, Markdown, Liquid templates and CSS, with GitHub Pages hosting. Research software and its installation instructions belong in the individual project repositories linked from the site.

## Where to make changes

| Content or setting | Source |
| --- | --- |
| Homepage, research highlights and latest work | [`_pages/about.md`](_pages/about.md), served at `/` |
| Research themes | [`_pages/research.md`](_pages/research.md) |
| Team profiles and alumni | [`_pages/people.md`](_pages/people.md) |
| Publication records | [`_publications/`](_publications/), one Markdown file per paper |
| Publication listing and its layout | [`_pages/publications.md`](_pages/publications.md), which renders `site.publications` |
| Software descriptions and project links | [`_pages/software.md`](_pages/software.md) |
| Contact details and joining the group | [`_pages/contact.md`](_pages/contact.md) |
| Main navigation | [`_data/navigation.yml`](_data/navigation.yml) |
| Site title, description, URL, author settings, collections and plugins | [`_config.yml`](_config.yml) |
| Images and downloadable documents | [`images/`](images/) and [`files/`](files/) |
| BAM-specific styling | [`assets/css/lab.css`](assets/css/lab.css), loaded by [`_includes/head/custom.html`](_includes/head/custom.html) |
| Shared theme templates and styles | [`_layouts/`](_layouts/), [`_includes/`](_includes/), [`_sass/`](_sass/) and [`assets/css/main.scss`](assets/css/main.scss) |

The homepage, Research, People, Software and Contact pages are edited directly. There is no separate team or software database. The homepage's “Latest work” section is also maintained manually.

## Updating content

1. Create a branch from the latest `master`. Edit the relevant files using GitHub's web editor or a local checkout.
2. Preserve each page's YAML front matter between the opening `---` lines. Keep its `permalink` stable unless a URL change is intentional. The BAM pages generally use `author_profile: false` to hide the inherited personal-profile sidebar.
3. Update the page body in Markdown or its existing HTML blocks. Keep headings, links and image alternative text descriptive. Upload images to `images/` and downloadable documents to `files/`, then link to their exact, case-sensitive paths.
4. For a new page, add a Markdown file under `_pages/` with a title and a unique permalink. Add a corresponding entry under `main:` in `_data/navigation.yml` if it should appear in the menu.
5. Open a pull request into `master`. Check the diff, YAML indentation, destination URLs and media paths. GitHub's Markdown preview does not show the final Jekyll/Liquid rendering; check a Jekyll preview when available.
6. After review and merge, follow the GitHub Pages deployment procedure below and check the published pages.

### Adding a publication

Add a file such as `_publications/YYYY-MM-DD-short-title.md`. Use the fields read by the existing publication templates, replacing every example value with the paper's actual metadata:

```yaml
---
title: "Full paper title"
collection: publications
permalink: /publication/year-short-title/
date: YYYY-MM-DD
venue: "Journal or conference name"
paperurl: "https://doi.org/REPLACE_WITH_ACTUAL_DOI"
citation: "Authors. (Year). Title. Journal or conference."
excerpt: "One-sentence summary."
author_profile: false
---
```

Add any longer description below the front matter. Use a real ISO date and a unique permalink; optional fields may be omitted when unavailable. `paperurl` can point to the DOI, publisher page or an authorised public manuscript. If hosting a PDF in `files/`, check redistribution rights before uploading it.

The Publications page loops over `site.publications` in reverse order, so no separate list entry is needed. Keep the publication index in `_pages/publications.md`; add papers to `_publications/`. The inherited `markdown_generator/` scripts are optional legacy utilities, not an automatic import pipeline for BAM.

## GitHub Pages deployment

The configured site address is **https://ghjuvangrimaud.github.io/**. `_config.yml` sets:

```yaml
url: "https://ghjuvangrimaud.github.io"
baseurl: ""
repository: "GhjuvanGrimaud/ghjuvangrimaud.github.io"
```

The repository's default branch is `master`. The [Pages build and deployment for the BAM redesign](https://github.com/GhjuvanGrimaud/ghjuvangrimaud.github.io/actions/runs/34104300902) successfully built with Jekyll and deployed commit `b450cfd` on 7 September 2026. There is no custom workflow committed under `.github/workflows/`.

Before publishing, confirm **Settings → Pages → Build and deployment**. The expected source for this layout is **Deploy from a branch → `master` → `/ (root)`**. This is inferred from the repository layout and recorded deployment; the current Pages settings must be checked in GitHub.

With that source confirmed:

1. Merge the reviewed content change into `master`.
2. Open the repository's [Actions tab](https://github.com/GhjuvanGrimaud/ghjuvangrimaud.github.io/actions) and check the **pages build and deployment** run for that commit. Both build and deployment must succeed.
3. Open the published site and verify the changed pages, navigation, downloads and mobile layout. If the run fails, inspect its logs before making further changes; do not assume that a successful commit means the site was updated.

GitHub also uses an Actions run for branch-based Pages publishing; seeing that run does not imply a custom workflow. See [GitHub's publishing-source documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site).

Keep `baseurl` empty for the current root-level site. Several BAM page links use root-relative paths such as `/research/`; moving the site under a URL subpath would require reviewing those links as well as the configuration.

## Local preview and current limits

- **Local build setup is incomplete.** No `Gemfile` or `Gemfile.lock` is committed, so this repository does not currently define a reproducible Bundler environment. Before documenting local build commands, add and validate a Pages-compatible Ruby/Jekyll dependency setup using [GitHub's local-preview guidance](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/testing-your-github-pages-site-locally-with-jekyll). `_config.dev.yml` supplies development overrides, but does not install dependencies.
- **The npm package only rebuilds the theme's JavaScript.** `package.json` is inherited from Minimal Mistakes; it is not a build system for the whole site. Editing text or `assets/css/lab.css` does not require rebuilding the JavaScript bundle.
- **Content is still being completed.** The homepage's latest work, team, software and contact sections contain editorial placeholders. `_publications/` still contains demonstration papers.
- **Legacy pages remain publishable.** Sample posts, talks, teaching and portfolio records, plus extra pages under `_pages/`, remain in the tree. Collections have `output: true`, `_pages/` is included, and `future: true` enables future-dated posts. Removing a menu item does not remove its page; the sitemap also lists content outside the main navigation. Review and remove or explicitly exclude unwanted examples.
- **Some shared settings remain generic.** Author/profile links, analytics settings and other inherited metadata still need review. The Publications index currently enables the author sidebar, unlike most BAM pages.
- **This is a static site.** Content is maintained through repository changes. There is no application backend or configured contact form; contact information is maintained in `_pages/contact.md`.

## Theme attribution

The site derives from [Academic Pages](https://github.com/academicpages/academicpages.github.io), based on Michael Rose's [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes). Retain the copyright and licence notice in [`LICENSE`](LICENSE). Check separate reuse permissions for papers, images and other third-party material.

`CONTRIBUTING.md` and `CHANGELOG.md` are inherited template documentation and have not yet been adapted to BAM. Use the content-maintenance workflow in this README for this site.
