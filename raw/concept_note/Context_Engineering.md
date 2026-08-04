# 怎么设计
## 缓存机制
- **KV Cache**：在一次推理过程中，缓存已计算的 token 的键值对，避免重复计算。
- **Prompt Cache** ：是 API 服务层的优化——跨多次 API 请求之间，缓存相同前缀的计算结果。
在设计上下文时，两个层级的缓存都要求前缀稳定。**一条铁律：前缀里改一个字节，后面的缓存就全废。**
## 设计上下文原则
在设计上下文时，把最关键的信息放在开头或结尾。即：
- **系统提示词和工具定义一旦确定就不要改。**
- **动态信息永远追加到末尾**——时间戳、用户状态等变化的内容，作为新消息追加到对话末尾，而不是修改已有的系统提示词。
- **使用标准 API 格式，不要自行拼接消息**：至于缓存——它只认 token 字节序列，只要拼出的前缀字节级稳定，照样能命中；但若拼接方式不稳定（如每次向前缀注入动态内容），缓存也会随之失效。**Chat Template**解释了**KV Cache 为什么对前缀如此敏感**。Chat Template 将 system 消息和工具定义转换为固定的 token 序列放在最前面。

**常见的错误上下文管理模式**
1. **动态系统提示词**是最常见的错误之一。正确的做法是将时间信息作为用户消息的一部分追加到对话末尾，或者只在真正需要时通过工具调用来获取。
2. **滑动窗口（Sliding Window）对话历史**通过只保留最近几条消息来控制上下文长度。举个例子：如果窗口大小设为 10 条消息，那么第 11 条消息进来时，最早的一条就会被丢弃。这种做法存在两个严重的问题。第一，它会破坏上下文的前缀一致性，导致 KV Cache 失效。第二，它可能丢失关键的工具调用结果。
## 缓存机制影响Agent架构选择
缓存一致性会反过来主导系统的架构选择。架构设计决策遵循：
1. **提示词的结构由缓存边界决定**。系统提示词在物理上被一个缓存边界标记一分为二——标记之前的内容可以跨用户、跨会话进行全局缓存，标记之后的内容则包含用户和会话的特定信息。这意味着提示词的排列顺序首先由缓存的经济性决定，其次才是语义逻辑。
2. **子 Agent 必须与父 Agent 字节级对齐**。当主 Agent 派生子 Agent 或进行旁路查询时，子 Agent 的提示词、工具定义、模型配置、消息前缀和思考配置必须与父 Agent 的缓存键逐字节匹配。这样做的原因是：子 Agent 发起的 API 请求如果前缀与父 Agent 的请求一致，就能命中 API 服务商的 Prompt Cache，从而减少计费和延迟。这个约束从缓存层向上传导，影响了 Agent 的生成方式和参数传递机制。
3. **工具结果的替换字符串在首次出现时就被冻结**。当大型工具输出被替换为摘要预览时，替换后的字符串会被持久化保存。即使后续会话重启，系统也会使用完全相同的替换字符串——以保证恢复后的消息序列与缓存中的字节流一致，避免缓存失效。
## 上下文学习
**模型的长思维链能力和工具调用能力都对上下文学习（In-Context Learning）能力有很强的依赖**——所谓上下文学习，是指模型不需要重新训练，仅凭输入中给出的指令和示例就能适应新任务的能力。
# 上下文放什么
## 提示工程
提示工程（Prompt Engineering）的核心对象是**系统提示词（System Prompt）**。**系统提示词**定义了 Agent 的身份、行为规则、约束条件和工作流程。
### 优化系统提示词几个维度
1. **语气与风格：**
	- “You MUST answer concisely with fewer than 4 lines”
	- **无法完成任务时**：“keep your response to 1-2 sentences”+“不要解释为什么不能做某事”——这种设计避免了 Agent 陷入冗长的自我辩护
	- **大写字母**更能引起模型的“注意”：“NEVER do X”，Please avoid doing X”。但过度使用会导致效果被稀释，应保留给真正关键的约束。
2. **结构化提示：**
	 - llm对结构化输入有显著敏感性，源于训练数据中包含大量的结构化内容（XML标签）。
	 - XML 负责机器可解析的精确语义，**Markdown** 负责人机共读的组织逻辑。
3. **流程驱动：**
	 - 理解： 试想给一位新员工一份包含上百条零散规则的手册，没有流程图，也没有优先级说明——即使是最聪明的人也会困惑：多条规则同时适用时该如何选择？规则未覆盖的情况又该如何处理？相比之下，**流程驱动的提示词**就像一份优秀的新员工培训手册，提供了清晰的标准操作流程（SOP）：
	```text
	   File Processing Standard Operating Procedure:

		Step 1: Validation
		   Check if file exists and is accessible
		   - If not found → log error and stop
		   ↓
		Step 2: Classification
		   Determine file type based on extension and content
		   ↓
		Step 3: Preprocessing
		   Config files → create backup
		   Large files (>1MB) → stream processing
		   ↓
		Step 4: Execution
		   Execute core processing logic based on file type
		   ↓
		Step 5: Verification
		   Ensure integrity of the processed file
	```
