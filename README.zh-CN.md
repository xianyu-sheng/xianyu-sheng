**English** | [简体中文](README.zh-CN.md)

# 你好，我是 Xianyu Sheng 👋

重邮（CQUPT）计算机科学硕士研究生（2027 届）。我做的是 **Agent Harness** —— 决定 AI 智能体输出"能不能被信任"的那一层运行时。我的工作靠可复现的基准测试、对抗性边界探测和上游贡献来验证，不靠形容词。

贯穿我所有项目的一条设计哲学：

> **让模型思考，让程序裁决。**
> LLM 的输出只是*主张*，只有工具返回的结果才是*证据*。

我反复回到的一个推论是：能力基准测的是模型，但**让结果变得可信的是 harness 本身**。所以我专门做"模型说了话"和"系统能据此行动"之间那一层 —— 约束边界、证据闸门，以及你能亲手复现的评测。

---

## 代表项目

### [Xenon](https://github.com/xianyu-sheng/Xenon) —— Agent Harness

一个用于运行、约束和评测 AI 编程智能体的开源运行时。核心贡献在**架构层面**：把"约束"和"验证"当一等公民，让它们位于推理与工具执行*之间*，而不是事后补丁。

**为什么重要：** 多数智能体项目用基准测试证明能力，然后交给用户一个不一样的系统。Xenon 的交互模式与评测 harness 共用同一套隔离边界和验证闸门 —— 所以 SWE-bench_Lite 的成绩说的是你真正会上手的那个 CLI，而不是另外做的 demo 版本。

