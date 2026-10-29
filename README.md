<h1 align="center">Hi 👋, I'm Xianyu Sheng</h1>
<h3 align="center">Building verifiable AI Agent infrastructure | CQUPT Undergraduate</h3>

<p align="center">
  <a href="https://github.com/xianyu-sheng"><img src="https://img.shields.io/badge/GitHub-xianyu--sheng-181717?style=flat-square&logo=github" alt="GitHub"></a>
  <a href="https://github.com/xianyu-sheng/Xenon/releases"><img src="https://img.shields.io/github/v/release/xianyu-sheng/Xenon?style=flat-square&label=Xenon" alt="Xenon release"></a>
  <a href="https://github.com/xianyu-sheng/SmartBench/releases"><img src="https://img.shields.io/github/v/release/xianyu-sheng/SmartBench?style=flat-square&label=SmartBench" alt="SmartBench release"></a>
  <a href="https://github.com/xianyu-sheng/Agent-hub/releases"><img src="https://img.shields.io/github/v/release/xianyu-sheng/Agent-hub?style=flat-square&label=Agent-hub" alt="Agent-hub release"></a>
</p>

<p align="center">
  <b>📦 Quick Install:</b> &nbsp;
  <code>pip install https://github.com/xianyu-sheng/Xenon/releases/download/v0.9.5/xenon_harness-0.9.5-py3-none-any.whl</code>
</p>

---

### 🧠 About Me

I'm an undergraduate at **CQUPT (Chongqing University of Posts and Telecommunications)**, building practical AI agent systems. My focus is **verifiable agent runtimes**: one control loop, one append-only ledger, typed tool receipts, deterministic verification, and projections that never become a second source of truth.

> *The model proposes; the harness proves. A model can be wrong, but it must not be able to turn an unverified claim into a delivery.*

---

### 🚀 Featured Projects

<p align="center">
  <a href="https://github.com/xianyu-sheng/Xenon">
    <img src="https://github-readme-stats.vercel.app/api/pin/?username=xianyu-sheng&repo=Xenon&theme=tokyonight" />
  </a>
  <a href="https://github.com/xianyu-sheng/SmartBench">
    <img src="https://github-readme-stats.vercel.app/api/pin/?username=xianyu-sheng&repo=SmartBench&theme=tokyonight" />
  </a>
</p>

#### 🧬 [Xenon](https://github.com/xianyu-sheng/Xenon) — Verifiable Coding Agent Harness

A single-loop coding agent runtime: `LoopRuntime` is the only writer, the ledger is the only truth, and every tool result is a typed receipt. Capability catalog + MCP per-tool ToolSpecs, policy/approval, V0/V1/V2 verification, claim→fact binding, V2 coverage audit, debt/repair, and a finalizer that owns all delivery commits.

- **SWE-bench Lite**: 62.2% on the frozen 30-case subset, 52.2% on a zero-overlap held-out set (blind protocol, official harness, 3-run mean).
- **4,000+** tests across Python 3.10–3.12; evidence chain, TTY transcripts and rollback paths are tested.
- Listed in **Awesome-MCP-ZH**, **awesome-opensource-ai**, **Collabnix awesome-mcp-lists**, and **awesome-ai-coding-tools**.

#### 🔬 [SmartBench](https://github.com/xianyu-sheng/SmartBench) — Evidence-Constrained Code Diagnosis

Deterministic analyzers own the source facts; the LLM may only propose hypotheses. A resolver/validator decides whether a hypothesis binds back to real operations, types and control flow; anything unbound stays `unknown` or `abstained`.

- **50/50** regression snapshots pass; **6/6** controlled real-world concurrency/resource-lifetime cases verified.
- **4** upstream reports: qscan, stunner, sniproxy, Robyn.
- Go type evidence: **40,650** items; internal grounding **22% → 81%**.

<p align="center">
  <a href="https://github.com/xianyu-sheng/omniagent">
    <img src="https://github-readme-stats.vercel.app/api/pin/?username=xianyu-sheng&repo=omniagent&theme=tokyonight" />
  </a>
  <a href="https://github.com/xianyu-sheng/Agent-hub">
    <img src="https://github-readme-stats.vercel.app/api/pin/?username=xianyu-sheng&repo=Agent-hub&theme=tokyonight" />
  </a>
</p>

#### 🔧 [OmniAgent](https://github.com/xianyu-sheng/omniagent) — Local Multi-Model AI Coding Agent CLI

A local-first coding assistant with multi-model routing (DeepSeek, OpenAI, Claude, Gemini, Qwen, Ollama), ReAct / Plan-Execute / Reflection workflows, MCP tools, memory, checkpoint protection, and a Textual TUI.

#### 🎯 [Agent Hub](https://github.com/xianyu-sheng/Agent-hub) — Multi-Agent Orchestration System

A decoupled central scheduler that discovers agents via `agent.yaml` manifests, routes natural-language tasks into cross-agent DAGs, and executes them with debate, reflection, voting and human-in-the-loop strategies.

#### 📄 [Resume-Sync](https://github.com/xianyu-sheng/resume-sync) — Git → LaTeX Resume Auto-Sync

Detects project commits, calls an LLM to draft resume bullets, updates LaTeX source and compiles the PDF — built to remove manual resume maintenance during job hunting.

---

### 🛠️ Tech Stack

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" />
  <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white" />
  <img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" />
</p>

**Agent Runtime:** Single-loop execution · Event sourcing · Append-only ledger · Projection-only state · Typed receipts · Capability catalogs · Policy/approval · V0/V1/V2 verification · Finalizer/rollback

**AI/LLM:** Agent architecture · Multi-agent systems · MCP · Tool use · RAG/GraphRAG · Prompt engineering · SWE-bench evaluation

**Engineering:** CLI/TUI · Code analysis · Distributed systems · CI/CD · Developer productivity

---

### 📊 GitHub Stats

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=xianyu-sheng&show_icons=true&theme=tokyonight&hide_border=true&count_private=true" height="165" />
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=xianyu-sheng&layout=compact&theme=tokyonight&hide_border=true" height="165" />
</p>

---

### 🌱 What I'm Working On

- 🔭 Making **Xenon** a kernel-first, replayable coding harness: one ledger, typed receipts, V2 coverage, MCP, approvals and deterministic delivery.
- 🧪 Turning **SmartBench** from a controlled audit workbench into a measurable evidence-constrained diagnosis system.
- 🌍 Bilingual docs, reproducible benchmarks, and stricter CI evidence for every release.

---

### 🏷️ Featured In

- [Awesome-MCP-ZH](https://github.com/yzfly/Awesome-MCP-ZH)
- [awesome-opensource-ai](https://github.com/alvinreal/awesome-opensource-ai)
- [awesome-mcp-lists](https://github.com/collabnix/awesome-mcp-lists)
- [awesome-ai-coding-tools](https://github.com/mahmoudsajjadi/awesome-ai-coding-tools)

<p align="center">
  <i>⭐ If you find my projects useful, a star means a lot! Let's connect and build together.</i>
</p>
