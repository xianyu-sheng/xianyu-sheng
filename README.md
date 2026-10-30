# Hi, I'm Xianyu Sheng · 你好，我是 Xianyu Sheng 👋

M.S. in Computer Science @ CQUPT (2027). I build **Agent Harnesses** — the runtime layer that decides whether an AI agent's output can be trusted. I verify my work with reproducible benchmarks, adversarial boundary probing, and upstream contributions, not adjectives.

重邮（CQUPT）计算机科学硕士研究生，2027 届。我做的是 **Agent Harness** —— 决定 AI 智能体输出"能不能被信任"的那一层运行时。我的工作靠可复现的基准测试、对抗性边界探测和上游贡献来验证，不靠形容词。

> **Let the model think. Let the program decide.**
> LLM output is a *claim*; only a tool result is *evidence*.
>
> **让模型思考，让程序裁决。**
> LLM 的输出只是*主张*，只有工具返回的结果才是*证据*。

The corollary I keep returning to: capability benchmarks measure the model, but **the harness is what makes a result trustworthy**. So I work on the layers between "the model said something" and "the system can act on it" — constraint boundaries, evidence gates, and evaluation you can reproduce.

我反复回到的一个推论是：能力基准测的是模型，但**让结果变得可信的是 harness 本身**。所以我专门做"模型说了话"和"系统能据此行动"之间那一层 —— 约束边界、证据闸门，以及你能亲手复现的评测。

---

## Featured work · 代表项目

### [Xenon](https://github.com/xianyu-sheng/Xenon) — Agent Harness

An open-source runtime for running, constraining, and evaluating AI coding agents. The core contribution is **architectural**: treating constraint and verification as first-class layers that sit *between* reasoning and tool execution, rather than as afterthoughts.

**Why it matters:** Most agent projects prove capability with benchmarks, then ship a different system to users. Xenon's interactive mode and evaluation harness share the same isolation boundaries and verification gates — so the SWE-bench_Lite results are claims about the CLI you'd actually use, not about a separate demo build.

一个用于运行、约束和评测 AI 编程智能体的开源运行时。核心贡献在**架构层面**：把"约束"和"验证"当一等公民，让它们位于推理与工具执行*之间*，而不是事后补丁。

**为什么重要：** 多数智能体项目用基准测试证明能力，然后交给用户一个不一样的系统。Xenon 的交互模式与评测 harness 共用同一套隔离边界和验证闸门 —— 所以 SWE-bench_Lite 的成绩说的是你真正会上手的那个 CLI，而不是另外做的 demo 版本。

