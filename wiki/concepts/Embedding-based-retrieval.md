---

type: concept
created: 2026-08-24
updated: 2026-08-24
sources: ["[[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]"]
tags: [method]
aliases:
  - "embedding retrieval"
  - "embedding-based skill retrieval"
sources:
  - [[sources/Demystifying-Agent-Skills-Why-They-Work—Until-They-Don’t_b13e06]]
generation_complete: true
---


# Embedding-based retrieval

## 定义

Embedding-based retrieval（基于嵌入的检索）是论文 RQ4 中用于技能检索评估的离线诊断方法之一（Arm 1）。该方法使用 Qwen3-Embedding-0.6B 将任务指令和每个技能描述编码为向量，并依据余弦相似度对候选技能排序；在严格设置下返回最近邻的单个技能，并报告 top-1 精确率。

## 关键特征

- 离线诊断方法：属于 RQ4 的 Arm 1，用于测试检索器能否直接识别最佳技能
- 向量化编码：使用 Qwen3-Embedding-0.6B 将任务指令与技能描述映射为向量表示
- 余弦相似度排序：按任务指令向量与各技能描述向量的余弦相似度对技能排序
- 严格单技能输出：只返回最近邻的单个技能，并以 top-1 精确率作为评估指标
- 随技能池规模退化：技能池从 5 增大到 100 时，top-1 精确率从 88.3% 下降到 76.9%
- 相似干扰项是主要压力源
- 测量独立性：检索输出不会传递给执行实验，与显式代理选择（Arm 2）和执行时技能使用（Arm 3）相互独立

## 应用

- 技能检索离线评估：在无需执行交互的情况下诊断技能检索质量
- 检索瓶颈测试：通过改变技能池规模评估检索性能的退化与瓶颈
- 互补测量：与显式代理选择和执行时技能使用共同构成对技能识别与使用的多维评估

## 相关概念

- [[concepts/retrieval-bottleneck|Retrieval bottleneck]]
- [[concepts/semantic-confusability|Semantic confusability]]
- [[concepts/actual-use-precision|actual-use precision]]
- [[concepts/skill-pool-construction|Skill pool construction]]

## 相关实体

- [[entities/Qwen3-Embedding-0-6B|Qwen3-Embedding-0-6B]]

## 来源提及

- "In Arm 1, embedding-based retrieval, we encode the task instruction and each skill description with Qwen3-Embedding-0.6B and rank skills by cosine similarity."
- "The strict setting returns the single nearest skill and reports top-1 precision."
- "Figure 3(a) reports average top-1 embedding precision decreasing from 88.3% at pool size 5 to 76.9% at pool size 100, while explicit agent selection decreases from 70.0% to 63.7%."