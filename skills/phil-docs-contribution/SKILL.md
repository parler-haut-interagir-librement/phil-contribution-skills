---
name: phil-docs-contribution
description: Rules for the documentation of a phil/* or tilttek/* package - README, doc/, its French mirror README.fr.md and doc/fr/, CHANGELOG, composer.json description and docblocks - and the phil-dev command that checks each one. Use when writing, changing or reviewing any of those files in such a package. Not for PHP behaviour (phil-code-contribution).
---

# Contributing documentation to a `phil/*` or `tilttek/*` package

`phil-dev check-docs` is the gate, and [its list of checks][checks] is the executable truth. Commands run from the root
of the monorepo. *Project rule* marks a rule no document states yet and no gate checks: reviewers hold you to it.

## Language and voice

1. **Write in English first**: the README, `doc/`, the `composer.json` description, docblocks and exception messages.
   The packages are published for readers everywhere; the French is a mirror of the README and `doc/` (see below).
   Source: [skeleton][wording].
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

## The French mirror

15. **Keep a French mirror of the README and of `doc/`**: `README.fr.md` beside `README.md`, and `doc/fr/<name>.md` for
    each `doc/<name>.md`, same names and same tree. A document without its mirror, or a mirror without its document,
    fails. English stays the source, and only the README and `doc/` are translated: comments, docblocks, the
    `composer.json` description, the CHANGELOG and the community files stay in English.
    Source: [the French mirror][mirror]. Check: `composer docs:translations`.
16. **Update the French in the commit that changes the English**, then record it:
    `vendor/bin/phil-dev stamp-translations <package> --file=<document>`. The stamp, on the first line of the mirror, is
    a fingerprint of the English: without it, or when the English has changed since, the translation is reported as
    late. Stamp only what you translated, and never write the stamp by hand. Source: [the stamp][stamp].
    Check: `composer docs:translations`.
17. **Keep the structure**: as many headings of each level as the English, and every fenced code block identical,
    comments included. Translate the headings and the prose, never an identifier. Source: [the French mirror][mirror].
    Check: `composer docs:translations`.
18. **Follow [the glossary][glossary]**: its words, in neutral technical Québec French, and its tone: address the reader
    as « vous », in simple sentences, with links to the matching `doc/fr/` files. *Project rule.* Check:
    `composer docs:lint` for the spelling.
19. **Make a translated package blocking**: `'docs' => ['translations' => 'blocking']` in its `phil-dev.php`, which
    `phil-dev new` writes. Only a package still to translate is `advisory`. Narrow the gate to your packages with
    `PHIL_DEV_PACKAGES`, and read an advisory package's findings with `-v`. Source: [the catch-up][catchup].

## CHANGELOG

20. **Keep one "Added" section until the package is public.** A change rewrites the entry it touches; never add
    "Changed" or "Fixed". Source: [the CHANGELOG][changelog]. Check: `composer docs`.
21. **Order entries for a reader**: model and core, ports and services, persistence, integrations (Twig, Stimulus,
    commands, API), documentation, community files. Never by arrival. Source: [the CHANGELOG][changelog].
22. **Use the usual sections once the package's `phil-dev.php` sets `'docs' => ['public' => true]`.** Source:
    [the CHANGELOG][changelog].

Before you push: `composer docs`, `composer docs:translations`, then `composer docs:lint`. A code change also goes
through `phil-code-contribution`.

[checks]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/skeleton.md#the-documentation-checks
[skeleton]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/skeleton.md
[wording]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/skeleton.md#the-wording
[changelog]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/skeleton.md#the-changelog
[prose]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/workflow.md#the-prose-of-the-documentation
[mirror]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/quality-gates.md#the-french-mirror-of-the-documentation
[stamp]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/quality-gates.md#how-a-late-translation-is-found
[catchup]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/quality-gates.md#while-the-existing-packages-catch-up
[glossary]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/fr-glossary.md
[normalize]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/quality-gates.md#the-advisories-the-unused-packages-and-the-normalized-composerjson
