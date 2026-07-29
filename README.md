# sjungwon03.github.io

Personal site. Built and deployed by GitHub Pages (Jekyll).
English is the default; Korean lives under `/ko/`.

## Layout

```
_config.yml        site settings (en + ko strings)
_layouts/          default · page · post
_includes/         head · header · footer
_posts/            posts — lang: en | ko
assets/css/        styles
index.html         English home        →  /
resume.md          English résumé      →  /resume/
about.md           English about       →  /about/
ko/index.html      Korean home         →  /ko/
ko/resume.md       Korean résumé       →  /ko/resume/
ko/about.md        Korean about        →  /ko/about/
feed.xml           Atom feed
```

## Language pairing

Every page carries `lang` and `alt_url` in its front matter.
`alt_url` points at the same page in the other language and drives both the
header toggle and the `hreflang` tags. Omit it and the toggle simply doesn't render.

```yaml
lang: en
alt_url: /ko/resume/
```

## Writing a post

Create `_posts/YYYY-MM-DD-slug.md`.

```markdown
---
title: Post title
description: One line, shown in the list and in search results
tags: [backend, infrastructure]
lang: en
alt_url: /ko/posts/2026/07/30/slug/   # only if a translation exists
---

Body.
```

Korean posts need an explicit `permalink` under `/ko/posts/...`, since the
default permalink pattern is language-agnostic.

Push to `main` and GitHub Pages rebuilds.

## Local preview

```bash
bundle install
bundle exec jekyll serve
```

## Analytics

Self-hosted Rybbit, loaded from `_includes/head.html`.

## Note on the résumé pages

`resume.md` and `ko/resume.md` are derived from a separately maintained résumé.
Because the site is public, certification registration numbers and detailed
military service records are left out.
