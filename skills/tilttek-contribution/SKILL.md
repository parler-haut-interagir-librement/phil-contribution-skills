---
name: tilttek-contribution
description: Rules specific to tilttek/* packages - deciding whether a package belongs to Tilttek or PHIL, and the fairness, randomness, replay and privacy guardrails of games and gamification. Use when creating, changing or reviewing a tilttek/* package, or when deciding where a game-related package belongs. Load it alongside phil-code-contribution for code and phil-docs-contribution for documentation, which hold every rule the two families share.
---

# Contributing to a `tilttek/*` package

Every rule of `phil-code-contribution` and `phil-docs-contribution` applies, with the same gates and commands. This page
adds only what is specific to games and gamification. *Project rule* marks a rule no document states yet and no gate
checks: reviewers hold you to it.

## Where a package belongs

1. **Put it in Tilttek only if it serves nothing but games or gamification.** Content warnings, for instance, also fit
   a book or an event, so that kind of package is `phil/*`, even when the idea came from a game. *Project rule.*
2. **Scaffold with `vendor/bin/phil-dev new tilttek/example [--bundle]`**, which writes the vendor's wording in
   `packages/tilttek-example`. Source: [commands][commands].
3. **Reuse PHIL rather than rewrite it**: `phil/resource` for references, `phil/ddd-bundle` for the buses,
   `phil/almanac` for computed dates, `phil/enums` for states. *Project rule.* Check: `composer deps`.

## The three foundations

4. **Treat a member as an opaque reference.** The application provides it; a package never reads a name, an email or
   an account. Source: `doc/installation.md` of `tilttek/activity`.
5. **Derive every gain, badge and rank from recorded activity.** Changing a rule and replaying the activity must give
   the state the new rule would have given. Source: `doc/projections.md` of `tilttek/activity`.
6. **Take randomness as a parameter**: a secure source in production, a fixed seed in tests, a verifiable draw when the
   application asks for it. *Project rule.* Check: `composer phpstan`, which refuses weak random calls.

## Privacy

7. **Publish nothing about a member without their choice.** A board, a displayed badge or a progression profile shows
   something about them. *Project rule.*
8. **Erase everything a member earned with them**: a bundle provides the eraser of `phil/privacy-bundle` for its
   activity, points and badges. Source: `doc/erasure.md` of the library, and `doc/export-and-erasure.md` of
   `phil/privacy-bundle`.
9. **Keep comparison private by default**: boards and ratings, and hide a badge's rarity under twenty members and five
   awards. *Project rule.*

## Fair rewards

10. **Never let points become a means of payment.** A challenge prize may be a store credit, offered as a prize and
    never as a conversion of points. *Project rule.*
11. **Never sell chances.** Publish the odds of a pack, make draws verifiable, and let predictions be staked in points
    only. *Project rule.*
12. **Reward a survey regardless of its answers.** *Project rule.*
13. **Never unlock access with a level.** A badge for a gesture stays a gesture. *Project rule.*

## Pressure

14. **Give a mechanic that adds pressure its guardrail**, and place each new package under the motivations it touches.
    Reuse concepts from motivation frameworks, never their schema, texts or protected names. *Project rule.*
15. **Allow a gain multiplier only during an announced event.** *Project rule.*
16. **Offer a streak reminder, never impose it**, and provide freezes and grace days. *Project rule.*
17. **Make punitive mechanics opt-in**, by the member and the application, and for that member alone. *Project rule.*
18. **Hide who broke a shared streak.** *Project rule.*

## Accessibility

19. **Never tell a die face or game piece apart by colour alone.** *Project rule.*

[commands]: https://github.com/parler-haut-interagir-librement/dev-tools/blob/main/doc/commands.md#new
