# Quantization Briefing - {{date_or_range}}

## 一句话结论

- 本周最值得注意的是：
- 建议优先点开的内容：
- 可以暂时跳过的内容：

## 1. 新模型与量化 Artifact

只写和量化、压缩、serving 或 runtime 有关的信息。每条控制在 2-4 行。

### {{model_or_artifact_name}}

- 更新：
- 量化信号：INT8 / INT4 / FP8 / FP4 / MXFP4 / NVFP4 / KV cache / GGUF / GPTQ / AWQ / 其他
- 模型卡 / 技术博客 / checkpoint：
- 开源状况：open weights / quantized checkpoint / API only / 未公开
- 判断：`inspect` / `track-code` / `watch` / `ignore`

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
- 作用对象：weight / activation / KV cache / optimizer / multimodal / kernel / serving
- 数据格式/压缩率：
- 证据：accuracy / perplexity / latency / memory / benchmark / code / 未充分
- 建议动作：`inspect` / `replicate` / `skim` / `watch`

## 4. 高优先级开源项目

关注可运行、可复现、有 checkpoint、kernel、runtime 集成或 benchmark 的项目。

### {{project_name}}

- 链接：
- 做什么：
- 亮点：
- 工程落地：checkpoint / kernel / runtime integration / benchmark / prototype
- 建议动作：`track-code` / `inspect` / `replicate` / `watch`

## 5. 高价值技术博客 / 工程文章

只放有技术细节、benchmark、release note、实现路径或部署经验的博客/工程文章。过滤纯营销发布。

### {{blog_or_article_title}}

- 链接：
- 来源：
- 核心内容：
- 量化相关信号：format / recipe / calibration / runtime / kernel / benchmark / deployment / model artifact
- 为什么值得读：
- 建议动作：`inspect` / `skim` / `update-map` / `watch`

## 6. 重要仓库 PR / Release 趋势

关注 `config/tracked-repos.yml` 中和本频道相关的仓库，以及量化相关项目的新 PR、release 和近期 activity。这里写趋势，不堆 commit 列表。

### {{repo_or_framework}}

- 本周变化：
- 量化相关信号：new model support / low-bit kernel / KV cache / FP8 / FP4 / GGUF / runtime compatibility
- 影响：
- 建议动作：`track-code` / `watch`

## 7. Near Miss / 暂不展开

- {{item}}：为什么暂不展开

## 运行元信息

- 时间范围：
- 来源范围：
- 频道：`quantization`
- 读取：profile + watchlist + sources + rubric
- 是否读取 tracked-repos：否 / 是，原因：
- 是否读取 experts：否 / 是，原因：
- 是否读取 venues：否 / 是，原因：
- 是否展开 full topics：否 / 是，原因：
- 是否展开 research map：否 / 是，原因：
