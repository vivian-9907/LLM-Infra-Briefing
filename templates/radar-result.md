# LLM Infra Briefing - {{channel}} - {{date_or_range}}

## 本次运行上下文

- 时间范围：
- 来源范围：
- 频道：`quantization` / `ai-infra`
- 默认 profile：读取 `config/channels/{{channel}}/profile.yml`
- 是否展开 full topics：否 / 是，原因：
- 是否展开 research map：否 / 是，原因：
- 是否读取 watchlist：是，常规 radar 默认读取；用于固定关注模型、agent 产品、机构和框架
- 是否读取 tracked-repos：否 / 是，原因：
- 是否读取 experts：否 / 是，原因：
- 是否读取 venues：否 / 是，原因：
- 主题依据：profile / watchlist / tracked-repos / experts / venues / full topics / research map
- 领域限定：无 / {{core_subtopic}}
- 软过滤口径：核心候选优先；相邻候选必须说明关联原因
- 筛选规则：按 `config/radar-rubric.yml` 初筛，只列有价值条目，不强行凑数量

## 本轮方向摘要

先给出本轮 radar 的方向判断，再进入候选表。这里不是复述每个条目，而是回答：本轮哪些子类出现了值得关注的信号，哪些子类没有强结果，是否形成了值得专项跟踪的趋势。

- 强信号子类：
- 弱信号或 near-miss 子类：
- 达到专项洞察门槛的子类：
- 暂不展开的子类及原因：
- 本轮无专项洞察时说明：

## 候选总览表

先按子类聚合，再按价值信号排序。子类来自频道 topics 和频道 research map。`quantization` 频道可包含 KV cache、weight-only、weight-activation、optimizer quantization、balanced/outlier-aware quantization、rotation/transform、多模态量化、visual token compression、DiT quantization、kernel/runtime、serving-aware quantization 等；`ai-infra` 频道可包含 serving/runtime、speculative decoding、MoE systems、training systems、communication、kernel/operator、architecture infra impact、performance analysis 等。

| 子类 | 时间 | 工作 | 类型 | 数据格式/压缩率 | 核心技术 | 意义/评价 | kernel/artifact 落地状态 | 建议动作 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  | 论文 / 项目 / 博客 / benchmark / model release / agent product update / framework release |  |  |  |  | `inspect` / `track-code` / `replicate` / `watch` / `ignore` |

## 分方向候选详情

### {{title}}

- 链接：
- 来源：
- 日期：
- 类型：
- 子类：
- 领域限定关系：核心候选 / 相邻候选 / 无领域限定
- 相邻候选关联原因：
- 命中的频道技术方向：
- 数据格式/压缩率：
- 核心技术：
- kernel/artifact 落地状态：
- 为什么重要：
- 证据：
- 初筛信号摘要：
- 建议动作：`inspect` / `track-code` / `replicate` / `watch` / `ignore`

## 专项洞察（可选）

只在“本轮方向摘要”中已经点名某个子类达到专项洞察门槛时使用本节。专项洞察要解释一个方向为什么在本轮值得看，而不是简单重复候选条目；例如 KV cache 压缩、optimizer quantization、FP4/NVFP4/MXFP4、多模态量化、visual token compression、DiT quantization、balanced/outlier-aware quantization、rotation-based quantization 或 kernel/runtime 集成。

- 子类：
- 触发依据：
- 本轮信号：
- 代表工作：
- 横向共同点：
- 分歧或不确定性：
- 置信度：高 / 中 / 低
- 初步判断：
- 下一步建议：

## 值得观察

### {{title}}

- 链接：
- 为什么值得观察：
- 缺少什么证据：
- 建议后续动作：

## 本轮无强候选

只在适用时使用本节。明确说明为什么没有条目达到高价值标准。

## 历史表格（预留）

只有在已有历史记录或用户明确要求维护历史表格时使用本节。默认不要为了形式补历史。

- 本轮新增：
- 与历史方向的关系：
- 需要后续跟踪的条目：

## 注意事项

- 不要填充低价值条目。
- `quantization` 频道排除金融量化内容。
- 优先给出简洁、判断明确的说明，不要写成长摘要。
