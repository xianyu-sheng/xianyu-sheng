**English** | [简体中文](README.zh-CN.md)

# Hi, I'm Xianyu Sheng 👋

M.S. in Computer Science @ CQUPT (2027). I build **Agent Harnesses** — the runtime layer that decides whether an AI agent's output can be trusted. I verify my work with reproducible benchmarks, adversarial boundary probing, and upstream contributions, not adjectives.

My design philosophy, shared across everything I build:

> **Let the model think. Let the program decide.**
> LLM output is a *claim*; only a tool result is *evidence*.

The corollary I keep returning to: capability benchmarks measure the model, but **the harness is what makes a result trustworthy**. So I work on the layers between "the model said something" and "the system can act on it" — constraint boundaries, evidence gates, and evaluation you can reproduce.

---

## Featured work

### [Xenon](https://github.com/xianyu-sheng/Xenon) — Agent Harness

An open-source runtime for running, constraining, and evaluating AI coding agents. The core contribution is **architectural**: treating constraint and verification as first-class layers that sit *between* reasoning and tool execution, rather than as afterthoughts.

**Why it matters:** Most agent projects prove capability with benchmarks, then ship a different system to users. Xenon's interactive mode and evaluation harness share the same isolation boundaries and verification gates — so the SWE-bench_Lite results are claims about the CLI you'd actually use, not about a separate demo build.

**Key results:**
- **SWE-bench_Lite** (deepseek-v4-flash, react engine, 120 steps, official harness, blind — no test patch, no test-name hints): three runs average **62.2%** on a frozen 30-instance sample (seed 20260729) and **52.2%** on a zero-overlap held-out sample (seed 20261016). The previous generation (v0.8.5) scores 63.3% and 46.7% on the same two samples — the sign flip between samples showed the original sample carried in-sample tuning, so the held-out number is the one to trust. (Superseded: the v0.8.2 "40.0% instance-level" was a five-engine union, not a single-engine score; and v0.8.3+ runs before 2026-10 injected test names into the prompt.) Methodology, manifests, per-run results and sha256-checked archives: [EVAL_RESULTS.md](https://github.com/xianyu-sheng/Xenon/blob/main/docs/EVAL_RESULTS.md).
- **Security hardening (v0.8.5)**: Found and fixed two real sandbox escapes via systematic boundary probing — path fence symlink bypass + runtime binding gap. Each came with POC, validity self-check (revert → must fail), and regression tests, validated end-to-end.
- **Kernel architecture**: one `LoopRuntime`, one append-only ledger, one set of read-only projections. Capability catalog (read/search/edit/verify/vcs/shell/remote), typed receipts, V0/V1/V2 verification, claim→fact binding, V2 coverage audit, one-shot approvals, MCP per-tool ToolSpecs, and a finalizer that owns delivery commits with preflight audit/rollback.
- **Engineering**: 4,000+ tests across Python 3.10–3.12, hash-chain tail checks, real TTY approval transcripts, and reproducible delivery-failure/rollback tests.

**Recognition:** featured in [Awesome-MCP-ZH](https://github.com/yzfly/Awesome-MCP-ZH) (MCP clients → verifiable terminal coding agent), [awesome-opensource-ai](https://github.com/alvinreal/awesome-opensource-ai) (Agentic AI & Multi-Agent Systems → Autonomous Coding Agents), [awesome-mcp-lists](https://github.com/collabnix/awesome-mcp-lists) (Collabnix; MCP Clients → Command Line Tools), and [awesome-ai-coding-tools](https://github.com/mahmoudsajjadi/awesome-ai-coding-tools) (CLI coding agents — special thanks to @xianyu-sheng).

The project demonstrates that **trustworthiness is an architectural property**, not a tuning target.

### [SmartBench](https://github.com/xianyu-sheng/SmartBench) — evidence-constrained code diagnosis

A code-diagnosis workbench that splits responsibility deliberately: language frontends and deterministic analyzers own source facts; the LLM may only *propose* hypotheses; resolvers and validators decide whether a claim binds back to real operations, types, and control flow. Under-supported conclusions stay `unknown`/`abstained` — they are never promoted to findings.

**Real bugs found and verified:**
- [stunner #89](https://github.com/firefart/stunner/issues/89) — TURN connection leak (confirmed fixed upstream)
- [qscan #22](https://github.com/qi4L/qscan/issues/22) — SQL database leak on error paths
- [sniproxy #203](https://github.com/mosajjal/sniproxy/pull/203) — process crash from panic in goroutine
- [go-imap #773](https://github.com/emersion/go-imap/pull/773) — malformed APPEND left the client without a tagged response (**fix merged upstream**)
- [webdav #374](https://github.com/hacdias/webdav/pull/374) — CORS early return made "unprotected config" warnings unreachable (**fix merged upstream, 2026-10-24**)
- [Robyn #1432](https://github.com/sparckles/Robyn/issues/1432) — SSE test hygiene issue

**Capability added through this work (2026-10):** counterfactual patch review and engineering trade-off adjudication — SmartBench flags patches that are *worse than the status quo* under the failure they address (e.g. replacing fail-stop with an unbacked retry loop), and labels findings by documented intent, patch risk and reachability before anything is filed upstream.

**Systematic validation on real-world cases:**
- **50/50** regression snapshots pass (25 before/after cases)
- **6 real-world cases from 4 major projects** (Kubernetes, etcd, Prometheus, Python Requests)
- **100% detection (6/6)** on the selected true concurrency bugs and resource leaks
- **40,650** Go type-evidence items; internal grounding **22% → 81%**
- **0 false positives on these 6 controlled before/after cases** — regression-style validation on fixed snapshots (not a blind benchmark over full codebases); includes the unbounded-goroutine pattern behind [CVE-2026-73500](https://nvd.nist.gov/vuln/detail/cve-2026-73500) (etcd TLS DoS)
- Covers: goroutine leaks, channel misuse, constructor error paths, context cancellation failures

Full validation results: [REAL_WORLD_CASES.md](https://github.com/xianyu-sheng/SmartBench/blob/main/REAL_WORLD_CASES.md)

---

## Open-source contributions

**Merged into [DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix)** (DeepSeek's official agent framework):

- [#7086](https://github.com/esengine/DeepSeek-Reasonix/pull/7086) — preserve advisory diagnostics without weakening the evidence gate (merged 2026-07-31)
- [#6618](https://github.com/esengine/DeepSeek-Reasonix/pull/6618) — honour `finish_reason=stop` on reasoning-only final answers (merged 2026-07-17)

**Open / under discussion:**

- [NousResearch/hermes-agent #80155](https://github.com/NousResearch/hermes-agent/pull/80155) — gate finalization on active todos; surfaced a boundary that drew maintainer triage and a "facing the same problem" from the community.

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
- Kernel-first agent runtimes: event-sourced ledgers, typed receipts, projection-only state

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
- **Email**: 2107644732@qq.com (primary) · xianyu.sheng.research@gmail.com
- **Technical blog**: [掘金 @闲余生](https://juejin.cn/user/1131827254804154)
- **Location**: Chongqing / Chengdu, China (open to relocation)

---

<sub>💡 **Open-source philosophy**: Every claim should be reproducible. Every benchmark should publish its methodology. Every "smart" system should show its work.</sub>
