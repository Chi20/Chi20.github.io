# AGENTS.md

## Repository Purpose

This repository is a Jekyll-based academic personal homepage for Zhiyuan Ji.

## Best-Practice Reference Structure

Use the following directory layout as the preferred reference when extending or refactoring the homepage:

```text
./
  .gitignore
  Gemfile
  Gemfile.lock
  LICENSE
  README.md
  _config.yml
  run_server.sh
  .github/
    workflows/
      google_scholar_crawler.yaml
      update_github_myprofile.yaml
  _data/
    navigation.yml
  _includes/
    analytics.html
    author-profile.html
    browser-upgrade.html
    fetch_google_scholar_stats.html
    head.html
    masthead.html
    scripts.html
    seo.html
    sidebar.html
    head/
      custom.html
  _layouts/
    default.html
  _pages/
    about.md
    includes/
      homepage.md
      honers.md
      intro.md
      news.md
      others.md
      pub.md
      pub_short.md
  _sass/
    _animations.scss
    _archive.scss
    _base.scss
    _buttons.scss
    _footer.scss
    _forms.scss
    _masthead.scss
    _mixins.scss
    _navigation.scss
    _notices.scss
    _page.scss
    _print.scss
    _reset.scss
    _sidebar.scss
    _syntax.scss
    _tables.scss
    _utilities.scss
    _variables.scss
    vendor/
  assets/
    css/
      academicons.css
      academicons.min.css
      collapse.css
      main.scss
    fonts/
      ...
    js/
      _main.js
      collapse.js
      main.min.js
  docs/
    README-zh.md
    screenshot.png
  github_myprofile_updater/
    update.py
    images/
      logo-sea-header-desktop.webp
      microsoft_logo.svg
      tiktok.png
  google_scholar_crawler/
    .gitignore
    main.py
    requirements.txt
  images/
    ... (site assets, including `ry_profile.jpeg`)
```

## Current Repository Mapping

The current repository does not yet contain `_pages/includes/` or `github_myprofile_updater/`.

When reorganizing the homepage later, prefer splitting homepage content from `_pages/about.md` into partial markdown files under `_pages/includes/`, following the reference structure above.

## Navigation Scroll Implementation

The navigation-related scrolling behavior already exists in this repository.

### Smooth Anchor Scrolling

- Source file: `assets/js/_main.js`
- Key implementation: `$("a").smoothScroll({offset: -20});`
- Purpose: smoothly scroll to anchor targets after clicking navigation links.

### Responsive Navigation Collapse / Expand

- Structure: `_includes/masthead.html`
- Key DOM nodes: `#site-nav`, `.visible-links`, `.hidden-links`
- Source logic: `assets/js/plugins/jquery.greedy-navigation.js`
- Key function: `updateNav()`
- Runtime bundle: `_includes/scripts.html` loads `assets/js/main.min.js`
- Note: `assets/js/main.min.js` already contains the minified `updateNav` logic and smooth-scroll code used on the live site.

## Sidebar Avatar Placement

The sidebar avatar is controlled by configuration plus template rendering:

- Config field: `_config.yml`
- Active value: `author.avatar: "images/chi_profile.jpeg"`
- Render template: `_includes/author-profile.html`
- Key line: `<img src="{{ author.avatar }}" class="author__avatar" alt="{{ author.name }}">`
- Actual image file: `images/chi_profile.jpeg`

## Editing Guidance

- Put homepage profile images under `images/`.
- Keep the sidebar avatar path in `_config.yml` aligned with the actual filename.
- If navigation links are changed, update both `_data/navigation.yml` and the corresponding anchor IDs in `_pages/about.md`.
- If `assets/js/_main.js` or `assets/js/plugins/jquery.greedy-navigation.js` is edited, regenerate or sync `assets/js/main.min.js`, otherwise the live site may still use stale behavior.
