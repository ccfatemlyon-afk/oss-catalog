# 起点雷达 · 开源底库（486 条）

做产品方向之前先看这里：**这个想法有没有现成底座能改**。

486 个开源项目，带星数、语言、最后推送时间，并按**读者视角的场景**归类（语音、RAG、
爬虫、自托管、支付、监控…）。数据每天从 [起点雷达 oss 站](https://qidian-radar.pages.dev/oss/)
自动同步，口径与站点完全一致。

- 想筛着看：<https://qidian-radar.pages.dev/oss/>（场景多选 + 星数/语言/搜索叠加）
- 想直接拿数据：本仓库的 `catalog.csv` / `catalog.json`

## 文件

| 文件 | 说明 |
|---|---|
| `catalog.csv` | UTF-8 BOM，Excel 直接打开不乱码；按星数降序；`scenes` 列用 ` 竖线 ` 连接多个中文场景名 |
| `catalog.json` | 同字段的结构化版：`{generated_at, enriched_at, count, items[]}` |
| `README.md` | 本文件 |

## 字段

| 字段 | 含义 |
|---|---|
| `name` | `owner/repo` |
| `url` | 仓库地址 |
| `desc` | 中文一句话简介（上游合集提供，非本仓库撰写） |
| `stars` | GitHub stargazers 数（采集当日值） |
| `lang` | 主语言 |
| `tags` | 上游合集目录名（AI开源项目 / 开源工具 / 实战项目 / 学习资源 / 好玩项目 / 大厂开源 / 信息获取） |
| `scenes` | **读者视角场景**（见下），可多标签，规则匹配、非人工策展 |
| `archived` | 仓库是否已归档（站点默认隐藏） |
| `pushed` | 最后推送时间 |
| `forks` / `license` / `topics` | GitHub 元数据 |
| `error` | 采集异常（如仓库改名/删除）时的说明，空串为正常 |

### 场景 key

`agent` Agent 与自动化 · `rag` RAG 与知识库 · `voice` 语音/ASR-TTS ·
`vision` 图像与视频生成 · `devtool` 开发工具与代码 · `scrape` 爬虫与信息采集 ·
`selfhost` 自托管与私有部署 · `notes` 笔记/文档/写作 · `llm` 大模型与对话 ·
`commerce` 电商/支付/订阅 · `ops` 监控/日志/运维 · `i18n` 翻译与本地化 ·
`privacy` 隐私/安全/账号 · `notify` 邮件与通知 · `dashboard` 数据看板与可视化 ·
`fun` 娱乐与生活小工具 · `other` 未命中（约 9.7%）

> **场景只帮助检索，不代表质量或可抄性。** 同一个场景里既有 3 万星的成熟项目，
> 也有 90 星的新项目；`awesome-*` 这类清单型仓库是资料，不是可抄的产品底座——
> 请自己看 `desc` 与 `stars` 判断。

## 怎么用

- **找可抄的底座**：先按场景筛，再看 1k–10k 星那档（有真实用户但还没定型）。
- **Excel**：直接打开 `catalog.csv`。
- **脚本**：

```python
import json
items = json.load(open("catalog.json", encoding="utf-8"))["items"]
scrape = [x for x in items if "scrape" in x["scenes"] and 1000 <= x["stars"] <= 50000]
print(len(scrape), scrape[0]["name"])
```

## 更新方式

- **每天自动**：GitHub Actions 定时（见 `.github/workflows/sync.yml`）从站点拉取最新
  `catalog.json` / `catalog.csv`，有变化才提交；也可以手动在 Actions 页面点
  `Run workflow`。
- **数据源头**：起点雷达每天扫描海外开发者社区与 GitHub 元数据；本仓库只是站点数据的一份
  镜像，字段口径以站点为准。
- 提交历史即快照：想看某天的星数，`git log -- catalog.csv` 翻即可。

## 边界

- **不含**：日报正文、读者邮箱、任何账号凭据。本仓库只有公开的 GitHub 元数据与场景标签。
- 星数会随时间变（甚至掉），它是当日快照，不是"永久知名度"。
- `desc` 来自上游中文合集，个别条目描述与仓库现状可能不完全一致，转载时请保留 `url` 供核对。

## 许可

数据为 GitHub 公开元数据的聚合结果，按 **CC BY 4.0** 提供，使用时请注明来源
「起点雷达 · 开源底库」（<https://qidian-radar.pages.dev/oss/>）。仓库中每个项目的
代码版权归各自作者，本仓库不重新分发其源码。
