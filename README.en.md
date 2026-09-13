# Pelican Gallery Data

[中文](README.md) · English

One prompt, different models, a pelican riding a bicycle in an SVG animation. This repository contains the complete generated HTML files and records of model configuration, harness, elapsed time, and cost for anyone to download, inspect, and compare.

[Interactive gallery](https://pelican.lightai.io/) · [GitHub dataset](https://github.com/vastxie/pelican-gallery-data)

Snapshot: **2026-09-13 — 102 artifacts across 33 displayed models**. Reasoning levels have separate records. The website's default filters do not change what is included here.

## Prompt

All new samples use this original Chinese prompt:

```text
创建一个HTML，内容是SVG绘制一个鹈鹕骑自行车的2D动画
```

English translation for reference: “Create an HTML page containing a 2D animation, drawn with SVG, of a pelican riding a bicycle.” The translation was not the sampling prompt.

## How the samples were collected

1. New local CLI samples start in separate directories with the prompt above. Each configuration generally contributes one generated artifact. The collection also includes a few existing works and user submissions.
2. Models use supported harnesses and reasoning levels. These include Codex, Claude Code, Deepseek Harness, Grok Build, Pi, ChatGPT Web, and MiMo Desktop. Versions are recorded per artifact.
3. A model may use tools, preview its work, check it, and revise its own code during that run. The curator does not edit the collected HTML, SVG, or animation afterward. SHA-256 hashes verify the originals.
4. Known model IDs, snapshots, reasoning levels, elapsed time, cost, and run status are recorded. Unknown values remain `null`; display names are not used to infer missing facts.

These are individual run results, without repeated-sample averages or a common score. Harnesses differ in system prompts, tools, permissions, and cache conditions. A single image or elapsed time does not establish a model's overall capability.

Known exceptions: Grok-4.5 Medium was rerun once after getting stuck. Its main record uses the second artifact, duration, and cost; `prior_attempts` summarizes the first run, whose HTML is outside this 102-artifact collection. Some Grok runs wrote HTML but ended with a cancelled status. In individual Grok and Hunyuan runs, the curator terminated hung preview child processes without adding a user prompt or editing the HTML. Those waits count toward elapsed time. See `generation_status` and `run_notes`.

## Time and cost

Local CLI timing generally covers process launch through exit, including tools, checks, and waiting. It is not pure model output time. User-submitted durations retain their reported basis; see `duration_source` and `duration_scope`. Generation and collection dates are recorded separately.

Costs are **official API-equivalent estimates**, not subscription charges or actual bills. Where native usage is available, estimates use recorded input, cache reads, cache writes, and output with the applicable pricing conditions. Reasoning tokens already included in output are not counted again. Unverified submitter amounts retain `verified: false`. Unknown pricing or incomplete usage leaves the full cost as `null`, never zero.

Current exceptions: Grok costs exclude compaction and helper calls missing from its native ledger. Hunyuan has one interrupted response without usage, so its full cost is unknown. Gemini uses published non-promotional regular rates effective **2027-01-01** as a comparison baseline, not the charge on the sampling date. Per-record price dates, sources, and coverage notes are retained in `cost`.

## Repository contents

```text
README.md       Chinese README
README.en.md    English README
results.json    Artifact index and result metadata
artifacts/      Complete original HTML, unedited by the curator
```

This repository shares artifacts and result data. It excludes gallery website source, adapted previews, runner scripts, full conversation logs, and usage receipts.

The top level of `results.json` contains `schema_version`, `snapshot_date`, the original `prompt`, and a `results` array. Main fields per result:

| Field | Meaning |
| --- | --- |
| `id`, `artifact` | Stable record ID and original file path relative to the repository root |
| `model_display_name`, `model_label` | Normalized display name and original recorded label |
| `model_id`, `model_snapshot` | Known model ID and backend snapshot; `null` when unknown |
| `reasoning_effort`, `configuration_label` | Recorded reasoning level and display label; a Pro label is not a verified API parameter |
| `harness`, `harness_key`, `harness_version` | Harness display name, internal identifier, and version |
| `duration_seconds`, `duration_source`, `duration_scope` | Elapsed seconds, source, and timing boundaries |
| `cost` | Amount, currency, verification, price dates, and coverage; amounts are decimal strings or `null` |
| `generated_at`, `collected_at` | Known generation and collection timestamps, with time zones |
| `generation_attempts`, `native_request_retries` | Recorded whole-run attempts and internal harness request retries; these are distinct |
| `generation_status`, `run_notes`, `prior_attempts` | Known run status, relevant notes, and a first-attempt summary when rerun |
| `provenance`, `edited_after_collection` | Source type and whether the original was modified after collection |
| `sha256`, `bytes` | Original file's SHA-256 hash and byte count |

## View an original

Find a model and configuration in [results.json](results.json), download the HTML at its `artifact` path, and open it in a browser. You can also download the repository and open files in [artifacts](artifacts/).

Originals retain the complete generated page, including text, controls, and any flaws. Inspect the running HTML to judge the actual result.

## 2026-09-13: OpenCode Go configurations

Added MiniMax M3 (Off / On), MiniMax M2.7 (On), Kimi K2.7 Code (On), Qwen 3.8 Flash (Off / Low / Medium / XHigh), and Qwen 3.7 Plus (Off / Minimal / Low / Medium / High). These five models are hidden by default and remain available through filters.

On means thinking enabled, not High effort. Qwen 3.7 Plus labels represent Pi budgets of 1024 / 2048 / 8192 / 16384 thinking tokens; they are not four officially named effort levels. Qwen 3.8 Flash High and Max aliases map to XHigh, so they are not sampled separately. Actual request controls and the Pi launch level are recorded separately.

Each configuration retains one final original. Models may preview and revise within that run. `visual_tool_usage` records images actually returned by tools to the model, excluding curator checks. M2.7 had two failed transport attempts before producing HTML and completed after switching to Messages. Qwen 3.8 Flash Off had a native retry after an interrupted stream. Complete costs for these two records are unknown; reported usage and earlier elapsed times are preserved separately.
