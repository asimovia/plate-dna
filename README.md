# Plate

**Version 1.3.1** · [DNApps](https://meshkore.com/dnapps) capsule, spec v0.1 · MIT

Plate comes as a **capsule**: a single text file that a coding agent builds the
whole app from. There is no code in this repository, only
[`plate.dna.yaml`](plate.dna.yaml), the app's DNA. You give it to your agent and
it writes the app for you, adapted to you.

## What the app does

Plate is a calorie and nutrition tracker:

- **Photo or words:** take a photo of what you're eating or describe it in a
  sentence. An AI model estimates the calories, protein, carbohydrates, fat and
  a quality score from 1 to 5.
- **Today:** see how much you have left against your goal.
- **Trends:** charts for the last 30 days.
- **Weekly review:** a review of how you ate in plain language.

It runs in the browser, and you open it by double-clicking `index.html`. You
can also install it on your phone as an app. Your data stays on your device.

It is the nutrition part of [Evolvea](https://evolvea.pages.dev), a larger
personal fitness app, split out on its own.

## Create the app

1. Open **Claude Code** (with Opus 5.5) or **Codex** in an empty folder.
2. Paste this prompt:

```
Build the app described in https://github.com/asimovia/plate-dna/blob/main/plate.dna.yaml following the DNApps standard at https://meshkore.com/dnapps/spec.md. The capsule includes a conformance kit: follow builder.loop and keep fixing the app until node tests/conformance.mjs passes.
```

3. The agent builds the app, runs the conformance kit that comes inside the capsule and keeps fixing the app until every check passes. Then open the `index.html` it creates. To check a build yourself, run `node tests/conformance.mjs` in its folder.

> The agent starts writing the code right away. It may ask you about things to
> personalize, such as language, design or which AI provider to use. Answer them
> or let it decide: if you don't reply, it uses the defaults written in the
> capsule (English and Spanish, your system's light or dark theme) and finishes
> on its own. When it's done, it saves every choice it made in
> `plate.dna.lock.yaml`.

To estimate meals from photos you need an API key for an AI model with vision
(OpenAI, Gemini, Claude…). You enter it in the app's settings, and it never
leaves your device. Without a key you can still log meals by hand.

## DNApps

DNApps is an open standard for sharing **the DNA of an app** instead of the app
itself. The DNA records what the app does and what is fixed. Everything else
(language, platform, design, accessibility, hosting) adapts to the person
who builds it.

- Standard and spec: <https://meshkore.com/dnapps>
- JSON schema: <https://meshkore.com/dnapps/schema.json>

## Versions

| Version | Changes |
|---|---|
| 1.3.1 | Three fixes to the kit, all found by the seventh build (Opus 5.5 on 1.3.0). F10.1 counted model calls made by earlier checks, so no app could pass it; the builder recorded this as a dispute and did not touch the kit. The meal screen check looked for the route instead of the screen id. The heading check had its order reversed. |
| 1.3.0 | The capsule now carries its own conformance kit: a contract that makes the app testable from outside (routes, data-dna hooks, a seeding hook, the lock format) and the checks themselves, which the builder copies verbatim and may not change. The builder works in rounds, fixing the app until the kit passes. Before this, every builder wrote its own tests, and two builds of the same capsule by the same agent checked very different things. |
| 1.2.3 | Checks on what a person sees or hears now run against the app itself: tests/index.html loads index.html in an iframe and inspects it after switching language and opening each screen. Comparing dictionaries doesn't count. The builder runs the tests over localhost so none of these are skipped. Found by the fifth build, which left English accessible names in the Spanish version while its language tests passed. The sixth build (1.2.3) ignored the new check and several older ones; see the build log in the DNApps guide. |
| 1.2.2 | F9.3 now spells out the cache name: version plus a hash of the cached files. A new deliverable, tests/check-build.mjs, checks with node what the browser tests can't: that cache name, the capsule hash in the lock, and a source for every model marked checked. A browser test that can't run reports skipped, not pass. Hidden file inputs need an accessible name or must be out of the tab order. Found by the fourth build, whose own tests passed while all of these were wrong. The fifth build got all of them right; it missed English accessible names in the Spanish version. |
| 1.2.1 | New acceptance line F9.3: an updated app never stays stuck on an old cached copy. Found while checking the third build. The fourth build (1.2.1) still missed the file hash in the cache name, so the line needs a sharper check. |
| 1.2.0 | The translation and accessibility tests now spell out how to check: the whole rendered document, the navigation bar included. Model ids need a source in the lock. Found by the second unattended build, whose own tests passed with the navigation bar still in English. |
| 1.1.0 | Required test harness (tests/index.html, one group per acceptance line, fake model provider), current model ids checked at build time, profile defaults, accessibility and translation checks. Found by the first unattended build. |
| 1.0.2 | American spelling throughout. |
| 1.0.1 | Plainer wording in the capsule comments and texts. |
| 1.0.0 | First version of the capsule. |

The version lives in `identity.version` inside the capsule. Every change gets
a git tag (`v1.3.1`), so you can always rebuild a specific version.
