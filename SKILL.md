---
name: research-radar
description: AI research radar assistant. 用于按固定频道搜索和筛选近期有价值的 LLM quantization、AI infra、serving/runtime、training systems、MoE、communication、kernel/operator、hardware affinity 和 performance analysis 相关论文、项目、博客或 artifact。
---

# Research Radar

## 概览

使用这个 skill 执行固定频道的研究雷达工作流：

- `radar`：从固定配置的主题和来源中，发现并筛选有价值的论文/项目/博客/artifact。

当前频道来自 [config/channels.yml](config/channels.yml)：

- `quantization`：LLM quantization、低 bit 推理/训练、多模态/全模态模型量化、模型压缩、serving 优化和系统/runtime 工作。不要把这里的“量化”理解成金融量化。
- `ai-infra`：LLM infrastructure、serving/runtime、training systems、MoE、通信并行、kernel/operator、硬件亲和和端到端性能分析。

## 工作流选择

- 当用户要求搜索、扫描、监控、推送、发现或总结近期有价值的论文/项目/博客/artifact 时，使用 [workflows/radar.md](workflows/radar.md)。
- 如果用户没有显式指定频道，但提到量化、低 bit、KV cache compression、FP4/FP8、multimodal quantization，默认使用 `quantization`。
- 如果用户没有显式指定频道，但提到 serving、vLLM、SGLang、推理系统、训练系统、MoE、通信、kernel、硬件或性能分析，默认使用 `ai-infra`。

## 共享规则

- 频道路由来自 [config/channels.yml](config/channels.yml)。
- 固定主题来自 `config/channels/<channel>/topics.yml`。兼容旧量化入口：[config/topics.yml](config/topics.yml)。除非用户明确要求临时覆盖，不要再向用户索要额外关键词。
- 来源配置来自 [config/sources.yml](config/sources.yml)。
- radar 初筛使用 [config/radar-rubric.yml](config/radar-rubric.yml)。
- 标签、技术方向、应用场景和成熟度阶段参考 `references/channels/<channel>-map.md`。兼容旧量化入口：[references/research-map.md](references/research-map.md)。
- 消费关系：频道 topics 用于 radar 搜索召回和主题过滤；频道 research map 用于 radar 候选打标签、分类、场景、成熟度和算子/系统视角分析。
- 输出风格遵循 [references/prompt-style.md](references/prompt-style.md)：简洁、判断明确、证据优先。
- 优先保证有用和高信号，不强行凑固定数量；如果高价值候选很少，就少列或说明本轮没有强候选。

## 输出约定

如果需要保存文件，写入：

- `outputs/<channel>/radar/`：保存 radar 报告。

如果用户没有要求保存文件，就在对话中按对应模板输出：

- [templates/radar-result.md](templates/radar-result.md)
