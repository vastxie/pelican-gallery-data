# Pelican Gallery Data

中文 · [English](README.en.md)

用同一句提示词，让不同模型生成「鹈鹕骑自行车」的 SVG 动画。本仓库公开生成后的完整 HTML 原件，以及每份作品的模型、档位、运行工具、耗时和费用，供下载、查看和比较。

[在线画廊](https://pelican.lightai.io/) · [GitHub 数据仓库](https://github.com/vastxie/pelican-gallery-data)

SVG 当前快照：**2026-09-24，157 份作品，44 个展示模型**。同一模型的不同档位分别记录；网站的默认筛选不影响本仓库的完整收录。

## 提示词

```text
创建一个HTML，内容是SVG绘制一个鹈鹕骑自行车的2D动画
```

每份作品是一次生成的结果，不是多次采样的均值，也没有统一评分。

## 炫技时刻

[炫技时刻](https://pelican.lightai.io/?lang=zh&tab=showtime) 收录开放式提示生成的完整 3D 交互页面，使用独立的 [作品索引](showtime.json)，与 SVG 对比的提示词、展示集合分开。

**《鹈鹕环岛骑行 · Pelican Island Loop》— Claude-Opus-5.5 XHigh · Claude Code · 37m20s · USD 8.82（官方 API 等价下限）。** [HTML 原件](artifacts/showtime-pelican-island-opus-5-5.html)

```text
生成一个鹈鹕骑自行车的3D页面，尽可能把你所有的能力全部都用上
```

这份作品原是 claude.ai Artifact。原件是 claude.ai 返回的版本 1 完整页面：模型写的正文字节不变，前后是 claude.ai 自己的 HTML 外壳。运行时需联网从 jsDelivr 加载 three.js 0.160.0，但不需要 claude.ai；只能在 claude.ai 使用的对话、多人同骑、排行榜和保存按钮在其他地方自动隐藏。在线画廊有意拦截页面引用的 Google Fonts，改用系统字体；直接打开下载的文件时，浏览器仍会尝试加载这些字体。在窄于约 406px 的手机上单独打开时，原件自己的触控行会部分裁掉最右侧的“冲刺”按钮（390px 宽时约裁掉 28%，360px 时大部分不可见）；在线画廊按 430px 渲染再缩小，可避开这一问题。

**《去吹海风 · Pelican Coast Club》— GPT-6-Astra Pro · ChatGPT 网页 · 43m14s · 费用未知。** [HTML 原件](artifacts/showtime-pelican-coast-astra-pro.html)

```text
生成一个鹈鹕骑自行车的3D网页，尽可能把你所有的能力全部都用上
```

每份记录包含原始提示词、标题、模型、模式、运行工具、耗时、已知费用、日期、原件路径与哈希。Pro 是展示模式，未知的 API 推理参数保留为 `null`。

## 仓库内容

```text
README.md       中文说明
README.en.md    English README
results.json    SVG 对比索引
showtime.json   炫技时刻索引
artifacts/      完整 HTML 原件
```

原件逐字节保留模型生成的完整页面，包括页面文字、控件和可能存在的问题，整理者不作修改；上述 Claude Artifact 作品另含 claude.ai 自己的页面外壳，同样按 claude.ai 返回的字节原样保存。SVG 作品的 SHA-256 在 `results.json`，炫技时刻作品在 `showtime.json`，均可用于核对。

`results.json` 顶层保存 `schema_version`、`snapshot_date`、原始 `prompt` 和 `results` 数组。每条结果的字段：

| 字段 | 含义 |
| --- | --- |
| `id`、`artifact` | 记录 ID、相对于仓库根目录的原件路径 |
| `model`、`model_label` | 统一显示名、原始记录名称 |
| `model_id`、`model_snapshot` | 已知的模型 ID 与后端快照；未知为 `null` |
| `reasoning_effort`、`configuration_label` | 已记录的推理档位、界面标签；Pro、On、Off 等标签不是官方档位参数 |
| `harness`、`harness_version` | 运行工具及版本 |
| `duration_seconds` | 该次生成从开始到结束的秒数，包含工具调用与等待 |
| `cost_usd` | 按官方 API 价格折算的美元等价金额，十进制字符串；未知为 `null`，不填零 |
| `generated_at`、`collected_at` | 生成时间与收录时间，带时区 |
| `sha256`、`bytes` | 原件 SHA-256 与字节数 |

费用是官方 API 等价估算，不是订阅扣费或实际账单。

## 查看原件

在 [results.json](results.json) 中找到模型和档位，按 `artifact` 路径下载对应 HTML，用浏览器打开即可查看。也可以下载整个仓库后打开 [artifacts](artifacts/) 中的文件。
