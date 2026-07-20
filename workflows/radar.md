# Radar 工作流

## 目的

从固定频道的研究范围内发现有价值的论文、项目、模型发布、框架 release、博客、benchmark 和 artifact，输出精选候选清单。不要为了数量填充低价值条目。

## 输入

只需要：

- `channel`：`quantization` 或 `ai-infra`。如果用户没有显式指定，按 `SKILL.md` 的默认频道规则推断。
- `time_range`：今天、本周、过去 30 天，或明确日期范围。
- `source_scope`：全部来源、只查 arXiv、只查 GitHub、只查 Hugging Face、只查 RSS、只查 model releases、只查 framework releases，或 `config/sources.yml` 中定义的来源组。

默认不要要求用户提供临时关键词。常规 radar 只读取 `config/channels/<channel>/profile.yml`。当 source scope 是 `model_releases` / `framework_releases`、用户询问具体模型/机构、或候选命中重点实体时，读取 `config/watchlist.yml`。只有在专项扫描、召回不足、分类不确定或用户要求完整覆盖时，才展开读取 `topics.full.yml` 和频道 research map。

## 领域限定与软过滤

当用户使用“专项”“只看”“聚焦”“某个方向”“某个领域”“围绕某类”等表达时，把它理解为本轮 radar 的领域限定，而不是新的自由关键词系统。

处理方式：

- 先把用户表达映射到本频道 profile 中最接近的核心方向；如果 profile 不够判断，再展开 `topics.full.yml` 和频道 research map。例如 `quantization` 频道可映射到 KV cache、optimizer quantization、balanced/outlier-aware quantization、FP4/MXFP4/NVFP4、多模态量化、visual token compression、kernel/runtime、rotation/transform、long-context mechanisms for compression；`ai-infra` 频道可映射到 serving/runtime、speculative decoding、MoE systems、training systems、communication、kernel/operator、architecture infra impact、performance analysis。
- 搜索和筛选时优先保留该子类的核心候选；明显不属于该子类、且无法解释关系的条目应过滤掉。
- 允许保留相邻候选，但必须满足至少一个条件：提供该子类的 baseline、benchmark、runtime 依赖、kernel/artifact 路径、上游/下游方法，或能解释该方向的技术趋势。
- 对相邻候选必须在候选表或详情中标注“关联原因”，例如“作为 KV cache 压缩 baseline”“提供 FP4 runtime artifact”“与 outlier balancing 共享 activation scaling 思路”。
- 不要因为用户说“只看某方向”就机械丢弃所有交叉工作。量化与 infra 常有交叉：例如 balanced/outlier-aware 与 rotation/transform 交叉，KV cache 压缩与 serving/runtime 交叉，optimizer quantization 与 training/finetuning 交叉，MoE 与通信/算子/runtime 交叉。
- 如果相邻候选太多，最多保留少量高证据条目，并把其余方向写入“暂不展开的子类及原因”。

如果用户的领域限定无法通过 profile 映射到现有子类，再用 `topics.full.yml` 的同义词和频道研究地图做近似归类；仍不确定时，在输出中明确说明本轮采用的解释口径。

## 专项洞察限制

专项洞察默认不写。只有满足下面条件之一，才允许在本轮 radar 中展开：

- 同一子类下出现至少 2 个有价值候选，且它们共享明确技术主题、系统问题、数据格式、runtime 路径或实验趋势。
- 同一子类下只有 1 个候选，但它同时具备强证据：清晰论文/项目/模型发布/release note、明确 benchmark 或 artifact、明显工程落地信号，并且和频道 profile 或 research map 中的重要方向直接相关。
- 用户明确要求对某个子类做专项观察。

禁止写专项洞察的情况：

- 只有 1 个弱候选或 near-miss。
- 只是关键词相同，但问题、方法、场景或落地路径没有可比较关系。
- 只能从标题猜测，没有摘要、README、benchmark、代码或其他证据支持。
- 需要阅读全文才能判断，但本轮 radar 只看到了标题/摘要/项目简介。

专项洞察最多展开 1-3 个子类。每个专项洞察必须说明触发依据、代表工作、共同点、分歧或不确定性、置信度和下一步动作。它不能写成单篇论文摘要。

## 执行步骤

1. 读取 `config/channels.yml`，确定本轮 `channel`。
2. 读取该频道的 `profile.yml`、`config/sources.yml` 和 `config/radar-rubric.yml`。
3. 当 source scope 是 `model_releases` / `framework_releases`、用户询问具体模型/机构、或候选命中重点实体时，读取 `config/watchlist.yml`。
4. 默认不要读取 `topics.full.yml` 和频道 research map；只有在专项扫描、召回不足、分类不确定、需要专项洞察或用户明确要求完整覆盖时才展开读取。
5. 在指定时间范围和来源范围内搜索。
6. 如果用户给出领域限定，先按“领域限定与软过滤”确定本轮核心子类和允许保留的相邻子类。
7. 先用频道 profile、必要时结合 watchlist 和 `config/radar-rubric.yml` 的 `prefilter_gates` 做主题过滤；未通过过滤的条目直接丢弃或标记为 `ignore`。
8. 对领域限定场景，再用软过滤判断条目是核心候选、相邻候选还是应过滤条目；相邻候选必须能解释其关系。
9. 将通过过滤的结果整理成 Discover Card：
   - 标题
   - 链接
   - 来源
   - 发布或更新时间
   - 类型：论文、代码、博客、benchmark、数据集、报告、model release 或 framework release
   - 子类：默认使用频道 profile 中的核心方向；展开时可使用 full topics / research map 中的子类
   - 如果本轮有领域限定，说明是否属于核心候选或相邻候选；相邻候选必须写关联原因
   - 命中的研究主题
   - 数据格式/压缩率：例如 INT8、INT4、FP8、FP4、MXFP4、NVFP4、2-bit、1-bit、KV cache 压缩率；未知时写“未说明”
   - 核心技术：用一句话概括方法、系统机制或工程实现
   - kernel/artifact 落地状态：是否有代码、kernel、runtime 集成、benchmark、artifact 或复现实验
   - 证据
   - 初筛信号摘要
   - 建议动作
