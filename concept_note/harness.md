[学习资料](https://walkinglabs.github.io/learn-harness-engineering/zh/)
Harness = 指令 + 工具 + 环境 + 状态 + **反馈**
- 不是模型权重的部分全是 harness，你的 harness 决定了模型能力能被发挥多少。
- 五个子系统中，反馈子系统通常是投入最少、回报最高的。先把验证命令写清楚。
- 用"控制变量排除法"量化各子系统的边际贡献；定位真正瓶颈要靠失败记录和归因，不能只靠拆除实验。
- Harness 和代码一样会腐化，定期审计，像还技术债一样还 harness 债。
## Anthropic 的三 agent 架构实验
**Planner（规划者）**：接收一段 1-4 句话的用户需求，扩展成完整产品规格。被要求"大胆设定范围"并且"专注于产品上下文和高层技术设计，而不深入详细的技术实现"。原因是：如果 planner 过早指定了粒度技术细节且搞错了，错误会级联到下游实现。更好的做法是约束交付物，让 agent 在执行中自己找到路径。
**Generator（生成者）**：按 sprint 逐个功能实现。每个 sprint 前和 evaluator 协商一份 sprint 合同，约定这个功能块"做完"的标准。然后按合同实现，自评后交给 QA。
**Evaluator（评估者）**：用 Playwright MCP 像用户一样点击运行中的应用，测试 UI 功能、API 端点和数据库状态。对每个 sprint 按四个维度评分：产品深度、功能性、视觉设计和代码质量。每个维度有硬性阈值，任一不达标则 sprint 失败，generator 收到详细反馈后修复。
## Loop Engineering
**Addy Osmani**（Google Chrome 工程负责人）在 26年6 月 7 日[撰文](https://addyosmani.com/blog/loop-engineering/)将这个概念命名为 **Loop Engineering**，并给了它一句话定义：
**Loop engineering 就是用系统取代你自己去 prompt agent。**
[实践：autoresearch](https://github.com/karpathy/autoresearch)