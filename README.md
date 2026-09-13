# Pelican Gallery Data

中文 · [English](README.en.md)

用同一句提示词，让不同模型生成「鹈鹕骑自行车」的 SVG 动画。本仓库保存生成后的完整 HTML 原件，以及模型、推理档位、运行工具、耗时和费用等记录，供下载、查看和自行比较。

[在线画廊](https://pelican.lightai.io/) · [GitHub 数据仓库](https://github.com/vastxie/pelican-gallery-data)

当前快照：**2026-09-13，119 份作品，36 个展示模型**。不同推理档位分别记录；网站的默认筛选不影响本仓库的完整收录。

## 提示词

```text
创建一个HTML，内容是SVG绘制一个鹈鹕骑自行车的2D动画
```

## 怎么测试

1. 使用上面的中文提示词。新增的本地 CLI 采样在独立目录启动，每个配置通常收录一次生成的作品；也包含少量既有作品和用户提交的结果。
2. 使用各模型实际支持的运行工具（Harness）和档位。当前包括 Codex、Claude Code、Deepseek Harness、Grok Build、Pi、ChatGPT 网页和 MiMo Desktop，具体版本见每条记录。
3. 允许模型在该次运行中调用工具、预览、自查和修改自己的代码。生成结束后，整理者不修改收录的 HTML、SVG 或动画；以 SHA-256 核对原件。
4. 记录已知的模型 ID、快照、档位、耗时、费用和运行状态。未知值保留为 `null`，不根据显示名称猜测。

这是一组具体运行的作品记录，没有多次采样均值或统一评分。不同 Harness 的系统提示、工具、权限和缓存条件存在差异，不能仅凭一张图或一次耗时推断模型的总体能力。

已知例外：Grok-4.5 的 Medium 在卡住后重跑过一次，主记录使用第二次的作品、耗时和费用，首次数据摘要见 `prior_attempts`；首次 HTML 不在这 119 份作品中。部分 Grok 运行在写出 HTML 后以取消状态结束；Grok 和 Hunyuan 的个别运行由整理者结束了挂起的预览子进程，未追加用户提示词或修改 HTML，等待计入耗时。详见 `generation_status` 和 `run_notes`。

## 耗时与费用

本地 CLI 耗时通常从进程启动计到退出，包含工具调用、自查和等待，并非纯模型输出时间。用户提交的耗时按提供的信息记录；具体来源和起止范围见 `duration_source`、`duration_scope`。生成日期与收录日期分开保存。

费用为 **官方 API 等价估算**，不是订阅扣费或实际账单。有原生用量的记录按已记录的输入、缓存读取、缓存写入和输出，结合适用的价格条件计算；推理 Token 已包含在输出时不重复计费。提交者提供但未核验的金额保留 `verified: false`；价格未知或用量不完整时，完整费用为 `null`，不填零。

当前数据的几项特殊口径：Grok 的已计费用不含原生账本未覆盖的压缩和辅助请求；Hunyuan 的一次中断响应缺少用量，完整费用未知；Gemini 采用已公布、于 **2027-01-01** 生效的非促销常规价作比较，不代表采样日实付价格。各条记录的价格日期、来源和覆盖说明保留在 `cost` 中。

## 仓库内容

```text
README.md       中文说明
README.en.md    English README
results.json    作品索引与结果元数据
artifacts/      完整、未经整理者修改的 HTML 原件
```

这里公开作品与结果数据。画廊的网站源码、展示副本、运行脚本、完整会话日志和用量收据不包含在仓库中。

`results.json` 顶层保存 `schema_version`、`snapshot_date`、原始 `prompt` 和 `results` 数组。每条结果的主要字段：

| 字段 | 含义 |
| --- | --- |
| `id`、`artifact` | 稳定记录 ID、相对于仓库根目录的原件路径 |
| `model_display_name`、`model_label` | 统一显示名、原始记录名称 |
| `model_id`、`model_snapshot` | 已知的模型 ID 与后端快照；未知为 `null` |
| `reasoning_effort`、`configuration_label` | 已记录的推理档位、界面标签；例如 Pro 标签不等于已核验的 API 参数 |
| `harness`、`harness_key`、`harness_version` | 运行工具的显示名称、内部标识与版本 |
| `duration_seconds`、`duration_source`、`duration_scope` | 耗时秒数、来源和计时范围 |
| `cost` | 金额、币种、核验情况、价格日期及覆盖说明；金额为十进制字符串或 `null` |
| `generated_at`、`collected_at` | 已知的生成日期与收录日期，时间带时区 |
| `generation_attempts`、`native_request_retries` | 已记录的整次生成尝试数、Harness 内部请求重试数；两者不同 |
| `generation_status`、`run_notes`、`prior_attempts` | 已知运行状态、必要备注，以及有重跑时的首次摘要 |
| `provenance`、`edited_after_collection` | 来源类型、收录后是否修改原件 |
| `sha256`、`bytes` | 原件 SHA-256 和字节数 |

## 查看原件

在 [results.json](results.json) 中找到模型和档位，按 `artifact` 路径下载对应 HTML，用浏览器打开即可查看。也可以下载整个仓库后打开 [artifacts](artifacts/) 中的文件。

原件保留模型生成的完整页面，包括页面文字、控件和可能存在的问题；实际效果以浏览器运行结果为准。

## 2026-09-13：OpenCode Go 新增配置

新增 MiniMax M3（Off / On）、MiniMax M2.7（On）、Kimi K2.7 Code（On）、Qwen 3.8 Flash（Off / Low / Medium / XHigh）、Qwen 3.7 Plus（Off / Minimal / Low / Medium / High）。这五款模型默认隐藏，可在筛选菜单显示。

On 是思考开启状态，不代表 High。Qwen 3.7 Plus 的四个思考标签分别是 Pi 的 1024 / 2048 / 8192 / 16384 token 预算上限，并非四个官方命名档位。Qwen 3.8 Flash 的 High / Max 别名会映射到 XHigh，因此不重复采样。请求配置和 Pi 启动档位分别记录。

每个配置保留一份最终原件；允许模型在同一轮中自行预览和修改。`visual_tool_usage` 记录工具实际返回给模型的图片，与整理者检查分开。M2.7 前两次接口调用在生成 HTML 前失败，切换 Messages 后完成；Qwen 3.8 Flash Off 曾由 Pi 自动续试中断响应。这两条的完整费用未知，已有用量及失败耗时另行保留。

## 2026-09-13：Claude Code 新增配置

新增 Claude Opus 4.7（Low / Medium / High / XHigh / Max）、Claude Sonnet 4.6（Low / Medium / High / Max）、Claude Haiku 4.5（1 份），并补齐 Claude Opus 4.8 的 Low / Medium / High / XHigh 与 Claude Opus 4.6 的 Low / Medium / High。Opus 4.6 与 Sonnet 4.6 没有 XHigh。Haiku 4.5 的 API 没有 effort 参数，运行时未指定档位，`reasoning_effort` 与 `configuration_label` 为 `null`，`model_id` 为 API 返回的带日期快照 `claude-haiku-4-5-20251001`。Opus 4.6 在网站默认隐藏，可在筛选菜单显示。

所有 Claude Code 记录使用 Claude 桌面应用随附的 Claude Code CLI 2.1.266，以 `--safe-mode` 启动（不加载 CLAUDE.md、技能、插件、钩子、MCP 服务器和自定义代理），模型用官方 API ID、档位用 `--effort` 指定，每个配置在独立空目录单次生成。费用按原生会话记录逐请求计算：未缓存输入、缓存读取、缓存写入（1 小时缓存写入按 2 倍输入价）和含思考 token 的输出分别计价，并计入 CLI 自报的会话标题等辅助请求；官方价格页于 2026-09-13 核对，Sonnet 5 的首发价已转为标准价。Claude Code 系统提示的静态前缀跨会话共用 1 小时缓存，只有 Fable 5 的 Medium 与 Low 两条记录遇到冷缓存并各多计约 USD 0.19，见其 `cost.cache_state_note`。
