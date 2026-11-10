# PHIL contribution skills

**Agent skills that teach Claude Code, OpenAI Codex and Gemini CLI the rules of the open `phil/*` and `tilttek/*`
packages, so that a contribution passes on the first try.**

The packages are held to strict gates: PHPStan at its maximum level, 100 % of mutants killed, each package installed
alone, documentation checks. An agent that knows the rules before it writes spends its time on the contribution
instead of on the failures. Each rule is short, gives its reason when that is not obvious, links its source and names
the command that verifies it. The gates of [`phil/dev-tools`](https://github.com/parler-haut-interagir-librement/dev-tools)
stay the executable truth.

## Skills

| Skill | Use it when |
|---|---|
| [`phil-code-contribution`](skills/phil-code-contribution/SKILL.md) | Writing or reviewing the PHP, Twig or Stimulus code of a `phil/*` library or bundle. |
| [`phil-docs-contribution`](skills/phil-docs-contribution/SKILL.md) | Writing or reviewing a README, `doc/`, its French mirror, a CHANGELOG or docblocks in a `phil/*` or `tilttek/*` package. |
| [`tilttek-contribution`](skills/tilttek-contribution/SKILL.md) | Working on a `tilttek/*` package, or deciding whether a package belongs to Tilttek or PHIL. It adds the rules of games and gamification to the two others. |

## Installation

Each agent reads the same [`skills/`](skills/) directory through its own mechanism.

### Claude Code

```text
/plugin marketplace add parler-haut-interagir-librement/phil-contribution-skills
/plugin install phil-contribution-skills@phil-contribution-skills
/reload-plugins
```

### OpenAI Codex

```sh
codex plugin marketplace add parler-haut-interagir-librement/phil-contribution-skills
```

Then install `phil-contribution-skills` from `/plugins` and start a new session. Without the plugin, append
[`AGENTS.md`](AGENTS.md) and the skills to the instructions of your project.

### Gemini CLI

```sh
gemini extensions install https://github.com/parler-haut-interagir-librement/phil-contribution-skills
```

The extension loads [`GEMINI.md`](GEMINI.md), which imports the three skills.

## Contributing

Read the [contribution guide](CONTRIBUTING.md) and the [code of conduct](CODE_OF_CONDUCT.md). Report a vulnerability
privately, as the [security policy](SECURITY.md) explains, never in a public issue.

## License

MIT. See [LICENSE](LICENSE).
