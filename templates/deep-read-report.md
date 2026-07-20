# 精读报告 - {{paper_title}}

## 快速结论与元信息

- 作者：
- 作者单位/机构：
- 日期/版本：
- 论文链接：
- 开源仓/项目地址：
- 来源：
- 频道：`quantization` / `ai-infra`
- 使用的研究地图：`references/channels/{{channel}}-map.md`
- 价值侧重：`reproduce_experiment` / `inspect_code_or_kernel` / `operator_insight` / `experiment_reference` / `conceptual_reference` / `monitor_followup`
- 一句话判断：
- 最值得做的下一步：

## 维度画像与分析重点

使用 `config/deep-read-rubric.yml` 和 `templates/paper-scorecard.md` 生成评分卡。

- 读者视角：评分卡用于展示这项工作的多维画像，让读者快速看到它强在哪里、弱在哪里。
- 分析分配：高分维度需要在正文中展开得更充分；低分维度需要在风险、薄弱点或后续验证中明确说明。
- 不机械求总分：分数用于分配分析重点和辅助判断，不替代基于证据的技术结论。

## 问题定义

这篇论文解决了什么问题？

- 面向 AI infra 从业者的全局定位：这项工作在 LLM/多模态模型推理、训练、serving、runtime、kernel、压缩版图里处在什么位置？
- 它主要优化哪条链路：模型权重、激活、KV cache、optimizer state、vision/audio/video encoder、modality projector、cross-modal attention、visual tokens、DiT/diffusion block、kernel、runtime 调度、serving 系统、训练系统、通信并行、硬件执行，还是端到端部署？
- 它和已有方向的关系：是补齐工程缺口、改进已有量化范式、提出新算法，还是提供 benchmark/系统经验？
- 适用场景：
  - 推理：
  - 训练：
  - Finetuning：
  - 优化器状态压缩：
  - Serving：
  - 长上下文：
  - KV cache 压缩：
  - 边缘部署：
  - MoE：
  - 多模态/全模态：

## 方法与新颖性

- 核心思路：
- 直觉解释：先用物理/几何/数学直觉解释这件事，不直接上公式。
- 小白例子：用一个小规模、可手算或可想象的例子说明算法在做什么。
- 图解：优先给简单示意图；不能画图时，用 ASCII/mermaid/步骤图表达。
- 抽象化/推导：在直觉和例子之后，再写必要公式或严格推导。
- 频道技术方向：
- 量化方向（仅 quantization 频道必填）：
- 量化时机：离线量化 / 在线量化 / 混合方案
- KV cache 压缩：量化 / 稀疏剪枝 / 驱逐保留 / 合并聚合 / 低秩投影 / 混合方案
- 优化器量化：是否涉及 optimizer states / gradient / momentum / variance / Adam 状态 / 通信压缩
- 多模态量化：是否涉及 language backbone / vision/audio/video encoder / modality projector / cross-modal attention / visual tokens / multimodal KV cache / DiT 或 diffusion block
- 新在哪里：
- 借用了什么已有思路：
- 和经典/近期工作的对比：
  - 相比经典方法：
  - 相比近期论文：
  - 作者自称的优势：
  - 客观看成立的优势：
  - 可能夸大的地方：
- 如果算法晦涩，必须先给直觉和例子，再给抽象说明：

## 关键图表分析

- 是否完成图表视觉分析：是 / 否
- 关键图表：
- 图里最有启发的信息：
- 图表揭示的 trade-off：
- 如果未能查看图片，说明限制并基于 caption/正文做替代分析：

## 工程与 Runtime 适配

- 工程成熟度：
- 离线/在线量化对工程路径的影响：
- vLLM 兼容性：
- SGLang 兼容性：
- TensorRT-LLM 兼容性：
- llama.cpp 兼容性：
- Triton/CUDA kernel 需求：
- Runtime 或调度改动：
- Packing/layout/calibration 改动：

## 对算子从业者的意义

- Kernel 优化机会：
- 算子融合机会：
- Packing/layout 影响：
- 访存带宽影响：
- Latency/throughput 权衡：
- 硬件兼容性挑战：
- Benchmark 设计启发：
- 集成痛点：

## 实验扎实程度

- Baseline：
- Ablation：
- 指标：
- Workload：
- 模型家族和规模：
- 文本/多模态/全模态覆盖：
- 多模态校准与评测覆盖：
- 结论是否被实验支撑：
- 薄弱点：

## 实际价值

- 预期实际价值：
- 可复现性：
- 主要风险：
- 建议下一步：
