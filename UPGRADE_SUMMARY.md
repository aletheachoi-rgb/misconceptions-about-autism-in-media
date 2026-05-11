---
layout: default
title: Upgrade Summary
---

## Upgrade Summary
- **From:** 1.2.0
- **To:** 1.3.0
- **Date:** 2026-05-11
- **Automated changes:** 19
- **Manual steps:** 2

## Automated Changes Applied

### Configuration (2 files)

- [x] Updated _config.yml: version 1.2.1 (2026-05-11)
- [x] Updated _config.yml: version 1.3.0 (2026-05-11)

### Layouts (3 files)

- [x] Updated _layouts/index.html — Homepage layout (i18n fall-through + empty_states + JS i18n)
- [x] Updated _layouts/objects-index.html — Objects index layout (errors + empty_states wiring)
- [x] Updated _layouts/glossary-index.html — Glossary index layout (empty_states wiring)

### Includes (1 file)

- [x] Updated _includes/iiif-url-warning.html — IIIF URL warning (now references lang.errors.iiif_mismatch)

### Scripts (2 files)

- [x] Updated scripts/fetch_demo_content.py - Demo content fetcher (v-prefix tolerance fix)
- [x] Updated scripts/generate_collections.py — Sister-file localization for pages/ (about.md/acerca.md)

### Documentation (2 files)

- [x] Updated README.md - README (v1.2.1 badges and beta notice, bilingual)
- [x] Updated README.md — README (v1.3.0 badges and beta notice)

### Other (9 files)

- [x] Updated CHANGELOG.md - CHANGELOG (v1.2.1 release notes)
- [x] Updated _data/languages/en.yml — English language pack (new keys: glossary_intro, index_page.welcome, etc.)
- [x] Updated _data/languages/es.yml — Spanish language pack
- [x] Updated CHANGELOG.md — CHANGELOG (v1.3.0 release notes)
- [x] Removed stale frontmatter keys from index.md: stories_heading, objects_heading, objects_intro (matched v1.2.1 defaults)
- [x] Updated homepage welcome in index.md (matched v1.2.1 default; replaced with v1.3.0 lang-key template)
- [x] Updated glossary intro in pages/glossary.md (matched v1.2.1 default; replaced with v1.3.0 lang-key template)
- [x] Updated objects intro in pages/objects.md (matched v1.2.1 default; replaced with v1.3.0 lang-key template)
- [x] Updated about page in telar-content/texts/pages/about.md (matched v1.2.1 default; replaced with v1.3.0 lang-key template)

## Manual Steps Required

Please complete these after merging:

1. **Bug fix applied automatically — no action required.**

This patch updates `scripts/fetch_demo_content.py` so it tolerates v-prefixed `telar.version` values in `_config.yml` (for example `version: "v1.2.0"` instead of `version: "1.2.0"`). An earlier version of the Telar Compositor's upgrade flow wrote v-prefixed strings into some sites, which caused the demo content fetcher to silently fail and build sites with no demo content. The fix is in the framework file you just received from this upgrade — no further steps are needed on your end.

If your `_config.yml` has a v-prefixed version string, you may leave it as-is; the script now handles both forms. If you prefer, you can also remove the leading `v` manually under the `telar:` section to keep the file consistent with current Telar conventions. ([guide](https://telar.org/docs))
2. **i18n hygiene update applied — most users need to take no action.**

This release wires up Telar's existing language packs in places that previously hardcoded English (homepage empty states, IIIF URL warning, objects-index error messages, JS thumbnail load fallbacks). It also moves the homepage welcome, glossary intro, objects intro, and about page contents into the language pack so Spanish-speaking site owners with `telar_language: es` get sensible defaults.

The migration changed your user-content files **only when a SHA-256 hash check confirmed the file was byte-for-byte identical to the v1.2.1 default**. If you customised any of those pages (welcome paragraph, about description, glossary or objects intros) — even with whitespace edits — the hash differs and your file is preserved untouched.

A new sister-file convention now localizes the about page: a file named `acerca.md` next to `about.md` in `telar-content/texts/pages/`, carrying frontmatter `localized_for: about.md` and `language: es`, is picked up automatically when `telar_language: es`. For sites with `telar_language: es` whose `about.md` is unchanged from the v1.2.1 default, this migration creates `acerca.md` with the default Spanish content automatically. For sites that customised their `about.md`, the migration skips the create — otherwise the new sister file would shadow your customisation at build time. To add another language, create a sister with `language: <code>` (e.g. `language: fr`). ([guide](https://telar.org/docs))

## Resources

- [Full Documentation](https://telar.org/docs)
- [CHANGELOG](https://github.com/UCSB-AMPLab/telar/blob/main/CHANGELOG.md)
- [Report Issues](https://github.com/UCSB-AMPLab/telar/issues)
