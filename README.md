# Plate

**Version 1.2.2** · [DNApps](https://meshkore.com/dnapps) capsule, spec v0.1 · MIT

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

1. Open **Claude Code** or **Codex** in an empty folder.
2. Paste this prompt:

```
Build the app described in https://github.com/asimovia/plate-dna/blob/main/plate.dna.yaml following the DNApps standard at https://meshkore.com/dnapps/spec.md
```

3. Open the `index.html` it creates. To check the build, open `tests/index.html`.

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
| 1.2.2 | F9.3 now spells out the cache name: version plus a hash of the cached files. A new deliverable, tests/check-build.mjs, checks with node what the browser tests can't: that cache name, the capsule hash in the lock, and a source for every model marked checked. A browser test that can't run reports skipped, not pass. Hidden file inputs need an accessible name or must be out of the tab order. Found by the fourth build, whose own tests passed while all of these were wrong. The fifth build got all of them right; it missed English accessible names in the Spanish version. |
| 1.2.1 | New acceptance line F9.3: an updated app never stays stuck on an old cached copy. Found while checking the third build. The fourth build (1.2.1) still missed the file hash in the cache name, so the line needs a sharper check. |
| 1.2.0 | The translation and accessibility tests now spell out how to check: the whole rendered document, the navigation bar included. Model ids need a source in the lock. Found by the second unattended build, whose own tests passed with the navigation bar still in English. |
| 1.1.0 | Required test harness (tests/index.html, one group per acceptance line, fake model provider), current model ids checked at build time, profile defaults, accessibility and translation checks. Found by the first unattended build. |
| 1.0.2 | American spelling throughout. |
| 1.0.1 | Plainer wording in the capsule comments and texts. |
| 1.0.0 | First version of the capsule. |

The version lives in `identity.version` inside the capsule. Every change gets
a git tag (`v1.2.2`), so you can always rebuild a specific version.