**Key results:**
- **SWE-bench_Lite** (deepseek-v4-flash, react engine, 120 steps, official harness, blind — no test patch, no test-name hints): three runs average **62.2%** on a frozen 30-instance sample (seed 20260729) and **52.2%** on a zero-overlap held-out sample (seed 20261016). The previous generation (v0.8.5) scores 63.3% and 46.7% on the same two samples — the sign flip between samples showed the original sample carried in-sample tuning, so the held-out number is the one to trust. (Superseded: the v0.8.2 "40.0% instance-level" was a five-engine union, not a single-engine score; and v0.8.3+ runs before 2026-10 injected test names into the prompt.) Methodology, manifests, per-run results and sha256-checked archives: [EVAL_RESULTS.md](https://github.com/xianyu-sheng/Xenon/blob/main/docs/EVAL_RESULTS.md).
- **Security hardening (v0.8.5)**: Found and fixed two real sandbox escapes via systematic boundary probing — path fence symlink bypass + runtime binding gap. Each came with POC, validity self-check (revert → must fail), and regression tests, validated end-to-end.
- **Kernel architecture**: one `LoopRuntime`, one append-only ledger, one set of read-only projections. Capability catalog (read/search/edit/verify/vcs/shell/remote), typed receipts, V0/V1/V2 verification, claim→fact binding, V2 coverage audit, one-shot approvals, MCP per-tool ToolSpecs, and a finalizer that owns delivery commits with preflight audit/rollback.
- **Engineering**: 4,000+ tests across Python 3.10–3.12, hash-chain tail checks, real TTY approval transcripts, and reproducible delivery-failure/rollback tests.

**关键结果：**
- **SWE-bench_Lite**（deepseek-v4-flash，react 引擎，120 步，官方 harness，盲测 —— 不给测试补丁、不给测试名提示）：在冻结的 30 题样本（seed 20260729）上三次运行平均 **62.2%**，在零重叠的留出样本（seed 20261016）上为 **52.2%**。上一代（v0.8.5）在同一批两个样本上分别是 63.3% 和 46.7% —— 两个样本之间符号翻转，说明原样本带有调参痕迹，因此应采信留出集上的数字。（已作废：v0.8.2 的"40.0% instance-level"是五引擎并集而非单引擎成绩；另外 2026-10 之前的部分 v0.8.3+ 运行把测试名注入进了 prompt。）方法、清单、逐次结果与 sha256 校验归档见 [EVAL_RESULTS.md](https://github.com/xianyu-sheng/Xenon/blob/main/docs/EVAL_RESULTS.md)。
- **安全加固（v0.8.5）**：通过系统化的边界探测，发现并修复了两个真实的沙箱逃逸 —— 路径围栏的符号链接绕过 + 运行时绑定缺口。每个都配了 POC、有效性自检（回滚后必须失败）和回归测试，并做了端到端验证。
- **内核架构**：一个 `LoopRuntime`、一个只追加账本、一套只读投影。能力目录（read/search/edit/verify/vcs/shell/remote）、类型化回执、V0/V1/V2 三级验证、主张→事实绑定、V2 覆盖审计、一次性审批、MCP 按工具生成的 ToolSpec，以及一个负责交付提交（含预检审计 / 回滚）的 finalizer。
- **工程**：Python 3.10–3.12 上 4000+ 测试、哈希链尾部校验、真实 TTY 审批记录，以及可复现的交付失败 / 回滚测试。

**Recognition:** featured in [Awesome-MCP-ZH](https://github.com/yzfly/Awesome-MCP-ZH) (MCP clients → verifiable terminal coding agent), [awesome-opensource-ai](https://github.com/alvinreal/awesome-opensource-ai) (Agentic AI & Multi-Agent Systems → Autonomous Coding Agents), [awesome-mcp-lists](https://github.com/collabnix/awesome-mcp-lists) (Collabnix; MCP Clients → Command Line Tools), and [awesome-ai-coding-tools](https://github.com/mahmoudsajjadi/awesome-ai-coding-tools) (CLI coding agents — special thanks to @xianyu-sheng).

**认可：** 被 [Awesome-MCP-ZH](https://github.com/yzfly/Awesome-MCP-ZH)（MCP 客户端 → 可验证终端编程智能体）、[awesome-opensource-ai](https://github.com/alvinreal/awesome-opensource-ai)（Agentic AI & Multi-Agent Systems → Autonomous Coding Agents）、[awesome-mcp-lists](https://github.com/collabnix/awesome-mcp-lists)（Collabnix；MCP Clients → Command Line Tools）、[awesome-ai-coding-tools](https://github.com/mahmoudsajjadi/awesome-ai-coding-tools)（CLI coding agents —— 特别感谢 @xianyu-sheng）收录。

The project demonstrates that **trustworthiness is an architectural property**, not a tuning target.

这个项目想说明的是：**可信性是一种架构属性，不是一个调参目标。**

### [SmartBench](https://github.com/xianyu-sheng/SmartBench) — evidence-constrained code diagnosis

A code-diagnosis workbench that splits responsibility deliberately: language frontends and deterministic analyzers own source facts; the LLM may only *propose* hypotheses; resolvers and validators decide whether a claim binds back to real operations, types, and control flow. Under-supported conclusions stay `unknown`/`abstained` — they are never promoted to findings.

一个代码诊断工作台，职责被刻意拆开：语言前端和确定性分析器负责源事实；LLM 只能*提出*假设；解析器和校验器决定一个主张能否绑定回真实的操作、类型和控制流。证据不足的结论保持 `unknown` / `abstained` —— 它们永远不会被升级成"发现"。

**Real bugs found and verified:**
- [stunner #89](https://github.com/firefart/stunner/issues/89) — TURN connection leak (confirmed fixed upstream)
- [qscan #22](https://github.com/qi4L/qscan/issues/22) — SQL database leak on error paths
- [sniproxy #203](https://github.com/mosajjal/sniproxy/pull/203) — process crash from panic in goroutine
- [go-imap #773](https://github.com/emersion/go-imap/pull/773) — malformed APPEND left the client without a tagged response (**fix merged upstream**)
- [webdav #374](https://github.com/hacdias/webdav/pull/374) — CORS early return made "unprotected config" warnings unreachable (**fix merged upstream, 2026-10-24**)
- [Robyn #1432](https://github.com/sparckles/Robyn/issues/1432) — SSE test hygiene issue

**已发现并验证的真实 bug：**
- [stunner #89](https://github.com/firefart/stunner/issues/89) — TURN 连接泄漏（上游已确认修复）
- [qscan #22](https://github.com/qi4L/qscan/issues/22) — 错误路径上的 SQL 数据库泄漏
- [sniproxy #203](https://github.com/mosajjal/sniproxy/pull/203) — goroutine 内 panic 导致进程崩溃
- [go-imap #773](https://github.com/emersion/go-imap/pull/773) — 畸形 APPEND 让客户端收不到带 tag 的响应（**修复已合并上游**）
- [webdav #374](https://github.com/hacdias/webdav/pull/374) — CORS 提前返回让"配置未受保护"的警告变成不可达代码（**修复已合并上游，2026-10-24**）
- [Robyn #1432](https://github.com/sparckles/Robyn/issues/1432) — SSE 测试的卫生问题

**Capability added through this work (2026-10):** counterfactual patch review and engineering trade-off adjudication — SmartBench flags patches that are *worse than the status quo* under the failure they address (e.g. replacing fail-stop with an unbacked retry loop), and labels findings by documented intent, patch risk and reachability before anything is filed upstream.

**由此项工作新增的能力（2026-10）：** 反事实补丁评审与工程权衡裁决 —— SmartBench 会标记那些在它所针对的故障下*比现状更糟*的补丁（例如把 fail-stop 换成没有依据支撑的 retry loop），并在向上游提交之前，按文档化意图、补丁风险和可达性给结论打标签。

**Systematic validation on real-world cases:**
- **50/50** regression snapshots pass (25 before/after cases)
- **6 real-world cases from 4 major projects** (Kubernetes, etcd, Prometheus, Python Requests)
- **100% detection (6/6)** on the selected true concurrency bugs and resource leaks
- **40,650** Go type-evidence items; internal grounding **22% → 81%**
- **0 false positives on these 6 controlled before/after cases** — regression-style validation on fixed snapshots (not a blind benchmark over full codebases); includes the unbounded-goroutine pattern behind [CVE-2026-73500](https://nvd.nist.gov/vuln/detail/cve-2026-73500) (etcd TLS DoS)
- Covers: goroutine leaks, channel misuse, constructor error paths, context cancellation failures

**在真实案例上的系统化验证：**
- **50/50** 回归快照通过（25 组 before/after）
- **6 个来自 4 个大型项目的真实案例**（Kubernetes、etcd、Prometheus、Python Requests）
- 在所选取的并发 bug 和资源泄漏上 **100% 检出（6/6）**
- **40,650** 条 Go 类型证据；内部 grounding 从 **22% → 81%**
- 在这 6 组受控 before/after 案例上 **0 误报** —— 这是在已修复快照上做的回归式验证（不是覆盖全代码库的盲测）；其中包含 [CVE-2026-73500](https://nvd.nist.gov/vuln/detail/cve-2026-73500)（etcd TLS DoS）背后的无界 goroutine 模式
- 覆盖范围：goroutine 泄漏、channel 误用、构造函数错误路径、context 取消失败

Full validation results: [REAL_WORLD_CASES.md](https://github.com/xianyu-sheng/SmartBench/blob/main/REAL_WORLD_CASES.md) · 完整验证结果同上。

---

## Open-source contributions · 开源贡献

**Merged into [DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix)** (DeepSeek's official agent framework):

- [#7086](https://github.com/esengine/DeepSeek-Reasonix/pull/7086) — preserve advisory diagnostics without weakening the evidence gate (merged 2026-07-31)
- [#6618](https://github.com/esengine/DeepSeek-Reasonix/pull/6618) — honour `finish_reason=stop` on reasoning-only final answers (merged 2026-07-17)

**已合并进 [DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix)**（DeepSeek 官方 agent 框架）：

- [#7086](https://github.com/esengine/DeepSeek-Reasonix/pull/7086) —— 在不削弱证据闸门的前提下保留建议性诊断（2026-07-31 合并）
- [#6618](https://github.com/esengine/DeepSeek-Reasonix/pull/6618) —— 纯推理式最终回答尊重 `finish_reason=stop`（2026-07-17 合并）

**Open / under discussion:**
- [NousResearch/hermes-agent #80155](https://github.com/NousResearch/hermes-agent/pull/80155) — gate finalization on active todos; surfaced a boundary that drew maintainer triage and a "facing the same problem" from the community.

**开放中 / 讨论中：**
- [NousResearch/hermes-agent #80155](https://github.com/NousResearch/hermes-agent/pull/80155) —— 用未完成的 todo 作为 finalization 的闸门；暴露出一个边界问题，引来维护者 triage，以及社区里"我们也遇到同样问题"的反馈。

---

## Technical focus · 技术方向

**Research interests:**
- Agent harness design: constraint boundaries, evidence gates, and trust semantics
- Reasoning-paradigm comparison and evaluation methodology
- Static analysis + semantic IR for deterministic code understanding
- Cost-efficiency in production LLM applications

**研究兴趣：**
- Agent harness 设计：约束边界、证据闸门、信任语义
- 推理范式比较与评测方法论
- 静态分析 + 语义 IR 用于确定性代码理解
- 生产级 LLM 应用的成本效率

**Currently exploring:**
- Cross-language semantic analysis (Python, Go, TypeScript, Rust)
- MCP protocol integration for agent tool ecosystems
- Benchmark design for agent reliability measurement
- Kernel-first agent runtimes: event-sourced ledgers, typed receipts, projection-only state

**正在探索：**
- 跨语言语义分析（Python、Go、TypeScript、Rust）
- 面向智能体工具生态的 MCP 协议集成
- 面向智能体可靠性度量的基准设计
- 内核优先（kernel-first）的智能体运行时：事件溯源账本、类型化回执、仅投影状态

---

## Open to opportunities · 求职意向

**Seeking:** AI Agent / LLM Infrastructure engineering roles (2027 grad, available from July 2027)

**寻求：** AI Agent / LLM 基础设施方向的工程岗位（2027 届，2027 年 7 月起可入职）

**What I bring:**
- Reproducible evaluation methodology (SWE-bench official harness, same-model A/B, committed seeds)
- Adversarial self-review: I probe my own systems for boundary failures and fix them with POCs and regression locks
- Architecture that keeps guarantees consistent between benchmark and production paths
- Cross-stack engineering (Python/Go/C++/TypeScript, static analysis, distributed systems)

**我能带来的：**
- 可复现的评测方法论（SWE-bench 官方 harness、同模型 A/B、提交随机种子）
- 对抗性自我评审：主动探测自己系统的边界失效，并用 POC 和回归锁把它修死
- 让基准路径与生产路径保持同一套保证的架构能力
- 跨栈工程能力（Python / Go / C++ / TypeScript、静态分析、分布式系统）

---

## Contact · 联系方式

- **GitHub**: [@xianyu-sheng](https://github.com/xianyu-sheng)
- **Email 邮箱**: 2107644732@qq.com (primary 主) · xianyu.sheng.research@gmail.com
- **Technical blog 技术博客**: [掘金 @闲余生](https://juejin.cn/user/1131827254804154)
- **Location 所在地**: Chongqing / Chengdu, China (open to relocation) · 中国 重庆 / 成都（可接受异地）

---

<sub>💡 **Open-source philosophy**: Every claim should be reproducible. Every benchmark should publish its methodology. Every "smart" system should show its work.
**开源信条**：每个结论都应当可复现。每个基准都应当公开方法论。每个"聪明"的系统都应当展示它的推导过程。</sub>
