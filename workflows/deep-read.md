# Deep-Read 工作流

## 目的

对一篇选中的论文、项目或报告做深度技术评审，重点判断技术新颖性、系统落地性、实验质量、模型覆盖，以及对 infra/kernel/runtime 从业者的价值。

## 输入

接受以下任意输入：

- arXiv 链接
- PDF 链接或本地 PDF 路径
- 论文标题和足够上下文
- 与论文相关的 GitHub 仓库
- radar 里选中的候选
- `channel`：`quantization` 或 `ai-infra`。如果用户没有显式指定，按内容自动推断。

## 执行步骤

1. 确认论文/项目、作者、作者单位/机构、日期、来源、开源仓/项目地址和版本。
2. 阅读摘要、方法、实验、局限性和关联代码仓库。
3. 如果执行环境支持 PDF/图片视觉理解，检查论文中的关键图表、架构图、算法流程图、实验图和表格；如果不支持，明确说明“未做图表视觉分析”，并尽量根据正文和 caption 分析。
4. 读取 `config/channels.yml`，确定本轮 `channel`。
5. 使用频道 research map 分类；兼容旧量化入口 `references/research-map.md`。
6. 使用 `config/deep-read-rubric.yml` 评分。
7. 按 `templates/deep-read-report.md` 输出报告。
8. 在报告中嵌入一份符合 `templates/paper-scorecard.md` 的简洁评分卡。

## 必须回答的问题

按最终报告结构组织思考，不要把问题散列成无序 checklist。

### 快速结论与元信息

- 作者、作者单位/机构、日期/版本、论文链接、开源仓/项目地址和来源是什么？
- 这篇论文的价值侧重是什么：复现实验、看代码/kernel、算子启发、实验参考、概念参考，还是等待后续？
- 一句话判断和最值得做的下一步是什么？

### 问题定义与全局定位

- 论文解决了什么量化、压缩、推理系统、训练系统、kernel/runtime 或 AI infra 问题？
- 面向 AI infra 从业者，这项工作在 LLM 推理/训练/serving/runtime/kernel/压缩版图中处在什么位置？
- 它主要优化哪条链路：模型权重、激活、KV cache、optimizer state、kernel、runtime 调度、serving 系统、训练系统、通信并行、硬件执行，还是端到端部署？
- 它和已有方向的关系是什么：补齐工程缺口、改进已有量化范式、提出新算法，还是提供 benchmark/系统经验？
- 适用场景是什么：推理、训练、finetuning、serving、长上下文、KV cache 压缩、optimizer state 压缩、边缘部署、MoE、多模态推理、视频/语音语言模型、DiT/扩散生成或全模态模型？

### 方法与新颖性

- 方法或算法的新颖性在哪里？
- 属于哪类量化或压缩方向：PTQ、QAT、optimizer quantization、weight-only、weight-activation、KV cache quantization、KV cache non-quant compression、FP8、INT8、INT4、FP4/MXFP4/NVFP4、1-bit/2-bit、balanced/outlier-aware quantization、rotation/transform-based、mixed precision、sparse/low-rank、multimodal quantization、visual token compression、DiT quantization、serving-aware quantization，或其他类别？
- 如果涉及 KV cache 压缩，它是量化类、稀疏/剪枝类、驱逐/保留策略、合并/聚合类、低秩/投影类，还是混合方案？对长上下文精度、显存、latency 和 serving 复杂度有什么影响？
- 如果涉及 optimizer quantization，它量化的是 optimizer states、gradient、momentum/variance、Adam 状态，还是通信/同步过程？对训练稳定性、收敛、显存和通信有什么影响？
- 如果涉及多模态量化，它量化或压缩的是语言 backbone、vision/audio/video encoder、modality projector、cross-modal attention、visual tokens、多模态 KV cache、diffusion/DiT block，还是端到端 pipeline？校准数据和评测任务是否覆盖目标模态？
- 这是离线量化、在线量化还是混合方案？量化时机对 latency、吞吐、显存、calibration、packing 和 serving 集成有什么影响？
- 和该方向经典论文、近期论文相比，它继承了什么、改进了什么、没有解决什么？作者自称的优势哪些被证据支持，哪些可能夸大？
- 如果算法有创新或晦涩，必须按“物理/几何/数学直觉 -> 小白例子 -> 图解 -> 必要公式/推导”的顺序解释；不要一上来堆公式。

### 关键图表

- 论文里的关键图、架构图、算法流程图、实验图或表格传达了什么信息？
- 有没有正文不明显但图里很有启发的结构、趋势或 trade-off？
- 如果不能访问图片，是否明确说明限制，并基于 caption、正文和表格文本替代分析？

### 工程、Runtime 与算子视角

- 工程落地成熟度如何？
- 是否支持或容易接入 vLLM、SGLang、TensorRT-LLM、llama.cpp、Triton kernel、CUDA kernel 或自定义 runtime？
- 是否需要新算子、新 kernel、新 packing layout、新 calibration 流程、runtime 调度、计算图改动或内存管理改动？
- 对算子/kernel/runtime 从业者意味着什么？

### 实验、模型覆盖与实际价值

- 实验是否 solid：baseline、ablation、指标、任务、模型规模、模型家族和结论支撑是否足够？
- 覆盖了哪些模型类型：大模型、中模型、小模型、纯文本模型、多模态模型、视觉语言模型、视频语言模型、语音/音频语言模型、扩散/DiT 生成模型、全模态模型、MoE 模型？
- 是否值得继续投入？主要风险和下一步具体应该做什么？

## 算子从业者视角

必须单独包含这一节。覆盖：

- kernel 优化机会
- 算子融合机会
- packing/layout 影响
- 访存带宽和 cache 行为
- latency/throughput 权衡
- 硬件兼容性挑战
- benchmark 设计启发
- 可能的集成痛点

## 实验质量视角

如果论文缺少有意义的 baseline、ablation、模型覆盖、真实 workload 或可复现证据，要明确指出。不要让结论强于实验本身。

## 图表分析视角

如果能访问论文图片，必须重点检查：

- 方法/系统架构图：看量化流程、runtime 位置、offline/online 边界和数据流。
- 算法流程图：看 calibration、rotation、packing、dequantization、optimizer state 处理等关键步骤。
- 实验曲线和表格：看精度、PPL、latency、throughput、memory、compression ratio 的 trade-off。
- 消融图表：看论文核心 claim 是否真的被图表支撑。

如果不能访问图片，必须在报告中说明限制，并基于 caption、正文描述和表格文本做替代分析。

## 必需输出

使用 `templates/deep-read-report.md`。最后必须明确这篇论文的价值侧重，例如复现实验、看代码/kernel、算子启发、实验参考、概念参考或等待后续。
