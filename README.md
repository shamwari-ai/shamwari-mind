# shamwari-mind

Training pipeline, QLoRA configuration and eval harness for **Shamwari
Mind** — the on-device, open-weights model.

> **Status: not started.** This repo is a placeholder created alongside the
> monorepo split. The phase it belongs to has not opened yet. Nothing here
> is implemented.

## Scope

Reads `mind_training_chunks` **and nothing else**. That narrowness is the
point: the training corpus is the only input, so this repo never needs
access to live request data, to `personal`-scope pods, or to any customer
account.

Because it touches neither the scope gate nor `licenseClass`, it sits
outside rule 1 and rule 2 entirely — see
[CONTRIBUTING](https://github.com/shamwari-ai/.github/blob/main/CONTRIBUTING.md).

## Language discipline

This model ships **open weights**. Never describe it as an "open source
model" — that wording is wrong about what is actually released, and the
sites' `check.mjs` fails a build that uses it. The full table is in
`shamwari`'s `CLAUDE.md`.

## Related

- [`shamwari`](https://github.com/shamwari-ai/shamwari) — umbrella: architecture, migration log, repo index
- [`shamwari-core`](https://github.com/shamwari-ai/shamwari-core) — owns the store `mind_training_chunks` lives in
- Tracking issue: [shamwari#20](https://github.com/shamwari-ai/shamwari/issues/20)