**关键结果：**
- **SWE-bench_Lite**（deepseek-v4-flash，react 引擎，120 步，官方 harness，盲测 —— 不给测试补丁、不给测试名提示）：在冻结的 30 题样本（seed 20260729）上三次运行平均 **62.2%**，在零重叠的留出样本（seed 20261016）上为 **52.2%**。上一代（v0.8.5）在同一批两个样本上分别是 63.3% 和 46.7% —— 两个样本之间符号翻转，说明原样本带有调参痕迹，因此应采信留出集上的数字。（已作废：v0.8.2 的"40.0% instance-level"是五引擎并集而非单引擎成绩；另外 2026-10 之前的部分 v0.8.3+ 运行把测试名注入进了 prompt。）方法、清单、逐次结果与 sha256 校验归档见 [EVAL_RESULTS.md](https://github.com/xianyu-sheng/Xenon/blob/main/docs/EVAL_RESULTS.md)。
- **安全加固（v0.8.5）**：通过系统化的边界探测，发现并修复了两个真实的沙箱逃逸 —— 路径围栏的符号链接绕过 + 运行时绑定缺口。每个都配了 POC、有效性自检（回滚后必须失败）和回归测试，并做了端到端验证。
- **内核架构**：一个 `LoopRuntime`、一个只追加账本、一套只读投影。能力目录（read/search/edit/verify/vcs/shell/remote）、类型化回执、V0/V1/V2 三级验证、主张→事实绑定、V2 覆盖审计、一次性审批、MCP 按工具生成的 ToolSpec，以及一个负责交付提交（含预检审计 / 回滚）的 finalizer。
- **工程**：Python 3.10–3.12 上 4000+ 测试、哈希链尾部校验、真实 TTY 审批记录，以及可复现的交付失败 / 回滚测试。

**认可：** 被 [Awesome-MCP-ZH](https://github.com/yzfly/Awesome-MCP-ZH)（MCP 客户端 → 可验证终端编程智能体）、[awesome-opensource-ai](https://github.com/alvinreal/awesome-opensource-ai)（Agentic AI & Multi-Agent Systems → Autonomous Coding Agents）、[awesome-mcp-lists](https://github.com/collabnix/awesome-mcp-lists)（Collabnix；MCP Clients → Command Line Tools）、[awesome-ai-coding-tools](https://github.com/mahmoudsajjadi/awesome-ai-coding-tools)（CLI coding agents —— 特别感谢 @xianyu-sheng）收录。

这个项目想说明的是：**可信性是一种架构属性，不是一个调参目标。**

### [SmartBench](https://github.com/xianyu-sheng/SmartBench) —— 证据约束的代码诊断

一个代码诊断工作台，职责被刻意拆开：语言前端和确定性分析器负责源事实；LLM 只能*提出*假设；解析器和校验器决定一个主张能否绑定回真实的操作、类型和控制流。证据不足的结论保持 `unknown` / `abstained` —— 它们永远不会被升级成"发现"。

**已发现并验证的真实 bug：**
- [stunner #89](https://github.com/firefart/stunner/issues/89) —— TURN 连接泄漏（上游已确认修复）
- [qscan #22](https://github.com/qi4L/qscan/issues/22) —— 错误路径上的 SQL 数据库泄漏
- [sniproxy #203](https://github.com/mosajjal/sniproxy/pull/203) —— goroutine 内 panic 导致进程崩溃
- [go-imap #773](https://github.com/emersion/go-imap/pull/773) —— 畸形 APPEND 让客户端收不到带 tag 的响应（**修复已合并上游**）
- [webdav #374](https://github.com/hacdias/webdav/pull/374) —— CORS 提前返回让"配置未受保护"的警告变成不可达代码（**修复已合并上游，2026-10-24**）
- [Robyn #1432](https://github.com/sparckles/Robyn/issues/1432) —— SSE 测试的卫生问题

**由此项工作新增的能力（2026-10）：** 反事实补丁评审与工程权衡裁决 —— SmartBench 会标记那些在它所针对的故障下*比现状更糟*的补丁（例如把 fail-stop 换成没有依据支撑的 retry loop），并在向上游提交之前，按文档化意图、补丁风险和可达性给结论打标签。

**在真实案例上的系统化验证：**
- **50/50** 回归快照通过（25 组 before/after）
- **6 个来自 4 个大型项目的真实案例**（Kubernetes、etcd、Prometheus、Python Requests）
- 在所选取的并发 bug 和资源泄漏上 **100% 检出（6/6）**
- **40,650** 条 Go 类型证据；内部 grounding 从 **22% → 81%**
- 在这 6 组受控 before/after 案例上 **0 误报** —— 这是在已修复快照上做的回归式验证（不是覆盖全代码库的盲测）；其中包含 [CVE-2026-73500](https://nvd.nist.gov/vuln/detail/cve-2026-73500)（etcd TLS DoS）背后的无界 goroutine 模式
- 覆盖范围：goroutine 泄漏、channel 误用、构造函数错误路径、context 取消失败

完整验证结果：[REAL_WORLD_CASES.md](https://github.com/xianyu-sheng/SmartBench/blob/main/REAL_WORLD_CASES.md)

---

## 开源贡献

**已合并进 [DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix)**（DeepSeek 官方 agent 框架）：

- [#7086](https://github.com/esengine/DeepSeek-Reasonix/pull/7086) —— 在不削弱证据闸门的前提下保留建议性诊断（2026-07-31 合并）
- [#6618](https://github.com/esengine/DeepSeek-Reasonix/pull/6618) —— 纯推理式最终回答尊重 `finish_reason=stop`（2026-07-17 合并）

**开放中 / 讨论中：**

- [NousResearch/hermes-agent #80155](https://github.com/NousResearch/hermes-agent/pull/80155) —— 用未完成的 todo 作为 finalization 的闸门；暴露出一个边界问题，引来维护者 triage，以及社区里"我们也遇到同样问题"的反馈。

---

## 技术方向

**研究兴趣：**
- Agent harness 设计：约束边界、证据闸门、信任语义
- 推理范式比较与评测方法论
- 静态分析 + 语义 IR 用于确定性代码理解
- 生产级 LLM 应用的成本效率

**正在探索：**
- 跨语言语义分析（Python、Go、TypeScript、Rust）
- 面向智能体工具生态的 MCP 协议集成
- 面向智能体可靠性度量的基准设计
- 内核优先（kernel-first）的智能体运行时：事件溯源账本、类型化回执、仅投影状态

---

## 求职意向

**寻求：** AI Agent / LLM 基础设施方向的工程岗位（2027 届，2027 年 7 月起可入职）

**我能带来的：**
- 可复现的评测方法论（SWE-bench 官方 harness、同模型 A/B、提交随机种子）
- 对抗性自我评审：主动探测自己系统的边界失效，并用 POC 和回归锁把它修死
- 让基准路径与生产路径保持同一套保证的架构能力
- 跨栈工程能力（Python / Go / C++ / TypeScript、静态分析、分布式系统）

---

## 联系方式

- **GitHub**：[@xianyu-sheng](https://github.com/xianyu-sheng)
- **邮箱**：2107644732@qq.com（主） · xianyu.sheng.research@gmail.com
- **技术博客**：[掘金 @闲余生](https://juejin.cn/user/1131827254804154)
- **所在地**：中国 重庆 / 成都（可接受异地）

---

<sub>💡 **开源信条**：每个结论都应当可复现。每个基准都应当公开方法论。每个"聪明"的系统都应当展示它的推导过程。</sub>
