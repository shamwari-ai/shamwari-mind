# Shamwari Mind

> The training pipeline, QLoRA configuration and eval harness for the on-device, open-weights model.

[![CI](https://github.com/shamwari-ai/shamwari-mind/actions/workflows/ci.yml/badge.svg)](https://github.com/shamwari-ai/shamwari-mind/actions/workflows/ci.yml)
[![Lint](https://github.com/shamwari-ai/shamwari-mind/actions/workflows/lint.yml/badge.svg)](https://github.com/shamwari-ai/shamwari-mind/actions/workflows/lint.yml)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)
![Status](https://img.shields.io/badge/status-not%20started-lightgrey?style=flat-square)

**Status:** not started | **Tracking:** [shamwari#20](https://github.com/shamwari-ai/shamwari/issues/20) | **Docs:** [docs.shamwari.ai](https://docs.shamwari.ai)

---

## What it is

Nothing is implemented here yet. This repo is a placeholder created alongside
the monorepo split, and the phase it belongs to has not opened. Everything
below describes what it is _for_, not what it contains.

Shamwari Mind is the on-device, open-weights model — distilled and quantized
to run on modest hardware, and the part that makes the sovereignty promise
real for everyday use rather than only for the API. If personal-scope data can
never reach Cloud, and personal-scope data is what makes a companion feel like
_your_ companion, then Mind is the product and Cloud is the general-knowledge
fallback.

This repo will hold the training pipeline, the QLoRA configuration and the
eval harness. Both the weights and the training corpus are meant to be
genuinely publishable, released through the Bundu Foundation rather than sold.

## Scope

It reads `mind_training_chunks` **and nothing else**. That narrowness is the
point: the training corpus is the only input, so this repo never needs access
to live request data, to `personal`-scope pods, or to any customer account.

`mind_training_chunks` is a Postgres view in
[`shamwari-core`](https://github.com/shamwari-ai/shamwari-core)'s schema, and
it is already the far end of rule 2's enforcement — `licenseClass` is resolved
from the model that actually served a request, Core rejects anything without a
valid one, and `training_examples.license_class` carries a
`CHECK (= 'open_weight')` so a restricted row physically cannot enter the
table. This repo therefore implements neither rule: it consumes what the rules
have already filtered. That does not make the rules irrelevant here — rule 2
exists precisely so that this view is safe to train on.

## Language discipline

This model ships **open weights**. Never describe it as an "open source
model" — that wording is wrong about what is actually released, and the CI on
[`docs`](https://github.com/shamwari-ai/docs) and the sites' `check.mjs` both
fail a build that uses it. The full table is in `shamwari`'s `CLAUDE.md`; the
short version is "open weights", not "open source"; "we train Shamwari Mind,
we route Shamwari Cloud", not "we built our own model"; and sovereignty
attaches to Mind and Ground, never to Cloud.

## Ecosystem

- [`shamwari`](https://github.com/shamwari-ai/shamwari) — the umbrella:
  architecture, migration log, repo index, and `CLAUDE.md`
- [`shamwari-core`](https://github.com/shamwari-ai/shamwari-core) — owns the
  schema `mind_training_chunks` is a view over
- [`docs`](https://github.com/shamwari-ai/docs) —
  [docs.shamwari.ai](https://docs.shamwari.ai)
- [Org standards](https://github.com/shamwari-ai/.github/blob/main/ORG_STANDARDS.md)

## Contributing

See the org's
[CONTRIBUTING.md](https://github.com/shamwari-ai/.github/blob/main/CONTRIBUTING.md),
[SECURITY.md](https://github.com/shamwari-ai/.github/blob/main/SECURITY.md) and
[CODE_OF_CONDUCT.md](https://github.com/shamwari-ai/.github/blob/main/CODE_OF_CONDUCT.md).

## Licence

Licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)
— see `LICENSE` and `NOTICE`. The model itself is intended to ship as open
weights on an Apache-2.0 base.

© Bundu Foundation. Shamwari is Bundu Foundation IP, sold commercially under
Nyuchi Africa.
