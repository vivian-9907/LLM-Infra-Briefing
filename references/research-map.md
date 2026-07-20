# LLM 量化研究地图

用这份研究地图给 radar 候选和 deep-read 报告打标签。这里的“量化”指 LLM quantization，不是金融量化。

## 技术方向

- PTQ：post-training quantization，不重新训练或只做很轻的校准。
- QAT：训练或 finetuning 时引入量化感知，常见信号包括 fake quantization、STE、低 bit training。
- Optimizer quantization：量化 optimizer states、gradient、momentum/variance 或 Adam 状态，主要目标是降低训练/finetuning 的显存和通信开销。
- Weight-only quantization：压缩权重，激活通常保持较高精度。
- Weight-activation quantization：权重和激活都量化。
- KV cache quantization：降低 attention cache 的显存和带宽压力。
- KV cache non-quant compression：不依赖低 bit 表示，而通过稀疏、剪枝、驱逐、合并、低秩或 cache policy 降低长上下文 KV cache 成本。
- Rotation/transform-based quantization：通过 Hadamard、正交变换、旋转或 outlier smoothing 改善激活/权重分布，降低低 bit 量化难度。
- Balanced/outlier-aware quantization：通过缩放、迁移、平衡或抑制 outlier，让不同 channel/token 的数值范围更均匀。它常和 rotation/transform、SmoothQuant、AWQ、OmniQuant 类方法交叉，但 radar 里可以单独标记，便于观察“先改分布再量化”的方法族。
- FP8、INT8、INT4、FP4、MXFP4、NVFP4、NF4、1-bit、2-bit、mixed precision。
- Sparse、low-rank、pruning、distillation，前提是和 LLM 效率或量化强相关。
- Serving-aware quantization：围绕 runtime、batching、cache 或部署约束设计的量化方法。
- Multimodal quantization：面向 VLM、MLLM、LVLM、视频/语音语言模型、全模态模型和扩散/DiT 生成模型的量化与压缩。重点区分量化对象是语言 backbone、vision/audio/video encoder、modality projector、cross-modal attention、visual tokens、KV cache，还是 diffusion/DiT block。

## 量化挑战视角

这些标签用于 radar 判断“为什么这篇工作可能对量化有指导意义”。它们不是新的主技术方向；只有和 LLM 量化、KV cache 压缩、长上下文 serving、activation outlier、memory/inference efficiency 等目标有明确关系时才保留。

- 深层误差传播与 sink 机制：关注量化误差如何在深层 Transformer 中累积或放大，以及 attention sink、residual sink、residual stream 是否提示某些 token、通道或方向需要更谨慎地量化、裁剪、旋转或保留。
- 长尾分布与 outlier：关注 activation/weight/KV 的 heavy-tailed distribution、outlier channel、salient token/channel、massive activation，以及它们对 clipping、scaling、mixed precision、balanced quantization 的影响。
- 长上下文机制与位置影响：关注 RoPE、位置编码、attention sink、heavy hitter token、long-context behavior 对 KV cache 量化、非量化压缩、cache eviction 和 serving 稳定性的影响。

## 量化时机

- 离线量化：部署前完成 calibration、weight packing、scale/zero-point 计算或权重转换，推理时直接使用量化产物。
- 在线量化：推理、serving 或运行时动态决定/更新量化参数、cache 量化、激活量化或调度策略。
- 混合方案：权重离线量化，activation、KV cache 或部分 runtime 决策在线处理。
- 读论文时要判断量化时机对 latency、吞吐、显存、工程复杂度和 serving 集成的影响。

## KV Cache 压缩地图

