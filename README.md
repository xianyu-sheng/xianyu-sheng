# Hi, I'm Xianyu Sheng 👋

M.S. in Computer Science @ CQUPT (2027). I build **Agent Harnesses** — the runtime layer that decides whether an AI agent's output can be trusted. I verify my work with reproducible benchmarks, adversarial boundary probing, and upstream contributions, not adjectives.

My design philosophy, shared across everything I build:

> **Let the model think. Let the program decide.**
> LLM output is a *claim*; only a tool result is *evidence*.

The corollary I keep returning to: capability benchmarks measure the model, but **the harness is what makes a result trustworthy**. So I work on the layers between "the model said something" and "the system can act on it" — constraint boundaries, evidence gates, and evaluation you can reproduce.

---

## Featured work

### [Xenon](https://github.com/xianyu-sheng/Xenon) ⭐ 54 — Agent Harness

An open-source runtime for running, constraining, and evaluating AI coding agents. The core contribution is **architectural**: treating constraint and verification as first-class layers that sit *between* reasoning and tool execution, rather than as afterthoughts.

**Why it matters:** Most agent projects prove capability with benchmarks, then ship a different system to users. Xenon's interactive mode and evaluation harness share the same isolation boundaries and verification gates — so the 40.0% SWE-bench_Lite pass rate is a valid claim about the CLI you'd actually use.

**Key results:**
- **SWE-bench_Lite**: 40.0% instance-level (12/30, single attempt) on deepseek-v4-flash — **+6.7pp over the previous version in same-model A/B**. Full methodology, sampling seed, and cost accounting are committed and reproducible ([report](https://github.com/xianyu-sheng/Xenon/blob/main/evals/results/SWEBENCH_REPORT.md)).
- **Security hardening (v0.8.5)**: Found and fixed two real sandbox escapes via systematic boundary probing — path fence symlink bypass + runtime binding gap. Each came with POC, validity self-check (revert → must fail), and regression tests. Verified in production use.
- **Architecture**: 7 swappable reasoning paradigms, Evidence Runtime verification layer, MCP-native tooling, 2300+ unit tests with CI on every commit.

The project demonstrates that **trustworthiness is an architectural property**, not a tuning target.

### [SmartBench](https://github.com/xianyu-sheng/SmartBench) — evidence-constrained code diagnosis

A code-diagnosis workbench that splits responsibility deliberately: language frontends and deterministic analyzers own source facts; the LLM may only *propose* hypotheses; resolvers and validators decide whether a claim binds back to real operations, types, and control flow. Under-supported conclusions stay `unknown`/`abstained` — they are never promoted to findings.

- Real upstream bugs found and verified before submission — e.g. [stunner #89](https://github.com/firefart/stunner/issues/89) (TURN connection leak) confirmed fixed upstream; issues/PRs to sniproxy, Robyn, qscan.

---

## Open-source contributions

**Merged into [DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix)** (DeepSeek's official agent framework):

- [#7086](https://github.com/esengine/DeepSeek-Reasonix/pull/7086) — preserve advisory diagnostics without weakening the evidence gate (merged 2026-07-31)
- [#6618](https://github.com/esengine/DeepSeek-Reasonix/pull/6618) — honour `finish_reason=stop` on reasoning-only final answers (merged 2026-07-17)

**Open / under discussion:**

- [NousResearch/hermes-agent #80155](https://github.com/NousResearch/hermes-agent/pull/80155) — gate finalization on active todos; surfaced a boundary that drew maintainer triage and a "facing the same problem" from the community.
- [volcengine/veadk-python #716](https://github.com/volcengine/veadk-python/pull/716) — Xenon Skill + MCP interoperability docs.
- [deepseek-ai/awesome-deepseek-agent #301](https://github.com/deepseek-ai/awesome-deepseek-agent/pull/301) — listing Xenon as a DeepSeek V4 terminal agent.

---

## Technical focus

**Research interests:**
- Agent harness design: constraint boundaries, evidence gates, and trust semantics
- Reasoning-paradigm comparison and evaluation methodology
- Static analysis + semantic IR for deterministic code understanding
- Cost-efficiency in production LLM applications

**Currently exploring:**
- Cross-language semantic analysis (Python, Go, TypeScript, Rust)
- MCP protocol integration for agent tool ecosystems
- Benchmark design for agent reliability measurement

---

## Open to opportunities

**Seeking:** AI Agent / LLM Infrastructure engineering roles (2027 grad, available from July 2027)

**What I bring:**
- Reproducible evaluation methodology (SWE-bench official harness, same-model A/B, committed seeds)
- Adversarial self-review: I probe my own systems for boundary failures and fix them with POCs and regression locks
- Architecture that keeps guarantees consistent between benchmark and production paths
- Cross-stack engineering (Python/Go/C++/TypeScript, static analysis, distributed systems)

---

## Contact

- **GitHub**: [@xianyu-sheng](https://github.com/xianyu-sheng)
- **Email**: xianyu.sheng.research@gmail.com
- **Technical blog**: [掘金 @闲余生](https://juejin.cn/user/1131827254804154)
- **Location**: Chongqing / Chengdu, China (open to relocation)

---

<sub>💡 **Open-source philosophy**: Every claim should be reproducible. Every benchmark should publish its methodology. Every "smart" system should show its work.</sub>
