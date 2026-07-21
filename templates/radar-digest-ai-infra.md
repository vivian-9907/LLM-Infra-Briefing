# 【AI Infra Radar | {{date_or_range}}】

用于工作群每周发送的短简报。它不是完整归档版；完整证据、Near Miss、运行元信息和候选细节仍放在 `templates/radar-result-ai-infra.md` 对应的 full report 中。

## 一句话

{{one_sentence_takeaway}}

## 1. 新模型 / Agent 产品

只收有 infra、quant、serving 或 agent workflow 信号的发布；不要做泛模型新闻汇总。每条 2-3 行。

### {{model_or_agent_name}}

- 信号：架构 / context / multimodal / coding-agent / API 行为 / runtime 支持
- infra 影响：KV cache / serving / quant artifact / MoE / kernel / workflow
- 动作：`精读` / `看代码` / `观察` / `跳过`
- 链接：

## 2. 本周必看

优先放 3-5 条：论文、技术报告、framework release、repo activity 或高价值工程博客都可以混排。每条要有“为什么值得看”。

### {{item_title}}

- 类型：模型发布 / 论文 / 技术报告 / 开源项目 / framework release / repo activity / 博客
- 关键词：
- 为什么值得看：
- 动作：`精读` / `看代码` / `观察` / `跳过`
- 链接：

## 3. 本周趋势

只写 1-3 条方向判断。每条必须来自本周候选，不写空泛判断。

- {{trend_1}}：代表信号是 {{representative_items}}；建议 {{action}}。
- {{trend_2}}：代表信号是 {{representative_items}}；建议 {{action}}。

## 4. 可跳过

只列群里容易被问到、但本轮判断低信号的内容。

- {{near_miss}}：跳过原因。

## 完整版

- Full report：{{full_report_link_or_path}}
