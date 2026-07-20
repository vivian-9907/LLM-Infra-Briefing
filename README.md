# Research Radar

这是一个给 Codex 使用的轻量研究雷达 skill，用来按固定知识源、频道 profile、重点 watchlist 和评分标准发现新论文、新项目、模型发布、agent 产品更新、框架 release 和高价值技术资料。

当前支持两个频道：

- `quantization`：LLM quantization / low-bit / compression / inference optimization，包括低 bit 量化、模型压缩、多模态/全模态模型量化、serving/runtime 集成、算子/kernel 相关工作。这里不是金融量化研究。
- `ai-infra`：LLM infrastructure，包括 serving/runtime、训练系统、MoE、通信并行、kernel/operator、硬件亲和和端到端性能分析。

## 工作流

- `radar <channel>`：在指定频道的固定研究范围内，按时间和来源搜索论文/项目/博客/artifact，只输出真正有价值的候选。

## 项目目录

```text
.
├── SKILL.md
├── workflows/
│   └── radar.md
├── config/
│   ├── channels.yml
│   ├── watchlist.yml
│   ├── channels/
│   │   ├── quantization/
│   │   │   ├── profile.yml
│   │   │   └── topics.full.yml
│   │   └── ai-infra/
│   │       ├── profile.yml
│   │       └── topics.full.yml
│   ├── sources.yml
│   └── radar-rubric.yml
├── templates/
│   ├── radar-result.md
│   ├── radar-result-quantization.md
│   └── radar-result-ai-infra.md
├── references/
│   ├── channels/
│   │   ├── quantization-map.md
│   │   └── ai-infra-map.md
│   └── prompt-style.md
├── outputs/
│   ├── quantization/
│   └── ai-infra/
└── agents/
    └── openai.yaml
```

- `SKILL.md`：Codex skill 入口，负责触发和选择 `radar` 工作流。
- `workflows/`：核心 radar 工作流说明。
- `config/`：频道配置、固定研究范围、信息来源和 radar 初筛标准。
- `templates/`：雷达结果模板；量化和 infra 有各自的频道模板，通用模板作为 fallback。
- `references/`：频道研究地图和输出风格约束。
- `outputs/`：按频道保存实际运行后的 radar 结果。
- `agents/`：Codex UI 元数据。

## 资源消费关系

```text
channels.yml
  └─ 决定本轮 radar 使用哪个频道、轻量 profile、完整 topics、研究地图、结果模板和输出目录

sources.yml
  └─ 决定 radar 去哪里搜，包括 arXiv、GitHub、GitHub Releases、Hugging Face、模型发布页、RSS 和厂商博客

watchlist.yml
  └─ 常规 radar 每次读取；维护“重点盯谁”，包括模型、agent 产品、机构和框架，不是 source 列表

config/channels/<channel>/profile.yml
  └─ 默认读取的轻量频道画像，用于常规搜索召回、主题过滤和噪音过滤

config/channels/<channel>/topics.full.yml
  └─ 只在专项扫描、召回不足或分类不确定时读取，用于展开完整关键词和同义词

radar-rubric.yml
  └─ 被 radar 消费，用于对通过主题过滤的候选做初筛排序和动作建议

references/channels/<channel>-map.md
  └─ 只在需要解释方向、写专项洞察或分类不确定时读取

templates/radar-result-<channel>.md
  └─ 决定本频道最终报告形态；量化强调数据格式/压缩率/精度/落地，infra 强调系统层级/性能/扩展性/runtime
```

简短理解：

- `channels.yml` 是路由表，决定本轮使用哪个频道。
- `config/channels/<channel>/profile.yml` 是默认入口过滤器，短、轻、省 token。
- `config/watchlist.yml` 是重点实体表，用于 LongCat、MiMo、DeepSeek、Kimi、GPT/ChatGPT、Claude、Qwen、Codex、Claude Code、Kimi Code、Qwen Code、Cursor、vLLM、SGLang 等发布监控。
- `topics.full.yml` 和 `references/channels/<channel>-map.md` 是按需展开层，用来处理专项扫描或不确定分类。

## 状态

当前是 v0.5 lightweight radar-only multi-channel baseline。默认读取 profile 和 watchlist；需要时再展开完整 topics 和 research map。
