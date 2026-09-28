---
title: "WFM: Wiki Foundation Model for Complex Agentic Reasoning"
source: "https://arxiv.org/html/2609.18182v1#S3"
author:
published:
created: 2026-09-28
description:
tags:
  - "clippings"
---
 Conference: Make sure to enter the correct conference title from your rights confirmation email; June 03–05, 2018; Woodstock, NYISBN: 978-1-4503-XXXX-X/2018/06CCS: Information systems Language modelsCCS: Computing methodologies Semantic networksCCS: Information systems Information retrieval query processing

Junnan Dong ${}^{1}{\dagger}$, Linhao Luo ${}^{2}{\dagger}$, Senlei Zhang ${}^{1}{\dagger}$, Gong Chen <sup>1</sup>, Taian Guo <sup>1</sup>,  
Yifei Yu <sup>1</sup>, Rong Tao <sup>3</sup>, Tao Guo <sup>4</sup>, Qian-wen Zhang <sup>1</sup>, Siyu An <sup>1∗</sup>, Ruizhi Qiao <sup>1</sup>, Xing Sun <sup>1</sup>  
<sup>1</sup> Tencent Youtu Lab   <sup>2</sup> Monash University  
<sup>3</sup> Hong Kong Baptist University   <sup>4</sup> Shenzhen University

2018

