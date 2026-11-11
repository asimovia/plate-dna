# Plate — a DNApps capsule

This repository holds no code. It holds the **DNA** of an app:
[`plate.dna.yaml`](plate.dna.yaml), one text file that a coding agent turns into a
working app.

**Plate** is the nutrition part of a larger personal fitness app (Evolvea), split
out on its own. You photograph what you eat, a vision model estimates calories
and macros, and you see each day and month against your goal. It runs as a web
app you open with a double-click, and it can be installed as a PWA.

## Build it

Open an empty folder in Claude Code, Codex or any other coding agent and say:

> Build the app described in https://raw.githubusercontent.com/asimovia/plate-dna/main/plate.dna.yaml
> following https://meshkore.com/dnapps/spec.md. Honour every fixed gene and adapt the rest to me.

The agent should finish without asking you anything. It leaves:
- a folder whose `index.html` opens the app;
- a README;
- `plate.dna.lock.yaml`, which lists every choice it made.

To estimate meals from photos you need an API key for a vision model. You add
it in the app's settings, and it stays on your device.

## About DNApps

DNApps is an open draft specification for describing an entire app in one
file:
- what it does and the acceptance criteria that prove it;
- what is **fixed** and what **adapts** to the person who builds it (language,
  platform, design, accessibility, hosting);
- the ordered build plan.

Spec and schema: <https://meshkore.com/dnapps>

## License

MIT
