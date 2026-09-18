---
title: "AI FDE是什么？一篇文章带你了解（附学习资源）"
source: "https://mp.weixin.qq.com/s/yFuMA3WUSfveMllVhOVk7g"
author:
  - "[[Simonlin]]"
published:
created: 2026-09-18
description: "Anthropic工程师的17分钟演讲，讲透了AI FDE：是什么、什么情况才需要、工作流程四步，以及这个岗位的发展前景如何，附逐字稿和资源清单。"
tags:
  - "clippings"
---
Simonlin Simonlin的精神世界 *2026年9月17日 14:45*

SIMONLIN / AI TOOL NOTE 先看判断

给普通人看的 AI 工具学习记录

AI FDE是什么？一篇文章带你了解

Anthropic工程师的17分钟演讲，讲透了AI FDE：是什么、什么情况才需要、工作流程四步、国内外真实案例。海外岗位涨729%、国内还在招人搭台，附逐字稿和资源清单。

![图片](https://mmbiz.qpic.cn/mmbiz_png/gBevQ6puE7D8CeP4FXVsMK2Vt2R7CgPOu86GPMlnsN6NLUgWWcYNw1PQGGNH5ILN5T6mhah2UibHazACiaqwWqibyq51cmJTKtGMyEdukVA83U/640?from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=0)

先讲结论，再讲过程；能复核，才值得推荐AI 工具小白视角

Hello啊朋友们，我是Simonlin，用通俗易懂的语言，手把手带你玩转AI，提升10倍效率！

最近看了一场17分钟的演讲，讲的人叫 Kevin Bai，Anthropic 的工程师，之前在 Palantir 做了很多年 FDE（Forward Deployed Engineer，前置部署工程师，一种常驻客户现场的工程师岗位，下面细讲），后来去 Rippling 从零搭建 FDE 团队，一年从1个人扩到25人。

这场分享叫 Forward Deployed Engineering 101，算是这个岗位目前讲得最清楚的一堂入门课。

![Kevin Bai 在 AI Engineer World's Fair 现场分享](https://mmbiz.qpic.cn/sz_mmbiz_jpg/gBevQ6puE7BzKLFOC3YJoib1CNdkUB9RjW1Fejv0VIRUgXWia3EG5frMD656UNMgRJT9wC9iaaqibH39tzmq6Ro5LlsHRNIdtUVYNZlSyiaCLJYI/640?from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=1)

Kevin Bai 在 AI Engineer World's Fair 现场分享

演讲看完我又去翻了 Anthropic、Palantir、OpenAI 的官方资料和几家媒体的报道，最后出炉了这篇文章～

在这篇文章里，我想告诉你：FDE是个啥，AI FDE是啥，负责做些啥，工资如何，以及我个人的一些判断。

分享的逐字稿我们整理好了，文章末尾自取。

01

PART

FDE是什么：定义

VIEW / 往下看判断

![FDE定义：工程师空投到客户现场，卖结果](https://mmbiz.qpic.cn/mmbiz_jpg/gBevQ6puE7BsRBXleib2xPSkl5YHjv578Eh9xpo3hMKjSHlnRkJj8sRdrwPI4kFvLJYibVgbEXTjgsUSsdibEJPTe0cBPVD11J0umITGOLbe5g/640?from=appmsg&watermark=1#imgIndex=2)

FDE定义：工程师空投到客户现场，卖结果

FDE，Forward Deployed Engineering，中文一般叫前置部署工程师。

Kevin 给的定义就一句话：「FDE 不过就是一个面向客户的软件工程师。」你会把他当软件工程师招进团队，同时，你敢把他放在客户面前。

听着平平无奇，但这个词的来历不简单。Palantir 当年卖数据平台 Foundry，遇到一个死结：客户买的不是软件，也不是人的时间，而是一个结果。做石油的老板在乎的是管道，不是数据管道；做快消的在乎货架上多摆几个位子。数据怎么组织是实现细节，客户不在乎，也不应该在乎。

所以 Palantir 的解法是把工程师直接派到最前线，理解客户的业务本质，然后在平台上把方案建出来。客户拿到手的是那个结果。

用创业圈的话说，FDE 就是把公司早期的「设计伙伴」放大到企业级：我不知道产品该长什么样，你不知道该买什么，我们一起做出来。

这个定义现在有了官方背书。

Anthropic 在招 FDE 的职位说明里写的是：直接嵌入最重要的客户，用 Claude 构建生产级应用，交付 MCP server（让AI模型连接外部工具和数据的标准接口）、子代理、agent skill（给AI预装的技能包）这类技术产物，再把可复用的模式反哺给产品和工程团队。

Palantir 的官方博客说得更直白：传统工程师是为很多客户做一个功能，FDE 是为一个客户解锁很多功能。

02

PART

什么情况才需要FDE

VIEW / 往下看判断

![2x2判定矩阵](https://mmbiz.qpic.cn/mmbiz_jpg/gBevQ6puE7BmoS63AHRTm6E92DdWDkLcfJWOx5YCYE6eQTicBmwcCszrZa6x3py2I3r6icpsz0mfzKzSMCVEPz362bTh5vjtJAPwluy1I6aZA/640?from=appmsg&watermark=1#imgIndex=3)

2x2判定矩阵

Kevin 给了一个2x2判定矩阵，两个轴：你在卖什么，买你东西的人是谁。

卖技术性很强的产品，比如 GitHub、Datadog，买家是CTO（首席技术官），用户是工程师，复杂性他们自己吸收得了。卖不太复杂的东西，比如 Jira、Slack，买家不太技术化也没关系，工具是可配置的。

只有一种情况需要 FDE： **把技术性非常强的东西，卖给一个非技术买家。**

![Kevin 讲解判定矩阵的段落（视频4:10）](https://mmbiz.qpic.cn/sz_mmbiz_jpg/gBevQ6puE7AsKF5siamAcppRjOkROsoDpD3qYrMiagzNxqVRE6TXia8ZV2rncS9PJsr4xenkUOrgP4ZyNJicShMR6H4bHpJtKuye0XesYqMv2iaA/640?from=appmsg&watermark=1#imgIndex=4)

Kevin 讲解判定矩阵的段落（视频4:10）

Kevin 特意强调：想搞FDE之前先问自己，是「需要」还是「想要」？想要流行的东西太容易了，想搞AI太容易了。业务里没有那个「必须把复杂东西卖给非技术买家」的场景，就不用硬上。

03

PART

AI FDE是什么：2026年的船新版本

VIEW / 往下看判断

![2026：平台自己会动了](https://mmbiz.qpic.cn/mmbiz_jpg/gBevQ6puE7A3L5cRa2iaKYFibBH791BC25ia7IQQsyr1T4nc0bUItucl0SWuzxEaem6rREUMagsC0q3ZGWxNIjveV61NH2E65Wdpd6hHgoFBTQ/640?from=appmsg&watermark=1#imgIndex=5)

2026：平台自己会动了

Palantir 2004、2005年就在这么干了，为什么这个词2026年突然火？

Kevin 的个人假设是：不是因为世界突然发现 Palantir 的模式很好用，而是软件行业做生意的方式变了。

AI 让写代码、构建复杂可定制的软件变得非常容易，现在几乎每一个平台都是 agentic（智能体化，指AI能自己干活而不只是回答问题）的，都可定制。直接后果是：几乎每个做产品的人，都会遇到客户根本搞不清你到底是干什么的。

外面发生的事印证了这个判断。

Anthropic 的 FDE 团队直接驻进了 FIS，全球最大的金融科技公司之一，跟对方一起共建金融犯罪 AI Agent（AI智能体，能自主执行任务的AI程序），目标把反洗钱调查从数天压缩到分钟，BMO（加拿大蒙特利尔银行）和 Amalgamated Bank（美国合众银行）首批接入。OpenAI 走得更远：直接成立了一家独立公司做部署，收购 Tomoro 一次带来约150名 FDE，初始投资超过40亿美元。

一家做模型的公司，斥巨资养一批派驻客户现场的工程师，这件事本身就是答案。

这门生意到底有多赚？Kevin 在演讲里报了一组数字。

Palantir 的 ACV（平均合同价值，单个客户平均一年付的钱）是400万美元。第二名 ServiceNow，120万；第三名 Workday，60万。而整个美股市场，没有任何一家公开上市的 SaaS（订阅制软件生意）公司，能从一个客户身上一年收到50万美元。

这已经不是领先了，是存在着数量级上的差距。

更扎眼的是，做到这个数，Palantir 全公司才几千人。

![Kevin 讲 ACV 数字的段落（视频6:45）](https://mmbiz.qpic.cn/sz_mmbiz_jpg/gBevQ6puE7Cf3A8SBKpJAnSNtE4Cblrr0FXOS9cv2eZFRMA3k5hEm7JNV9qjn9NqaJBfYPO4zaE7f9qbhWoVIr6ZFpVwODrRYNxibJO2ckE4/640?from=appmsg&watermark=1#imgIndex=6)

Kevin 讲 ACV 数字的段落（视频6:45）

04

PART

FDE做什么：工作流程

VIEW / 往下看判断

![FDE工作流程闭环](https://mmbiz.qpic.cn/sz_mmbiz_jpg/gBevQ6puE7CI5X6d4je0oBrmY69bEShTDlcqIAcyTVb1yHO3kn6hCcskrDVuIeaTdaFfYLmCRUTvR3nVL5d4UQlYaNOdAK1sAtvwUcuiaq60/640?from=appmsg&watermark=1#imgIndex=7)

FDE工作流程闭环

根据 Kevin 讲的内容和一些从业者的公开分享，我整合出了一套FDE 的工作链条：

第一步，「钻」进客户的业务里。前 Palantir 高管 Vinoo Ganesh 的说法很传神：FDE 的工作就是收集客户的名词和动词——对方用什么词说仓库、用什么词说审批，这些名词动词就是业务的本体。

第二步，在平台的共享原语（primitives，指平台上预先造好的通用积木——数据连接、权限模型、工作流模板这类，工程师直接拿来组装，不用每次从零造）上做组装。这是整个模式最关键的一条：FDE 永远不从零写软件。如果每个 FDE 都从零开始构建，Kevin 原话说，那你拥有的不是FDE职能，是一个外包开发作坊——维护成本会把损益表活活吃掉，前提是工程师没先集体辞职。

第三步，交付结果，然后盯着改动分层。只为某个客户定制的东西留在客户那里；可以泛化的东西，长期都要泛化回平台，变成明天的共享原语。

第四步，回传情报。Vinoo Ganesh 有一句话值得单独抄下来：一个只解决现场问题、从不把信号传回产品团队的 FDE 职能，就是「换了个好头衔的咨询团队」。FDE 冲在最前线，真正的价值是发现下一步该往平台上加什么。

他举过一个很细的例子。某客户的 CSV（最常见的表格数据文件）转 Parquet（大数据场景用的高效存储格式）迁移被一位数据质量工程师卡了很久，FDE 驻场观察后发现她一直是双击 CSV 肉眼检查数据的，就连夜给她做了个 Parquet 查看器，两天后迁移获批，整条流水线从17个小时降到2小时。

FDE 的日常就是这种事：坐在客户旁边，看清楚问题真正卡在哪。

05

PART

实战案例

VIEW / 往下看判断

![海外交付 vs 国内招人](https://mmbiz.qpic.cn/mmbiz_jpg/gBevQ6puE7Dj7UNVX5Z9vwN9qEUibRGiaj0AwWLtZe0jG9meFzbL36yOJfC4Me3AiaY6BuPg9kZbWDSP849ia4vX0QaMSHNgFxbGsibpLtaHJQtU/640?from=appmsg&watermark=1#imgIndex=8)

海外交付 vs 国内招人

FDE到底有没有市场呢？还是说它只是又一个虚幻的泡沫？我整理了几个案例，大家可以看看。

**Anthropic × FIS（金融）** ：前面提过。FDE 嵌入 FIS 共建金融犯罪 AI Agent，BMO 和 Amalgamated Bank 首批部署，2026年下半年开放。有意思的是商业模式——两家银行不是直接按咨询费率付 Anthropic 的 FDE 费用，而是 FIS 承担这笔投入、摊到整个银行客户群里。

**OpenAI × Deployment Company** ：OpenAI 成立独立部署公司，Tomoro 并入带来约150名 FDE，TPG（美国大型私募基金）牵头19家投资机构和咨询公司入局，初始投资超40亿美元。客户名单里有 Tesco、维珍航空这些公司交付过的业务。

**Cognition × Nubank（拉美金融科技）** ：Cognition 是做 AI 程序员 Devin 的公司，养了一支 FDE 团队驻进客户现场。他们公开的案例是 Nubank——拉美最大的数字银行，1.1亿用户——把一套跑了8年、几百万行代码的老 ETL 系统做迁移，原本估计要一年半、上千名工程师分摊的活，Devin 加驻场团队把它压缩到了2个月量级，官方页面报的数字是提升了8倍工程效率，节省了20倍成本。

国内情况如何呢？可以看看大厂们的动作。

字节跳动旗下火山引擎在招「豆包AI大模型FDE」，职责写的就是面向行业头部客户驻场、识别客户流程里的核心问题，开价月薪3.5万–7万、15薪；腾讯云也在社招「前线部署工程师」；蚂蚁数科把 FDE 写进了生态合作新闻里，要让这些岗位「走向生产一线」。也就是说，国内现在处在招人、搭台子的阶段，谁家先拿到了结果，谁就先立得住。

06

PART

我的判断：未来趋势，值不值得往这个方向努力

VIEW / 往下看判断

![能力还是依赖](https://mmbiz.qpic.cn/sz_mmbiz_jpg/gBevQ6puE7CAwMWIawyAp1kdh8Ufgiagfj9lRvhdAux4UoGxeibjctkndzqCiaMMicIXRgSBpbRb9rOWXibzls7TRan5B0QsBJX8vQvNIReuphJU/640?from=appmsg&watermark=1#imgIndex=9)

能力还是依赖

先看看行业人士对这个岗位的讨论是怎么样的方向。

a16z（美国知名风投机构）合伙人 Joe Schmidt 说 FDE 是「创业公司现在最热的岗位」，企业买AI像奶奶买iPhone——想用，但需要你帮忙装好。数据也在那边：Indeed 的数据显示 FDE 岗位2026年4月同比涨了729%，平均底薪17.2万美元；Levels.fyi（科技行业薪资查询网站）上美国 FDE 总包中位数20.6万；Anthropic 自家 JD（职位说明）开到28–32万美元底薪，差旅25%。亚马逊也在往这个角色上砸10亿美元。

然后就到了大家最关心的薪资问题了。

国外：Levels.fyi 上美国 FDE 总包中位数约20.6万美元（约合人民币145万），Indeed 口径平均底薪17.2万美元，Anthropic 这种头部开到28–32万美元。

国内：字节跳动「豆包AI大模型FDE」挂出的月薪是3.5万–7万、15薪，折算年薪约52万–105万；投中网报道国内初级 FDE 月薪普遍2万起步，高级岗位多在4万×15薪以上，猎聘口径一线大厂资深 FDE 年薪在60万–120万。

取个平均数的话：国外年薪大致在140万人民币这个量级，国内大厂大致在60万–100万人民币之间，差一倍左右，但方向和涨幅都在同一张牌桌上。

Gartner（全球权威IT研究机构）的分析师 Alex Coqueiro 有个很扎心的预测：到2028年，70%的企业会因为供应商成本太高、自己又接不住，被迫放弃从 FDE 项目里买来的 agentic AI 方案。

他还说了一句话，我真觉得说的挺在理的：

「连续几次部署里 FDE 投入降不下来，说明这个项目产出的是依赖，不是能力」。还有人说得更狠：「CIO 以为买的是软件，其实买的是一份专业服务合约。」

那我的判断呢？

第一，这个方向的热度是真实的，不是炒概念。

当每个软件平台都可定制之后，「客户自己会用」这个假设塌了，总得有人替客户把结果做出来。大厂用真金白银投了票：OpenAI 40亿美元、亚马逊10亿美元、Anthropic 把 FDE 写进官方战略。岗位数据只是这个事实的滞后指标。

第二，对个人来说，值不值得取决于你是不是那块料。

这个岗位要求你既写得动代码，又敢坐在客户会议室里听对方讲业务——Kevin 的原话是，你敢把他放在客户面前，「敢」这个字是重点。两种能力同时具备的人非常稀缺，稀缺就意味着溢价，年薪30万美元级别的报价已经说明了市场怎么定价。但它也意味着这个岗位有一大半时间不在代码库里，在客户的现场，差旅25%起步，有人分析连 OpenAI 的 JD 都写到最多50%——burnout（职业倦怠）是这个岗位的职业病。也就是说，你得到处跑来跑去，到客户业务第一线去。

第三，也是我最想说的：FDE 的长期价值不在「驻场服务」，在回传。Gartner 那个70%的预测背后是一个真问题——客户买的到底是能力还是依赖。

这个岗位真正的护城河，是把现场学到的东西变成平台的一部分，让下一个项目不用从头再来。

对个人也是同理。

如果你的工作只是帮客户跑腿干活，你随时会被换掉；如果你每做一单都让自己对某个行业的理解变厚一层，你就在积累别人拿不走的东西。选这个方向之前，先问自己能不能做到后者。

一句话总结以上的内容。AI FDE 是个真实的、正在长大的方向，适合「技术过得去、也愿意跟人打交道」的人重点投入；但它不是避风港，是前线。

07

PART

最后

VIEW / 往下看判断

![后台回复FDE领逐字稿](https://mmbiz.qpic.cn/mmbiz_jpg/gBevQ6puE7Dp2A79s7NoDWw2bWAnXl4L4kug3iaRrSocJiaJZ6LsH8oBasULNwRIxUNjBqXbKWsjBzsn6PglKaXGdSa4oaLb5uVvKObjYjDicQ/640?from=appmsg&watermark=1#imgIndex=10)

后台回复FDE领逐字稿

完整演讲视频在这里：https://youtu.be/KwhgfwOSToQ ，17分钟。

这场分享的完整中文逐字稿我们已经整理好了，Kevin 讲的每个细节都在里面。 **后台回复「FDE」** ，可以要一份。

最后的最后，我为大家整理了一些FDE相关的资源，建议直接收藏：

- 《FDE白皮书》（zlbigger 出品，约35页滚动维护，V1.7 更新于2026-09-16，国内视角目前最全的一本），链接：https://zlbigger.com/fde/
- 《FDE工程师指南》（范冰 XDash 的 GitHub 开源书，从零入门带案例），链接：https://github.com/xdash/FDE-the-Guidance-Book-of-Forward-Deployed-Engineer
- Awesome-FDE-Roadmap（FDE 技术栈清单，GitHub 开源），链接：https://github.com/pierpaolo28/Awesome-FDE-Roadmap
- a16z：Trading Margin for Moat（FDE 为什么是创业公司最热岗位，2025-06），链接：https://a16z.com/services-led-growth/
- Latent Space 访谈：FDE 最佳实践（前 Palantir 高管讲实战方法论，2026-09），链接：https://www.latent.space/p/forward-deployed-engineer-best-practices
- LeadDev：FDE 岗位崛起（岗位涨729%的数据出处，2026），链接：https://leaddev.com/career-development/the-rise-of-the-forward-deployed-engineer-fde
- Anthropic 官方 FDE 职位说明（base $280k–320k 那份），链接：https://job-boards.greenhouse.io/anthropic/jobs/5302966008
- OpenAI 官方 FDSWE 职位说明（出差最多50%那份），链接：https://openai.com/careers/forward-deployed-software-engineer-sf-san-francisco/
- Kevin Bai 演讲原视频（17分钟，本文的主要底稿），链接：https://youtu.be/KwhgfwOSToQ

我是Simonlin，下次见。