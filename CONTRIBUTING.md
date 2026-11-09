# Contributing

This repository holds the agent skills of the open `phil/*` and `tilttek/*` packages of
[Parler Haut Interagir Librement](https://github.com/parler-haut-interagir-librement) (PHIL) and of Tilttek. Open
issues and pull requests here.

## Reporting a problem

- Check first that the problem is not already reported.
- Name the skill and the rule, and show what it says against what the gate or the source says.
- A security vulnerability is not a bug report: follow the [security policy](SECURITY.md) instead.

## Proposing a change

Open an issue before adding a rule whose reason is not obvious. Then:

1. **Write it from scratch.** Another project may serve as a reference to read, never as a source to copy, translate
   or port.
2. **Keep it public and general.** A rule never names an application, site or customer that uses the packages.
3. **Keep the gates as the truth.** A rule a gate already checks takes one line and its command; change the gate in
   [`phil/dev-tools`](https://github.com/parler-haut-interagir-librement/dev-tools), not the skill, when the check is
   wrong.
4. **Keep a rule short and imperative**, with its reason when that is not obvious and its source: a public document, a
   path that exists in the package, or the mark *Project rule*.
5. **Write a shared rule once.** What applies to both families belongs in `phil-code-contribution` or
   `phil-docs-contribution`; `tilttek-contribution` holds only what is specific to games and gamification.
6. **Say when to use a skill** in its `description`, without ambiguity, and update the table of the README when a skill
   is added, with the imports of `GEMINI.md` and the table of `AGENTS.md`.
7. **Validate it**: `claude plugin validate .` checks the manifests and the skills.

## Licence

By contributing, you agree to license your contribution under the MIT licence of this repository, whose holder its
[LICENSE](LICENSE) names.

## Code of conduct

Everyone taking part follows the [code of conduct](CODE_OF_CONDUCT.md).
