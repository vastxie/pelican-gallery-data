# Pelican Gallery Data

中文 · [English](README.en.md)

用同一句提示词，让不同模型生成「鹈鹕骑自行车」的 SVG 动画。本仓库公开生成后的完整 HTML 原件，以及每份作品的模型、档位、运行工具、耗时和费用，供下载、查看和比较。

[在线画廊](https://pelican.lightai.io/) · [GitHub 数据仓库](https://github.com/vastxie/pelican-gallery-data)

当前快照：**2026-09-22，149 份作品，43 个展示模型**。同一模型的不同档位分别记录；网站的默认筛选不影响本仓库的完整收录。

## 提示词

```text
创建一个HTML，内容是SVG绘制一个鹈鹕骑自行车的2D动画
```

每份作品是一次生成的结果，不是多次采样的均值，也没有统一评分。

## 仓库内容

```text
README.md       中文说明
README.en.md    English README
results.json    作品索引
artifacts/      完整 HTML 原件
```

原件逐字节保留模型生成的完整页面，包括页面文字、控件和可能存在的问题，整理者不作修改；`results.json` 中的 SHA-256 可用于核对。

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
