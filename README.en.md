# Pelican Gallery Data

[中文](README.md) · English

One prompt, different models, a pelican riding a bicycle in an SVG animation. This repository publishes the complete generated HTML files together with each work's model, reasoning level, harness, elapsed time, and cost, for anyone to download, inspect, and compare.

[Interactive gallery](https://pelican.lightai.io/) · [GitHub dataset](https://github.com/vastxie/pelican-gallery-data)

Snapshot: **2026-09-17 — 129 artifacts across 37 displayed models**. Reasoning levels of the same model have separate records. The website's default filters do not change what is included here.

## Prompt

Every work was generated from this Chinese prompt:

```text
创建一个HTML，内容是SVG绘制一个鹈鹕骑自行车的2D动画
```

English translation for reference: “Create an HTML page containing a 2D animation, drawn with SVG, of a pelican riding a bicycle.” The translation was not the sampling prompt.

Each work is the result of a single generation, without repeated-sample averages or a common score.

## Repository contents

```text
README.md       Chinese README
README.en.md    English README
results.json    Index of works
artifacts/      Complete original HTML files
```

Originals keep the complete generated page byte for byte, including text, controls, and any flaws; the curator does not edit them. The SHA-256 in `results.json` verifies each file.

The top level of `results.json` contains `schema_version`, `snapshot_date`, the original `prompt`, and a `results` array. Fields per result:

| Field | Meaning |
| --- | --- |
| `id`, `artifact` | Record ID and original file path relative to the repository root |
| `model`, `model_label` | Normalized display name and original recorded label |
| `model_id`, `model_snapshot` | Known model ID and backend snapshot; `null` when unknown |
| `reasoning_effort`, `configuration_label` | Recorded reasoning level and display label; labels such as Pro, On, or Off are not official level parameters |
| `harness`, `harness_version` | Tool used to run the model, and its version |
| `duration_seconds` | Seconds from the start to the end of that generation, including tool calls and waiting |
| `cost_usd` | USD equivalent at official API prices, as a decimal string; `null` when unknown, never zero |
| `generated_at`, `collected_at` | Generation and collection timestamps, with time zones |
| `sha256`, `bytes` | Original file's SHA-256 hash and byte count |

Costs are official API-equivalent estimates, not subscription charges or actual bills.

## View an original

Find a model and level in [results.json](results.json), download the HTML at its `artifact` path, and open it in a browser. You can also download the repository and open files in [artifacts](artifacts/).
