# htlb-api · 高性价比人生指南：在线检索 + 数据接口

- **在线检索**：https://666ghj.github.io/htlb-api/
- **数据接口**：https://666ghj.github.io/htlb-api/data/htlb.json （全量 JSON，676+ 条，可自由 fetch / 下载）

## 这是什么

《高性价比人生指南》（[eternity4719/HowToLiveBetter](https://github.com/eternity4719/HowToLiveBetter)）的在线检索页 + 机器可读数据接口。数据来自社区结构化数据集 [sin0317/htlb-dataset](https://github.com/sin0317/htlb-dataset)，每日自动同步上游。

## 数据接口用法

数据文件（静态 JSON，无需服务器）：

| 文件 | 内容 |
|---|---|
| `data/htlb.json` | 全量：`meta` / `sections` / `items` |
| `data/stats.json` | 统计与校验数字 |
| `data/schema.json` | 字段说明 |

每条条目的关键字段：`id`（节-条）、`section_title`、`title`、`plain`（说人话）、`benefit_text`（收益与证据）、`ratio`（性价比档）、`evidence`（A/B/C）、`cost_money/cost_time/cost_willpower`、`sources`、`note`。

一行搜索示例（Python）：

```bash
curl -s https://666ghj.github.io/htlb-api/data/htlb.json | python -c "
import json,sys
db=json.load(sys.stdin)
for it in db['items']:
    t=it['title']+it.get('plain','')
    if '低钠盐' in t: print(it['id'], it['title'], it['evidence'])
"
```

## 自动同步

`.github/workflows/sync-dataset.yml` 每天 02:30 UTC（北京 10:30）自动从 htlb-dataset 拉取最新数据并提交；上游更新 → 本页自动跟进。

## 许可

- 正文数据：CC BY 4.0（《高性价比人生指南》，eternity4719 及贡献者；解析自 [htlb-dataset](https://github.com/sin0317/htlb-dataset)）
- 本仓库代码（index.html、workflow）：MIT
- 书给的是通用口径，不替代医生、律师、会计。