10. 丢弃明显过时、浅层或只有营销信息的低信号条目。
11. 对 `quantization` 频道的 `long_context_mechanisms_for_compression` 这类相邻机制/挑战标签，只有在候选明确连接到量化、KV cache 压缩、serving、activation outlier、memory 或 inference efficiency 时才保留；否则过滤或标为 `ignore`。
12. 对 `quantization` 频道的 `multimodal_quantization` 这类多模态标签，优先保留明确涉及 VLM/MLLM/LVLM、视觉/视频/语音 encoder、modality projector、cross-modal attention、visual tokens、多模态 KV cache、DiT/diffusion transformer、serving/runtime 或 kernel 的候选；纯图像压缩、传统视频 codec 或和 LLM/transformer 推理无关的图像量化应过滤。
13. 对综述/benchmark/taxonomy，只在它明确聚焦本频道核心范围时保留；主要建议动作为 `skim`、`inspect` 或 `update-map`。
14. 对模型发布和框架 release，结合 watchlist 判断是否属于重点实体；只有当它包含模型版本、架构、context length、runtime 支持、量化 artifact、benchmark、kernel 或兼容性信息时才保留。
15. 先按子类聚合候选，并按“专项洞察限制”判断是否有子类达到专项洞察门槛。
16. 在子类内按初筛评分排序，不按固定 Top N 凑数。
17. 在输出开头给出“本轮方向摘要”：哪些子类强、哪些子类弱、哪些子类达到专项洞察门槛、哪些子类暂不展开以及原因。
18. 输出候选总览表，便于快速比较不同方向的时间、工作、类型、数据格式/压缩率、核心技术、意义和落地状态。
19. 只有当“本轮方向摘要”已经点名某个子类达到门槛时，才补充“专项洞察”。专项洞察要总结方向级信号、共同点、分歧和下一步，而不是重复单条候选。
20. 如果某个子类本轮信号明显，可以补充专项洞察；证据不足时必须写入“暂不展开的子类及原因”。
21. 如果用户已有历史表格或明确要求维护历史记录，可以追加“历史表格”；第一版默认只预留，不强制维护。
22. 如果没有高价值结果，直接说明；只有在有帮助时才列出少量 near-miss。

## 来源说明

- arXiv：重点看标题、摘要、日期、类别、作者，以及是否有代码。
- GitHub：优先关注论文关联仓库、kernel/runtime 集成、活跃维护、stars、近期提交和 benchmark 证据。
- GitHub Releases：优先关注 vLLM、SGLang、TensorRT-LLM、transformers、llama.cpp、FlashInfer、Triton 等项目的模型支持、serving、量化、kernel 和 breaking changes。
- Hugging Face：按频道过滤模型卡、paper/project 关联、artifact、benchmark、推理示例和 runtime 使用说明。不要扩展成泛模型能力新闻监控；只保留和本频道目标相关的条目。
- Model hubs：关注新模型版本、模型卡、context length、架构、license、quantized checkpoint、GGUF/safetensors、runtime 兼容和 benchmark。
- Vendor blogs：关注官方模型发布、技术博客和框架公告；过滤只有营销表述、没有技术细节的普通新闻。
- RSS：实验室、公司、博客和工程团队文章只有在有明确技术细节，或指向论文/代码时才保留。

## 候选动作

使用以下动作之一：

- `ignore`：相关性或证据不足。
- `skim`：可能有用，但证据较弱。
- `inspect`：值得后续人工检查、代码检查或单独技术分析的强候选。
- `track-code`：主要价值在实现、runtime 集成或代码。
- `watch`：有潜力但还不成熟，等待代码、实验或后续版本。
- `update-map`：主要价值在更新研究地图、关键词、benchmark 视角或评分标准，常用于综述、taxonomy、benchmark 或 position paper。

## 必需输出

使用 `templates/radar-result.md`。必须包含：

- 搜索时间范围和来源范围
- 本轮频道、读取的 profile、是否展开 full topics / research map、来自配置的主题/查询依据
- 如用户给出“专项/只看某方向”等领域限定，说明本轮核心子类、软过滤口径和相邻候选保留规则
- 本轮方向摘要：强信号子类、弱信号子类、达到专项洞察门槛的子类、暂不展开的子类及原因
- 按子类分组的候选总览表
- 只列有价值候选
- 每个候选为什么重要
- 数据格式/压缩率、核心技术、kernel/artifact 落地状态
- 初筛信号摘要
- 下一步建议动作
- 只有满足“专项洞察限制”时才补充专项洞察；否则明确写“本轮无专项洞察”
- 必要时补充历史表格预留

不要写死 “Top N”。可以使用“高价值候选”“值得观察”“本轮无强候选”等标题。