- 量化类：对 key/value cache 使用 INT/FP/低 bit 表示，重点看精度损失、dequantization 开销和 runtime 集成。
- 稀疏/剪枝类：保留重要 token 或 attention pattern，丢弃低价值 cache，重点看选择策略和精度退化。
- 驱逐/保留策略：基于 recency、attention score、heavy hitter、attention sink 等规则管理 cache。
- 合并/聚合类：将相近 token/cache 表示合并，重点看信息损失和长上下文稳定性。
- 低秩/投影类：用低秩表示或投影压缩 KV，重点看重构误差、计算开销和硬件友好性。
- 读论文时要区分它是 KV 量化、非量化压缩，还是二者混合方案。

## 多模态量化地图

- VLM/MLLM 推理量化：常见对象包括语言 backbone、vision encoder、modality projector、cross-modal attention 和多模态 KV cache。读论文时要判断它是否只复用文本 LLM 量化，还是专门处理视觉 token、跨模态对齐和多模态 benchmark 退化。
- Visual token 压缩：通过 token pruning、merging、selection、resampler 或低秩表示减少图像/视频 token。它不一定是量化，但如果目标是多模态 LLM 推理显存、attention 成本、KV cache 或 serving 延迟，就应作为相邻候选保留。
- 视频/长序列多模态：视频 token 数量大，常和长上下文、KV cache、attention sparsity、token pruning、chunked prefill 和 serving 调度交叉。重点看质量保持、时序一致性和吞吐/显存 trade-off。
- 语音/音频多模态：关注 audio encoder、speech tokens、streaming ASR/LLM pipeline、低延迟和端侧部署。只有和 LLM/VLM/MLLM 推理或低 bit 压缩明确相关时保留。
- 生成式多模态和 DiT：包括 text-to-image、text-to-video、diffusion transformer、U-Net diffusion 的权重/激活/attention 量化。它和 LLM 量化相邻但不完全相同，只有涉及 transformer attention、LLM-conditioned generation、serving/runtime、低 bit kernel 或多模态生成部署时纳入。
- 全模态/omni-modal：关注多种模态共享 backbone 或统一 token space 时的量化敏感性、模态间误差传播、outlier 分布差异和 benchmark 覆盖。
- 读多模态量化论文时必须回答：量化对象是哪一段；校准数据是否覆盖目标模态；是否评估跨模态理解/生成质量；是否报告视觉/视频 token 数、KV cache、latency、throughput、显存和端侧/serving 路径；是否需要新的 kernel、layout 或 runtime 调度。

## 系统方向

- Serving 框架：vLLM、SGLang、TensorRT-LLM、llama.cpp。
- 多模态 serving：vision/audio/video encoder 前处理、projector、prefill、KV cache、chunked prefill、图像/视频 token batching 和跨模态 cache 复用。
- Kernel 栈：CUDA、Triton、CUTLASS、厂商库、自定义算子。
- Layout 和数据搬运：packing layout、dequantization path、memory bandwidth、cache locality。
- 性能目标：latency、throughput、显存占用、能耗、上下文长度、batch size。
- Runtime 行为：continuous batching、paged attention、speculative decoding、scheduling、graph capture。

## 应用场景

- 推理加速。
- 训练或预训练效率。
- Finetuning 效率。
- 优化器状态压缩和低 bit optimizer。
- 大规模 serving。
- 长上下文 serving。
- 边缘或本地部署。
- MoE 推理。
- 纯文本 LLM。
- 多模态模型。
- 视觉语言模型。
- 视频语言模型。
- 语音/音频语言模型。
- 扩散/DiT 生成模型。
- 全模态/omni-modal 模型。

## 成熟度阶段

- 概念启发：想法有意思，但证据有限。
- 可实验：细节足够支撑小规模复现。
- 可复现：代码、配置、数据或实现细节比较完整。
- 可集成：能较自然接入已知 serving/runtime 栈。
- 生产成熟：benchmark 强、实现稳定、硬件/runtime 路径清晰。

## 算子/Kernel 从业者标签

- kernel-optimization
- operator-fusion
- packing-layout
- dequantization
- memory-bandwidth
- tensor-core
- cache-behavior
- benchmark-design
- hardware-portability
- runtime-integration
