# Research Radar

这是一个给 Codex 使用的研究雷达 skill，用来按固定知识源、主题配置和评估标准发现新论文、新项目和高价值技术资料。

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
│   ├── channels/
│   │   ├── quantization/topics.yml
│   │   └── ai-infra/topics.yml
│   ├── topics.yml              # legacy quantization entry
│   ├── sources.yml
│   └── radar-rubric.yml
├── templates/
│   └── radar-result.md
├── references/
│   ├── channels/
│   │   ├── quantization-map.md
│   │   └── ai-infra-map.md
│   ├── research-map.md         # legacy quantization entry
│   └── prompt-style.md
├── outputs/
│   ├── quantization/
│   ├── ai-infra/
│   └── radar/                  # legacy output directory
└── agents/
    └── openai.yaml
```

- `SKILL.md`：Codex skill 入口，负责触发和选择 `radar` 工作流。
- `workflows/`：核心 radar 工作流说明。
- `config/`：频道配置、固定研究范围、信息来源和 radar 初筛标准。
- `templates/`：雷达结果模板。
- `references/`：频道研究地图和输出风格约束。
- `outputs/`：按频道保存实际运行后的 radar 结果。
- `agents/`：Codex UI 元数据。

## 资源消费关系

```text
channels.yml
  └─ 决定本轮 radar 使用哪个频道、主题配置、研究地图和输出目录

sources.yml
  └─ 决定 radar 去哪里搜，包括 arXiv、GitHub、Hugging Face Hub、RSS 等来源

config/channels/<channel>/topics.yml
  └─ 被 radar 消费，用于对应频道的搜索召回、主题过滤和排除误召回

radar-rubric.yml
  └─ 被 radar 消费，用于对通过主题过滤的候选做初筛排序和动作建议

references/channels/<channel>-map.md
  └─ 被 radar 消费，用于给候选打标签、描述技术方向、应用场景、成熟度和系统视角
```

简短理解：

- `channels.yml` 是路由表，决定本轮使用哪个频道。
- `config/channels/<channel>/topics.yml` 是入口过滤器，决定什么能被搜到和留下。
- `references/channels/<channel>-map.md` 是分类解释器，决定留下来的内容怎么被理解和描述。

## 状态

当前是 v0.3 radar-only multi-channel baseline。后续应该通过真实运行 `quantization` 和 `ai-infra` 两个频道的 radar 来迭代关键词、评分标准和输出模板。
