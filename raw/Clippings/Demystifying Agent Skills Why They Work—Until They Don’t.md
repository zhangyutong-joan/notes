---
title: "Demystifying Agent Skills: Why They Work—Until They Don’t"
source: "https://arxiv.org/html/2608.14036v1"
author:
published:
created: 2026-08-24
description: "Agent Skills解读论文"
tags:
  - "clippings"
---
## Demystifying Agent Skills: Why They Work—Until They Don’tThanks: Preprint.

Zhiyuan Jiang <sup>1,∗,‡</sup> Fangrui Huang <sup>3,∗</sup> Hanwen Xing <sup>4</sup> Xander Wu <sup>3</sup> Yipeng Gao <sup>4</sup>  
Rui Cao <sup>5</sup> Mengdi Wang <sup>1,†</sup> Shilong Liu <sup>1,†</sup> Yijiang Li <sup>2,†</sup>  
<sup>1</sup> Princeton University   <sup>2</sup> UC San Diego  <sup>3</sup> Stanford University    
<sup>4</sup> University of Southern California  <sup>5</sup> Johns Hopkins University  
<sup>∗</sup> Equal contribution;  <sup>†</sup> Corresponding authors. <sup>‡</sup> Work done during an internship at Princeton University

###### Abstract

Skills have emerged as a practical and effective approach for enhancing LLM agents at inference time through structured packages of knowledge. However, existing evaluations largely measure whether skills improve aggregated task success, leaving a more fundamental question underexplored: *When do skills help, why do they work, and where do they fail?* Through controlled experiments across various benchmarks, agent harnesses and LLMs, we isolate the effects of representation, outcome annotation, retrieval difficulty, and cross-framework robustness of skills. To further answer this question, we design a contrastive study that combines controlled quantitative experiments with paired trajectory analysis. We normalize 8,135 trial records from controlled experiments and retain 238 valid unique labels from 240 open-coded records. We consolidate these observations into a taxonomy of three high-level categories and twelve skill-use modes: skills work when noisy trajectories become procedural anchors that stabilize execution. Skills improve over Workflow Memory by 6.06 points in matched comparisons. Procedural anchoring accounts for 65.7% of skill cases, versus 4.5% for explicit knowledge injection, showing that skills stabilize action rather than inject missing facts. Retrieval is a separate bottleneck: as pools grow from 5 to 100, actual-use precision falls from 29.6% to 3.3%. Confusable distractors impair offline identification, yet downstream success remains stable; exact ground-truth invocation is neither sufficient nor necessary. Skills fail under brittle assumptions, incompatible contexts, or insufficient adaptation. These findings move evaluation beyond aggregate success rates and guide reliable self-evolving agents.

