# AI Infra Briefing - {{date_or_range}}

## 一句话结论

- 本周最值得注意的是：
- 建议优先点开的内容：
- 可以暂时跳过的内容：

## 1. 新模型与 Agent 产品

只写有技术信息增量的发布或更新。每条控制在 2-4 行。

### {{model_or_agent_name}}

- 更新：
- 技术信号：架构 / context / serving / tool-use / coding workflow / benchmark / API 行为
- 技术博客或文档：
- 开源状况：open weights / model card / API only / repo / 未公开
- 判断：`inspect` / `watch` / `ignore`

## 2. 新论文趋势

按方向写趋势，不逐篇长摘要。只保留 1-3 个真的有信号的方向。

### {{trend_area}}

- 本周信号：
- 代表论文：
- 为什么值得看：
- 不确定性：

## 3. 高优先级论文

只放值得继续精读的论文。每篇控制在 3-5 行。

### {{paper_title}}

- 链接：
- 主要内容：
- 系统层级：serving / runtime / training / MoE / communication / kernel / agent workflow
- 证据：benchmark / artifact / code / strong abstract / 未充分
- 建议动作：`inspect` / `replicate` / `skim` / `watch`

## 4. 高价值技术报告 / 架构报告 / 工程文章

只放有实质技术细节的官方技术报告、架构 deep dive、系统设计文章、benchmark 报告或工程博客。过滤纯发布稿和营销文章。

### {{report_or_article_title}}

- 链接：
- 来源：官方技术报告 / 架构报告 / 工程博客 / benchmark 报告 / 白皮书
- 核心内容：
- 系统层级：hardware platform / serving / runtime / training / MoE / communication / kernel / model architecture / agent workflow
- infra 影响：latency / throughput / memory / scaling / MFU / KV cache / interconnect / kernel path / deployment
- 证据：architecture detail / benchmark / implementation detail / official note / 未充分
- 建议动作：`inspect` / `skim` / `update-map` / `watch`

## 5. 高优先级开源项目

关注能运行、能复现、能接到 runtime 或有明确 benchmark 的项目。

### {{project_name}}

- 链接：
- 做什么：
- 亮点：
- 成熟度：prototype / active repo / release / production signal
- 建议动作：`track-code` / `inspect` / `replicate` / `watch`

## 6. 重要仓库 PR / Release 趋势

关注 `config/tracked-repos.yml` 中和本频道相关的仓库，以及 AI infra 相关项目的新 PR、release 和近期 activity。这里写趋势，不堆 commit 列表。

### {{repo_or_framework}}

- 本周变化：
- 趋势判断：模型支持 / serving / batching / KV cache / MoE / quantization / kernel / breaking change
- 影响：
- 建议动作：`track-code` / `watch`

## 7. Near Miss / 暂不展开

- {{item}}：为什么暂不展开

## 运行元信息

- 时间范围：
- 来源范围：
- 频道：`ai-infra`
- 读取：profile + watchlist + sources + rubric
- Hardware smoke-check：已执行 / 未执行；关键词：
- Hardware smoke-check 命中：是 / 否；是否展开 `hardware_platform_reports`：是 / 否；保留 / 过滤候选：
- 是否读取 tracked-repos：否 / 是，原因：
- 是否读取 experts：否 / 是，原因：
- 是否读取 venues：否 / 是，原因：
- 是否展开 full topics：否 / 是，原因：
- 是否展开 research map：否 / 是，原因：
