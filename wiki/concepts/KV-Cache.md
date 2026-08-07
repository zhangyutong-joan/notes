---

type: concept
created: 2026-08-06
updated: 2026-08-06
sources: ["[[sources/Context_Engineering_223615]]"]
tags: [method]
aliases:
  - "键值缓存"
  - "KV 缓存"
sources:
  - [[sources/Context_Engineering_223615]]
generation_complete: true
---


# KV Cache

## 定义
KV Cache（键值缓存）是 Transformer 模型在自回归推理过程中用来避免重复计算的一种优化方法：模型将先前生成 token 的 Key 矩阵和 Value 矩阵保存在显存中，后续步骤仅计算当前 token 的 Query，并直接复用缓存的 Key 和 Value 完成注意力计算。在上下文工程的语境中，KV Cache 对前缀的字节级稳定性高度敏感──任何前缀字节的微小变化都会导致缓存整体失效，迫使模型重新计算全部后续 token。

## 关键特征
- **复用计算**：每一步推理只计算最新 token 的 Key/Value，旧 token 的 Key/Value 从缓存中直接读取，将 O(n²) 的计算复杂度降低为 O(n)。
- **前缀稳定性要求极高**：缓存的 Key/Value 与输入前缀的精确字节序列强绑定。只要前缀的任意一个字节发生改变（例如系统提示词中多一个空格），整个 KV Cache 即告失效，所有后续 token 必须完整重新计算。
- **通过 Chat Template 固化**：Chat Template 将系统消息与工具定义转化为固定的 token 序列，置放于对话最前方，强制保证前缀的不变性，从而最大化 KV Cache 的命中率。
- **代价敏感**：当前缀频繁变动时（例如动态拼接系统提示词），缓存频繁失效会导致重复的前向计算，显著增加首 token 延迟和整体推理成本。

## 应用
- **大语言模型推理优化**：几乎所有生产环境的自回归 LLM 推理引擎（vLLM、TensorRT-LLM 等）都依赖 KV Cache 来降低首 token 延迟与吞吐成本。
- **系统提示词固化**：在设计 AI 应用时，将固定不变的系统提示词、角色描述、规则指令置于会话最前方，利用 Chat Template 确保其 token 序列不变，使 KV Cache 可复用，避免重复计算开销。
- **Prompt Cache 的物理基础**：KV Cache 的复用机制直接催生出 Prompt Cache（前缀缓存）技术，在多个请求间共享相同前缀的 KV 缓存，进一步提升并发吞吐。
- **调试与成本监控**：理解 KV Cache 失效条件有助于排查大模型应用中的延迟突增问题，及通过分析缓存命中率来优化 token 使用成本。

## 相关概念
- [[concepts/Prompt-Cache|Prompt Cache]]
- [[concepts/Chat-Template|Chat Template]]
- [[concepts/缓存一致性|缓存一致性]]

## 相关实体
_暂无相关实体。_

## 来源提及

- "KV Cache：在一次推理过程中，缓存已计算的 token 的键值对，避免重复计算。" (KV Cache：在一次推理过程中，缓存已计算的 token 的键值对，避免重复计算。) — [[raw/concept_note/Context_Engineering|Context_Engineering]]
- "一条铁律：前缀里改一个字节，后面的缓存就全废。" (一条铁律：前缀里改一个字节，后面的缓存就全废。) — [[raw/concept_note/Context_Engineering|Context_Engineering]]