![Refer to caption](https://arxiv.org/html/2608.14036v1/assets/experimental_pipeline_procmem_skills.png)

(a) Skill-vs-procedural-memory pipeline.

Figure 2: Taxonomy label distribution across trajectory mixtures and experimental arms. Stacked bars show trajectory-level labels for Raw, Workflow Memory, and Skill across the six source-trajectory mixtures from $5s0f$ to $0s5f$. Labels are grouped into three high-level categories; per-mode percentages are reported in Appendix Table 11.

## 1 Introduction

Large language model (LLM) agents are increasingly expected to improve through experience rather than solve each task from scratch. Recent agent systems therefore store and reuse traces of prior execution: environment setup sequences, tool-use patterns, debugging routines, and verification steps that were discovered in earlier runs. This shift is especially appealing for tool-using agents [^49] [^29] [^26] [^36] [^45], where repeated failures often arise not from a lack of high-level reasoning, but from rediscovering the same procedural details again and again.

Among the proposed memory forms, *skills* [^2] have emerged as a particularly compelling abstraction. A skill is not simply a record of past execution, but a compact description of what to do, what to check, and what pitfalls to avoid. Compared to storing raw execution traces or direct workflow memories, skills promise three advantages. They can compress noisy experience into a shorter context, standardize procedural knowledge into a stable format, and potentially transfer that knowledge across related tasks.

Despite the significance of skills, existing work studies skills only through aggregated task success: if a skill-augmented agent solves more tasks, the skill is considered useful. Although such evaluations establish that skills do matter, they reveal little about *why* they matter. In particular, they do not explain what fundamentally changes in an agent’s behavior before and after a skill is loaded, which parts of execution are stabilized by skill guidance, or why the same skill can help one task while harming another. This leaves the field with a largely empirical view of skill design and improvement: skills are often written, retrieved, and revised through heuristic iteration, prompt tuning, or benchmark-specific trial and error, rather than through a principled understanding of what makes a skill genuinely valuable.

We therefore ask *when skills help, why they work, and where they fail*, moving beyond the preliminary question of *whether skills work*. Our key contribution is a taxonomy of skill utility and failure, together with a paired research methodology for making skill effects observable rather than treating them as a black box. At a high level, our method compares matched executions with and without skill access and analyzes where the two runs diverge across the skill-use pipeline, including how prior experience is represented, transferred across agent frameworks, retrieved, and invoked. This contrastive view lets us attribute gains and failures to concrete mechanisms instead of aggregate outcomes alone, and provides a more rigorous foundation for studying skill use and for eventually automating the generation of reliably useful skills.

This perspective suggests that skill utility cannot be understood from end-to-end success alone, but must be analyzed along the stages of the skill-use pipeline. Concretely, we organize our study around four questions: (1) whether representing the same prior experience as a standardized skill differs from injecting it as direct procedural memory; (2) whether skill gains come from the underlying experience itself or from explicit success/failure annotations; (3) whether distilled procedural guidance remains useful when transferred across agent frameworks; and (4) how skill-pool size and confusability affect retrieval and downstream execution.

Through comprehensive controlled experiments and comparative trajectory analysis, we find that skills are most useful when they convert noisy prior experience into compact procedural guidance. The dominant mechanism is not the injection of factual knowledge (4.5%), but *procedural anchoring* (65.7%): skills help agents follow more reliable setup steps, tool sequences, implementation routines and verification checks. Consistent with this view, skills reduce several execution-layer failures, including environment setup errors, output-format mismatches, service-lifecycle failures, and shell-command corruption. In comparison, direct workflow memory exposes a complementary weakness: it preserves useful procedural evidence but carries irrelevant exploration, failed branches, and verbose process noise that can increase timeout and drift.

However, our results also show that skills are not universally beneficial. A skill must still be retrieved, interpreted, and applied in the right context. Our retrieval experiments show that retrieval quality cannot be reduced to top-level selection accuracy alone. Hard negative distractors substantially degrade explicit skill selection, but downstream execution is not determined by retrieval accuracy in a one-to-one manner: selecting the correct skill does not guarantee task success, while related non-ground-truth skills can still provide useful procedural support. This reveals a second failure boundary of skills: even when a useful skill exists in the pool, the agent may fail because the skill is retrieved for the wrong procedural context, invoked only superficially, or insufficient to overcome task-level execution bottlenecks such as timeout, numerical precision, missing dependencies, and brittle implementation requirements.

These findings motivate a lifecycle view of skill use. Skills work when prior experience is distilled into reusable procedural anchors that are retrieved and invoked in compatible contexts. They fail when the distilled guidance is noisy, over-specific, mismatched to the current task, or followed without adaptation. Thus, skill-based self-improvement is not merely a problem of accumulating more memories, but of building agents that can generate, retrieve, and apply procedural abstractions reliably.

Overall, our contributions can be summarized as follows:

- We formulate a systematic analysis of *when skills help, why they work, and where they fail*, shifting skill evaluation from aggregate success rates to the mechanisms by which skills change agent behavior.
- We introduce a contrastive trajectory-analysis methodology for studying skill effects. We normalize 8,135 trial records, perform open coding over 240 sampled trajectories, and consolidate 238 valid unique labels into a taxonomy of three high-level categories and twelve skill-use modes.
- We conduct controlled skill-vs-workflow experiments that isolate how the same prior experience behaves when represented as direct procedural memory or as a distilled skill. Our results show that skills primarily work as procedural anchors, while workflow memory often preserves verbose exploration, failed branches, and process noise.
- We analyze retrieval and downstream execution jointly, showing that retrieval accuracy alone does not explain task success. Skills fail not only when retrieval misses the right artifact, but also when retrieved guidance is procedurally incompatible, weakly invoked, or insufficient for the execution bottleneck.

<table><tbody><tr><th rowspan="2">Agent + Model</th><th rowspan="2">Trajectory Mix</th><td colspan="2">Terminal-Bench-2</td><td colspan="2">SkillsBench</td><td colspan="2">Terminal-Bench-Pro</td></tr><tr><td>Workflow</td><td>Skill</td><td>Workflow</td><td>Skill</td><td>Workflow</td><td>Skill</td></tr><tr><th colspan="2">Codex + GPT-5.3-Codex Raw</th><td colspan="2">0.5935</td><td colspan="2">0.5083</td><td colspan="2">0.5394</td></tr><tr><th rowspan="6">Codex GPT-5.3-Codex</th><th>5s0f</th><td>0.4452</td><td>0.7548</td><td>0.5250</td><td>0.7250</td><td>0.7333</td><td>0.7455</td></tr><tr><th>4s1f</th><td>0.4000</td><td>0.7290</td><td>0.5667</td><td>0.6167</td><td>0.7333</td><td>0.7939</td></tr><tr><th>3s2f</th><td>0.4194</td><td>0.7806</td><td>0.6417</td><td>0.6250</td><td>0.6970</td><td>0.7333</td></tr><tr><th>2s3f</th><td>0.3677</td><td>0.6839</td><td>0.6083</td><td>0.7083</td><td>0.6667</td><td>0.6667</td></tr><tr><th>1s4f</th><td>0.2710</td><td>0.7097</td><td>0.5167</td><td>0.6167</td><td>0.6121</td><td>0.5818</td></tr><tr><th>0s5f</th><td>0.2839</td><td>0.5161</td><td>0.5833</td><td>0.4500</td><td>0.4788</td><td>0.4303</td></tr><tr><th colspan="2">Gemini CLI + Gemini-3.1-Pro-Preview Raw</th><td colspan="2">0.5000</td><td colspan="2">0.4762</td><td colspan="2">0.5615</td></tr><tr><th rowspan="6">Gemini CLI Gemini-3.1-Pro-Preview</th><th>5s0f</th><td>0.6231</td><td>0.7923</td><td>0.5524</td><td>0.7429</td><td>0.5308</td><td>0.6692</td></tr><tr><th>4s1f</th><td>0.5308</td><td>0.7615</td><td>0.5238</td><td>0.6190</td><td>0.6923</td><td>0.6308</td></tr><tr><th>3s2f</th><td>0.6462</td><td>0.7462</td><td>0.5619</td><td>0.6667</td><td>0.6462</td><td>0.5462</td></tr><tr><th>2s3f</th><td>0.6000</td><td>0.7000</td><td>0.5524</td><td>0.6762</td><td>0.6846</td><td>0.5077</td></tr><tr><th>1s4f</th><td>0.5846</td><td>0.6923</td><td>0.4857</td><td>0.6000</td><td>0.5923</td><td>0.5692</td></tr><tr><th>0s5f</th><td>0.5231</td><td>0.4769</td><td>0.4286</td><td>0.4095</td><td>0.4769</td><td>0.4615</td></tr></tbody></table>

Table 1: Task success rates for Workflow Memory and Skill injection across trajectory mixtures. Gray rows denote Raw baselines. Green, red, and unshaded cells indicate values above, below, and equal to the corresponding Raw baseline, respectively; bold marks the row-wise maximum across mixture settings. Mixture labels denote the numbers of successful (s) and failed (f) source trajectories. Terminal-Bench-Pro rates use 130 trials per condition, with infrastructure or verifier errors counted as failures.

## 2 Related Works

### 2.1 Memory Reuse in LLM Agents

Recent work has studied memory as a mechanism for enabling LLM agents to adapt across tasks and interactions. Early systems store and retrieve episodic experiences, reflections, or interaction histories to support future planning and decision-making [^25] [^30] [^33] [^56]. This direction has expanded to structured external memory [^24] [^44], retrieval-augmented experience reuse [^54] [^58] [^51] [^39], procedural-memory management [^4], and task-agnostic memory graphs that compress episodic observations into knowledge-centric structures [^46]. Recent surveys frame agent memory as a write-manage-read loop and identify persistent challenges in consolidation, retrieval, contradiction handling, and evaluation [^53] [^8].

A related line of work shifts from remembering *what happened* to reusing *how to act*. Workflow memories summarize past trajectories into action-level procedures for future tasks [^38] [^9]. Skill-based systems make such procedural knowledge more explicit by storing reusable procedures as first-class artifacts, including executable routines, scripts, skill directories, or hierarchical skill knowledge bases [^23] [^47] [^50] [^35] [^13]. Recent work further studies skill activation and selection during execution [^40] [^55], as well as automatic skill discovery, revision, and evolution through experience [^20] [^1] [^16] [^18] [^12]. However, skills are still often evaluated through aggregate task success, obscuring how they differ from broader procedural memory and why they help or fail in specific executions. We address this gap by comparing skills against procedural memory and attributing their effects to stages of representation, retrieval, invocation, transfer, and abstraction.

### 2.2 Benchmarks for Evaluating Agent Behavior

Existing agent benchmarks provide natural settings for studying agent behavior. General tool-use and computer-use benchmarks evaluate multi-step decision-making, tool invocation, and environment interaction [^37] [^43] [^21] [^6] [^57] [^15] [^7] [^42] [^41] [^27] [^32] [^5] [^48] [^3]. Software and terminal benchmarks [^14] [^34] [^19] [^45] [^36] are particularly relevant because they require long-horizon execution over files, tests, and environment states. Especially, Terminal-Bench [^19] provides realistic command-line tasks with isolated environments and test-based verification, making it well suited for observing whether procedural guidance improves execution.

Recent work further introduces benchmarks that explicitly test agent skills. SkillsBench [^17] measures structured skills across diverse tasks, while SWE-Skills-Bench [^10] studies the marginal utility of skill documents in real-world software-engineering settings. However, these benchmarks mainly report final task success. Our work extends this analysis perspective to skill-based memory by connecting success and failure modes to specific memory decisions: which skill is retrieved, how it is interpreted, and whether its procedural abstraction matches the current task.

## 3 Study Design

### 3.1 Research Questions

*When do skills help, why do they work, and where do they fail?* Rather than treating skill use as a black-box performance improvement, we analyze it as a controlled transformation of prior agent experience into procedural knowledge.

RQ1: How does procedural representation shape experience reuse? Prior executions can be reused either as direct workflow memories or as distilled skills. Both representations expose the agent to procedural experience, but they differ in how that experience is packaged: workflow memory preserves trace-level execution details, while a skill compresses them into a standardized procedural artifact. RQ1 asks how this representational form affects downstream behavior when the underlying trajectories are held fixed. In particular, we compare whether workflow memory and skills both act as procedural anchors, and whether skills provide additional robustness by reducing trace dependence, context burden, or framework-specific coupling.

RQ2: What role do outcome signals play in learning from trajectories? Prior trajectories may help because they contain reusable procedures, or because outcome information indicates which behaviors succeeded or failed. RQ2 isolates the role of these signals by comparing standard settings with no-hint settings, where the same trajectories are used but explicit success/failure annotations are removed. This tests whether the benefit of prior experience comes mainly from procedural content itself or from outcome labels that guide selection, distillation, and use.

RQ3: Does distilled procedural guidance transfer across agent frameworks? Procedural knowledge may be coupled to the prompting style, tool interface, and execution loop of the framework that produced it. RQ3 studies whether workflow memories and skills constructed from trajectories in one agent framework remain useful when evaluated in another. By holding the source experience fixed and changing the target framework, we test whether distillation into skills provides a more portable representation than direct workflow memory.

RQ4: How does skill-pool construction affect retrieval and downstream use? In realistic settings, skills are selected from a library rather than provided directly. RQ4 examines how retrieval quality changes as the skill pool becomes larger or more confusable. We evaluate retrieval both as an isolated skill-selection problem and in downstream execution, varying pool size and distractor type. This lets us distinguish failures caused by not finding the right skill from failures that occur after a skill is available but is applied, adapted, or verified incorrectly.

### 3.2 Experimental Setup

#### Model and benchmark selection.

We evaluate skill use under complementary controlled settings. For the skill-vs-procedural-memory and no-hint studies in RQ1–RQ2, we instantiate the same experimental protocol with two agent–model pairings: Codex + GPT-5.3-Codex and Gemini CLI + Gemini-3.1-Pro-Preview. RQ3 constructs prior-experience artifacts from the primary Codex setting and evaluates their cross-framework transfer in Gemini CLI with Gemini-3.1-Pro-Preview. RQ4 uses Qwen3-Embedding-0.6B [^52] for embedding retrieval, and evaluates explicit selection and downstream execution with Gemini CLI + Gemini-3.1-Pro-Preview and Codex + GPT-5.4. GPT-5.3-Codex was no longer available under the same evaluation access when RQ4 was conducted, so GPT-5.4 was used for the Codex pairing in RQ4. Accordingly, RQ4 is interpreted strictly as a within-pairing comparison among its three independent experiments; its absolute values are not directly compared with the RQ1–RQ3 results, whose Codex experiments use GPT-5.3-Codex. Our evaluation suite combines Terminal-Bench [^19] and SkillsBench [^17]. Downstream execution experiments follow Harbor’s standard evaluation workflow [^11] with $n=5$ unique trials per task and a parallelism of $20$ unless otherwise noted; retrieval-isolation experiments use one query per task–pool setting. In skill-based conditions, skills are placed in the execution environment as reusable procedural resources rather than fully incorporated into the initial context [^2]. The complete agent, model, benchmark and task-split information is provided in Appendix A.1.

### 3.3 Experimental Design

To answer these questions, we design a set of controlled studies, as well as fine-grained trajectory analyses that examine the full skill-use pipeline. Full implementation details can be found in AppendixA.

#### Controlled study of procedural experience representation (RQ1–RQ2).

We first study how prior agent experience becomes reusable procedural knowledge. The key question is whether skills help simply because they expose the agent to past trajectories, or because distilling those trajectories into a standardized procedural form changes how the agent can use them. To isolate this effect, we compare three conditions: *Raw*, which receives no prior experience; *Workflow Memory*, which receives cleaned procedural traces from prior executions; and *Skill*, which receives a standardized SKILL.md distilled from the same workflows.

For each selected task, we collect successful and failed raw trajectories and construct a balanced trajectory pool. We then instantiate a fixed-budget composition grid, varying the source evidence from success-only to failure-only, e.g., $5s0f$ through $0s5f$. For every composition, Workflow Memory and Skill are built from the same selected trajectories and evaluated on the same target tasks. This holds the underlying experience constant while varying only its representation. To separate procedural content from explicit outcome signals during skill construction, we further create *standard* and *no-hint* Skill variants. In the standard setting, success/failure identities are visible to the skill creator; in the no-hint setting, these annotations are removed while preserving the same trajectories and execution protocol.

#### Cross-framework transfer evaluation (RQ3).

RQ3 tests whether procedural knowledge remains useful when moved outside the agent framework in which it was produced. We construct skills and workflow memories from trajectories collected in the primary Codex setting, then evaluate them in Gemini CLI with Gemini-3.1-Pro-Preview. This setting isolates framework transfer: the source experience is fixed, but the target agent differs in prompting style, tool-use interface, and execution behavior. Comparing transferred Skill and Workflow Memory against the target-framework Raw baseline lets us examine whether distilled skills preserve reusable procedural guidance more robustly than direct workflow traces.

#### Controlled study of skill retrieval and downstream execution (RQ4).

RQ4 first evaluates whether a growing and increasingly confusable skill library remains operationally usable during task execution. We make the complete candidate pool available to the agent, without preselecting skills, and measure both the ground-truth overlap of the skills accessed during execution and the final verifier outcome. To characterize whether the relevant skills are also difficult to identify outside the execution setting, we conduct two additional offline diagnostics on matched candidate pools. An embedding retriever ranks skills using task–description similarity, while an agent explicitly selects potentially useful skills without executing the task. These diagnostics are run independently, and their outputs are not passed to the execution experiment. Because the Codex pairing in this study uses GPT-5.4 for availability reasons, all RQ4 results are interpreted as within-pairing comparisons among these three experiments and should not be interpreted as direct model-to-model or cross-RQ comparisons with the GPT-5.3-Codex results reported for RQ1–RQ3.

Throughout, these experiments are denoted Arm 1 (embedding retrieval), Arm 2 (explicit agent selection), and Arm 3 (full-pool real execution), respectively.

All three experiments use the same controlled candidate-pool construction. Each pool contains the task’s ground-truth skill set and distractors; pool size ranges from 5 to 100, and distractors are sampled as random, semantically similar, or dissimilar skills [^28] [^31] [^22]. The resulting measurements characterize complementary aspects of skill use: offline identification quality, execution-time skill access, and downstream task completion. They are compared as independent measurements rather than as sequential stages, and no selection output is transferred from either offline diagnostic to the execution experiment. Full implementation details can be found in Appendix A.7.

(a) Precision across the three independent RQ4 experiments.

(b) Arm 3 skill-use precision and downstream success.

Figure 3: Skill retrieval and execution-time skill use on SkillsBench. Left: precision for the two offline diagnostics. Right: parsed actual-use precision (solid lines) and downstream success (dashed lines) for Arm 3. Curves average over random, similar, and dissimilar pool regimes; outputs are not passed between experiments.

Figure 4: Cross-framework transfer of procedural experience. Prior-experience artifacts constructed in one agent framework are evaluated in another. Dashed lines indicate the target framework’s Raw baseline.

| Mechanism | Meaning |
| --- | --- |
| procedural\_anchor | The artifact gives a usable procedure, ordering, checklist, tool sequence, or verification plan. |
| knowledge\_ injection | The artifact supplies concrete domain knowledge that the agent otherwise lacked. |
| failure\_warning | The artifact warns about a pitfall that the agent avoids. |
| none | The artifact is not used in a meaningful way. |
| counterproductive | The artifact misleads the agent or makes the run worse. |

Table 2: Mechanism labels used to characterize how injected prior experience affects execution.

## 4 Skill-Use Mechanisms: A Contrastive Taxonomy

Aggregate success rates show whether skills help, but do not explain what changes when a skill is available. To make these changes observable, we build a contrastive trajectory-analysis pipeline over the controlled skill-vs-workflow experiments. We first normalize heterogeneous benchmark outputs into a shared manifest of 8,135 trial records, including task identity, execution arm, verifier outcome, injected artifact and trajectory transcript when available. Among these records, 7,837 contain agent transcripts. We then perform an open-coding pass over 240 sampled trajectories, retain 238 valid unique labels, and merge the resulting open-ended failure and success descriptions into a 12-mode canonical taxonomy.

We validate both LLM-assisted stages of this taxonomy construction with an independent human check. For each of the 238 valid raw labels, a human annotator inspected three supporting trajectories, giving 714 trajectory–label checks in total, and confirmed that the raw label was grounded in the recorded agent behavior. The annotator then independently mapped all 238 raw labels to the 12 canonical modes using only the taxonomy definitions. As summarized in Table 3, the human and LLM aggregation assignments achieve 95.8% exact agreement and Cohen’s $\kappa=0.952$. This provides direct evidence that the taxonomy is stable beyond the judgments of a single LLM.

| Validation stage | Evaluation units | Result |
| --- | --- | --- |
| Trajectory grounding | 714 checks (238 labels $\times$ 3 trajectories) | All labels confirmed |
| Taxonomy aggregation | 238 valid unique labels | 95.8% exact; Cohen’s $\kappa=0.952$ |

Table 3: Human validation of the taxonomy construction pipeline. The first stage checks whether raw labels are supported by their source trajectories; the second independently maps those labels to the 12 canonical modes.

The main unit of analysis is a paired triple. Each triple compares the same task and setting under three arms: raw execution, workflow-memory injection, and skill injection. We construct 528 such triples, covering SkillsBench (144), Terminal-Bench 2.0 (186), and Terminal-Bench-Pro (198). This gives 1,584 arm-level mode assignments. For each triple, an LLM judge assigns a taxonomy mode to each arm, records pairwise changes between arms, and identifies whether the injected artifact acts through procedural anchoring, knowledge injection, failure warning, no meaningful use, or counterproductive guidance. This paired design lets us ask not only whether an arm succeeds, but also which behavior changes when the same prior experience is represented as direct workflow memory or as a distilled skill.

At the coarse level, each trajectory is assigned a Skill-use Category (SC), which serves as its top-level taxonomy label. The three SCs group the 12 fine-grained modes summarized in Table 11. SC1 captures successful procedural anchoring, where the agent either succeeds autonomously or prior experience provides useful guidance. SC2 captures execution-layer and verification failures, including environment setup, output formatting, service management, shell execution, algorithmic implementation, and runtime validation. SC3 captures invocation, applicability, and boundary failures, where guidance is present but misused, over-applied, ignored, or constrained by external limits. At the group level, skill arms shift more trajectories into SC1 than workflow memory (326/528 skill-arm SC1 assignments vs. 294/528 for workflow memory), reduce SC2 execution-layer failures relative to raw and workflow memory (124/528 vs. 197/528 and 176/528), but also increase SC3 invocation or boundary failures (78/528 vs. 19/528 for raw). This organization directly decomposes the central question of the paper: when skills help, why they work, and where they fail.

## 5 Findings

### 5.1 Skills work as procedural anchors, not merely external knowledge

Skill-augmented runs achieve the highest oracle-status success rate, with 61.9% success (oracle-status success rate) compared to 59.1% for raw execution and 55.9% for workflow memory. The strongest aggregate effect is therefore not skill over raw execution, but skill over direct workflow memory: skill improves over workflow memory by +6.06 percentage points, with a 95% bootstrap confidence interval of \[+0.76, +11.36\]. This comparison is important because workflow memory and skill are constructed from the same source trajectories. The improvement therefore cannot be attributed merely to giving the agent more prior experience, but rather to how that experience is represented.

The taxonomy supports this interpretation. Under taxonomy-mode grouping, skill arms fall into the successful-procedure class in 61.7% of cases (taxonomy-mode successful-procedure proportion), compared with 59.1% for raw execution and 55.7% for workflow memory. This is closely aligned with the oracle-status success rates, while allowing the judge to mark rare successful trajectories whose dominant behavior is still a failure-recovery pattern. More importantly, the mechanism labels show that skills mainly help through procedural anchoring: procedural\_anchor accounts for 65.7% of skill mechanisms, whereas explicit knowledge\_injection accounts for only 4.5%. Thus, skills usually do not work by supplying missing facts. They work by stabilizing action: which setup steps to run, which tool sequence to follow, what intermediate checks to perform, and which recurring pitfalls to avoid. A concrete matched trajectory example is provided in Appendix A.3.

The success modes make this distinction concrete. In the skill arm, skill\_guided\_success accounts for 61.6% of cases. In the workflow arm, workflow\_guided\_success accounts for 54.5%. This shows that workflow memory can also be useful: raw traces often contain reusable commands, parameter choices, and debugging evidence. However, workflow memory remains closer to the original trajectory and therefore preserves more incidental process, failed attempts, and task-specific details. Skills are more effective when they compress those traces into a cleaner operational procedure.

As an additional check that this effect is not simply caused by any compact procedural hint, we evaluate two lightweight baselines on the 26 selected Terminal-Bench-2 tasks: an instruction-derived short plan and a workflow-derived test-first template. These reach 47.7% and 59.2% success, respectively, below Workflow Memory (62.3%) and substantially below Skill injection (79.2%); full details are provided in Appendix A.8. Appendix A.9 further shows an effectiveness–efficiency trade-off between Skill and Workflow Memory.

### 5.2 Skills improve execution robustness but fall short on tasks requiring reformulation or verification

The clearest practical advantage of skills appears in execution-layer and verification failures. SC2 modes account for 37.3% of raw-arm labels and 33.3% of workflow-arm labels, but only 23.5% of skill-arm labels. This reduction supports the claim that skills are especially useful for operational fragility: they help agents avoid repeated setup mistakes, preserve output constraints, manage services more reliably, and use more robust command patterns.

The strongest example is environment\_ infrastructure\_failure, which drops from 5.3% in raw execution to 1.7% with workflow memory and 0.2% with skills. This pattern suggests that environment and tooling problems are highly skillable. Once a reliable setup sequence, dependency workaround, or path convention has been discovered, it can be encoded as reusable procedural guidance. Similar reductions appear in output\_format\_schema\_mismatch, which decreases from 7.4% in raw execution to 3.2% with skills, and background\_ service\_lifecycle\_failure, which decreases from 2.7% to 0.8%. These failures are not usually caused by missing high-level reasoning; they arise when the agent fails to keep concrete execution constraints active during the run.

However, the taxonomy also shows the boundary of procedural guidance. algorithmic\_ logic\_error remains substantial across arms, at 8.3% for raw execution, 11.0% for workflow memory, and 7.4% for skills. static\_verification\_without\_runtime is similarly persistent, at 12.5% for raw execution, 12.5% for workflow memory, and 11.7% for skills. These modes show that skills do not automatically repair a wrong algorithm or force oracle-aligned validation. Skills improve execution robustness, but they do not eliminate failures that require deeper problem reformulation or stronger runtime verification.

### 5.3 Skills introduce invocation and applicability failures

The same abstraction that makes skills useful also creates a new failure surface. A skill is not self-executing: the agent must decide whether it applies, which parts to follow, how to adapt it, and when to abandon it. This is where many skill-specific failures arise. The mode skill\_guidance\_misapplied\_or\_ignored appears in 10.0% of skill-arm cases, compared with only 0.8% in raw execution and 0.4% in workflow memory. These failures are not simply cases where the skill is absent or irrelevant. Often, the skill contains plausible guidance, but the agent applies it mechanically, misses a condition, or carries over assumptions that no longer hold.

Workflow memory fails differently. Its main penalty is not misapplication of a compact abstraction, but process overload. timeout\_budget\_exhaustion appears in 10.6% of workflow-memory cases, compared with 1.7% in raw execution and 4.4% with skills. This suggests that direct traces can burden the agent with too much procedural residue: long explorations, failed attempts, and low-level debugging paths that distract from the decisive procedure. Skills reduce this overhead through distillation, but they do not eliminate the need for applicability judgment. A failed skill run may therefore reflect not bad skill content, but a failure to decide when and how the skill should govern the current execution.

Together, these patterns refine the interpretation of skill utility. A failed skill run is not always caused by bad skill content, just as a successful skill run is not always caused by the skill. Skill utility depends on a pipeline: prior experience must be distilled into the right level of abstraction, transferred or retrieved for a compatible context, invoked by the agent, and adapted during execution. The taxonomy therefore motivates our cross-framework and retrieval studies: we test whether distilled procedural guidance remains portable across agent frameworks and whether useful skills remain usable when retrieved from a larger or more confusable pool.

### 5.4 Outcome annotations guide skill construction

Figure 5 compares skills created from the same trajectory pools with and without explicit success/failure labels for Codex and Gemini CLI. The complete numerical results are reported in Appendix Table 16.

Figure 5: Effect of outcome labels during skill creation. Panels compare skills created with outcome labels visible (normal) or withheld (no-hint) across trajectory mixtures and benchmarks. Dashed lines indicate the corresponding Raw baselines. Terminal-Bench-Pro entries use 130 trials per condition; missing or infrastructure-error trials count as failures.

For the completed Codex and Gemini rows, withholding outcome labels has little effect when the source pool contains only successful trajectories, but its impact grows sharply once failed trajectories are introduced. As failed trajectories enter the pool, normal skill creation is generally stronger; for Gemini on Terminal-Bench-2 at 3s2f, it reaches 0.7462 versus 0.4000 without outcome hints, and the same pattern holds across all completed Gemini Terminal-Bench-2 and SkillsBench ratios.

### 5.5 Retrieval exposes the gap between skill availability and skill use

We evaluate retrieval on SkillsBench using the benchmark’s ground-truth task–skill annotations. Each task is paired with a controlled candidate pool that contains the ground-truth skill and distractors. RQ4 comprises one downstream execution experiment and two independent offline retrieval diagnostics over matched pools. In the execution experiment, the complete pool is made available to the agent without preselecting skills; we parse the skills accessed during execution and measure their ground-truth overlap together with final task success. The offline diagnostics separately evaluate embedding-based retrieval, which ranks skill descriptions against the task instruction with Qwen3-Embedding-0.6B, and agent selection, which asks the agent to explicitly choose useful skills without executing the downstream task. The diagnostics do not provide inputs to the execution experiment.

Figure 3(b) first reports the independent downstream execution experiment. Gemini’s parsed skill-use precision is low and decreases from 16.9% to 0.7%, while task success remains comparatively flat around 36–39%. Codex starts with higher actual-use precision, 42.3% at pool size 5, but also drops to 5.9% at pool size 100; its task success instead increases from 35.4% to 42.0%. Averaged across the two reported pairings, downstream success changes only from 36.4% to 39.3% while actual-use precision falls from 29.6% to 3.3%. Moreover, Arm 3 recall remains 54.3–73.6% at $k=100$, despite precision being only 0.7–8.1%. This combination indicates that execution-time failure is not simply a failure to inspect any skill: agents often inspect or invoke multiple candidates, but do not reliably restrict use to the task’s annotated ground-truth skill. Thus, exact ground-truth skill invocation is neither sufficient nor strictly necessary for success.

The two offline diagnostics show a different pattern. Figure 3(a) reports average top-1 embedding precision decreasing from 88.3% at pool size 5 to 76.9% at pool size 100, while explicit agent selection decreases from 70.0% to 63.7%. These values are independent measurements, not successive retrieval stages, and no selected skill is passed to the execution experiment. The offline results nevertheless locate the difficulty of identifying the relevant artifact before execution; the execution results above separately show what happens when the full pool is available during task solving.

The composition analysis identifies where offline identification becomes difficult. In Arm 1, top-1 precision on similar pools falls from 70.5% at $k=5$ to 53.4% at $k=100$, compared with 97.7% to 84.1% for random pools and 96.6% to 93.2% for dissimilar pools. The same asymmetry appears in explicit selection: at $k=5$, precision on similar pools is 54.3% for Gemini and 51.9% for Codex; at $k=100$, it is 55.4% and 31.9%, respectively. Thus, pool size contributes to the difficulty, but semantic confusability is the more important stressor for identifying the correct procedural artifact. The relatively high selection recall at $k=100$ (70.5–85.2% across the reported conditions) further suggests that agents often include the ground-truth skill together with distractors rather than failing to consider it at all. A correct skill must ultimately be identified, noticed, adapted, and operationalized, while related non-ground-truth skills may still provide partial procedural support.

Table 4 reports the complete size trend behind the figure. It makes explicit that similar distractors are the dominant stressor for the offline identification diagnostics, whereas Arm 3 precision collapses across all three regimes as the pool grows. Downstream success is comparatively insensitive to this collapse, reinforcing that exact skill-use matching and task completion are independent measurements of different aspects of skill use rather than successive stages of one pipeline.

<table><thead><tr><th colspan="2">Pool / metric</th><th colspan="5">Skill-pool size <math><semantics><mi>k</mi> <annotation>k</annotation></semantics></math></th></tr><tr><th></th><th></th><th>5</th><th>10</th><th>20</th><th>50</th><th>100</th></tr></thead><tbody><tr><th rowspan="4">Random</th><th>Arm 1 P</th><td>97.7</td><td>95.5</td><td>95.5</td><td>92.0</td><td>84.1</td></tr><tr><th>Arm 2 P</th><td>78.1</td><td>77.9</td><td>82.1</td><td>76.5</td><td>69.8</td></tr><tr><th>Arm 3 P</th><td>25.9</td><td>23.2</td><td>19.5</td><td>8.6</td><td>4.4</td></tr><tr><th>Arm 3 Succ.</th><td>31.8</td><td>36.8</td><td>40.1</td><td>36.3</td><td>41.9</td></tr><tr><th rowspan="4">Similar</th><th>Arm 1 P</th><td>70.5</td><td>63.6</td><td>60.2</td><td>56.8</td><td>53.4</td></tr><tr><th>Arm 2 P</th><td>53.1</td><td>52.9</td><td>47.1</td><td>48.6</td><td>43.7</td></tr><tr><th>Arm 3 P</th><td>34.5</td><td>22.3</td><td>15.7</td><td>7.3</td><td>3.7</td></tr><tr><th>Arm 3 Succ.</th><td>41.7</td><td>39.6</td><td>39.2</td><td>39.5</td><td>39.6</td></tr><tr><th rowspan="4">Dissimilar</th><th>Arm 1 P</th><td>96.6</td><td>96.6</td><td>96.6</td><td>94.3</td><td>93.2</td></tr><tr><th>Arm 2 P</th><td>78.9</td><td>81.6</td><td>82.6</td><td>78.4</td><td>77.8</td></tr><tr><th>Arm 3 P</th><td>28.6</td><td>19.2</td><td>9.0</td><td>4.4</td><td>1.7</td></tr><tr><th>Arm 3 Succ.</th><td>35.7</td><td>36.9</td><td>33.7</td><td>38.8</td><td>36.4</td></tr></tbody></table>

Table 4: Effect of pool composition and size on SkillsBench. Entries report percentages for the indicated retrieval arm, pool composition, and pool size. Arms 2 and 3 are arithmetic means over the reported agent–model pairings. Full recall and F1 values are given in Appendix Table 15.

## 6 Conclusion

This paper studies the behavior of skills through controlled experiments and contrastive trajectory analysis, moving beyond aggregate success rates to ask when skills help, why they work, and where they fail. Our results show that skills are most effective as procedural anchors and can also fail when they are retrieved incorrectly, invoked in the wrong context, followed too rigidly, or used on tasks that require deeper reformulation and runtime validation.

Overall, our findings suggest that skill use should be understood as a lifecycle problem rather than a single memory-injection mechanism. Building better self-evolving agents requires not only generating more skills, but also improving how agents represent, retrieve, and leverage procedural knowledge. We hope this analysis provides a foundation for more principled evaluation and design of future skill-based agent systems.

## 7 Limitations

Our evaluation focuses on terminal- and tool-using benchmarks that emphasize multi-step execution, debugging, and verification, and therefore does not cover the full range of agentic behavior, such as long-horizon web interaction or open-ended collaboration. It also evaluates a limited number of agent–model configurations, so the findings may not generalize to other scaffolds, model families, or model versions; we will extend the study to broader settings in future work. Finally, the mechanism taxonomy is derived from a stratified open-coding sample covering approximately 3% of the normalized records rather than exhaustive labeling, so rare behavioral modes may be underrepresented.

## References

## Appendix A Implementation Details

This part provides additional details for the four research questions described in the main text. Across the experiments, we use controlled comparisons designed to isolate representation, outcome annotation, cross-framework transfer, and retrieval difficulty. Unless otherwise stated, all conditions within an experiment share the same target tasks, benchmark interface, agent framework, model, execution harness, and trial budget.

### A.1 Model–Framework Pairings and Benchmarks

We evaluate skill use in both realistic agent-framework deployments and controlled retrieval settings. For RQ1 and RQ2, the skill-vs-procedural-memory and no-hint protocols are implemented for two agent–model pairings: Codex + GPT-5.3-Codex and Gemini CLI + Gemini-3.1-Pro-Preview. RQ3 transfers workflow memories and skills constructed in the primary Codex setting to Gemini CLI with Gemini-3.1-Pro-Preview. RQ4 uses Qwen3-Embedding-0.6B for embedding retrieval and evaluates explicit agent selection and end-to-end execution with Gemini CLI + Gemini-3.1-Pro-Preview and Codex + GPT-5.4. GPT-5.3-Codex was no longer available under the same evaluation access when RQ4 was conducted, so GPT-5.4 was used for its Codex pairing. RQ4 is therefore interpreted only through within-pairing comparisons across its three independent experiments, rather than through direct numerical comparison with RQ1–RQ3.

Our evaluation suite combines Terminal-Bench [^19] and SkillsBench [^17]. RQ1–RQ3 use controlled subsets drawn from the public split of Terminal-Bench Pro, Terminal-Bench 2.0, and SkillsBench. Terminal-Bench Pro provides a 200-task public split from a 400-task benchmark spanning 8 domains; Terminal-Bench 2.0 contains 89 terminal-agent tasks; and SkillsBench contains 86 tasks across 11 domains designed for skill-based procedural reuse. RQ4 uses SkillsBench because it provides native task–skill annotations needed to evaluate retrieval precision and recall. These benchmarks are well suited to our setting because they require multi-step execution, tool use, debugging, service management, output validation, and runtime verification, making many failures procedural rather than purely factual.

Downstream execution experiments follow Harbor’s standard evaluation workflow [^11], with $n=5$ unique trials per task and a parallelism of $20$ unless otherwise noted. Retrieval-isolation arms use one query per task–pool setting because no benchmark execution is performed. For all skill-based execution conditions, we follow a standard agent-skill usage protocol in which skills are placed in the agent’s execution environment as reusable procedural resources, rather than fully inlined into the initial context [^2]. For RQ4, semantic similarity scores used for retrieval and distractor construction are calculated with Qwen3-Embedding-0.6B [^52], a 0.6B-parameter text embedding model from the Qwen3 Embedding series.

### A.2 Dive into Skill-Use Mechanisms: Trajectory Labeling and Comparative Analysis

The analysis is designed to answer a mechanism-level question: *when a prior-experience artifact is injected into an agent, what changes in the resulting trajectory and which failure modes are fixed or introduced?* Unlike aggregate success-rate evaluation, this pipeline treats each agent run as an executable trace. It aligns raw, workflow-memory and skill-injected executions for the same task, asks an LLM judge to compare the trajectories using a fixed taxonomy, and then aggregates the resulting paired labels into mode-level statistics. The complete prompts used for this part can be found in Appendix B.

#### Trajectory Source and Experimental Context

The trajectory corpus is derived from the controlled skill-vs-procedural-memory experiments. All trials were executed through the same benchmark harness, using a fixed agent-model configuration and a fixed task interface. The experiments cover three benchmark sources: Terminal-Bench 2.0, SkillsBench, and Terminal-Bench-Pro. As shown in Table 5, the agent is evaluated under three execution arms for each selected task: Raw, Workflow memory and Skill. The workflow and skill arms are evaluated under six prior-experience compositions, ranging from all successful trajectories to all failed trajectories. These settings allow our analysis to observe how the quality of the underlying experience pool changes the downstream failure modes.

| Arm | Injected prior experience | Purpose |
| --- | --- | --- |
| Raw | No injected prior trajectory or skill | Baseline behavior of the agent on the task. |
| Workflow memory | Cleaned prior workflows are appended as procedural memory | Tests whether direct trajectory-like procedural memory improves execution. |
| Skill | The same prior workflows are distilled into a standardized reusable skill | Tests whether compact skill representation improves over direct workflow memory. |

Table 5: Experimental arms in the contrastive trajectory analysis.

| Artifact | Role in the analysis |
| --- | --- |
| Trial result metadata | Stores task identity, reward, verifier result, exception type, timestamps, token usage, and execution phase durations. |
| Agent trajectory transcript | Stores the terminal/tool-use trajectory and the agent’s reasoning-visible interaction record. |
| Task instruction | Defines the task objective and, for workflow-memory arms, may include injected workflow content. |
| Skill artifact | Stores the injected skill used in the skill arm. |
| Task-side files | Used only as contextual artifacts when present; the main taxonomy labels are based on execution trajectories and verifier outcomes. |

Table 6: Input artifacts used by the taxonomy pipeline.

To make the analysis tractable, the raw execution bundle in Table 6 is not fully mapped to the labeling prompt. Instead, the pre-processing step selectively extracts only the artifacts needed for trajectory analysis: verifier results, agent transcripts, task instructions, injected skills, and task-side configuration or solution metadata when available. This reduces the working corpus from a large raw execution archive to a compact analysis subset while preserving the evidence needed to explain success and failure. After normalization, the manifest contains 8,135 trial records. The distribution can be found in Table 7. The manifest intentionally preserves records even when some auxiliary artifacts are missing. Later labeling stages filter to trials with sufficient evidence, especially an available trajectory transcript.

| Dimension | Count |
| --- | --- |
| Terminal-Bench 2.0 trials | 3,254 |
| Terminal-Bench-Pro trials | 2,993 |
| SkillsBench trials | 1,888 |
| Raw-arm trials | 1,883 |
| Workflow-memory trials | 2,658 |
| Skill-arm trials | 3,594 |
| Successful trials | 4,541 |
| Failed trials | 3,594 |
| Records with available agent transcript | 7,837 |
| Records with available task instruction | 6,210 |
| Skill-arm records with linked skill artifact | 3,570 |

Table 7: Coverage statistics after manifest construction and artifact linking.

#### Manifest Construction and Trial Normalization

The first stage converts heterogeneous benchmark outputs into a unified trial table. Each trial record stores the benchmark, task name, experimental setting, execution arm, reward, exception type, model identifier, timestamps, token metrics, and pointers to the relevant artifacts.

Success and failure are derived from the verifier reward rather than from free-form logs. A positive numeric verifier reward is treated as success; zero, missing, or non-positive reward is treated as failure. This design keeps the taxonomy aligned with the benchmark oracle rather than the agent’s self-assessment.

The manifest builder also resolves the relationship between injected artifacts and trial outputs. For workflow-memory trials, the task instruction may contain the injected workflow memory. For skill trials, the corresponding skill artifact is linked by benchmark, setting, and task. This alignment is necessary because the later LLM judge must see not only what the agent did, but also what prior-experience artifact was available to it.

The implementation records token and duration metadata when present. This enables secondary analyses of context cost, output length, and execution time, although some skill-arm token fields are incomplete in the current exported result metadata. For this reason, the taxonomy analysis relies primarily on trajectory content, verifier outcomes, and paired mode changes.

#### Open Coding of Individual Trajectories

Before applying a fixed taxonomy, the pipeline performs an open-coding stage over sampled individual trajectories. The goal is to induce a vocabulary from actual execution failures rather than impose a generic taxonomy from unrelated settings.

The sampler draws from cells defined by benchmark, setting, arm, and outcome. The default configuration targets 240 trials, with a minimum number of examples per cell and a fixed random seed. This stratification prevents the initial label pool from being dominated by the largest benchmark or by one execution arm.

Each sampled trajectory is passed to Claude Sonnet 4.6 through a headless command-line interface. Tool use is disabled and session persistence is disabled. These choices reduce contamination across labeling calls and force the model to judge only the evidence included in the prompt.

The context budget is fixed before labeling. For individual-trial open coding, the task instruction is truncated to 3000-characters, the skill artifact to 3,000 characters, and the trajectory transcript to a head of 6,000 characters plus a tail of 12,000 characters. The larger tail budget reflects the empirical observation that final errors, verifier-facing decisions, and timeout behavior are usually concentrated near the end of the trajectory. Each LLM call has a 600-second timeout and is cached by trial id so interrupted or resumed runs do not relabel completed trials.

The output schema asks for a short explanation, an open-ended primary mode candidate, secondary factors, evidence spans, skill-effect judgment, and a coarse distinction among missing knowledge, misused knowledge, capability limit, and environmental failure. The open-ended primary\_mode\_candidate field is critical: it allows the initial vocabulary to emerge from the data.

This stage produced 240 raw-label records, of which 238 were retained as valid unique labels for taxonomy induction.

#### Canonical Taxonomy Induction

The second stage converts open-ended labels into a canonical taxonomy. Because a single prompt over all labels would be long and brittle, the pipeline uses a two-round batched induction process.

First, labels are divided into batches of approximately 60 records. For each batch, the LLM proposes a small set of canonical modes and assigns each trajectory to exactly one mode. The prompt asks for specific procedural patterns rather than generic catch-all categories. It explicitly encourages coverage of environment failures, API or library misuse, debugging loops, verification mismatches, timeout, skill-specific behavior, workflow-specific behavior, and successful execution.

Second, batch-level modes are merged into a unified taxonomy. The merge prompt receives only the batch-level mode names, definitions, and counts, then produces a global set of modes and a mapping from every batch mode to one global mode. The local aggregation code then remaps individual assignments deterministically and validates that every trajectory id is assigned once.

The batch prompt asks for 8-14 modes per batch, and the merge prompt asks for 9-14 global modes. This range is a design choice: it prevents the taxonomy from collapsing into overly broad categories, such as the "wrong answer," while also avoiding a long tail of one-off labels that would not support statistical aggregation. The final merge produced 12 canonical modes.

This process yields a taxonomy with 12 modes. The modes are intentionally mixed success/failure modes: the goal is not only to classify why runs fail, but also to distinguish when success is attributable to skill guidance, workflow guidance, or autonomous agent behavior.

#### Paired Contrastive Trajectory Labeling

The main analysis stage compares the trajectories matched for the same task. For each benchmark, setting, and task, the pipeline constructs a triple containing one raw trajectory, one workflow-memory trajectory, and one skill-injected trajectory whenever all three are available. Raw trials are matched by benchmark and task because raw execution does not have a success/failure mixture setting. Workflow and skill trials are matched by benchmark, task, and setting.

The current paired dataset contains 528 triples. As shown in Table 8, every paired record includes all three arms. For each arm, the LLM judge receives the task instruction, the v1 taxonomy, the trial outcome, an excerpt of the agent trajectory, and the injected skill for the skill arm. The prompt asks the judge to output a structured comparison with three levels of information.

| Split | Count |
| --- | --- |
| SkillsBench triples | 144 |
| Terminal-Bench 2.0 triples | 186 |
| Terminal-Bench-Pro triples | 198 |
| Triples per mixture setting | 88 |
| Total triples | 528 |

Table 8: Paired triple sample used for contrastive taxonomy labeling.

First, the judge assigns a v1 mode to each arm and provides an evidence quote. Second, it compares workflow with raw, skill with raw, and skill with workflow. Each comparison records a summary written in natural-language, a categorical net effect, the modes fixed by the treatment, and the modes introduced by the treatment. Third, it labels the mechanism by which the skill or workflow affected execution (Table 2).

The paired-comparison prompt uses a shorter transcript budget than the individual open-coding prompt because it must include up to three trajectories in the same call. The task instruction and the injected skill are each truncated to 3,000 characters, while each trajectory contributes a 4,000-character head and an 8,000-character tail. This preserves the same head-to-tail evidence structure while fitting raw, workflow, and skill evidence into one comparison prompt.

Representative trial selection is deterministic by default: when multiple trials are available for the same task, setting, and arm, the first trial is selected under a stable trial-id ordering. A seeded random policy is also supported for sensitivity checks. The main run uses the deterministic policy to make the paired label set reproducible.

This paired design is the central methodological choice. Instead of asking which failure modes are frequent in isolation, it asks what changed when the representation of prior experience changed. This supports claims such as "skill fixed environment setup failures that raw execution encountered" or "skill introduced a misapplication failure that was absent in raw execution".

### A.3 Paired-Trajectory Example

The following excerpts show Raw, Workflow Memory, and Skill executions for the same SkillsBench task, react-performance-debugging, under the 1s4f setting. Unrelated file inspection and repeated build output are omitted.

Raw execution   (reward 0)

⬇

\[Agent\]

I hit an unexpected regression: /api/products is

returning 500 in the production run. I am checking

server logs now, then I will patch the route so it

stays fast without breaking correctness.

\[Runtime checks\]

api/products run1 total=0.018289 status=500

api/products run2 total=0.014010 status=500

api/checkout run1 total=0.005307 status=200

api/checkout run2 total=0.003592 status=200

\[Agent\]

I found a runtime issue in production mode: client

hydration is not completing. I am rebuilding and

restarting the production server from the latest source.

$ npm run start

Error: listen EADDRINUSE: address already in use:::3000

\[Verifier\]

test\_checkout\_fast PASSED

test\_external\_api\_actually\_called FAILED

AssertionError: Checkout API too fast (7 ms) -

external API may be bypassed

Result: 10 passed, 1 failed

Workflow Memory   (reward 0)

⬇

\[Agent\]

I found the main hotspots: server-side waterfalls on the

API response path, and a very heavy compare page bundle.

I am now implementing targeted fixes.

\[Final checkout patch\]

export async function POST() {

const \[user, config\] = await Promise.all(\[

fetchUserFromService(),

fetchConfigFromService(),

\]);

const profile =

await fetchProfileFromService(user.id);

return NextResponse.json({

success: true,

user: { id: user.id, name: user.name },

profile,

config: { currency: config.currency },

});

}

\[Verifier\]

test\_external\_api\_actually\_called PASSED

test\_checkout\_fast FAILED

AssertionError: Checkout took 915 ms

(should be <800 ms)

Result: 10 passed, 1 failed

Skill   (reward 1)

⬇

\[Injected SKILL.md\]

Eliminate server/API waterfalls:

\- Convert independent awaits to Promise.all.

\- Start promises early, await late.

\- For partially dependent flows, fetch independent data

in parallel, then trigger the dependent fetch as soon

as its prerequisite resolves.

\[Final checkout patch\]

export async function POST() {

const userPromise = fetchUserFromService();

const configPromise = fetchConfigFromService();

const user = await userPromise;

const profilePromise =

fetchProfileFromService(user.id);

const \[config, profile\] = await Promise.all(\[

configPromise,

profilePromise,

\]);

return NextResponse.json({

success: true,

user: { id: user.id, name: user.name },

profile,

config: { currency: config.currency },

});

}

\[Agent runtime measurement\]

POST /api/checkout:

0.722233, 0.709605, 0.713089, 0.710551, 0.713057 s

warm average = 0.711576 s

\[Verifier\]

test\_checkout\_fast PASSED

test\_external\_api\_actually\_called PASSED

test\_cart\_add\_item PASSED

test\_compare\_page\_works PASSED

Result: 11 passed in 11.74 s

Outcome. Raw bypasses the external-service check, Workflow Memory leaves the dependent profile request serialized and exceeds the latency threshold, and Skill starts that request as soon as its prerequisite resolves and passes all 11 tests.

#### Deterministic Aggregation and Statistical Reporting

The final stage aggregates the paired labels without additional LLM calls. It computes per-arm success rates, paired success-rate deltas, mode frequencies, mode-level fixed/introduced counts, mechanism distributions, setting-level trends, benchmark-level trends, and token/duration summaries.

Paired success-rate deltas are computed per triple and summarized with a 1,000-iteration bootstrap confidence interval. As shown in Table 10, the most robust aggregate difference in this taxonomy sample is not skill versus raw, but skill versus direct workflow memory. This is consistent with the paper’s broader claim: *skills are useful because they distill prior trajectories into a more compact and actionable form, while workflow memory can preserve too much noisy process*.

| Arm | Success / total | Success rate |
| --- | --- | --- |
| Raw | 312 / 528 | 59.1% |
| Workflow memory | 295 / 528 | 55.9% |
| Skill | 327 / 528 | 61.9% |

Table 9: Oracle-status success rates across the three execution arms.

| Comparison | Mean paired delta | 95% bootstrap CI |
| --- | --- | --- |
| WM vs Raw | $-0.0322$ | $[-0.0814,+0.0208]$ |
| Skill vs Raw | $+0.0284$ | $[-0.0227,+0.0795]$ |
| Skill vs WM | $+0.0606$ | $[+0.0076,+0.1136]$ |

Table 10: Paired success-rate deltas between execution arms.

#### Reproducibility and Reliability Controls

Several design choices make the pipeline reproducible and auditable. The manifest uses deterministic parsing rules for benchmark, setting, arm, task, and reward. The sampling stage uses a fixed seed and stratified cells. The taxonomy induction stage caches intermediate LLM outputs and validates that every input id is assigned exactly once. The paired-comparison stage caches each task-setting comparison, supports fixed representative-trial selection, and includes a kill switch to avoid producing long runs of invalid labels under rate limits. The final report is deterministic and does not use LLM calls.

The LLM judge is constrained by strict JSON schemas and evidence quotes. Evidence quotes are important because they make a label inspectable: each mode assignment should be traceable to the trajectory, instruction, result metadata, or skill artifact. The paired prompt also exposes the same task under multiple arms, reducing the risk that the judge attributes a failure to skill use when the same failure also appears in raw execution.

There are also limitations. The v1 taxonomy is induced from 238 valid unique labels, then applied to 528 paired triples. Although the trajectory grounding and taxonomy aggregation are independently human-validated (Table 3), the full paired-triple dataset remains LLM-assisted rather than exhaustively human-coded. The representative trial policy selects one trajectory per arm for each task-setting triple, so it does not average all repeated trials. Token metrics are incomplete for some skill-arm runs; we therefore report token cost only on a matched same-task intersection with complete metadata (Appendix A.9), while treating mechanism and mode analyses as the primary evidence for behavioral interpretation.

### A.4 RQ1: Representation of Prior Experience

RQ1 asks whether representing prior experience as a standardized skill differs from injecting the same experience as direct procedural memory. We compare three conditions: *Raw*, *Workflow Memory*, and *Skill*. In Raw, the agent receives no prior experience. In Workflow Memory, the agent receives cleaned procedural memories derived from prior executions. In Skill, the same workflows are distilled into a standardized reusable skill. The central control is that workflow memories and skills are constructed from the same underlying trajectory pool; the manipulated variable is only how that experience is represented and made available to the agent.

We first collect raw terminal and tool-use trajectories on Terminal-Bench 2.0, SkillsBench, and Terminal-Bench Pro under a fixed execution protocol. Within each agent–model pairing, we keep the benchmark interface, task definition, model, agent scaffold, and trial budget constant. The same protocol is instantiated for Codex + GPT-5.3-Codex and Gemini CLI + Gemini-3.1-Pro-Preview. We retain tasks whose raw runs contain both successful and failed trajectories and continue collecting executions until each selected task has a balanced trajectory pool with sufficient successful and failed runs for controlled recomposition. This shared pool serves as the common source for all subsequent Workflow Memory and Skill conditions.

Workflow memories are constructed by cleaning and structuring the trajectories while preserving their procedural flow. Skills are constructed by distilling the same workflows into a standardized SKILL.md representation. Under a fixed experience budget, we systematically vary the composition of successful and failed trajectories and rerun the selected tasks under Raw, Workflow Memory, and Skill conditions. We primarily report task success rate and token/context cost. This setup isolates whether representing the same prior experience as direct procedural memory or as a distilled skill changes downstream execution.

### A.5 RQ2: Outcome Annotation and No-Hint Ablation

RQ2 asks whether the benefits of skills come from the underlying experience itself or from explicitly exposing success/failure outcomes. Starting from the same selected tasks and balanced trajectory pools used in RQ1, we construct *standard* and *no-hint* Skill variants. In the standard setting, success/failure identities remain visible to the skill creator. In the no-hint setting, explicit outcome annotations are removed while the underlying trajectories, task pool, experience budget, and execution protocol remain unchanged.

For Skill, the no-hint variant withholds outcome annotations from the skill-construction stage while keeping the same workflow content and standardized skill format. We then rerun the same tasks under matched conditions and compare success rate and token/context cost across standard and no-hint settings. This design separates the effect of experience content from the effect of explicit annotation of results during skill construction.

### A.6 RQ3: Cross-Framework Transfer

RQ3 evaluates whether reusable procedural knowledge is tied to the framework that produced it. We construct workflow memories and skills from trajectories collected with Codex and GPT-5.3-Codex, then evaluate those fixed artifacts with Gemini CLI and Gemini-3.1-Pro-Preview. The target tasks and source experience are held fixed, while the agent framework changes in prompting style, tool interface, and execution loop.

We compare transferred Workflow Memory and Skill against the Gemini raw baseline across the same trajectory-mixture settings. Because both artifacts originate from the same Codex trajectories, differences between them reflect how directly preserved workflow traces and distilled skills survive the framework shift. This design operationalizes portability as downstream task success under a new agent framework rather than textual similarity between artifacts.

### A.7 RQ4: Skill Retrieval and Downstream Execution

To characterize skill identification and execution on SkillsBench, RQ4 comprises three independent experiments over matched candidate pools: two offline diagnostics and one downstream execution experiment. SkillsBench provides native ground-truth task–skill annotations, which lets us compute precision, recall, and F1 without using downstream task success as a circular proxy for relevance.

For each task $t$, we define the ground-truth skill set $G_{t}$ as the set of canonical skill identifiers attached to $t$ by the benchmark’s native task–skill annotations. We do not infer $G_{t}$ from retrieval outputs, agent success, or the skill descriptions generated in our experiments. Candidate-pool duplicates are removed by canonical skill identifier. For a query or execution trial $i$, let $\widehat{G}_{i}$ be the set of distinct skills selected by the agent or extracted by the execution-time parser. A skill counts as correct only when its canonical identifier occurs in both sets; a useful distractor that is not in $G_{t}$ remains a false positive. Repeated mentions or invocations of the same skill count once.

In Arm 1, *embedding-based retrieval*, we encode the task instruction and each skill description with Qwen3-Embedding-0.6B and rank skills by cosine similarity. The strict setting returns the single nearest skill and reports top-1 precision. We also retain top- $k$ retrieval statistics in the released artifacts, but the main figure reports the single-skill selection setting because it matches the question of whether the retriever can identify the best skill directly.

In Arm 2, *explicit agent selection*, each task is presented with an available\_skills candidate pool and the agent must explicitly choose the skills it would use. The downstream task is not executed. This arm evaluates whether an agent can use task context and skill descriptions to choose helpful skills, without conflating selection with later execution failures. We run this selection protocol with Gemini CLI + Gemini-3.1-Pro-Preview and Codex + GPT-5.4.

In Arm 3, *real execution*, the complete candidate pool is placed in the agent’s execution environment and the agent runs the benchmark task without receiving a preselected skill from either offline diagnostic. After the run, we parse the trajectory to identify which skills were actually inspected or invoked. We then compute precision, recall, and F1 over parsed skill use, together with the benchmark success rate. This arm uses the same two agent–model pairings as Arm 2 and measures whether skills available in the environment are actually operationalized during execution.

For each valid query or trial record, precision and recall are computed from the predicted and gold sets as

$$
P_{i}=\frac{|\widehat{G}_{i}\cap G_{t}|}{|\widehat{G}_{i}|},\qquad R_{i}=\frac{|\widehat{G}_{i}\cap G_{t}|}{|G_{t}|}.
$$

For a condition with $N$ valid records, we aggregate as

$$
P=\frac{1}{N}\sum_{i=1}^{N}P_{i},\qquad R=\frac{1}{N}\sum_{i=1}^{N}R_{i},\qquad F_{1}=\frac{2PR}{P+R}.
$$

Because every selected task has at least one annotated gold skill, $|G_{t}|>0$; an empty predicted set receives $P_{i}=R_{i}=0$, and $F_{1}$ is set to zero when $P+R=0$. For each pool-size and distractor condition, $P$ and $R$ are arithmetic means of the per-record values: Arm 1 and Arm 2 contribute one query record per task–pool setting, whereas Arm 3 contributes one record per task and trial. The reported $F_{1}$ is recomputed from the aggregated $P$ and $R$, rather than averaged from per-record F1 values, and task success is the mean of the binary verifier outcomes. When results are averaged across distractor regimes, the averages are computed from the unrounded condition-level values and rounded to one decimal place only for presentation.

All three experiments share the same candidate-pool construction. Each pool contains the task’s ground-truth skill set and distractors. Pool size varies over 5, 10, 20, 50, and 100. Distractors are sampled under three regimes: random distractors from unrelated skills, similar distractors selected as embedding-space near-neighbors, and dissimilar distractors selected from far-away skills. Thus, the benchmark, task set, ground truth, seed, and pool-size schedule remain fixed; only the evaluation procedure and distractor composition change.

This design measures three complementary aspects of skill use: offline semantic identification, deliberate selection, and execution-time access under a full candidate pool. The experiments are not sequential: correct offline selection is not supplied to the execution run, and execution-time access is not treated as a prerequisite for the offline diagnostics. This distinction is important because correct selection is not guaranteed to produce successful execution, and incorrect exact-ground-truth selection is not always fatal: related non-ground-truth skills can still provide useful procedural guidance.

| SC | Mode | Raw | WF | Skill |
| --- | --- | --- | --- | --- |
| SC1 | skill\_guided\_success | 10.4% | 0.4% | 61.6% |
| SC1 | workflow\_guided\_success | 0.0% | 54.5% | 0.0% |
| SC1 | autonomous\_clean\_success | 48.7% | 0.8% | 0.2% |
| SC2 | environment\_infrastructure\_failure | 5.3% | 1.7% | 0.2% |
| SC2 | output\_format\_schema\_mismatch | 7.4% | 3.8% | 3.2% |
| SC2 | background\_service\_lifecycle\_failure | 2.7% | 2.5% | 0.8% |
| SC2 | shell\_code\_corruption | 1.1% | 1.9% | 0.2% |
| SC2 | algorithmic\_logic\_error | 8.3% | 11.0% | 7.4% |
| SC2 | static\_verification\_without\_runtime | 12.5% | 12.5% | 11.7% |
| SC3 | timeout\_budget\_exhaustion | 1.7% | 10.6% | 4.4% |
| SC3 | skill\_guidance\_misapplied\_or\_ignored | 0.8% | 0.4% | 10.0% |
| SC3 | capability\_or\_safety\_limit | 1.1% | 0.0% | 0.4% |

Table 11: Contrastive skill-use taxonomy over 528 paired triples. SC abbreviates Skill-use Category, the top-level taxonomy label assigned to a trajectory; each SC groups the fine-grained modes listed in the table. Percentages are computed within each arm over the same paired-triple sample. SC1 denotes successful procedural anchoring, SC2 execution-layer and verification failures, and SC3 invocation, applicability, and boundary failures.

### A.8 Lightweight Compact Procedural Baselines

To test whether the observed skill advantage can be explained by compact procedural text alone, we add two lightweight baselines on the same 26 selected Terminal-Bench-2 tasks used in the Gemini CLI + Gemini-3.1-Pro-Preview comparison. Each condition is evaluated with five trials per task, giving 130 trials. The *short-plan* baseline provides a concise instruction-derived plan with three to five high-level steps. The *test-first* baseline provides a workflow-derived validation template that emphasizes success conditions, intermediate checks, and final verification. Both baselines are injected as plain procedural text rather than as reusable SKILL.md artifacts.

| Condition | Source | Success / total | Success rate |
| --- | --- | --- | --- |
| Raw | None | 65 / 130 | 50.0% |
| Short plan | Task instruction | 62 / 130 | 47.7% |
| Test-first template | Workflow | 77 / 130 | 59.2% |
| Workflow Memory | Workflow | 81 / 130 | 62.3% |
| Skill | Workflow | 103 / 130 | 79.2% |

Table 12: Lightweight compact procedural baselines on selected Terminal-Bench-2 tasks. Entries report downstream success for Raw, short-plan, test-first, Workflow Memory, and Skill conditions over 26 tasks with five trials per task.

<table><thead><tr><th colspan="7">Absolute metrics on the matched 83-task intersection</th></tr><tr><th>Representation</th><th>Success</th><th>Input</th><th>Output</th><th>Total</th><th><math><semantics><mi>Δ</mi> <annotation>\Delta</annotation></semantics></math> succ. vs Raw</th><th>Cost profile</th></tr></thead><tbody><tr><td>Raw trajectories</td><td>64.1%</td><td>541.5K</td><td>14.2K</td><td>555.7K</td><td>–</td><td>Full prior traces provide broad evidence but carry the largest context load.</td></tr><tr><td>Workflow Memory</td><td>64.8%</td><td>417.9K</td><td>8.3K</td><td>426.2K</td><td>+0.7 pp</td><td>Most token-efficient representation after cleaning trajectory noise.</td></tr><tr><td>Skill</td><td>69.6%</td><td>511.7K</td><td>9.8K</td><td>521.5K</td><td>+5.5 pp</td><td>Highest success rate, with lower token use than Raw but higher token use than Workflow Memory.</td></tr><tr><th colspan="7">Pairwise trade-offs</th></tr><tr><th>Comparison</th><th><math><semantics><mi>Δ</mi> <annotation>\Delta</annotation></semantics></math> success</th><th><math><semantics><mi>Δ</mi> <annotation>\Delta</annotation></semantics></math> input</th><th><math><semantics><mi>Δ</mi> <annotation>\Delta</annotation></semantics></math> output</th><th><math><semantics><mi>Δ</mi> <annotation>\Delta</annotation></semantics></math> total</th><th>Direction</th><th>Interpretation</th></tr><tr><td>Workflow Memory vs Raw</td><td>+0.7 pp</td><td>-123.6K</td><td>-5.9K</td><td>-129.5K</td><td>cheaper</td><td>Workflow Memory substantially reduces token cost with nearly unchanged success.</td></tr><tr><td>Skill vs Raw</td><td>+5.5 pp</td><td>-29.8K</td><td>-4.4K</td><td>-34.2K</td><td>better and cheaper</td><td>Skill improves success while still reducing token use relative to Raw trajectories.</td></tr><tr><td>Skill vs Workflow Memory</td><td>+4.8 pp</td><td>+93.8K</td><td>+1.5K</td><td>+95.3K</td><td>better but costlier</td><td>Skill trades additional context for stronger execution performance.</td></tr></tbody></table>

Table 13: Matched success and token-cost comparison. Entries are computed on the 83-task intersection with equal task weighting. Token counts are per-task averages reported in thousands (K); “pp” denotes percentage points.

### A.9 Matched Token-Cost Analysis

We report token usage on a matched intersection of 83 tasks for which Raw, Workflow Memory, and Skill runs all contain usable token metadata. To avoid over-weighting tasks with more completed trials, we first average success and token usage within each task and representation, then average across tasks. This same-task comparison keeps the task mix fixed when comparing representation choices.

The result reveals an effectiveness–efficiency trade-off. Workflow Memory is the most token-efficient representation, reducing both input and output tokens relative to Raw trajectories. Skill is not uniformly cheaper than Workflow Memory, but it achieves the highest success rate: it improves over Raw while also reducing token usage, and it trades additional context relative to Workflow Memory for stronger execution performance. We therefore interpret Skill as the more effective representation and Workflow Memory as the more token-efficient one.

## Appendix B Prompts

### B.1 skill-creator.md (Experiment 1)

⬇

You are a skill generator. Given one or more execution traces from an agent completing a task, you will produce a single reusable skill file that captures the repeatable process.

Analyze the traces to identify:

\- What repeatable process was performed

\- The distinct steps (in order)

\- What tools, commands, and libraries were used

\- Common patterns across traces (if multiple traces provided)

\- Failure modes that appeared (if any failed traces are included)

Then write a skill in the following markdown format:

\---

name: {{skill-name}}

description: {{one-line description}}

\---

\# {{Skill Name}}

\## Use This Skill When

\- {{condition 1}}

\- {{condition 2}}

\## Preconditions

\- {{what must be true before starting}}

\## Steps

1\. {{step 1}}

2\. {{step 2}}

...

\## Common Failure Modes To Avoid

\- {{failure mode 1: signal and mitigation}}

\- {{failure mode 2: signal and mitigation}}

\## If A Failure Happens

1\. Stop and inspect the latest output.

2\. Map the error to the failure modes above and apply the fix.

3\. Re-run verification before finishing.

\## Verify

\- {{how to confirm the skill completed successfully}}

Rules:

\- Produce exactly ONE skill, not multiple.

\- The skill should be general enough to apply to similar tasks, not just the exact task in the traces.

\- Steps should be concrete and actionable, not vague.

\- If multiple traces show different approaches, pick the most reliable one.

\- If failed traces are included, extract their failure patterns into the "Common Failure Modes" section.

\- Do not include task-specific file paths or data -- use placeholders.

### B.2 skill-creator-no-hint.md (Experiment 2)

⬇

You are a skill generator. Given one or more execution traces from an agent completing a task, you will produce a single reusable skill file that captures the repeatable process.

Analyze the traces to identify:

\- What repeatable process was performed

\- The distinct steps (in order)

\- What tools, commands, and libraries were used

\- Common patterns across traces (if multiple traces provided)

\- Failure signals and mitigations inferred from observable evidence in traces

Then write a skill in the following markdown format:

\---

name: {{skill-name}}

description: {{one-line description}}

\---

\# {{Skill Name}}

\## Use This Skill When

\- {{condition 1}}

\- {{condition 2}}

\## Preconditions

\- {{what must be true before starting}}

\## Steps

1\. {{step 1}}

2\. {{step 2}}

...

\## Common Failure Modes To Avoid

\- {{failure mode 1: signal and mitigation}}

\- {{failure mode 2: signal and mitigation}}

\## If A Failure Happens

1\. Stop and inspect the latest output.

2\. Map the error to the failure modes above and apply the fix.

3\. Re-run verification before finishing.

\## Verify

\- {{how to confirm the skill completed successfully}}

Rules:

\- Produce exactly ONE skill, not multiple.

\- The skill should be general enough to apply to similar tasks, not just the exact task in the traces.

\- Steps should be concrete and actionable, not vague.

\- If multiple traces show different approaches, pick the most reliable one.

\- Infer likely failure patterns only from observable evidence in the traces (e.g., command outputs, error text, exit status, retries).

\- Do not assume whether any trace is successful or failed unless the evidence supports it.

\- Do not include task-specific file paths or data -- use placeholders.

### B.3 Prompts for Trajectory Labeling and Comparative Analysis

⬇

You are labeling agent trajectories from a controlled study comparing three

conditions on a software-engineering benchmark:

\- raw: no procedural memory, no skill injected

\- workflow: past workflow memories appended to instruction

\- skill: a curated SKILL.md injected into the agent’s environment

The trial outcome is given (success/failure with a reward). Your job is to

explain WHY the trial ended that way, using the trajectory and (when relevant)

the candidate skill or injected workflow. Be concrete; cite tool calls or

output snippets.

Output STRICT JSON only (no preamble, no markdown fences) with this schema:

{

"freeform\_reasoning\_short": "1-2 sentences summarizing what happened",

"primary\_mode\_candidate": "short label, free text, e.g. ’missing python dependency’ or ’agent looped on same failing test’",

"secondary\_factors": \["short label", "..."\],

"evidence\_spans": \[

{"source": "codex.txt" | "result.json" | "instruction.md" | "SKILL.md",

"quote": "verbatim snippet, <=160 chars"}

\],

"skill\_effect\_judgment": "helps" | "neutral" | "hurts" | "not\_applicable",

"skill\_effect\_reason": "one short sentence; for arm!= skill use not\_applicable + ’’",

"capability\_vs\_knowledge": "knowledge\_missing" | "knowledge\_present\_but\_misused" | "capability\_limit" | "environmental"

}

Rules:

\- For arm=raw and arm=workflow trials, skill\_effect\_judgment MUST be "not\_applicable".

\- "primary\_mode\_candidate" should be a noun phrase, not a sentence.

\- Always provide at least one evidence\_span quoting the trajectory or result.

\- If trial succeeded, primary\_mode\_candidate should describe the success path

(e.g. "clean python implementation passed all tests") and capability\_vs\_knowledge

can be "knowledge\_present\_but\_misused" only if the agent recovered from misuse.

⬇

You are mining canonical failure/success modes from agent-trajectory labels.

Each input record (one trajectory) has:

id, benchmark, setting, arm, status,

primary\_mode\_candidate (free text), secondary\_factors,

skill\_effect\_judgment, capability\_vs\_knowledge.

Task: produce a small set of canonical modes (snake\_case names) covering THIS BATCH,

and assign every input id to exactly one mode.

Modes should be specific procedural patterns, not generic catch-alls. Cover:

\- environment/dependency failures

\- API or library misuse

\- debugging-loop / no-progress

\- verification/output-format mismatches

\- timeout / long-horizon failures

\- skill-specific patterns (skill misguidance, skill ignored, skill helped)

\- workflow-specific patterns

\- successful-execution patterns (clean / recovered / skill-guided)

Output STRICT JSON only (no markdown fences):

{

"modes": \[

{"name": "missing\_python\_dependency",

"definition": "1-3 sentences",

"n\_assigned": 17}

\],

"assignments": \[

{"id": "<trial\_id>", "mode": "missing\_python\_dependency", "reason": "one short sentence"}

\]

}

Rules:

\- Every input id MUST appear once in assignments.

\- Mode names in assignments MUST be defined in modes.

\- Aim for 8-14 modes per batch. Prefer fewer, clearer modes over many narrow ones.

Input records:

{INPUT\_RECORDS}

⬇

You are consolidating mode taxonomies from multiple batches into a single

canonical taxonomy.

Each batch proposed a list of modes (name + definition + n\_assigned). Many

batch modes will overlap. Your job: produce a unified set of 9-14 canonical

modes, and a mapping from each batch-level mode name to its unified target.

Output STRICT JSON only (no markdown fences):

{

"modes": \[

{"name": "unified\_snake\_case",

"definition": "1-3 sentences",

"merged\_from\_batch\_modes": \["batch1\_mode\_name", "batch2\_mode\_name"\]}

\],

"batch\_mode\_map": {

"batch1\_mode\_name": "unified\_snake\_case",

"batch2\_mode\_name": "unified\_snake\_case"

}

}

Rules:

\- Every batch mode name that appears in input MUST appear as a key in batch\_mode\_map.

\- Every value in batch\_mode\_map MUST be a name in modes\[\].

\- Aim for 9-14 unified modes total.

\- "merged\_from\_batch\_modes" lists the source-batch names that were folded into each unified mode.

Batch mode lists:

{BATCH\_MODE\_LISTS}

⬇

You compare 3 agent trajectories on the same task across 3 conditions

(raw / workflow-injected / skill-injected) and produce a structured paired analysis.

\---TASK INSTRUCTION (may contain injected workflow text if from workflow arm)---

{TASK\_INSTRUCTION}

\---SHARED MODE TAXONOMY (use these names in ‘mode‘ fields)---

{SHARED\_MODE\_TAXONOMY}

\[ARM=raw\] status={STATUS} reward={REWARD} exception={EXCEPTION\_TYPE}

\---codex.txt (head + tail)---

{RAW\_CODEX\_EXCERPT}

\[ARM=workflow\] status={STATUS} reward={REWARD} exception={EXCEPTION\_TYPE}

\---codex.txt (head + tail)---

{WORKFLOW\_CODEX\_EXCERPT}

\[ARM=skill\] status={STATUS} reward={REWARD} exception={EXCEPTION\_TYPE}

\---INJECTED SKILL.md---

{INJECTED\_SKILL}

\---codex.txt (head + tail)---

{SKILL\_CODEX\_EXCERPT}

Output STRICT JSON only (no markdown fences). Schema:

{

"per\_arm": {

"raw": {"mode": "\<mode name or null if MISSING>", "status": "...", "evidence\_quote": "<=160 chars verbatim or empty>"},

"workflow": {...},

"skill": {...}

},

"deltas": {

"workflow\_vs\_raw": {

"what\_changed": "1-2 sentences",

"net\_effect": "fixed" | "regressed" | "unchanged" | "mixed" | "not\_comparable",

"fixed\_mode": \[\],

"introduced\_mode": \[\]

},

"skill\_vs\_raw": {...same shape...},

"skill\_vs\_workflow": {...same shape...}

},

"skill\_mechanism": "knowledge\_injection | procedural\_anchor | failure\_warning | none | counterproductive",

"skill\_mechanism\_reason": "one sentence",

"workflow\_mechanism": "knowledge\_injection | procedural\_anchor | failure\_warning | none | counterproductive",

"workflow\_mechanism\_reason": "one sentence",

"confidence": "high | medium | low"

}

Rules:

\- Use exact mode names from the taxonomy (snake\_case). If a trial does not fit any, use "other".

\- For MISSING arms, set per\_arm.\<arm> = null and deltas involving that arm to net\_effect="not\_comparable".

\- fixed\_mode / introduced\_mode are mode names that the comparison arm eliminated or newly caused respectively (relative to the baseline arm).

\- evidence\_quote must be verbatim from codex.txt / instruction.md / SKILL.md.

\- skill\_mechanism = "none" if skill content was not used by agent at all.

\- skill\_mechanism = "counterproductive" if skill made the run worse than raw.

## Appendix C Complete Results for Skill Retrieval and Outcome Annotation Ablation

<table><thead><tr><th rowspan="2">Pool</th><th rowspan="2"><math><semantics><mi>k</mi> <annotation>k</annotation></semantics></math></th><th>Top-1</th><th colspan="3">Top-3</th><th colspan="3">Top-5</th></tr><tr><th>P</th><th>P</th><th>R</th><th>F1</th><th>P</th><th>R</th><th>F1</th></tr></thead><tbody><tr><th>Random</th><th>5</th><th>97.7</th><td>33.0</td><td>98.9</td><td>49.4</td><td>–</td><td>–</td><td>–</td></tr><tr><th></th><th>10</th><th>95.5</th><td>32.6</td><td>97.7</td><td>48.9</td><td>19.5</td><td>97.7</td><td>32.6</td></tr><tr><th></th><th>20</th><th>95.5</th><td>32.2</td><td>96.6</td><td>48.3</td><td>19.5</td><td>97.7</td><td>32.6</td></tr><tr><th></th><th>50</th><th>92.0</th><td>32.2</td><td>96.6</td><td>48.3</td><td>19.5</td><td>97.7</td><td>32.6</td></tr><tr><th></th><th>100</th><th>84.1</th><td>30.7</td><td>92.0</td><td>46.0</td><td>19.1</td><td>95.5</td><td>31.8</td></tr><tr><th>Similar</th><th>5</th><th>70.5</th><td>31.8</td><td>95.5</td><td>47.7</td><td>–</td><td>–</td><td>–</td></tr><tr><th></th><th>10</th><th>63.6</th><td>29.2</td><td>87.5</td><td>43.8</td><td>19.3</td><td>96.6</td><td>32.2</td></tr><tr><th></th><th>20</th><th>60.2</th><td>26.9</td><td>80.7</td><td>40.3</td><td>17.5</td><td>87.5</td><td>29.2</td></tr><tr><th></th><th>50</th><th>56.8</th><td>24.2</td><td>72.7</td><td>36.4</td><td>16.4</td><td>81.8</td><td>27.3</td></tr><tr><th></th><th>100</th><th>53.4</th><td>22.7</td><td>68.2</td><td>34.1</td><td>15.7</td><td>78.4</td><td>26.1</td></tr><tr><th>Dissimilar</th><th>5</th><th>96.6</th><td>33.0</td><td>98.9</td><td>49.4</td><td>–</td><td>–</td><td>–</td></tr><tr><th></th><th>10</th><th>96.6</th><td>32.2</td><td>96.6</td><td>48.3</td><td>19.8</td><td>98.9</td><td>33.0</td></tr><tr><th></th><th>20</th><th>96.6</th><td>32.2</td><td>96.6</td><td>48.3</td><td>19.5</td><td>97.7</td><td>32.6</td></tr><tr><th></th><th>50</th><th>94.3</th><td>32.2</td><td>96.6</td><td>48.3</td><td>19.5</td><td>97.7</td><td>32.6</td></tr><tr><th></th><th>100</th><th>93.2</th><td>32.2</td><td>96.6</td><td>48.3</td><td>19.3</td><td>96.6</td><td>32.2</td></tr></tbody></table>

Table 14: Complete Arm 1 embedding-retrieval results on SkillsBench. Entries report ranking metrics from Qwen3-Embedding-0.6B using task–skill-description similarity. Top-5 is omitted for $k=5$ because it covers the full candidate pool.

<table><thead><tr><th rowspan="2">Agent / Model</th><th rowspan="2">Pool</th><th rowspan="2"><math><semantics><mi>k</mi> <annotation>k</annotation></semantics></math></th><th colspan="3">Arm 2: Agent Selection</th><th colspan="4">Arm 3: Real Execution</th></tr><tr><th>P</th><th>R</th><th>F1</th><th>P</th><th>R</th><th>F1</th><th>Succ.</th></tr></thead><tbody><tr><td rowspan="15">Gemini CLI Gemini-3.1-Pro-Preview</td><td>Random</td><td>5</td><td>74.4</td><td>75.0</td><td>74.7</td><td>18.6</td><td>69.4</td><td>29.3</td><td>39.2</td></tr><tr><td>Random</td><td>10</td><td>72.7</td><td>72.7</td><td>72.7</td><td>7.1</td><td>66.4</td><td>12.9</td><td>38.1</td></tr><tr><td>Random</td><td>20</td><td>80.1</td><td>81.8</td><td>81.0</td><td>3.6</td><td>66.0</td><td>6.8</td><td>39.2</td></tr><tr><td>Random</td><td>50</td><td>81.2</td><td>84.1</td><td>82.6</td><td>1.4</td><td>65.8</td><td>2.8</td><td>37.6</td></tr><tr><td>Random</td><td>100</td><td>77.4</td><td>83.0</td><td>80.1</td><td>0.7</td><td>66.0</td><td>1.4</td><td>39.0</td></tr><tr><td>Similar</td><td>5</td><td>54.3</td><td>69.3</td><td>60.9</td><td>17.6</td><td>70.1</td><td>28.1</td><td>38.8</td></tr><tr><td>Similar</td><td>10</td><td>61.3</td><td>79.5</td><td>69.2</td><td>7.0</td><td>67.3</td><td>12.6</td><td>38.5</td></tr><tr><td>Similar</td><td>20</td><td>58.4</td><td>77.3</td><td>66.6</td><td>3.7</td><td>66.2</td><td>6.9</td><td>34.0</td></tr><tr><td>Similar</td><td>50</td><td>59.3</td><td>76.1</td><td>66.7</td><td>1.4</td><td>66.2</td><td>2.7</td><td>36.7</td></tr><tr><td>Similar</td><td>100</td><td>55.4</td><td>73.9</td><td>63.3</td><td>0.7</td><td>66.7</td><td>1.4</td><td>36.1</td></tr><tr><td>Dissimilar</td><td>5</td><td>74.4</td><td>76.1</td><td>75.3</td><td>14.6</td><td>63.2</td><td>23.7</td><td>34.0</td></tr><tr><td>Dissimilar</td><td>10</td><td>80.1</td><td>81.8</td><td>81.0</td><td>8.7</td><td>66.0</td><td>15.3</td><td>38.8</td></tr><tr><td>Dissimilar</td><td>20</td><td>82.4</td><td>83.0</td><td>82.7</td><td>5.1</td><td>65.5</td><td>9.5</td><td>35.6</td></tr><tr><td>Dissimilar</td><td>50</td><td>79.3</td><td>80.7</td><td>80.0</td><td>1.6</td><td>64.4</td><td>3.1</td><td>38.1</td></tr><tr><td>Dissimilar</td><td>100</td><td>83.5</td><td>84.1</td><td>83.8</td><td>0.7</td><td>61.6</td><td>1.5</td><td>34.5</td></tr><tr><td rowspan="15">Codex GPT-5.4</td><td>Random</td><td>5</td><td>81.8</td><td>84.1</td><td>82.9</td><td>33.1</td><td>41.6</td><td>36.8</td><td>24.3</td></tr><tr><td>Random</td><td>10</td><td>83.0</td><td>86.4</td><td>84.6</td><td>39.2</td><td>59.7</td><td>47.3</td><td>35.5</td></tr><tr><td>Random</td><td>20</td><td>84.1</td><td>87.5</td><td>85.8</td><td>35.3</td><td>69.3</td><td>46.8</td><td>40.9</td></tr><tr><td>Random</td><td>50</td><td>71.7</td><td>87.5</td><td>78.8</td><td>15.8</td><td>63.5</td><td>25.4</td><td>35.0</td></tr><tr><td>Random</td><td>100</td><td>62.2</td><td>85.2</td><td>71.9</td><td>8.1</td><td>73.6</td><td>14.6</td><td>44.8</td></tr><tr><td>Similar</td><td>5</td><td>51.9</td><td>81.8</td><td>63.5</td><td>51.3</td><td>72.4</td><td>60.0</td><td>44.5</td></tr><tr><td>Similar</td><td>10</td><td>44.4</td><td>83.0</td><td>57.8</td><td>37.5</td><td>66.0</td><td>47.9</td><td>40.7</td></tr><tr><td>Similar</td><td>20</td><td>35.8</td><td>77.3</td><td>48.9</td><td>27.7</td><td>66.1</td><td>39.1</td><td>44.3</td></tr><tr><td>Similar</td><td>50</td><td>37.8</td><td>76.1</td><td>50.5</td><td>13.1</td><td>61.8</td><td>21.6</td><td>42.3</td></tr><tr><td>Similar</td><td>100</td><td>31.9</td><td>70.5</td><td>43.9</td><td>6.7</td><td>54.3</td><td>11.9</td><td>43.0</td></tr><tr><td>Dissimilar</td><td>5</td><td>83.3</td><td>85.2</td><td>84.3</td><td>42.5</td><td>63.0</td><td>50.7</td><td>37.3</td></tr><tr><td>Dissimilar</td><td>10</td><td>83.0</td><td>85.2</td><td>84.1</td><td>29.7</td><td>61.3</td><td>40.0</td><td>35.0</td></tr><tr><td>Dissimilar</td><td>20</td><td>82.8</td><td>85.2</td><td>84.0</td><td>12.7</td><td>60.5</td><td>21.0</td><td>31.8</td></tr><tr><td>Dissimilar</td><td>50</td><td>77.5</td><td>85.2</td><td>81.2</td><td>7.2</td><td>65.1</td><td>12.9</td><td>39.5</td></tr><tr><td>Dissimilar</td><td>100</td><td>72.0</td><td>85.2</td><td>78.0</td><td>2.7</td><td>60.2</td><td>5.2</td><td>38.2</td></tr></tbody></table>

Table 15: Complete Arm 2 and Arm 3 retrieval results on SkillsBench. Rows correspond to agent–model, distractor regime, and pool size. Arm 2 reports explicit-selection precision, recall, and F1; Arm 3 reports parsed actual-use precision, recall, F1, and downstream success. Dashes indicate excluded entries.

<table><thead><tr><th>Agent + Model</th><th>Benchmark</th><th>Creator</th><th>5s0f</th><th>4s1f</th><th>3s2f</th><th>2s3f</th><th>1s4f</th><th>0s5f</th></tr></thead><tbody><tr><td rowspan="6">Codex GPT-5.3-Codex</td><td rowspan="2">TB2</td><td>normal</td><td>0.7548</td><td>0.7290</td><td>0.7806</td><td>0.6839</td><td>0.7097</td><td>0.5161</td></tr><tr><td>no-hint</td><td>0.7677</td><td>0.7355</td><td>0.5871</td><td>0.4968</td><td>0.5548</td><td>0.3871</td></tr><tr><td rowspan="2">SB</td><td>normal</td><td>0.7250</td><td>0.6167</td><td>0.6250</td><td>0.7083</td><td>0.6167</td><td>0.4500</td></tr><tr><td>no-hint</td><td>0.6667</td><td>0.6417</td><td>0.5583</td><td>0.5000</td><td>0.5083</td><td>0.3500</td></tr><tr><td rowspan="2">TB-Pro</td><td>normal</td><td>0.7455</td><td>0.7939</td><td>0.7333</td><td>0.6667</td><td>0.5818</td><td>0.4303</td></tr><tr><td>no-hint</td><td>0.8364</td><td>0.6606</td><td>0.5758</td><td>0.5152</td><td>0.4848</td><td>0.3758</td></tr><tr><td rowspan="6">Gemini CLI Gemini-3.1-Pro-Preview</td><td rowspan="2">TB2</td><td>normal</td><td>0.7923</td><td>0.7615</td><td>0.7462</td><td>0.7000</td><td>0.6923</td><td>0.4769</td></tr><tr><td>no-hint</td><td>0.4231</td><td>0.4923</td><td>0.4000</td><td>0.3692</td><td>0.5231</td><td>0.4308</td></tr><tr><td rowspan="2">SB</td><td>normal</td><td>0.7429</td><td>0.6190</td><td>0.6667</td><td>0.6762</td><td>0.6000</td><td>0.4095</td></tr><tr><td>no-hint</td><td>0.6190</td><td>0.5143</td><td>0.4095</td><td>0.4190</td><td>0.4095</td><td>0.4000</td></tr><tr><td rowspan="2">TB-Pro</td><td>normal</td><td>0.6692</td><td>0.6308</td><td>0.5462</td><td>0.5077</td><td>0.5692</td><td>0.4615</td></tr><tr><td>no-hint</td><td>0.6154</td><td>0.5769</td><td>0.6385</td><td>0.5923</td><td>0.5692</td><td>0.5154</td></tr></tbody></table>

Table 16: Complete numerical results for the outcome-annotation ablation. Entries report downstream success for skills constructed under the indicated trajectory mixture. normal exposes source-trajectory outcomes during construction; no-hint withholds them. Terminal-Bench-Pro entries use 130 trials per condition, with missing or infrastructure-error trials counted as failures.

[^1]: S. Alzubi, N. Provenzano, J. Bingham, W. Chen, and T. Vu EvoSkill: automated skill discovery for multi-agent systems. External Links: 2603.02766, [Link](https://arxiv.org/abs/2603.02766) Cited by: §2.1.

[^2]: Anthropic Skills: Public Repository for Agent Skills. Note: Accessed: 2026-05-23 External Links: [Link](https://github.com/anthropics/skills) Cited by: §A.1, §1, §3.2.

[^3]: V. Barres, H. Dong, S. Ray, X. Si, and K. Narasimhan $\tau^{2}$ -bench: evaluating conversational agents in a dual-control environment. External Links: 2506.07982, [Link](https://arxiv.org/abs/2506.07982) Cited by: §2.2.

[^4]: M. Belikova, S. Shapkin, I. Shilov, E. Levchenko, O. Goryachev, and M. Burtsev Managing procedural memory in llm agents. External Links: 2606.23127, [Link](https://arxiv.org/abs/2606.23127) Cited by: §2.1.

[^5]: J. Chen, J. Li, Y. Shen, H. Trivedi, Y. Zhang, T. Khot, A. Sabharwal, and N. Balasubramanian AppWorld-ul: a user-level benchmark for interactive coding agents. External Links: 2607.09869, [Link](https://arxiv.org/abs/2607.09869) Cited by: §2.2.

[^6]: X. Deng, Y. Gu, B. Zheng, S. Chen, S. Stevens, B. Wang, H. Sun, and Y. Su Mind2Web: towards a generalist agent for the web. External Links: 2306.06070, [Link](https://arxiv.org/abs/2306.06070) Cited by: §2.2.

[^7]: A. Drouin, M. Andriushchenko, M. Caccia, S. Reddy, D. Bahdanau, and Y. Bengio WorkArena: how capable are web agents at solving common knowledge work tasks?. External Links: 2403.07718, [Link](https://arxiv.org/abs/2403.07718) Cited by: §2.2.

[^8]: P. Du Memory for autonomous llm agents:mechanisms, evaluation, and emerging frontiers. External Links: 2603.07670, [Link](https://arxiv.org/abs/2603.07670) Cited by: §2.1.

[^9]: R. Fang, Y. Liang, X. Wang, J. Wu, S. Qiao, P. Xie, F. Huang, H. Chen, and N. Zhang Memp: exploring agent procedural memory. External Links: 2508.06433, [Link](https://arxiv.org/abs/2508.06433) Cited by: §2.1.

[^10]: T. Han, Y. Zhang, W. Song, C. Fang, Z. Chen, Y. Sun, and L. Hu SWE-skills-bench: do agent skills actually help in real-world software engineering?. External Links: 2603.15401, [Link](https://arxiv.org/abs/2603.15401) Cited by: §2.2.

[^11]: Harbor: A framework for evaluating and optimizing agents and models in container environments External Links: [Link](https://github.com/harbor-framework/harbor) Cited by: §A.1, §3.2.

[^12]: Z. He, H. Lin, B. Han, W. Zhu, H. Fang, B. Wang, X. Zhu, R. Li, and M. Reimherr ReSkill: reinforcement learning for strategic skill recommendation in large language model agents. External Links: 2606.01619, [Link](https://arxiv.org/abs/2606.01619) Cited by: §2.1.

[^13]: Y. Jiang, D. Li, H. Deng, B. Ma, X. Wang, Q. Wang, and G. Yu SoK: agentic skills – concepts, frameworks, and applications. External Links: 2602.20867, [Link](https://arxiv.org/abs/2602.20867) Cited by: §2.1.

[^14]: C. E. Jimenez, J. Yang, A. Wettig, S. Yao, K. Pei, O. Press, and K. Narasimhan SWE-bench: can language models resolve real-world github issues?. External Links: 2310.06770, [Link](https://arxiv.org/abs/2310.06770) Cited by: §2.2.

[^15]: J. Y. Koh, R. Lo, L. Jang, V. Duvvur, M. Lim, P. Huang, G. Neubig, S. Zhou, R. Salakhutdinov, and D. Fried VisualWebArena: evaluating multimodal agents on realistic visual web tasks. External Links: 2401.13649, [Link](https://arxiv.org/abs/2401.13649) Cited by: §2.2.

[^16]: C. Lei, C. Ye, Q. Yang, W. Li, Z. Huang, J. Guo, and Y. Yang SkillEvolBench: benchmarking the evolution from episodic experience to procedural skills for large language model agents. External Links: 2605.24117, [Link](https://arxiv.org/abs/2605.24117) Cited by: §2.1.

[^17]: X. Li, W. Chen, Y. Liu, S. Zheng, X. Chen, Y. He, Y. Li, B. You, H. Shen, J. Sun, S. Wang, B. Li, Q. Zeng, D. Wang, X. Zhao, Y. Wang, R. B. Chaim, Z. Di, Y. Gao, J. He, Y. He, L. Jing, L. Kong, X. Lan, J. Li, S. Li, Y. Li, Y. Lin, X. Liu, X. Liu, H. Lyu, Z. Ma, B. Wang, R. Wang, T. Wang, W. Ye, Y. Zhang, H. Xing, Y. Xue, S. Dillmann, and H. Lee SkillsBench: benchmarking how well agent skills work across diverse tasks. External Links: 2602.12670, [Link](https://arxiv.org/abs/2602.12670) Cited by: §A.1, §2.2, §3.2.

[^18]: H. Lin, P. Li, J. Song, F. Jiang, and T. Zhang MUSE-autoskill: improving complex scientific reasoning in large language models via automatic skill generation. External Links: 2605.27366, [Link](https://arxiv.org/abs/2605.27366) Cited by: §2.1.

[^19]: M. A. Merrill, A. G. Shaw, N. Carlini, B. Li, H. Raj, I. Bercovich, L. Shi, J. Y. Shin, T. Walshe, E. K. Buchanan, J. Shen, G. Ye, H. Lin, J. Poulos, M. Wang, M. Nezhurina, J. Jitsev, D. Lu, O. M. Mastromichalakis, Z. Xu, Z. Chen, Y. Liu, R. Zhang, L. L. Chen, A. Kashyap, J. Uslu, J. Li, J. Wu, M. Yan, S. Bian, V. Sharma, K. Sun, S. Dillmann, A. Anand, A. Lanpouthakoun, B. Koopah, C. Hu, E. Guha, G. H. S. Dreiman, J. Zhu, K. Krauth, L. Zhong, N. Muennighoff, R. Amanfu, S. Tan, S. Pimpalgaonkar, T. Aggarwal, X. Lin, X. Lan, X. Zhao, Y. Liang, Y. Wang, Z. Wang, C. Zhou, D. Heineman, H. Liu, H. Trivedi, J. Yang, J. Lin, M. Shetty, M. Yang, N. Omi, N. Raoof, S. Li, T. Y. Zhuo, W. Lin, Y. Dai, Y. Wang, W. Chai, S. Zhou, D. Wahdany, Z. She, J. Hu, Z. Dong, Y. Zhu, S. Cui, A. Saiyed, A. Kolbeinsson, J. Hu, C. M. Rytting, R. Marten, Y. Wang, A. Dimakis, A. Konwinski, and L. Schmidt Terminal-bench: benchmarking agents on hard, realistic tasks in command line interfaces. External Links: 2601.11868, [Link](https://arxiv.org/abs/2601.11868) Cited by: §A.1, §2.2, §3.2.

[^20]: Q. Mi, Z. Ma, M. Yang, H. Li, Y. Wang, H. Zhang, and J. Wang Skill-pro: learning reusable skills from experience via non-parametric ppo for llm agents. External Links: 2602.01869, [Link](https://arxiv.org/abs/2602.01869) Cited by: §2.1.

[^21]: G. Mialon, C. Fourrier, C. Swift, T. Wolf, Y. LeCun, and T. Scialom GAIA: a benchmark for general ai assistants. External Links: 2311.12983, [Link](https://arxiv.org/abs/2311.12983) Cited by: §2.2.

[^22]: N. Muennighoff, N. Tazi, L. Magne, and N. Reimers MTEB: massive text embedding benchmark. External Links: 2210.07316, [Link](https://arxiv.org/abs/2210.07316) Cited by: §3.3.

[^23]: J. Ni, Y. Liu, X. Liu, Y. Sun, M. Zhou, P. Cheng, D. Wang, E. Zhao, X. Jiang, and G. Jiang Trace2Skill: distill trajectory-local lessons into transferable agent skills. External Links: 2603.25158, [Link](https://arxiv.org/abs/2603.25158) Cited by: §2.1.

[^24]: C. Packer, S. Wooders, K. Lin, V. Fang, S. G. Patil, I. Stoica, and J. E. Gonzalez MemGPT: towards llms as operating systems. External Links: 2310.08560, [Link](https://arxiv.org/abs/2310.08560) Cited by: §2.1.

[^25]: J. S. Park, J. C. O’Brien, C. J. Cai, M. R. Morris, P. Liang, and M. S. Bernstein Generative agents: interactive simulacra of human behavior. External Links: 2304.03442, [Link](https://arxiv.org/abs/2304.03442) Cited by: §2.1.

[^26]: Y. Qin, S. Liang, Y. Ye, K. Zhu, L. Yan, Y. Lu, Y. Lin, X. Cong, X. Tang, B. Qian, S. Zhao, L. Hong, R. Tian, R. Xie, J. Zhou, M. Gerstein, D. Li, Z. Liu, and M. Sun ToolLLM: facilitating large language models to master 16000+ real-world apis. International Conference on Learning Representations. External Links: [Link](https://arxiv.org/abs/2307.16789) Cited by: §1.

[^27]: C. Rawles, A. Li, D. Rodriguez, O. Riva, and T. Lillicrap AndroidWorld: a dynamic benchmarking environment for autonomous agents. External Links: 2405.14573, [Link](https://arxiv.org/abs/2405.14573) Cited by: §2.2.

[^28]: N. Reimers and I. Gurevych Sentence-bert: sentence embeddings using siamese bert-networks. In Proceedings of the 2019 Conference on Empirical Methods in Natural Language Processing and the 9th International Joint Conference on Natural Language Processing, pp. 3982–3992. External Links: [Link](https://aclanthology.org/D19-1410) Cited by: §3.3.

[^29]: T. Schick, J. Dwivedi-Yu, R. Dessì, R. Raileanu, M. Lomeli, L. Zettlemoyer, N. Cancedda, and T. Scialom Toolformer: language models can teach themselves to use tools. Advances in Neural Information Processing Systems. External Links: [Link](https://arxiv.org/abs/2302.04761) Cited by: §1.

[^30]: N. Shinn, F. Cassano, E. Berman, A. Gopinath, K. Narasimhan, and S. Yao Reflexion: language agents with verbal reinforcement learning. External Links: 2303.11366, [Link](https://arxiv.org/abs/2303.11366) Cited by: §2.1.

[^31]: N. Thakur, N. Reimers, A. Rücklé, A. Srivastava, and I. Gurevych BEIR: a heterogeneous benchmark for zero-shot evaluation of information retrieval models. External Links: 2104.08663, [Link](https://arxiv.org/abs/2104.08663) Cited by: §3.3.

[^32]: H. Trivedi, T. Khot, Mausam, A. Sabharwal, and N. Balasubramanian AppWorld: a controllable world of apps and people for benchmarking interactive coding agents. External Links: 2407.18901, [Link](https://arxiv.org/abs/2407.18901) Cited by: §2.2.

[^33]: G. Wang, Y. Xie, Y. Jiang, A. Mandlekar, C. Xiao, Y. Zhu, L. Fan, and A. Anandkumar Voyager: an open-ended embodied agent with large language models. External Links: 2305.16291, [Link](https://arxiv.org/abs/2305.16291) Cited by: §2.1.

[^34]: L. Wang, L. Ramalho, A. Celestino, P. A. Pham, Y. Liu, U. K. Sinha, A. Portillo, O. Osunwa, and G. Maduekwe SWE-bench++: a framework for the scalable generation of software engineering benchmarks from open-source repositories. External Links: 2512.17419, [Link](https://arxiv.org/abs/2512.17419) Cited by: §2.2.

[^35]: T. Wang, Y. Xu, L. Qi, Z. Wei, L. Song, Y. Wang, B. Liang, Q. Wang, J. Gu, and R. Xu SkillX: automatically constructing skill knowledge bases for agents. External Links: 2604.04804, [Link](https://arxiv.org/abs/2604.04804) Cited by: §2.1.

[^36]: X. Wang, Y. Chen, L. Yuan, Y. Zhang, Y. Li, H. Peng, and H. Ji Executable code actions elicit better llm agents. External Links: 2402.01030, [Link](https://arxiv.org/abs/2402.01030) Cited by: §1, §2.2.

[^37]: Z. Wang, Y. Cui, L. Zhong, Z. Zhang, D. Yin, B. Y. Lin, and J. Shang OfficeBench: benchmarking language agents across multiple applications for office automation. External Links: 2407.19056, [Link](https://arxiv.org/abs/2407.19056) Cited by: §2.2.

[^38]: Z. Z. Wang, J. Mao, D. Fried, and G. Neubig Agent workflow memory. External Links: 2409.07429, [Link](https://arxiv.org/abs/2409.07429) Cited by: §2.1.

[^39]: J. Wu, Y. He, O. Irsoy, C. Tosh, A. Stolfo, S. Li, Y. Zhang, S. Ouyang, K. Paster, G. Neubig, and D. Wadden Procedural knowledge at scale improves reasoning. External Links: 2604.01348, [Link](https://arxiv.org/abs/2604.01348) Cited by: §2.1.

[^40]: P. Xia, J. Chen, H. Wang, J. Liu, K. Zeng, Y. Wang, S. Han, Y. Zhou, X. Zhao, H. Chen, Z. Zheng, C. Xie, and H. Yao SkillRL: evolving agents via recursive skill-augmented reinforcement learning. External Links: 2602.08234, [Link](https://arxiv.org/abs/2602.08234) Cited by: §2.1.

[^41]: T. Xie, D. Zhang, J. Chen, X. Li, S. Zhao, R. Cao, T. J. Hua, Z. Cheng, D. Shin, F. Lei, Y. Liu, Y. Xu, S. Zhou, S. Savarese, C. Xiong, V. Zhong, and T. Yu OSWorld: benchmarking multimodal agents for open-ended tasks in real computer environments. External Links: 2404.07972, [Link](https://arxiv.org/abs/2404.07972) Cited by: §2.2.

[^42]: F. F. Xu, Y. Xie, M. Liu, F. Neu, B. Li, Z. Wang, L. Y. Jiang, B. Haddar, X. Qin, S. Mukherjee, Z. Durumeric, D. Song, and G. Neubig TheAgentCompany: benchmarking llm agents on consequential real world tasks. External Links: 2412.14161, [Link](https://arxiv.org/abs/2412.14161) Cited by: §2.2.

[^43]: Q. Xu, F. Hong, B. Li, C. Hu, Z. Chen, and J. Zhang On the tool manipulation capability of open-source large language models. External Links: 2305.16504, [Link](https://arxiv.org/abs/2305.16504) Cited by: §2.2.

[^44]: W. Xu, Z. Liang, K. Mei, H. Gao, J. Tan, and Y. Zhang A-mem: agentic memory for llm agents. External Links: 2502.12110, [Link](https://arxiv.org/abs/2502.12110) Cited by: §2.1.

[^45]: J. Yang, C. E. Jimenez, A. Wettig, K. Lieret, S. Yao, K. Narasimhan, and O. Press SWE-agent: agent-computer interfaces enable automated software engineering. External Links: 2405.15793, [Link](https://arxiv.org/abs/2405.15793) Cited by: §1, §2.2.

[^46]: K. Yang, Z. Chen, X. He, J. Jiang, M. Galley, C. Wang, J. Gao, J. Han, and C. Zhai PlugMem: a task-agnostic plugin memory module for llm agents. External Links: 2603.03296, [Link](https://arxiv.org/abs/2603.03296) Cited by: §2.1.

[^47]: Y. Yang, Z. Sun, and A. Yan AutoSkill: experience-driven lifelong learning via skill self-evolution. External Links: 2603.01145, [Link](https://arxiv.org/abs/2603.01145) Cited by: §2.1.

[^48]: S. Yao, N. Shinn, P. Razavi, and K. Narasimhan $\tau$ -bench: a benchmark for tool-agent-user interaction in real-world domains. External Links: 2406.12045, [Link](https://arxiv.org/abs/2406.12045) Cited by: §2.2.

[^49]: S. Yao, J. Zhao, D. Yu, N. Du, I. Shafran, K. Narasimhan, and Y. Cao ReAct: synergizing reasoning and acting in language models. International Conference on Learning Representations. External Links: [Link](https://arxiv.org/abs/2210.03629) Cited by: §1.

[^50]: J. Zhang, H. Huang, X. Jin, Y. Song, C. Li, Y. Ni, J. Yan, and K. Gai MemSkill: learning and evolving memory skills for self-evolving agents. External Links: 2606.20041, [Link](https://arxiv.org/abs/2606.20041) Cited by: §2.1.

[^51]: X. Zhang, C. Ross, M. Rohaninejad, Y. Du, J. F. Santos, Y. Chandak, G. Inigo, C. Iverson, E. Hughes, Z. Yu, S. Z. Shen, M. Belkin, and A. Lamb Agentic context engineering: eliciting long horizon skills from frontier language models. External Links: 2510.04618, [Link](https://arxiv.org/abs/2510.04618) Cited by: §2.1.

[^52]: Y. Zhang, M. Li, D. Long, X. Zhang, H. Lin, B. Yang, P. Xie, A. Yang, D. Liu, J. Lin, F. Huang, and J. Zhou Qwen3 embedding: advancing text embedding and reranking through foundation models. External Links: 2506.05176, [Link](https://arxiv.org/abs/2506.05176) Cited by: §A.1, §3.2.

[^53]: Z. Zhang, X. Bo, C. Ma, R. Li, X. Chen, Q. Dai, J. Zhu, Z. Dong, and J. Wen A survey on the memory mechanism of large language model based agents. External Links: 2404.13501, [Link](https://arxiv.org/abs/2404.13501) Cited by: §2.1.

[^54]: A. Zhao, D. Huang, Q. Xu, M. Lin, Y. Liu, and G. Huang ExpeL: llm agents are experiential learners. External Links: 2308.10144, [Link](https://arxiv.org/abs/2308.10144) Cited by: §2.1.

[^55]: Y. Zheng, Z. Zhang, C. Ma, Y. Yu, J. Zhu, Y. Wu, T. Xu, B. Dong, H. Zhu, R. Huang, and G. Yu SkillRouter: skill routing for llm agents at scale. External Links: 2603.22455, [Link](https://arxiv.org/abs/2603.22455) Cited by: §2.1.

[^56]: W. Zhong, L. Guo, Q. Gao, H. Ye, and Y. Wang MemoryBank: enhancing large language models with long-term memory. External Links: 2305.10250, [Link](https://arxiv.org/abs/2305.10250) Cited by: §2.1.

[^57]: S. Zhou, F. F. Xu, H. Zhu, X. Zhou, R. Lo, A. Sridhar, X. Cheng, T. Ou, Y. Bisk, D. Fried, U. Alon, and G. Neubig WebArena: a realistic web environment for building autonomous agents. External Links: 2307.13854, [Link](https://arxiv.org/abs/2307.13854) Cited by: §2.2.

[^58]: T. Zhou, Y. Song, Y. Qiu, C. Wang, J. Hu, C. D. Hubbs, and J. Zhao Memento: fine-tuning llm agents without fine-tuning llms. External Links: 2508.16153, [Link](https://arxiv.org/abs/2508.16153) Cited by: §2.1.