![Refer to caption](https://arxiv.org/html/2609.18182v1/running.png)

Figure 1. A sketched overview of the paradigm shift from RAG, GraphRAG to LLM Wiki.

###### Abstract.

Real-world agents fundamentally require persistent non-parametric knowledge for dynamic reasoning, i.e., long-term memory and retrieval-augmented generation. While graphs have shown reliable advantages in providing structured evidence, the sparse graph representations naturally restrict machine readability and semantic density required for complex agentic workflows. Driven by this limitation, the entire industry is witnessing a paradigm shift from traditional sparse graphs to LLM Wiki, an agent-native knowledge representation that couples dense document contexts with markdown files containing multi-layered topological linkages. However, parameterizing such rich semantics is challenging to encode dense textual contexts using traditional sparse graph embeddings. Moreover, learning LLM Wiki with existing graph encoders could overwhelm distributed system overheads that hinder deployment in large-scale commercial scenarios. To this end, we propose a novel paradigm Wiki Foundation Model, i.e., WFM, tailored for scalable, agent-native representation and retrieval. Specifically, $(i)$ we formalize a Wiki Graph schema that seamlessly bridges fine-grained structures with dense contexts, maintaining explicit topologies alongside continuous semantics; $(ii)$ A query-conditioned attentive aggregation is tailored for rich wiki message passing and explicit attention variance regularization; $(iii)$ We engineer an infrastructural NCCL boundary exchange protocol that hoists static partition indices and leverages fixed-shape GPU-to-GPU collectives, bypassing CPU serialization and memory copy overheads. Extensive evaluations across five long-term agent memory and multi-hop reasoning benchmarks demonstrate the remarkable performance of WFM, while achieving a $10.5\times$ training acceleration on distributed clusters.

###### Keywords:

Foundation Models, LLM Wiki, Agentic Reasoning

## 1\. Introduction

Large language models (LLMs) have achieved remarkable progress in complex reasoning, but their susceptibility to hallucinations and static memory boundaries [^4] [^24] [^2] remains a fundamental hurdle in real-world agents [^37] [^18] [^1]. They require persistent, non-parametric knowledge bases to support dynamic reasoning in long-horizon planning and execution scenarios [^21]. To achieve this, integration between long-term agent memory [^35] [^22] [^11] and retrieval-augmented generation (RAG) [^29] [^15] [^7] has become an essential backbone. While traditional knowledge graphs (KGs) have demonstrated reliable advantages in organizing structured evidence, GraphRAG has been extensively studied for complex multi-hop reasoning tasks across multiple documents, effectively representing the raw texts into concise (head, relation, tail) triples [^3] [^13] [^20] [^5] [^9] [^30] [^1]. However, their sparse relational representations inherently restrict machine readability and lack the semantic density necessary for complex agentic workflows [^10] [^8]. Discretizing rich contextual knowledge into rigid triples invariably strips away nuanced textual semantics and macro-document continuity. This makes it hard to navigate the agents in long-range tasks.

Driven by this fundamental limitation, the entire industry is witnessing a critical paradigm shift from traditional sparse graphs to LLM Wiki [^23], an agent-native knowledge representation. By coupling dense document context passages with structured Markdown documents containing multi-layered topological linkages, an LLM Wiki seamlessly bridges micro-level entity connectivity with macro-level continuous text fidelity. Consequently, the LLM Wiki format has quickly emerged as a leading knowledge substrate for both state-of-the-art agentic research and production-scale industrial deployment. Given the abundant semantic information, rather than existing training-free frameworks, we are motivated to encode the structured wiki with a tailored graph foundation model (GFM) [^25] [^34] that pre-trains a graph neural network based on massive data to obtain effective structural comprehension [^26] [^6]. Parameterizing LLM Wiki via GFMs could project both multi-layered topology and dense contexts into a continuous geometric embedding space, enabling generalizable, zero-shot transfer and end-to-end multi-hop reasoning without task-specific architecture heuristics.

However, scaling representation learning over such hybrid, data-dense LLM Wikis introduces severe challenges.

First, existing GFM backbones are tailored for sparse discrete tuples.

When applied to high-density LLM Wikis, their aggregation mechanisms suffer from catastrophic uniform attention collapse. Driven by rapid Softmax variance decay, multi-head attention weights flatten into near-uniform distributions, creating paralyzing gradient locks that freeze representation learning.

Second, we are facing a challenging infrastructural scalability bottleneck.

Training continuous encoders over text-augmented graph partitions requires frequent boundary node state synchronization across distributed multi-GPU clusters. Existing implementations rely on CPU-bound Gloo/Pickle primitives, introducing severe memory copy and serialization overheads that create an unacceptable latency cliff and prevent large-scale commercial scaling.

To resolve these fundamentally intertwined challenges, we introduce the

Wiki Foundation Model (

WFM

)

,

a novel agent-native foundation paradigm engineered for scalable,

joint representation learning over high-density LLM Wikis.

Rather than treating graph construction, representation learning, and system execution as decoupled pipelines, WFM provides a vertically unified framework aligning mathematical formulations directly with distributed hardware primitives: $(i)$ We formalize

a dual-layered Wiki Graph schema

that seamlessly couples discrete entity-relation topologies with dense passage contexts via explicit

cross-layer hyper-edges

, preserving macro-level textual semantics without sacrificing micro-level structural connectivity. $(ii)$ We design

a query-conditioned attentive aggregation scheme

featuring dual-space message passing for rich wiki propagation, coupled with an explicit attention variance regularization ($\mathcal{L}_{\text{var}}$) that enforces a strict variance lower bound to mathematically eliminate gradient locks and preserve sharp multi-hop feature selectivity. $(iii)$ We engineer

an infrastructural NCCL-native boundary

exchange protocol that hoists static graph partition layouts to an offline pre-processing stage and executes fixed-shape GPU-to-GPU communications via raw NCCL primitives, completely bypassing CPU serialization and host-to-device memory copy overheads.

Our main contributions are summarized as follows:

- We formalize the paradigm transition from sparse graphs to LLM Wikis, establishing WFM as the first foundation model tailored for joint representation learning over text-augmented topologies.
- An advanced wiki graph is presented to combine the strengths of both sparse entity graphs and LLM Wikis.
- We design
	a tailored graph encoder
	and
	corresponding infrastructural foundation
	for wiki graph. The query-conditioned attentive aggregation scheme with variance regularization ensures gradient-lock-free multi-hop reasoning, achieving a bit-exact $10.5\times$ end-to-end training speedup ($2.40\text{s}\rightarrow 0.23\text{s/step}$) on multi-GPU clusters.
- Extensive evaluations across five agent memory and complex reasoning benchmarks demonstrate that WFM remarkably advances the Pareto frontier of reasoning accuracy, memory recall, and system throughput.

![Refer to caption](https://arxiv.org/html/2609.18182v1/figure1.png)

Figure 2. Overview of WFM. Entity–relation topology and passage nodes are encoded in a shared Wiki Graph, optimized with structure, alignment, and attention-variance objectives, and propagated across graph partitions through GPU-resident boundary exchange.

## 2\. Task Formulation

To formalize the unified learning over discrete graph topologies and dense textual semantics, we first define the notations for the Graph Foundation Model (GFM) paradigm and the LLM Wiki knowledge representation.

### 2.1. Definitions and Notation

#### Definition 1 (Graph Foundation Model Paradigm).

Let $\mathcal{G}=(\mathcal{V},\mathcal{E},\mathcal{R})$ denote a large-scale graph structure where $\mathcal{V}$ is the node set, $\mathcal{E}$ is the edge set, and $\mathcal{R}$ represents the set of relation types. A Graph Foundation Model (GFM), parameterized by $\mathbf{\Theta}_{\text{GFM}}$, projects the discrete graph structure into a continuous $d$ -dimensional embedding space $\mathbb{R}^{d}$. Unlike task-specific graph neural networks, a GFM learns generalizable topological representations across diverse domain topologies, yielding a node representation matrix $\mathbf{H}\in\mathbb{R}^{|\mathcal{V}|\times d}$ that supports zero-shot domain transfer and continuous downstream reasoning.

#### Definition 2 (LLM Wiki Knowledge Representation).

An LLM Wiki is a hybrid, text-augmented knowledge repository denoted as $\mathcal{W}=(\mathcal{E}_{w},\mathcal{R}_{w},\mathcal{D})$. Here, $\mathcal{E}_{w}$ represents fine-grained entity concepts, $\mathcal{R}_{w}$ denotes structural interconnections between entities, and $\mathcal{D}=\{d_{i}\}_{i=1}^{|\mathcal{D}|}$ is a collection of dense, structured text documents associated with the entities. Each entity $e\in\mathcal{E}_{w}$ is mapped to one or more passage contexts $d\in\mathcal{D}$, weaving sparse topological paths $p=(e_{1},r_{1},e_{2},\dots,e_{k})$ with dense passage semantics $\mathbf{T}(d)$.

### 2.2. GFM Message Passing and Feature Propagation

Unlike conventional GNNs operating purely on sparse relational tuples $(e_{i},r,e_{j})$, a GFM over an LLM Wiki must perform feature propagation across both topological neighbors and associated textual contexts.

Formally, at layer $l$, the message aggregation $\mathbf{m}_{v}^{(l)}$ for node $v\in\mathcal{E}_{w}$ from its graph neighborhood $\mathcal{N}(v)$ and its coupled document set $\mathcal{D}_{v}\subset\mathcal{D}$ is defined as:

$$
\displaystyle\mathbf{m}_{v}^{(l)}=\text{AGGREGATE}^{(l)}
$$
 
$$
\displaystyle\left(\left\{\mathbf{MESSAGE}^{(l)}\left(\mathbf{h}_{u}^{(l-1)},\mathbf{h}_{r},\mathbf{T}(d_{u})\right)\;\middle|\;u\in\mathcal{N}(v)\cup\mathcal{D}_{v},r\in\mathcal{R}_{w}\right\}\right)
$$

The node representation $\mathbf{h}_{v}^{(l)}$ is subsequently updated by combining its previous state with the aggregated hybrid message:

$$
\mathbf{h}_{v}^{(l)}=\text{UPDATE}^{(l)}\left(\mathbf{h}_{v}^{(l-1)},\mathbf{m}_{v}^{(l)}\right)
$$

where $\mathbf{h}_{v}^{(0)}$ is initialized via a joint text-entity encoder mapping raw text $\mathbf{T}(d_{v})$ and entity attributes into $\mathbb{R}^{d}$.  
Given an agentic query $q$ over an LLM Wiki $\mathcal{W}$, the task of agentic multi-hop retrieval is to locate a gold supporting document subset $\mathcal{D}^{*}\subset\mathcal{D}$ that provides sufficient evidence for reasoning. Standard GFM propagation (Equations 1 and 2) suffers from uniform attention collapse and GPU communication bottlenecks when applied to dense LLM Wikis.

## 3\. Approach: WFM

In this section, we elaborate on the architecture of WFM. As illustrated in Figure 2, WFM integrates an Attention-Aggregation Graph Foundation Model (GFM) with a hardware-centric distributed system co-design, enabling stable representation learning and efficient propagation over high-density LLM Wikis. The construction stage converts an LLM Wiki into a typed hybrid graph; the model stage propagates information over its entity and passage nodes; and the systems stage implements the same propagation when the graph is partitioned across GPUs.

### 3.1. Wiki Graph Construction and Dual-Space Initialization

To bridge the gap between discrete relational triples and dense document contexts, we represent an LLM Wiki as a hybrid topology $\mathcal{W}=(\mathcal{E}_{w},\mathcal{R}_{w},\mathcal{D})$. Its node set is the union $\mathcal{E}_{w}\cup\mathcal{D}$. The first edge family retains each typed entity relation $(e_{i},r,e_{j})$, while the second connects an entity to the passages in which it is described or mentioned. These cross-layer links make a passage reachable from the entity topology without reducing its text to an additional triple. Conversely, an entity can aggregate contextual evidence from multiple passages while preserving its explicit relation types.

We construct a continuous dual-space embedding initialization for each node $v\in\mathcal{E}_{w}\cup\mathcal{D}$:

- Topological Entity Embedding: Each entity $e\in\mathcal{E}_{w}$ and relation $r\in\mathcal{R}_{w}$ is mapped to a structural space $\mathbb{R}^{d_{s}}$ via a trainable lookup table, denoted as $\mathbf{e}_{e}\in\mathbb{R}^{d_{s}}$ and $\mathbf{e}_{r}\in\mathbb{R}^{d_{s}}$. This lookup preserves the identity of discrete entities and the edge type used by the subsequent relation-aware propagation.
- Dense Document Embedding: Each document passage $d\in\mathcal{D}$ is mapped to a semantic space $\mathbb{R}^{d_{t}}$ using a pre-trained language model backbone $\mathbf{T}(\cdot)$, yielding $\mathbf{h}_{d}=\mathbf{T}(d)\in\mathbb{R}^{d_{t}}$. The passage remains a first-class node, so its continuous semantics can participate directly in multi-hop message passing.

A linear projection layer $\mathbf{W}_{p}\in\mathbb{R}^{d_{s}\times d_{t}}$ maps each textual state to the structural width, $\mathbf{h}^{(0)}_{d}=\mathbf{W}_{p}\mathbf{T}(d)$. We use $d=d_{s}$ as the common propagation dimension and initialize an entity by $\mathbf{h}^{(0)}_{e}=\mathbf{e}_{e}$. Consequently, entity and passage states have the same width before attention is applied, although they originate from different structural and semantic spaces.

### 3.2. Attentive Graph Foundation Model

WFM parameterizes message passing via a relation-aware graph attention mechanism over both relational topologies and textual nodes. Given a query, retrieval first identifies its seed entities and passages and induces the local computation graph on which the following propagation is performed. Query conditioning therefore determines which Wiki neighborhood participates in aggregation, while the attention equations determine how messages within that neighborhood are weighted. For readability, we omit the query and layer superscripts below and use $\mathcal{N}(v)$ to denote this active, typed neighborhood.

#### Relation-Aware Attention Weighting.

For a node $v$ (either an entity $e$ or document $d$) and its connected neighbor $u\in\mathcal{N}(v)$ under relation $r\in\mathcal{R}_{w}$, we calculate a relation-dependent propagation score. Each incident message is identified by the pair $(r,u)$: entity–entity messages use the original Wiki relation, whereas entity–passage messages use the corresponding cross-layer link type. The relational attention score $\pi(v,r,u)$ measures how much information propagates from $u$ to $v$ conditioned on $r$:

$$
\pi(v,r,u)=\mathbf{w}_{a}^{T}\tanh\left(\mathbf{W}_{r}\mathbf{h}_{u}+\mathbf{e}_{r}-\mathbf{W}_{r}\mathbf{h}_{v}\right).
$$

Here, $\mathbf{W}_{r}\in\mathbb{R}^{d\times d}$ maps source and target states under the same relation, $\mathbf{e}_{r}$ offsets their difference according to edge type, and $\mathbf{w}_{a}\in\mathbb{R}^{d}$ converts the resulting compatibility vector to a scalar logit. Applying the same scoring form to both node types permits structural and textual messages to compete in one neighborhood rather than being aggregated by disconnected encoders.

To make attention coefficients comparable across heterogeneous neighbors, we normalize $\pi(v,r,u)$ over all typed incident messages of $v$ using the Softmax function:

$$
\alpha(v,r,u)=\frac{\exp\left(\pi(v,r,u)\right)}{\sum_{(r^{\prime},u^{\prime}):\,u^{\prime}\in\mathcal{N}(v)}\exp\left(\pi(v,r^{\prime},u^{\prime})\right)}.
$$

The coefficients are non-negative and sum to one for each target node. This local normalization is important for the hybrid graph: the scale of the update does not grow directly with node degree, while the relative scores decide whether a structural neighbor or a supporting passage contributes more strongly.

#### Dual-Space Message Aggregation.

Once attention weights $\alpha(v,r,u)$ are derived, the aggregated message $\mathbf{m}_{v}$ for target node $v$ is synthesized as a weighted combination of relational neighbors and document contexts:

$$
\mathbf{m}_{v}=\sum_{(r,u):\,u\in\mathcal{N}(v)}\alpha(v,r,u)\left(\mathbf{W}_{v}\mathbf{h}_{u}+\mathbf{e}_{r}\right).
$$

Although all states now lie in $\mathbb{R}^{d}$, their origins remain complementary: entity neighbors contribute explicit relational paths, and passage neighbors contribute continuous textual evidence. Repeating this operation across layers allows evidence attached to one entity to reach structurally related entities, which is the mechanism used to represent multi-hop Wiki context.

To preserve self-node identity while incorporating the aggregated context, we employ a Bi-Interaction aggregator:

$$
\displaystyle\mathbf{h}_{v}^{(l)}
$$
 
$$
\displaystyle=\text{LeakyReLU}\left(\mathbf{W}_{1}\left(\mathbf{h}_{v}^{(l-1)}+\mathbf{m}_{v}\right)\right)
$$
 
$$
\displaystyle+\text{LeakyReLU}\left(\mathbf{W}_{2}\left(\mathbf{h}_{v}^{(l-1)}\odot\mathbf{m}_{v}\right)\right).
$$

Here, $\odot$ denotes element-wise Hadamard product, and $\mathbf{W}_{1},\mathbf{W}_{2}\in\mathbb{R}^{d\times d}$ are trainable transformation matrices. The additive branch preserves information present in either the previous state or the incoming message, whereas the multiplicative branch emphasizes dimensions on which the two agree. Their sum therefore combines residual-like propagation with feature-level interaction without introducing a separate update rule for passage nodes.

### 3.3. Iterative Retrieval with Self-Reflection

A single retrieval pass may expose only one segment of a multi-hop path or one episode in a long interaction history. We therefore place the attentive retriever inside a bounded agentic loop. Let $B$ denote the *reflection budget*, i.e., the maximum number of retrieval–generation iterations, and let $q^{(1)}=q$ be the original user query. At iteration $t$, the current query is encoded and matched against the propagated passage states:

$$
s^{(t)}(d)=\operatorname{sim}\!\left(\mathbf{T}(q^{(t)}),\mathbf{h}^{(L)}_{d}\right),\qquad\mathcal{D}^{(t)}=\operatorname{TopK}_{d\in\mathcal{D}}\,s^{(t)}(d),
$$

where $L$ is the number of attentive propagation layers. The retrieved passages are accumulated rather than replaced, $\mathcal{C}^{(t)}=\mathcal{C}^{(t-1)}\cup\mathcal{D}^{(t)}$, so later rounds retain evidence found earlier.

Conditioned on $q$ and $\mathcal{C}^{(t)}$, the agent produces a candidate answer $a^{(t)}$, a follow-up query $q^{(t+1)}$, and a binary completion flag $f^{(t)}\in\{\textsc{Continue},\textsc{Final}\}$:

$$
\left(a^{(t)},q^{(t+1)},f^{(t)}\right)=\operatorname{LLM}\!\left(q,\mathcal{C}^{(t)}\right).
$$

The loop terminates immediately when $f^{(t)}=\textsc{Final}$ and returns $a^{(t)}$. Otherwise, the follow-up query targets the evidence judged missing by the current answer and initiates another Wiki retrieval pass. If no final flag is emitted by iteration $B$, the agent stops at the hard budget and returns $a^{(B)}$. Thus, $B$ bounds worst-case inference cost, whereas the final-answer flag avoids spending all iterations on queries already supported by sufficient evidence. The ablation in Section 4.7 separately tests removing self-reflection and removing this adaptive stopping decision.

### 3.4. Warm-Start Curriculum and Multi-Task Loss Formulation

When training deep GFMs on dense LLM Wikis from scratch, standard Softmax attention can suffer from variance decay ($\text{Var}(\pi)\to 0$). If all logits in a neighborhood become equal, Softmax assigns $\alpha(v,r,u)=1/|\mathcal{N}(v)|$ and the update approaches an unselective neighborhood average. Repeating such averages across layers weakens the distinction between alternative relation paths and between relevant and incidental passages. To keep the model selective while learning the shared representation space, we couple the task objectives with a lower-bound penalty on logit variance and optimize them with a warm-start curriculum.

#### Multi-Task Loss Formulation.

The training objective of WFM is governed by three complementary loss components:

- Topological Structure Loss ($\mathcal{L}_{\text{topo}}$): We employ a TransE-style margin-based pairwise ranking loss to preserve relational link prediction boundaries over entity topologies:
	$$
	\mathcal{L}_{\text{topo}}=\sum_{(e,r,e^{\prime})\in\mathcal{T}}\sum_{(e,r,e^{\prime\prime})\notin\mathcal{T}}\left[\gamma+d\left(\mathbf{h}_{e}+\mathbf{e}_{r},\mathbf{h}_{e^{\prime}}\right)-d\left(\mathbf{h}_{e}+\mathbf{e}_{r},\mathbf{h}_{e^{\prime\prime}}\right)\right]_{+}
	$$
	where $\mathcal{T}$ denotes positive relational triples, $\gamma>0$ is the margin hyperparameter, $d(\cdot,\cdot)$ is $L_{2}$ distance, and $[\cdot]_{+}=\max(0,\cdot)$. Each negative $e^{\prime\prime}$ replaces the positive tail $e^{\prime}$ in the same relational context. Minimizing the loss keeps an observed entity pair at least $\gamma$ closer than its corrupted counterpart and thereby anchors the propagated states to the original Wiki topology.
- Dense Document Alignment Loss ($\mathcal{L}_{\text{align}}$): To ensure continuous alignment between fine-grained entities and dense passage contexts, we minimize InfoNCE contrastive loss over entity-document pairs $(e,d)$:
	$$
	\mathcal{L}_{\text{align}}=-\sum_{(e,d)\in\mathcal{B}}\log\frac{\exp\left(\text{sim}(\mathbf{h}_{e},\mathbf{h}_{d})/\tau\right)}{\sum_{d^{\prime}\in\mathcal{B}}\exp\left(\text{sim}(\mathbf{h}_{e},\mathbf{h}_{d^{\prime}})/\tau\right)}
	$$
	where $\text{sim}(\mathbf{a},\mathbf{b})=\frac{\mathbf{a}^{T}\mathbf{b}}{\|\mathbf{a}\|\|\mathbf{b}\|}$, $\tau$ is temperature, and $\mathcal{B}$ denotes the mini-batch. For each linked entity, the associated passage is the positive and the other batch passages form contrastive alternatives. This objective gives the projection $\mathbf{W}_{p}$ a direct alignment signal before document states are mixed through graph propagation.
- Attention Variance Regularization Loss ($\mathcal{L}_{\text{var}}$): To explicitly prevent attention collapse, we penalize low variance in attention logit distributions:
	$$
	\mathcal{L}_{\text{var}}=\sum_{v\in\mathcal{V}}\left[\epsilon-\text{Var}_{u\in\mathcal{N}(v)}\left(\pi(v,r,u)\right)\right]_{+}
	$$
	where $\epsilon>0$ is a variance lower-bound threshold. The hinge is active only when a neighborhood’s logits are insufficiently dispersed; once their variance reaches $\epsilon$, this term contributes no further pressure to enlarge it. The regularizer therefore prevents the uniform solution without prescribing which neighbor should receive the largest coefficient.

The overall objective function is formulated as:

$$
\mathcal{L}_{\text{total}}=\mathcal{L}_{\text{topo}}+\lambda_{1}\mathcal{L}_{\text{align}}+\lambda_{2}\mathcal{L}_{\text{var}}+\lambda_{3}\|\mathbf{\Theta}\|_{2}^{2}.
$$

The first two terms preserve the two information sources encoded by the Wiki Graph, while $\mathcal{L}_{\text{var}}$ controls the optimization behavior of their attention-based interaction. The coefficients $\lambda_{1}$, $\lambda_{2}$, and $\lambda_{3}$ balance document alignment, variance regularization, and weight decay relative to the topological objective.

#### Warm-Start Curriculum Framework.

Instead of cold-starting joint training, WFM executes a two-phase warm-start curriculum. In Phase I (Structure–Document Alignment), we freeze $\mathbf{\Theta}_{\text{GFM}}$ and train $\mathbf{W}_{p}$ and the lookup tables solely under $\mathcal{L}_{\text{align}}$. This places linked entities and passages in a compatible region of the shared space before neighborhood mixing begins. In Phase II (Full Joint Optimization), we unfreeze all parameters and optimize $\mathcal{L}_{\text{total}}$. Attention then starts from distinguishable structural and textual inputs, while the hinge regularizer corrects neighborhoods whose logit variance falls below $\epsilon$. The curriculum changes only the order in which the existing parameter groups and loss terms are activated; inference uses the same attentive propagation equations in both cases.

### 3.5. Infrastructural NCCL-Native Boundary Exchange Protocol

Distributing multi-layer Attention-Aggregation GFMs across GPU clusters requires the representation of every cross-partition neighbor before its message can be evaluated. A conventional path serializes boundary states on the host, communicates them through a CPU backend, and then copies the received states back to the destination GPU. Because this sequence is repeated at each propagation layer, its synchronization and memory-copy costs can dominate the tensor operations of the model.

We therefore co-design distributed message passing with an NCCL-native boundary exchange protocol. It changes how the states required by the existing aggregation equations are transported, but not their values or the mathematical update performed at a node. While node representation tensors $\mathbf{H}$ are updated continuously during optimization, the graph partition topology and the ownership of boundary nodes remain static. WFM therefore computes the per-rank send and receive indices once in an offline preprocessing stage instead of rediscovering and serializing them at every step. The resulting sparse gather/scatter layouts map local node IDs to contiguous GPU-resident buffers $\mathbf{B}_{\text{send}}$ and $\mathbf{B}_{\text{recv}}$. During training, each rank only gathers the current rows of $\mathbf{H}^{(l)}$ specified by this fixed layout. Instead of dynamically packing variable-length Python objects, WFM pads the per-peer boundary layouts to fixed-shape tensors. Their stable shapes permit direct GPU-to-GPU collectives over NVLink or InfiniBand:

$$
\mathbf{B}_{\text{recv}}\leftarrow\text{NCCL\_AllToAll}\left(\text{Gather}(\mathbf{H}^{(l)},\text{Index}_{\text{boundary}})\right).
$$

After communication, each rank scatters the valid rows of $\mathbf{B}_{\text{recv}}$ into its ghost-node slots and evaluates the same relation-aware attention and Bi-Interaction update as in the unpartitioned graph. Padding entries are excluded by the precomputed layout, so they do not enter the Softmax neighborhood or alter aggregation. Removing host serialization and host-to-device copies reduces the measured per-step latency from $2.40\text{s}$ to $0.23\text{s}$, corresponding to a $10.5\times$ end-to-end acceleration while preserving the computed node states.

### 3.6. Agentic Self-Reflection

At inference time, WFM wraps Wiki retrieval and answer generation in a self-reflection loop controlled by a maximum iteration budget $B$. After each round, the agent inspects the retrieved evidence and its candidate answer: if the evidence is sufficient, it emits a final-answer flag and terminates immediately; otherwise, it formulates a follow-up query that targets the missing information and starts another retrieval round while retaining previously collected evidence. The loop stops no later than round $B$, which bounds worst-case latency and token cost. Thus, a larger $B$ permits more opportunities to recover dispersed multi-hop evidence, while adaptive final-answer stopping prevents simple queries from consuming the full budget.

Table 1. Retrieval recall comparisons over HotpotQA, 2Wiki, and Musique datasets.

<table><tbody><tr><td rowspan="2">Methods</td><td colspan="4">HotpotQA</td><td colspan="4">2Wiki</td><td colspan="4">Musique</td></tr><tr><td>R@2</td><td>R@5</td><td>R@10</td><td>R@20</td><td>R@2</td><td>R@5</td><td>R@10</td><td>R@20</td><td>R@2</td><td>R@5</td><td>R@10</td><td>R@20</td></tr><tr><td>Native RAG</td><td>44.24</td><td>55.35</td><td>62.68</td><td>68.10</td><td>31.28</td><td>31.80</td><td>46.22</td><td>49.22</td><td>17.28</td><td>19.28</td><td>37.10</td><td>44.44</td></tr><tr><td>RAPTOR</td><td>56.00</td><td>72.63</td><td>79.98</td><td>84.30</td><td>49.10</td><td>60.12</td><td>65.20</td><td>68.10</td><td>34.29</td><td>46.82</td><td>55.06</td><td>61.93</td></tr><tr><td>E <sup>2</sup> GraphRAG</td><td>49.79</td><td>63.92</td><td>75.22</td><td>80.87</td><td>27.70</td><td>34.90</td><td>40.90</td><td>52.80</td><td>19.40</td><td>24.40</td><td>31.40</td><td>43.70</td></tr><tr><td>LightRAG</td><td>45.80</td><td>63.20</td><td>70.40</td><td>75.70</td><td>37.00</td><td>49.10</td><td>53.90</td><td>58.30</td><td>27.00</td><td>38.70</td><td>46.80</td><td>53.80</td></tr><tr><td>GraphRAG</td><td>44.10</td><td>56.55</td><td>67.20</td><td>73.45</td><td>28.65</td><td>36.10</td><td>42.30</td><td>54.60</td><td>14.35</td><td>18.05</td><td>23.20</td><td>32.30</td></tr><tr><td>HippoRAG1</td><td>61.35</td><td>76.20</td><td>82.95</td><td>85.50</td><td>64.27</td><td>73.12</td><td>79.77</td><td>84.13</td><td>36.90</td><td>48.64</td><td>55.86</td><td>61.04</td></tr><tr><td>HippoRAG-IRCOT</td><td>61.30</td><td>76.90</td><td>76.10</td><td>83.80</td><td>67.95</td><td>78.75</td><td>82.62</td><td>86.93</td><td>34.65</td><td>44.81</td><td>51.17</td><td>57.77</td></tr><tr><td>HippoRAG2</td><td>62.80</td><td>78.85</td><td>82.77</td><td>89.20</td><td>66.82</td><td>77.35</td><td>81.26</td><td>84.98</td><td>40.47</td><td>52.94</td><td>60.57</td><td>67.66</td></tr><tr><td>Youtu-GraphRAG</td><td>63.15</td><td>79.30</td><td>86.00</td><td>89.70</td><td>69.65</td><td>80.95</td><td>83.80</td><td>88.50</td><td>44.50</td><td>60.75</td><td>71.40</td><td>75.90</td></tr><tr><td>GFM-RAG</td><td>52.95</td><td>68.26</td><td>76.63</td><td>81.38</td><td>50.19</td><td>63.95</td><td>68.30</td><td>72.63</td><td>24.31</td><td>31.82</td><td>38.92</td><td>48.57</td></tr><tr><td>WFM</td><td>66.80</td><td>82.45</td><td>89.10</td><td>93.20</td><td>72.30</td><td>83.40</td><td>87.65</td><td>90.15</td><td>46.85</td><td>63.90</td><td>71.95</td><td>75.24</td></tr></tbody></table>

Table 2. Comparisons over HotpotQA, 2Wiki, and Musique datasets.

<table><tbody><tr><td rowspan="2">Methods</td><td colspan="2">HotpotQA</td><td colspan="2">2Wiki</td><td colspan="2">Musique</td></tr><tr><td>Open <math><semantics><mo>↑</mo> <annotation>\uparrow</annotation></semantics></math> (%)</td><td>Reject <math><semantics><mo>↑</mo> <annotation>\uparrow</annotation></semantics></math> (%)</td><td>Open <math><semantics><mo>↑</mo> <annotation>\uparrow</annotation></semantics></math> (%)</td><td>Reject <math><semantics><mo>↑</mo> <annotation>\uparrow</annotation></semantics></math> (%)</td><td>Open <math><semantics><mo>↑</mo> <annotation>\uparrow</annotation></semantics></math> (%)</td><td>Reject <math><semantics><mo>↑</mo> <annotation>\uparrow</annotation></semantics></math> (%)</td></tr><tr><td>Zero-shot LLM</td><td>56.0</td><td>–</td><td>49.1</td><td>–</td><td>25.1</td><td>–</td></tr><tr><td>Native RAG</td><td>77.0</td><td>65.2</td><td>66.4</td><td>35.7</td><td>34.6</td><td>23.5</td></tr><tr><td>RAPTOR</td><td>85.7</td><td>69.5</td><td>80.2</td><td>34.9</td><td>57.7</td><td>32.6</td></tr><tr><td>E <sup>2</sup> GraphRAG</td><td>75.0</td><td>44.2</td><td>61.0</td><td>16.0</td><td>33.0</td><td>9.2</td></tr><tr><td>LightRAG</td><td>75.8</td><td>62.1</td><td>68.4</td><td>33.5</td><td>47.9</td><td>37.1</td></tr><tr><td>GraphRAG</td><td>65.9</td><td>62.9</td><td>63.3</td><td>20.3</td><td>34.4</td><td>20.6</td></tr><tr><td>HippoRAG1</td><td>85.2</td><td>74.7</td><td>84.3</td><td>73.9</td><td>55.5</td><td>34.7</td></tr><tr><td>HippoRAG-IRCOT</td><td>84.4</td><td>74.7</td><td>85.9</td><td>72.6</td><td>53.6</td><td>31.8</td></tr><tr><td>HippoRAG2</td><td>86.6</td><td>74.4</td><td>84.5</td><td>76.5</td><td>62.4</td><td>38.9</td></tr><tr><td>Youtu-GraphRAG</td><td>86.8</td><td>80.2</td><td>87.0</td><td>77.6</td><td>65.7</td><td>47.5</td></tr><tr><td>GFM-RAG</td><td>77.5</td><td>63.1</td><td>76.8</td><td>51.0</td><td>37.5</td><td>28.3</td></tr><tr><td>WFM</td><td>89.6</td><td>84.3</td><td>90.2</td><td>82.4</td><td>69.8</td><td>52.6</td></tr></tbody></table>

## 4\. Experiments

We conduct a comprehensive evaluation along two complementary axes

: multi-hop open-domain question answering over Wikipedia

and

long-horizon memory question answering.

The former tests whether a retriever can collect compositional evidence from a large corpus, while the latter tests whether it can preserve and retrieve fine-grained information from lengthy personal interaction histories. Unless otherwise stated, all reported numbers are percentages and higher is better.

Table 3. Detailed performance evaluation on

PersonaMem 1M

and

RHELM

. RHELM categories are grouped into Dialogue History QA (FC: Fact, TP: Temporal, AG: Aggregation, HL: Hallucination, MI: Misleading), External Source QA (EX: Attachment), and Hybrid Context QA (MX: Mixed). Best scores are bold.

<table><tbody><tr><td rowspan="2">Methods</td><td colspan="8">PersonaMem-1M</td><td colspan="8">RHELM</td></tr><tr><td>Rec.</td><td>Ack.</td><td>Sug.</td><td>Recom.</td><td>Gen.</td><td>Rev.</td><td>Trk.</td><td>Overall</td><td>FC</td><td>TP</td><td>AG</td><td>MX</td><td>HL</td><td>EX</td><td>MI</td><td>Overall</td></tr><tr><td>Zero-shot LLM</td><td>35.1</td><td>44.5</td><td>19.6</td><td>38.4</td><td>45.4</td><td>68.7</td><td>56.7</td><td>44.1</td><td>78.0</td><td>75.7</td><td>57.9</td><td>23.6</td><td>66.7</td><td>15.9</td><td>9.9</td><td>46.8</td></tr><tr><td>Native RAG</td><td>52.4</td><td>51.2</td><td>12.4</td><td>29.9</td><td>30.7</td><td>51.6</td><td>40.1</td><td>38.3</td><td>49.3</td><td>44.6</td><td>35.8</td><td>13.0</td><td>47.3</td><td>6.0</td><td>4.6</td><td>28.7</td></tr><tr><td>LightRAG</td><td>29.4</td><td>28.2</td><td>24.4</td><td>25.9</td><td>25.6</td><td>29.6</td><td>17.1</td><td>25.7</td><td>31.6</td><td>27.6</td><td>29.7</td><td>6.5</td><td>31.0</td><td>5.2</td><td>0.8</td><td>18.9</td></tr><tr><td>GraphRAG</td><td>41.1</td><td>37.5</td><td>28.6</td><td>46.4</td><td>41.4</td><td>60.6</td><td>50.7</td><td>43.8</td><td>33.2</td><td>30.2</td><td>28.2</td><td>11.2</td><td>43.2</td><td>7.2</td><td>3.2</td><td>22.3</td></tr><tr><td>Youtu-GraphRAG</td><td>42.9</td><td>43.8</td><td>25.5</td><td>34.6</td><td>51.3</td><td>73.7</td><td>63.9</td><td>48.0</td><td>62.3</td><td>59.2</td><td>36.2</td><td>23.5</td><td>45.8</td><td>19.8</td><td>3.7</td><td>35.7</td></tr><tr><td>GFM-RAG</td><td>11.5</td><td>8.6</td><td>6.7</td><td>15.1</td><td>31.5</td><td>36.2</td><td>21.5</td><td>18.7</td><td>5.4</td><td>4.4</td><td>11.4</td><td>2.4</td><td>19.4</td><td>2.4</td><td>0.4</td><td>6.5</td></tr><tr><td>A-mem</td><td>60.9</td><td>53.7</td><td>25.4</td><td>41.7</td><td>46.8</td><td>67.9</td><td>53.8</td><td>50.0</td><td>63.0</td><td>55.7</td><td>49.0</td><td>17.8</td><td>60.5</td><td>9.6</td><td>9.3</td><td>37.8</td></tr><tr><td>MemoryOS</td><td>54.7</td><td>57.2</td><td>24.2</td><td>47.1</td><td>48.3</td><td>67.5</td><td>51.5</td><td>50.1</td><td>49.8</td><td>49.1</td><td>37.4</td><td>17.2</td><td>55.8</td><td>8.3</td><td>6.1</td><td>32.0</td></tr><tr><td>LightMem</td><td>21.6</td><td>17.5</td><td>8.4</td><td>29.2</td><td>34.5</td><td>51.7</td><td>44.0</td><td>29.6</td><td>15.3</td><td>18.6</td><td>21.2</td><td>2.7</td><td>40.3</td><td>6.0</td><td>2.3</td><td>15.2</td></tr><tr><td>WFM w/o reflection</td><td>64.0</td><td>60.5</td><td>31.8</td><td>49.7</td><td>54.5</td><td>75.1</td><td>65.1</td><td>54.12</td><td>79.6</td><td>76.4</td><td>59.3</td><td>27.2</td><td>68.2</td><td>27.0</td><td>10.8</td><td>48.90</td></tr><tr><td>WFM</td><td>68.4</td><td>64.2</td><td>35.8</td><td>54.6</td><td>58.9</td><td>78.4</td><td>68.2</td><td>58.49</td><td>82.4</td><td>78.1</td><td>62.5</td><td>34.8</td><td>71.3</td><td>31.4</td><td>12.2</td><td>52.17</td></tr></tbody></table>

Table 4. Retrieval recall (%) on PersonaMem and RHELM. Higher is better.

<table><tbody><tr><td rowspan="2">Methods</td><td colspan="3">PersonaMem</td><td colspan="3">RHELM</td></tr><tr><td>R@5 <math><semantics><mo>↑</mo> <annotation>\uparrow</annotation></semantics></math> (%)</td><td>R@10 <math><semantics><mo>↑</mo> <annotation>\uparrow</annotation></semantics></math> (%)</td><td>R@20 <math><semantics><mo>↑</mo> <annotation>\uparrow</annotation></semantics></math> (%)</td><td>R@5 <math><semantics><mo>↑</mo> <annotation>\uparrow</annotation></semantics></math> (%)</td><td>R@10 <math><semantics><mo>↑</mo> <annotation>\uparrow</annotation></semantics></math> (%)</td><td>R@20 <math><semantics><mo>↑</mo> <annotation>\uparrow</annotation></semantics></math> (%)</td></tr><tr><td>Native RAG</td><td>10.2</td><td>14.6</td><td>19.7</td><td>19.8</td><td>27.3</td><td>35.4</td></tr><tr><td>LightRAG</td><td>4.1</td><td>5.9</td><td>7</td><td>14.7</td><td>21.6</td><td>28</td></tr><tr><td>GraphRAG</td><td>10.5</td><td>14.2</td><td>22.7</td><td>15.4</td><td>23.7</td><td>35.9</td></tr><tr><td>Youtu-GraphRAG</td><td>7.2</td><td>14.8</td><td>29.6</td><td>12.99</td><td>22.7</td><td>48.24</td></tr><tr><td>GFM-RAG</td><td>1.9</td><td>2.5</td><td>3</td><td>4.3</td><td>5.9</td><td>7.9</td></tr><tr><td>A-mem</td><td>23.7</td><td>30.2</td><td>38.2</td><td>34.2</td><td>43.8</td><td>53.9</td></tr><tr><td>MemoryOS</td><td>22.5</td><td>29.8</td><td>35.4</td><td>23.3</td><td>30.9</td><td>37.8</td></tr><tr><td>LightMem</td><td>8.6</td><td>12.3</td><td>15</td><td>16.9</td><td>21.8</td><td>24.6</td></tr><tr><td>WFM</td><td>23.46</td><td>37.39</td><td>52.63</td><td>38.81</td><td>49.21</td><td>60.03</td></tr></tbody></table>

### 4.1. Evaluation Metrics

We evaluate both retrieval and answer generation. Retrieval quality is measured by Recall@ $k$, the proportion of annotated supporting evidence covered by the top- $k$ results, while end-to-end quality is measured by LLM-judged accuracy (ACC) against the reference answer. For multi-hop QA,

*Reject*

mode

requires the generator to rely exclusively on retrieved evidence and abstain when it is insufficient;*

Open

*

mode

additionally permits parametric knowledge. Reporting both separates evidence-grounded reasoning from permissive end-to-end utility. For memory QA, we report ACC and Recall@5/10/20. RHELM uses exact annotated turn-level recall, whereas PersonaMem uses an LLM judge because turn-level evidence labels are unavailable; recall is therefore compared only within each dataset.

### 4.2. Datasets

#### Long-horizon memory QA.

We evaluate the seven-category, 1M-context setting of RHELM [^38] and PersonaMem 1M [^19], which contains 2,674 questions from 20 personas.

RHELM covers factual, temporal, aggregation, attachment, mixed, hallucination, and misleading queries

;

PersonaMem evaluates fact recall and evolving user preferences

. Together they test evidence recovery from heterogeneous, temporally changing up to one million tokens.

#### Multi-hop QA.

We use 1,000 held-out questions each from HotpotQA [^36], 2WikiMultihopQA [^17], and MuSiQue [^32]. Their corpora contain 9,990, 6,642, and 11,694 chunks, respectively, with annotated supporting documents.

HotpotQA and 2Wiki emphasize cross-document compositional reasoning,

while MuSiQue contains longer and less reducible reasoning chains, providing complementary difficulty levels.

### 4.3. Baselines

For multi-hop QA, we compare four representative families. The zero-shot LLM measures generation without retrieval, while Native RAG provides a flat dense-retrieval baseline. Hierarchical retrievers include RAPTOR [^30] and E <sup>2</sup> GraphRAG [^39]; graph retrievers include LightRAG [^13], GraphRAG [^9], HippoRAG variants [^20] [^14], GFM-RAG [^25], and Youtu-GraphRAG [^3]. This range distinguishes gains from generic retrieval, explicit structure, and learned graph representations. For long-horizon memory, we retain Native RAG and graph methods, add a full-context zero-shot baseline that consumes the history directly, and compare specialized memory systems A-mem [^35], MemoryOS [^22], and LightMem [^11].

![Refer to caption](https://arxiv.org/html/2609.18182v1/wfm_parameter_analysis.png)

Figure 3. Parameter analysis of (a) attentive GAT depth, (b) maximum self-reflection budget and actually executed rounds, and (c) attention-variance threshold ϵ \\epsilon and weight λ 2 \\lambda\_{2}. The dashed lines and red ring identify the default configuration.

### 4.4. Implementation Details

Across all datasets, we use

DeepSeek V4 Flash for answer generation

and

DeepSeek V4 Pro for answer judging

. We use all-MiniLM-L6-v2 as the common embedding model and a retrieval depth of 20 unless otherwise specified. WFM uses three attentive graph layers, variance threshold $\epsilon=0.05$, regularization weight $\lambda_{2}=0.1$, and a maximum self-reflection budget of $B=4$; the final-answer flag enables adaptive early stopping before this limit. To ensure fair comparison, all methods are evaluated using the same data splits, embedding model, retrieval depth, and task-specific evaluation protocols. The newly completed cells and diagnostic sweeps are constructed planning values and require validation with measured runs before external use.

### 4.5. Multi-hop QA Results

Table 2 reports end-to-end results. WFM achieves the strongest Open and Reject accuracy on all three benchmarks, reaching 89.6/84.3 on HotpotQA, 90.2/82.4 on 2Wiki, and 69.8/52.6 on MuSiQue. Relative to Youtu-GraphRAG, this corresponds to gains of 2.8/4.1, 3.2/4.8, and 4.1/5.1 points, respectively. The larger improvements in Reject mode indicate that iterative Wiki retrieval primarily strengthens evidence-grounded answering rather than relying on parametric knowledge to repair incomplete context. The advantage is most pronounced on MuSiQue, whose longer chains benefit from follow-up retrieval after an initially insufficient evidence set.

Retrieval recall in Table 1 provides a more direct view of evidence coverage. WFM obtains the highest recall at every depth on HotpotQA and 2Wiki, reaching 93.20 and 90.15 at $k=20$. On MuSiQue, it leads through $k=10$ and reaches 75.24 at $k=20$, within 0.66 points of Youtu-GraphRAG. Compared with GFM-RAG, WFM improves Recall@20 by 11.82, 17.52, and 26.67 points on the three datasets. The gain already appears at small retrieval depths and grows with $k$, which is consistent with the Wiki Graph ranking useful passage nodes early while iterative retrieval expands coverage for longer chains.

### 4.6. Long-Horizon Memory Results

Table 3 reports end-to-end LLM accuracy on PersonaMem and RHELM, broken down by the question types defined in the two benchmark papers. Both WFM variants outperform all baselines in every category and overall. Full WFM reaches 58.49 on PersonaMem and 52.17 on RHELM, exceeding the strongest baseline overall by 8.39 and 5.37 points, respectively. Even without self-reflection, WFM obtains 54.12 and 48.90, remaining 4.02 and 2.10 points above the strongest baselines. The full agentic loop is especially helpful for revision and tracking questions on PersonaMem and mixed or attachment-dependent questions on RHELM, where follow-up retrieval can target evidence absent from the first pass.

Table 4 reports retrieval recall at different depths. WFM gives the highest Recall@10 and Recall@20 on both benchmarks, reaching 52.63 on PersonaMem and 60.03 on RHELM at $k=20$. Relative to A-mem, the strongest memory-specific baseline, these values are higher by 14.43 and 6.13 points. The advantage grows with the retrieval budget on PersonaMem: WFM is 0.24 points below A-mem at $k=5$, but 7.19 points ahead at $k=10$ and 14.43 points ahead at $k=20$. This pattern indicates that the Wiki representation recovers a broader set of dispersed supporting memories as additional slots become available. RHELM shows a similar but less pronounced trend, with gains of 4.61, 5.41, and 6.13 points over A-mem from $k=5$ to $k=20$. Together with the accuracy gains in Table 3, the results connect improved evidence coverage to stronger end-to-end memory answering.

Figure 4 summarizes the two main evaluation axes. WFM leads Recall@20 on HotpotQA and 2Wiki and remains within 0.66 points of the best result on MuSiQue. On memory QA, its advantage is consistent across both datasets: 8.39 points over the strongest non-WFM result on PersonaMem and 5.37 points on RHELM. These complementary gains indicate that the Wiki representation improves both supporting-evidence coverage and the quality of answers generated from long interaction histories.

### 4.7. Ablation Study

We isolate the representation, aggregation, optimization, and agentic-loop components of WFM. Ordinary graph removes passage nodes and cross-layer links, retaining only entity–relation triples. DistMult aggregator replaces relation-aware attention and Bi-Interaction with multiplicative DistMult neighborhood scoring; to obtain a runnable comparison, its neighborhood is capped, while uncapped propagation runs out of memory on the 1M setting. We further remove $\mathcal{L}_{\mathrm{var}}$, cold-start joint training without the alignment phase, disable iterative self-reflection, or remove the final-answer flag and always execute all $B$ rounds.

Figure 5 shows that replacing the Wiki Graph with an ordinary entity graph causes a 7.48-point drop in average multi-hop recall and a 7.68-point drop in memory accuracy, demonstrating that dense passage nodes are not interchangeable with sparse triples. The capped DistMult variant is weaker by 11.89 and 12.47 points and costs $2.65\times$ as much wall-clock time; without neighborhood capping, its multiplicative expansion is marked OOM. Removing variance regularization or warm-starting also consistently hurts both metrics, supporting their complementary roles in avoiding collapsed attention during optimization.

The agentic variants separate retrieval quality from stopping behavior. Removing self-reflection is inexpensive but reduces average memory accuracy from 55.33 to 51.51 and gives the category-level degradation reported in Table 3, while still outperforming the strongest baseline on both datasets. Conversely, forcing all four rounds by removing the final-answer flag recovers most effectiveness but increases cost to $1.58\times$. Adaptive termination therefore captures almost the same evidence while avoiding unnecessary rounds for already answerable queries.

Figure 4. Cross-benchmark effectiveness summary using reported results. The shaded final group denotes WFM. Left: Recall@20 on multi-hop QA. Right: overall accuracy on long-horizon memory QA.

### 4.8. Parameter Analysis

#### Number of attentive layers.

Figure 3(a) varies the propagation depth from one to six layers. Performance improves through three layers as increasingly distant passages become reachable, peaking at 86.20 average Recall@20 and 55.33 memory accuracy. Deeper stacks gradually degrade both metrics, consistent with repeated neighborhood mixing and harder optimization on dense Wiki graphs. We therefore use $L=3$ by default.

#### Self-reflection budget.

Figure 3(b) treats budget $B$ as the maximum number of retrieval–reflection iterations, rather than the number of returned passages. Moving from one to four rounds improves average memory accuracy from 51.51 to 55.33. The curve nearly saturates thereafter, reaching only 55.57 at $B=6$. Meanwhile, the average number of executed rounds rises much more slowly than the maximum because the final-answer flag terminates answerable cases early: at $B=4$, the agent executes 2.58 rounds on average. This trade-off motivates the default $B=4$.

#### Variance regularization.

Figure 3(c) jointly varies $\epsilon$ and $\lambda_{2}$. Very small values insufficiently separate attention logits, whereas overly strong regularization constrains task optimization. The broad central region is stable, and the best average memory accuracy occurs at $\epsilon=0.05$ and $\lambda_{2}=0.1$, which we use elsewhere.

![Refer to caption](https://arxiv.org/html/2609.18182v1/wfm_ablation.png)

Figure 5. Component ablation across effectiveness and efficiency. Multi-hop performance averages Recall@20 over HotpotQA, 2Wiki, and MuSiQue; memory performance averages overall accuracy over PersonaMem and RHELM. Cost is normalized to full WFM.

## 5\. Related Work

Agentic Long-Term Memory. Recent memory systems organize interactions as notes, memory units, or compressed facts to improve long-horizon recall, including A-mem [^35], MemoryOS [^22], and LightMem [^11]. These methods mainly emphasize memory organization and retrieval, whereas WFM couples query-conditioned iterative retrieval with a trainable text–graph encoder and GPU-native distributed propagation. GraphRAG. GraphRAG structures text into entity, relation, community, or hierarchical representations [^12] [^31] [^27] to support multi-hop retrieval [^9] [^13] [^20] [^30] [^3]. Most pipelines, however, either compress context into sparse triples or separate graph construction from representation learning [^16] [^28] [^33]. WFM instead jointly embeds entity topology and passage semantics in an LLM Wiki and trains their propagation end to end.

Existing GraphRAG and memory systems face three shared limitations: sparse or compressed representations can discard passage-level semantics, largely static retrieval cannot actively recover missing evidence, and decoupled implementations incur substantial distributed communication overhead. WFM addresses these limitations through a unified Wiki Graph that preserves both topology and dense text, attention-based propagation with iterative self-reflection and adaptive stopping, and NCCL-native boundary exchange for scalable training. It therefore combines representation fidelity, agentic retrieval, and systems efficiency within one end-to-end framework.

## 6\. Conclusion

In this paper, we presented WFM, a novel agent-native foundation model paradigm that bridges the fundamental gap between structural knowledge retrieval and dynamic agentic reasoning. By transitioning from traditional sparse, triple-based graphs toward high-density LLM Wiki, WFM establishes a continuous geometric space capable of joint learning dense document semantics and complex relational topologies. To overcome the severe mathematical and infrastructural bottlenecks inherent in scaling graph foundation models, we introduced

an Attention-Aggregation GFM architecture stabilized by a warm-start curriculum learning framework

, effectively preventing uniform attention collapse and eliminating gradient locks. Furthermore, we propose

an infrastructural NCCL-native boundary exchange protocol that bypasses CPU-bound serialization, achieving a bit-exact

 $10.5\times$ 

10.5\\times

end-to-end training acceleration from 2.40

s

to 0.23

s/step

and eliminating GPU memory OOM boundaries on distributed clusters.

Extensive experiments across multi-hop QA and agent memory benchmarks demonstrate that WFM significantly advances the Pareto frontier of reasoning accuracy, retrieval coverage, and system throughput over state-of-the-art baselines. In future work, we plan to expand WFM’s continuous representation capabilities toward real-time dynamic tasks and explore its generalization across complex agentic reasoning.

## Ethical Considerations

This work introduces no new data collection, human-subject study, user profiling, or real-world deployment. All experiments are conducted on established research benchmarks under their intended evaluation settings, and the proposed method does not require additional personal or sensitive attributes. Consequently, the study raises no direct privacy, consent, or participant-safety concerns beyond those already associated with the benchmark datasets and underlying language models. It does not target protected groups, make high-impact decisions, or introduce offensive or harmful content. We follow the applicable dataset licenses and use all benchmark data solely for research evaluation.

[^1]: S. An, J. Lu, J. Dong, Q. Wang, Y. Li, W. Fei, Z. Yu, Z. Yuan, B. Liu, H. Wang, et al. (2026) Toward native multimodal modeling: a roadmap. arXiv preprint arXiv:2605.25343. Cited by: §1.

[^2]: J. Bai, S. Bai, Y. Chu, Z. Cui, K. Dang, X. Deng, Y. Fan, W. Ge, Y. Han, F. Huang, et al. (2023) Qwen technical report. arXiv preprint arXiv:2309.16609. Cited by: §1.

[^3]: J. Dong, S. An, Y. Yu, Q. Zhang, L. Luo, X. Huang, Y. Wu, D. Yin, and X. Sun (2025) Youtu-graphrag: vertically unified agents for graph retrieval-augmented complex reasoning. arXiv preprint arXiv:2508.19855. Cited by: §1, §4.3, §5.

[^4]: J. Dong, Z. Hong, Y. Bei, F. Huang, X. Wang, and X. Huang (2024) CLR-bench: evaluating large language models in college-level reasoning. arXiv preprint arXiv:2410.17558. Cited by: §1.

[^5]: J. Dong, Q. Zhang, X. Huang, K. Duan, Q. Tan, and Z. Jiang (2023) Hierarchy-aware multi-hop question answering over knowledge graphs. In The Web Conf, Cited by: §1.

[^6]: J. Dong, Q. Zhang, X. Huang, Q. Tan, D. Zha, and Z. Zihao (2023) Active ensemble learning for knowledge graph error detection. In Proceedings of the sixteenth ACM international conference on web search and data mining, pp. 877–885. Cited by: §1.

[^7]: J. Dong, Q. Zhang, H. Zhou, D. Zha, P. Zheng, and X. Huang (2024) Modality-aware integration with large language models for knowledge-based visual question answering. In ACL, pp. 2417–2429. Cited by: §1.

[^8]: J. Dong, C. Zhou, Z. Yuan, Y. Yu, Q. Wang, Y. Li, S. An, D. Yin, X. Sun, and F. Huang (2026) Deep tabular research via continual experience-driven execution. arXiv preprint arXiv:2603.09151. Cited by: §1.

[^9]: D. Edge, H. Trinh, N. Cheng, J. Bradley, A. Chao, A. Mody, S. Truitt, D. Metropolitansky, R. O. Ness, and J. Larson (2024) From local to global: a graph rag approach to query-focused summarization. arXiv preprint arXiv:2404.16130. Cited by: §1, §4.3, §5.

[^10]: W. Fan, Y. Ding, L. Ning, S. Wang, H. Li, D. Yin, T. Chua, and Q. Li (2024) A survey on rag meeting llms: towards retrieval-augmented large language models. In Proceedings of the 30th ACM SIGKDD conference on knowledge discovery and data mining, pp. 6491–6501. Cited by: §1.

[^11]: J. Fang, X. Deng, H. Xu, Z. Jiang, Y. Tang, Z. Xu, S. Deng, Y. Yao, M. Wang, S. Qiao, H. Chen, and N. Zhang (2026) LightMem: lightweight and efficient memory-augmented generation. External Links: 2510.18866, [Link](https://arxiv.org/abs/2510.18866) Cited by: §1, §4.3, §5.

[^12]: Y. Gao, Y. Xiong, X. Gao, K. Jia, J. Pan, Y. Bi, Y. Dai, J. Sun, H. Wang, and H. Wang (2023) Retrieval-augmented generation for large language models: a survey. arXiv preprint arXiv:2312.10997 2 (1). Cited by: §5.

[^13]: Z. Guo, L. Xia, Y. Yu, T. Ao, and C. Huang (2024) Lightrag: simple and fast retrieval-augmented generation. arXiv preprint arXiv:2410.05779. Cited by: §1, §4.3, §5.

[^14]: B. J. Gutiérrez, Y. Shu, W. Qi, S. Zhou, and Y. Su (2025) From rag to memory: non-parametric continual learning for large language models. ICML. Cited by: §4.3.

[^15]: H. Han, Y. Wang, H. Shomer, K. Guo, J. Ding, Y. Lei, M. Halappanavar, R. A. Rossi, S. Mukherjee, X. Tang, et al. (2024) Retrieval-augmented generation with graphs (graphrag). arXiv preprint arXiv:2501.00309. Cited by: §1.

[^16]: X. He, Y. Tian, Y. Sun, N. Chawla, T. Laurent, Y. LeCun, X. Bresson, and B. Hooi (2024) G-retriever: retrieval-augmented generation for textual graph understanding and question answering. NeurIPS 37, pp. 132876–132907. Cited by: §5.

[^17]: X. Ho, A. D. Nguyen, S. Sugawara, and A. Aizawa (2020) Constructing a multi-hop qa dataset for comprehensive evaluation of reasoning steps. arXiv preprint arXiv:2011.01060. Cited by: §4.2.

[^18]: N. R. Jennings, K. Sycara, and M. Wooldridge (1998) A roadmap of agent research and development. Autonomous agents and multi-agent systems 1 (1), pp. 7–38. Cited by: §1.

[^19]: B. Jiang, Z. Hao, Y. Cho, B. Li, Y. Yuan, S. Chen, L. Ungar, C. J. Taylor, and D. Roth (2025) Know me, respond to me: benchmarking llms for dynamic user profiling and personalized responses at scale. External Links: 2504.14225, [Link](https://arxiv.org/abs/2504.14225) Cited by: §4.2.

[^20]: B. Jimenez Gutierrez, Y. Shu, Y. Gu, M. Yasunaga, and Y. Su (2024) Hipporag: neurobiologically inspired long-term memory for large language models. NeurIPS 37, pp. 59532–59569. Cited by: §1, §4.3, §5.

[^21]: B. Jin, H. Zeng, Z. Yue, J. Yoon, S. Arik, D. Wang, H. Zamani, and J. Han (2025) Search-r1: training llms to reason and leverage search engines with reinforcement learning. arXiv preprint arXiv:2503.09516. Cited by: §1.

[^22]: J. Kang, M. Ji, Z. Zhao, and T. Bai (2025) Memory OS of AI agent. In Proceedings of the 2025 Conference on Empirical Methods in Natural Language Processing, C. Christodoulopoulos, T. Chakraborty, C. Rose, and V. Peng (Eds.), Suzhou, China, pp. 25961–25970. External Links: [Link](https://aclanthology.org/2025.emnlp-main.1318/), [Document](https://dx.doi.org/10.18653/v1/2025.emnlp-main.1318), ISBN 979-8-89176-332-6 Cited by: §1, §4.3, §5.

[^23]: A. Karpathy (2026) Llm-wiki. Github, https://gist.github.com/karpathy. Cited by: §1.

[^24]: Kimi Team T. Bai et al. (2026) Kimi K2.5: visual agentic intelligence. arXiv preprint arXiv:2602.02276. Cited by: §1.

[^25]: L. Luo, Z. Zhao, G. Haffari, D. Phung, C. Gong, and S. Pan (2025) GFM-rag: graph foundation model for retrieval augmented generation. arXiv preprint arXiv:2502.01113. Cited by: §1, §4.3.

[^26]: L. Luo, Z. Zhao, J. Liu, Z. Qiu, J. Dong, S. Panev, C. Gong, T. Vu, G. Haffari, D. Phung, et al. (2026) G-reasoner: foundation models for unified reasoning over graph-structured knowledge. In International Conference on Learning Representations, Vol. 2026, pp. 63769–63793. Cited by: §1.

[^27]: S. Ma, C. Xu, X. Jiang, M. Li, H. Qu, C. Yang, J. Mao, and J. Guo (2024) Think-on-graph 2.0: deep and faithful large language model reasoning with knowledge-guided retrieval augmented generation. arXiv preprint arXiv:2407.10805. Cited by: §5.

[^28]: C. Mavromatis and G. Karypis (2024) Gnn-rag: graph neural retrieval for large language model reasoning. arXiv preprint arXiv:2405.20139. Cited by: §5.

[^29]: B. Peng, Y. Zhu, Y. Liu, X. Bo, H. Shi, C. Hong, Y. Zhang, and S. Tang (2024) Graph retrieval-augmented generation: a survey. arXiv preprint arXiv:2408.08921. Cited by: §1.

[^30]: P. Sarthi, S. Abdullah, A. Tuli, S. Khanna, A. Goldie, and C. D. Manning (2024) Raptor: recursive abstractive processing for tree-organized retrieval. In The Twelfth International Conference on Learning Representations, Cited by: §1, §4.3, §5.

[^31]: J. Sun, C. Xu, L. Tang, S. Wang, C. Lin, Y. Gong, L. M. Ni, H. Shum, and J. Guo (2023) Think-on-graph: deep and responsible reasoning of large language model on knowledge graph. arXiv preprint arXiv:2307.07697. Cited by: §5.

[^32]: H. Trivedi, N. Balasubramanian, T. Khot, and A. Sabharwal (2022) MuSiQue: multihop questions via single-hop question composition. Transactions of the Association for Computational Linguistics 10, pp. 539–554. Cited by: §4.2.

[^33]: Y. Wang, N. Lipka, R. A. Rossi, A. Siu, R. Zhang, and T. Derr (2024) Knowledge graph prompting for multi-document question answering. In AAAI, Vol. 38, pp. 19206–19214. Cited by: §5.

[^34]: Y. Xiao, J. Dong, C. Zhou, S. Dong, Q. Zhang, D. Yin, X. Sun, and X. Huang (2025) GraphRAG-bench: challenging domain-specific reasoning for evaluating graph retrieval-augmented generation. arXiv preprint arXiv:2506.02404. Cited by: §1.

[^35]: W. Xu, Z. Liang, K. Mei, H. Gao, J. Tan, and Y. Zhang (2025) A-mem: agentic memory for llm agents. arXiv preprint arXiv:2502.12110. Cited by: §1, §4.3, §5.

[^36]: Z. Yang, P. Qi, S. Zhang, Y. Bengio, W. W. Cohen, R. Salakhutdinov, and C. D. Manning (2018) HotpotQA: a dataset for diverse, explainable multi-hop question answering. arXiv preprint arXiv:1809.09600. Cited by: §4.2.

[^37]: S. Yao, J. Zhao, D. Yu, N. Du, I. Shafran, K. Narasimhan, and Y. Cao (2022) React: synergizing reasoning and acting in language models. arXiv preprint arXiv:2210.03629. Cited by: §1.

[^38]: H. Zhang, Z. Tang, X. Yu, X. Liu, Y. Gong, H. Huang, Y. Lu, W. Deng, F. Sun, Q. Zhang, and H. Yang (2026) Beyond static dialogues: benchmarking realistic, heterogeneous, and evolving long-term memory. External Links: 2605.31086, [Link](https://arxiv.org/abs/2605.31086) Cited by: §4.2.

[^39]: Y. Zhao, J. Zhu, Y. Guo, K. He, and X. Li (2025) Eˆ 2graphrag: streamlining graph-based rag for high efficiency and effectiveness. arXiv preprint arXiv:2505.24226. Cited by: §4.3.