---
name: phil-code-contribution
description: Rules for code contributed to a phil/* PHP library or Symfony bundle, and the phil-dev command that checks each one. Use when writing, changing, reviewing or scaffolding PHP, Twig or Stimulus code in a phil/* package, and alongside tilttek-contribution for a tilttek/* package. Not for README, doc/, CHANGELOG or docblock prose (phil-docs-contribution), and not for applications that merely install these packages.
---

# Contributing code to a `phil/*` package

The gates of [`phil/dev-tools`][tools] are the executable truth: when this page and a gate disagree, the gate wins.
Commands run from the root of the monorepo; `PHIL_DEV_PACKAGES=<dir>,<dir> composer gates` narrows the gates to some
packages. *Project rule* marks a rule no document states yet and no gate checks: reviewers hold you to it.

Start a package with `vendor/bin/phil-dev new phil/example [--bundle]`. Finish with the commands at the end of this page.

## Origin and independence

1. **Write the code from scratch.** Another project is a reference to read, never a source to copy, translate or port,
   even under a compatible licence. Source: the package's `CONTRIBUTING.md`.
2. **Let a third-party licence in only through a declared Composer dependency, or data imported under a permissive
   licence and kept with its licence and notice.** Leave third-party files such as fonts to the application. *Project
   rule.*
3. **Keep copyleft out of a package's dependencies.** One that cannot be avoided stays alone in a separate adapter
   package, on the maintainers' decision. *Project rule.*
4. **Never name an application, site or customer that uses the package**, even as an example value: what is specific
   to one application is configuration. Source: [skeleton][wording]. Check: `composer docs`.
5. **Depend on open packages only.** An open package must install for anyone. *Project rule.*
6. **Name a third-party service as an adapter, not as the package.** The package stays about the capability. *Project
   rule.*

## Structure and dependencies

7. **Split a library from its bundle.** The library never depends on a bundle, so an application outside Symfony can
   take it alone; the bundle adds configuration, Doctrine, forms, Twig, Messenger and commands. Source:
   [dependencies][deps]. Check: `composer deptrac`.
8. **Use the Symfony component that already does the job** (`symfony/string`, `clock`, `yaml`, `uid`, `mime`, `lock`),
   and extend it rather than replace it. Require it in `composer.json`. Source: [dependencies][deps]. Check:
   `composer deps`.
9. **Ask in an issue before adding any other dependency to a library.** The `deptrac.allow` list of its `phil-dev.php`
   records what it was allowed. Source: [dependencies][deps]. Check: `composer deptrac`.
10. **Keep a bundle's layers apart.** `Domain` is plain PHP without container or I/O, `Application` holds the services
    and the ports, `Infrastructure` the adapters; the bundle class, on `AbstractBundle`, only wires them. Source: the
    package's `CONTRIBUTING.md`. Check: `composer deptrac`, `composer arkitect`.
11. **Give each class the shape of its layer.** `Domain\Model` is final and not readonly, `Domain\ValueObject` final
    and readonly, `Domain\Repository` holds `*Repository` interfaces. Source: [Arkitect][arkitect]. Check:
    `composer arkitect`.
12. **Require a component's own bundle rather than `symfony/framework-bundle`** where the component has one, so that
    an application installs only what it uses. *Project rule.*
13. **With `phil/ddd-bundle`, let the handler marker choose the bus.** A command returns nothing and its caller
    generates the identifier; the domain takes `Psr\Clock\ClockInterface` directly and has no aggregate base class.
    Source: `doc/command-and-query-buses.md` and `doc/out-of-scope.md` of `phil/ddd-bundle`.
14. **Release domain events after the flush, inside the handler's transaction.** Never use
    `DispatchAfterCurrentBusStamp`: it takes the write out of that transaction. Source: `doc/domain-events.md` of
    `phil/ddd-bundle`.

## PHP

15. **Let the formatters decide the style**, with `declare(strict_types=1)` and strict comparisons. Fix:
    `composer cs:fix`, `composer rector:fix`. Check: `composer cs`, `composer rector`.
16. **Never compare dates with `==` or `===`.** The tooling rewrites `==` to `===`, which compares object identity and
    is always false for two instances, and no gate notices. Compare `getTimestamp()`, `format()`, or use `<`, `>`, `<=>`,
    and test the exact case. Source: [PHP-CS-Fixer][cs].
17. **Do not name a class after a PHP pseudo-type such as `Resource`.** PHPDoc reads it as the pseudo-type and the
    formatter lowercases it. *Project rule.*
18. **Type everything natively**: PHPStan runs at its maximum level with 100 % type coverage, and a PHPDoc type only
    refines a native one. Prefer a native type to an `ignoreErrors` entry; an entry carries its reason. Source:
    [PHPStan][phpstan]. Check: `composer phpstan`.
19. **Follow the class rules.** A class is final or abstract, one per file; exceptions, attributes and interfaces live
    in `Exception`, `Attribute` and `Contract` namespaces. Source: [PHPStan][phpstan]. Check: `composer phpstan`.
20. **Stay under the complexity bars**: 25 for a method, 100 for a class. Split rather than excuse. Source:
    [PHPStan][phpstan]. Check: `composer phpstan`.
21. **Never call the forbidden functions**: `unserialize()`, dumps outside tests, `rand()`, `mt_rand()`, `uniqid()`,
    `shuffle()`, `array_rand()`. Source: [PHPStan][phpstan]. Check: `composer phpstan`.
22. **Type the dispatcher as `Symfony\Contracts\EventDispatcher\EventDispatcherInterface`**, never the component's
    interface. Source: [PHPStan][phpstan]. Check: `composer phpstan`.
23. **Write identifiers, comments and exception messages in English.** Source: the package's `CONTRIBUTING.md`.

## Behaviour

24. **Keep a service safe in worker mode**: no state between requests, or a reset through `kernel.reset`. *Project
    rule.* Measure: `composer bench:worker`.
25. **Bound everything a hostile input can grow**, and give each parser a fuzz target in `phil-dev.php`. A crash becomes
    a unit test. Source: [fuzzing][fuzz]. Check: `composer fuzz`, `composer taint`.
26. **Add a benchmark for each hot path.** Source: [benchmarks][bench]. Check: `composer bench:compare`.
27. **Make pure PHP work everywhere.** An accelerator in native code is a separate package with the same API, proposed
    with a worker-mode benchmark before and after, differential tests and fuzzing. *Project rule.*
28. **Keep Messenger messages short and free of personal data.** Send identifiers and opaque references; the handler
    rereads the data at its source, and a heavy payload travels by claim check or as a stored file. Source:
    `doc/messenger.md` of `phil/paged-media-bundle`.
29. **Let a bundle that stores personal data implement `PersonalDataEraser`** and offer field encryption. Source:
    `doc/export-and-erasure.md` of `phil/privacy-bundle`.
30. **Extend through Symfony events, service tags and public interfaces**, not a plugin system of your own. *Project
    rule.*
31. **Do not invent numeric ordering between extensions**: use `before` and `after`. A Symfony event priority is
    allowed. *Project rule.*
32. **Expose REST and JSON only.** *Project rule.*
33. **Write scripts as Stimulus controllers.** Free JavaScript belongs only inside a third-party SDK's iframe. *Project
    rule.* Check: `composer js`.
34. **Render interfaces through the Symfony UX Toolkit.** A bundle requires the recipes of the [PHIL UX kit][kit] it
    needs, reads `subdirectory` from `ux_toolkit`, renders nothing from `vendor/`, and is tested with this kit and the
    Shadcn kit. *Project rule.* Check: `composer twig`, `composer twigstan`.
35. **Name a Twig filter after its package, without a `phil_` prefix** unless a collision is likely. *Project rule.*

## Tests and versions

36. **Ship tests with every change, each naming what it covers** with `#[CoversClass]` or `#[CoversNothing]`. `Unit`
    runs without a kernel or server; `Integration` is skipped without one. Source: [PHPUnit][phpunit]. Check:
    `composer test`.
37. **Kill every mutant.** A survivor is a missing test or unreachable code; one no test can tell apart is named in
    `phil-dev.php` with its reason, and the bar never drops. Source: [Infection][infection]. Check:
    `composer infection:changed`.
38. **Make the package pass installed alone.** A sibling's dependency must not hide a missing `require`. Source:
    [commands][commands]. Check: `composer packages`.
39. **Support the next PHP and Symfony before enforcing them.** Constraints allow both; a deprecation fails the tests;
    a floor rises only in a new release. List them with `vendor/bin/phil-dev matrix`. Source: [version matrix][matrix].
    Check: `composer test:next`, `composer packages:next`.
40. **Keep the public API compatible once a package is tagged.** Source: [commands][commands]. Check: `composer bc`.

## Submitting

41. **Open issues and pull requests where the package's `CONTRIBUTING.md` says**: a split repository is a read-only
    copy. Open an issue first for a large change.
42. **Report a vulnerability privately**, as `SECURITY.md` says, and prefix the commit that fixes it with `security:`.

Before you push:

```sh
composer gates
composer packages
composer test:next
composer docs
```

[tools]: https://github.com/parler-haut-interagir-librement/dev-tools
[wording]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/skeleton.md#the-wording
[deps]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/dependencies.md
[arkitect]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/quality-gates.md#deptrac-and-arkitect
[cs]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/quality-gates.md#php-cs-fixer
[phpstan]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/quality-gates.md#phpstan
[phpunit]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/quality-gates.md#phpunit
[infection]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/quality-gates.md#infection
[fuzz]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/security.md#fuzzing
[bench]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/benchmarks.md
[commands]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/commands.md
[matrix]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/version-matrix.md#the-policy
[kit]: https://github.com/parler-haut-interagir-librement/ux-kit
