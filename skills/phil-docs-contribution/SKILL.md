---
name: phil-docs-contribution
description: Rules for the documentation of a phil/* or tilttek/* package - README, doc/, CHANGELOG, composer.json description and docblocks - and the phil-dev command that checks each one. Use when writing, changing or reviewing any of those files in such a package. Not for PHP behaviour (phil-code-contribution).
---

# Contributing documentation to a `phil/*` or `tilttek/*` package

`phil-dev check-docs` is the gate, and [its list of checks][checks] is the executable truth. Commands run from the root
of the monorepo. *Project rule* marks a rule no document states yet and no gate checks: reviewers hold you to it.

## Language and voice

1. **Write in English**: the README, `doc/`, the `composer.json` description, docblocks and exception messages. The
   packages are published for readers everywhere. Source: [skeleton][wording].
2. **Say "the application" for whatever installs the package.** Never name a site, customer or application, even as an
   example value. Source: [skeleton][wording]. Check: `composer docs`.
3. **Leave planning vocabulary out**: no phase, batch, milestone or link to a project plan. *Project rule.*
4. **Describe the current state only.** No "formerly", "no longer", "was changed", review notes or decision dates:
   `git log` is the history. *Project rule.*
5. **Write "UJO (Universal JSON Output)" at the first mention, then "UJO".** Never define it through an editor that
   writes a similar shape. *Project rule.*

## Files

6. **Keep the whole file set** that `phil-dev new` writes; do not edit `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`,
   `SECURITY.md` or the licence holder's wording for one package. Source: [skeleton][skeleton]. Check: `composer docs`.
7. **Give `doc/` one file per topic**: at least installation, extension points, testing and reference, plus
   configuration for a bundle. Source: [skeleton][skeleton]. Check: `composer docs`.
8. **Make the README the index.** It lists every `doc/` file and has the Documentation, Requirements, Contributing and
   License sections, with an honest Status table and a Quick start. Source: [skeleton][skeleton]. Check: `composer docs`.
9. **Update `doc/` in the same change as the code**, and the README table when a topic is added. Source: the package's
   `CONTRIBUTING.md`.
10. **Describe every service tag and public interface in `doc/extension-points.md`**, so that an add-on plugs in
    without a patch. *Project rule.* Check, for the file's presence: `composer docs`.
11. **Keep `doc/reference.md` complete**: every class, service, tag, parameter and template. *Project rule.*
12. **Keep links, tables and emphasis valid.** Source: [checks][checks]. Check: `composer docs`.
13. **Keep the prose clean**: English spelling, 120-column lines outside code and tables, words of your own in
    `docs.words`. Source: [workflow][prose]. Check: `composer docs:lint`.
14. **Keep `composer.json` normalized.** Source: [quality gates][normalize]. Fix: `composer deps:normalize:fix`.

## CHANGELOG

15. **Keep one "Added" section until the package is public.** A change rewrites the entry it touches; never add
    "Changed" or "Fixed". Source: [the CHANGELOG][changelog]. Check: `composer docs`.
16. **Order entries for a reader**: model and core, ports and services, persistence, integrations (Twig, Stimulus,
    commands, API), documentation, community files. Never by arrival. Source: [the CHANGELOG][changelog].
17. **Use the usual sections once the package's `phil-dev.php` sets `'docs' => ['public' => true]`.** Source:
    [the CHANGELOG][changelog].

Before you push: `composer docs`, then `composer docs:lint`. A code change also goes through `phil-code-contribution`.

[checks]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/skeleton.md#the-documentation-checks
[skeleton]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/skeleton.md
[wording]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/skeleton.md#the-wording
[changelog]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/skeleton.md#the-changelog
[prose]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/workflow.md#the-prose-of-the-documentation
[normalize]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/quality-gates.md#the-advisories-the-unused-packages-and-the-normalized-composerjson