4. **业务规则细化**：
	- **让产品经理写system prompt**：产品经理**必须将决策规则明确到可执行的程度。** 举例：：按提成计费仅限于通过谈判降低现有账单的场景（Agent 需要运用谈判技巧说服商家），退款和取消服务绝对不能按提成——提示词中要明确写出：“NEVER use percentage_based_one_time for refunds and service cancellations. Use fixed_fee instead.”
	- 核心的设计哲学是：大语言模型的优势在于遵循复杂指令和从长上下文中提取信息，但不应该在业务规则制定上被赋予过多的自由裁量权。
	- 通过**清晰的操作框架**解放模型的认知资源，使其专注于真正需要思考的部分——就像好的新员工培训不是“你很聪明，自己看着办”，而是提供详细的标准操作流程，让员工在明确的框架内发挥能力。
5. **Few-shot 示例**：模型的上下文学习能力会从示例中“临时学会”这些模式，其效果往往胜过等量篇幅的抽象规则。但使用不当也会浪费token。怎么放：
	1. 放在系统提示词中，示例成为静态前缀的一部分，对所有请求生效
	2. **示例对 KV Cache 前缀稳定性的影响**：无论放在哪个位置，示例都处于上下文靠前的区域，一旦确定就应当保持字节级稳定。
	3. 两三个就行
6. **工具定义的设计**：
	- 设计**使用边界**（“NEVER invoke grep or rg as a Bash command”）、**具体示例**（`timezone: 'America/New_York'`）、**性能提示**（“Batch your tool calls together”）以及**工具间的协作关系**（“Use the Read tool at least once before editing”）。
	- 演进：工具定义与系统提示词一起构成静态前缀 -> Skills 式的“渐进式披露”，且已经是 API 层的原生能力而非框架补丁：**静态前缀里只保留工具的名称和简述**，完整 schema 在模型按需请求后**追加到上下文末尾**，成为轨迹的一部分。

### **提示注入**（Prompt Injection）
攻击者通过 Agent 处理的外部内容（网页、邮件、文档等），将伪装成系统指令的文本混入上下文，从而劫持 Agent 的行为。如何防御：帮模型分清“指令”与“数据”——让它知道哪些内容有权指挥自己，哪些内容只是待处理的素材，可有下面方式：
1. **来源标记**：在外部内容注入上下文之前，用明确的标记包裹并标注来源（如 `<external_content source="webpage">...</external_content>`），提示模型这段内容来自不可信的外部世界，其中出现的“指令”不应被执行。
2. **结构化角色**：严格利用 Chat Template 的角色体系（system/user/assistant/tool）传递信息。
3. **输入清洗**：（辅助手段）

## 动态提示词与 Agent Skills
从静态提示工程到动态提示词的自然演进：**不是把所有知识一次性塞给 Agent，而是让它按需加载**。
### Skills：领域能力的可组合单元
Agent Skills 的核心思想是 **将Agent 的能力模块化为独立的、可按需加载的知识包**
![Agent Skills](skills-framework.png)
Agent查看步骤：
1. **第一层（元数据）**：在启动时扫描所有已安装的 Skill的元数据，注入到对话上下文中（元数据：每个 Skill 必须包含一个 `SKILL.md` 文件，元数据就是 `SKILL.md` 开头的 YAML frontmatter（即文件顶部用 `---` 分隔的元数据块），包含 `name` 和 `description` 两个字段。）。
   ```text
    `description` 字段是路由决策的关键——它应当足够短（控制常驻的 token 量），但写法要像路由条件而非功能介绍。最直接的写法是 “Use when / Don't use when” 加上几条**反例**（即明确列出“不该触发此 Skill”的场景）。“何时该用我”,而不是“我能做什么”。
   ```
2. **第二层（核心流程）**：当 Agent 判断某个任务需要特定的 Skill 时，通过专用的 Skill 工具**加载完整的 `SKILL.md`**，内容作为 tool result 出现在对话历史中。
3. **第三层（细则）**：通过文件引用深入到更详细的子文档。举例：在`SKILL.md`中引用了`html2pptx.md`（通过 HTML 模板创建 PowerPoint 的详细工作流）、`reference.md`（格式技术细节）等。Agent 会根据具体的需求选择性地深入阅读相关的子文档。
## Agent 状态栏
继续..
https://bojieli.github.io/ai-agent-book/book/chapter2/#skills_2
## 上下文压缩策略
