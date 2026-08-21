# Hi, I'm Xianyu Sheng 👋

M.S. in Computer Science @ CQUPT (2027). I build **AI Agent infrastructure** — and I verify it with reproducible benchmarks and upstream contributions, not adjectives.

My design philosophy, shared across everything I build:

> **Let the model think. Let the program decide.**
> LLM output is a *claim*; only a tool result is *evidence*.

---

## Featured work

### [Xenon](https://github.com/xianyu-sheng/Xenon) — extensible terminal AI coding agent

An open-source agent runtime built around an **online Evidence Runtime**: a deterministic, zero-LLM verification chain that runs *vertically* through the whole task lifecycle (plan → pre-tool → execution → patch-binding → delivery). It treats every LLM statement as a claim to be verified against real tool results — catching "pasted a diff but never wrote the file" hallucinations at delivery time with zero false-kills.

- **SWE-bench_Lite official harness**: 30 instances, **40.0% instance-level** (12/30, single attempt) on the *cheapest* model tier (deepseek-v4-flash) — **+6.7pp over the previous version in a same-model A/B** (33.3% → 40.0%). Approaching Claude 3.5 Sonnet-level agents at ~1/100 the cost. Full methodology, sampling seed, cost accounting, and per-engine breakdown are committed and reproducible ([report](https://github.com/xianyu-sheng/Xenon/blob/main/evals/results/SWEBENCH_REPORT.md)).
- 7 inference paradigms (direct / ReAct / Plan-Execute / Reflection + combinations) over one engine abstraction; MCP-native tool layer; **2000+ unit tests** + CI on every commit.
- Hardened via a systematic **boundary-probing methodology** (malformed input / path-traversal / corrupted-file probes on every public entry point) that surfaced and fixed real defects, including a session path-traversal and a permission-gate fail-open.

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

---

## Technical focus

**Research interests:**
- Agent reasoning paradigms and evaluation methodology
- Evidence-constrained architectures that treat LLM output as claims to be verified
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
- Reproducible evaluation methodology (SWE-bench, upstream bug verification)
- Production-focused architecture design (caching, observability, evidence gates)
- Cross-stack engineering (Python/Go/C++/TypeScript, static analysis, distributed systems)

---

## Contact

- **GitHub**: [@xianyu-sheng](https://github.com/xianyu-sheng)
- **Email**: xianyu.sheng.research@gmail.com
- **Technical blog**: [掘金 @闲余生](https://juejin.cn/user/1131827254804154)
- **Location**: Chongqing / Chengdu, China (open to relocation)

---

<sub>💡 **Open-source philosophy**: Every claim should be reproducible. Every benchmark should publish its methodology. Every "smart" system should show its work.</sub>
