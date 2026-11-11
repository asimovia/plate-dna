# Plate

**Version 1.0.1** · [DNApps](https://meshkore.com/dnapps) capsule, spec v0.1 · MIT

Plate is a **self-building capsule** of a piece of software. This repository
holds no code. It holds [`plate.dna.yaml`](plate.dna.yaml), the app's DNA in a
single text file. You give that file to a coding agent, and the agent writes
the app for you, adapted to you.

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

3. Open the `index.html` it creates.

> The agent starts writing the code straight away. It may ask you about things
> to personalise, such as language, design or which AI provider to use. Answer
> them or let it decide: if you don't reply, it uses sensible defaults and
> finishes on its own. When it's done, it saves every choice it made in
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
| 1.0.1 | Plainer wording in the capsule comments and texts. |
| 1.0.0 | First version of the capsule. |

The version lives in `identity.version` inside the capsule. Every change gets
a git tag (`v1.0.1`), so you can always rebuild a specific version.
