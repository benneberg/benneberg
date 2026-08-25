<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=22&pause=1000&color=00FFAA&center=true&vCenter=true&width=600&lines=Platform+Engineer;Systems+%26+Infrastructure;Edge+Computing+%26+Distributed+Systems;AI+Systems+%26+Platform+Architecture" alt="Typing animation" />

<br/>

<img src="https://img.shields.io/badge/Platform_Engineering-00FFAA?style=flat-square&logoColor=black" />
<img src="https://img.shields.io/badge/SRE_%26_Reliability-0088FF?style=flat-square&logoColor=white" />
<img src="https://img.shields.io/badge/Edge_%26_Embedded-FF0055?style=flat-square&logoColor=white" />
<img src="https://img.shields.io/badge/AI_Systems-9D00FF?style=flat-square&logoColor=white" />
<img src="https://img.shields.io/badge/Developer_Tooling-FF8800?style=flat-square&logoColor=white" />

</div>

---

```
$ whoami

  Software engineer building systems at the boundary of infrastructure, distributed systems, edge computing, and AI.

  The recurring question across all of it:
  How do you make complex technology reliable, observable,
  and useful — outside of a demo?

  Open to:  Platform Engineering · SRE · Systems Engineering
            Edge Architecture · AI Platform Engineering
            Technical Architecture · AI Systems Architecture
```

---

## Project Map

Projects appear in the category where they fit best. Some span multiple areas — that's noted in the description.

> **Status indicators:**
> `● Built` — implemented and working
> `○ Designed` — architecture designed, partially or not yet fully built
> `◌ Exploring` — experimental, proof-of-concept stage

---

## ▣ Infrastructure & Platform

Systems for running distributed environments reliably — fleet coordination, telemetry pipelines, observability, and what happens when things fail.

---

<table>
<tr>
<td width="50%" valign="top">

### [Insidr Management](https://github.com/benneberg/insidr-management)
`● Built`

Remote DevTools and telemetry platform for large fleets of locked-down Chromium-based signage devices (webOS, Tizen, Android TV, ChromeOS). Zero-dependency agent injected into any Chromium instance. Custom transport protocol (CDP-Lite v2) with sequence numbers, ACKs, batching, local buffering, and retry-with-jitter — designed for unreliable connections where direct device access is impossible.

`distributed-systems` `observability` `fleet-management` `telemetry` `edge` `cloudflare-workers`

</td>
<td width="50%" valign="top">

### [Insidr Telemetry](https://github.com/benneberg/insidr-telemetry)
`● Built` 🌐

Server-side control plane for distributed device telemetry. Agents buffer and sequence locally before delivery through the reliability-oriented transport layer to a Cloudflare Workers ingestion backend. Per-device metrics, fleet-wide activity stream, command audit trail, and error boundary reporting.

`cloudflare-workers` `durable-objects` `telemetry-pipeline` `edge-compute` `observability`

</td>
</tr>
<tr>
<td width="50%" valign="top">

### [Voila!](https://github.com/benneberg/voila)
`○ Designed` 🌐

> "One input, infinite understanding."

A universal file handler that exposes a single minimal interface while routing every file type through the appropriate processing environment. Magic number detection (file identity by content, not extension). Architecture: WASM/browser → Docker → Firecracker microVM depending on isolation requirements. Redis caching, rate limiting, Prometheus/Grafana observability stack. *Firecracker tier is architectural — not yet fully implemented.*

`containers` `wasm` `redis` `prometheus` `grafana` `sandboxing` `infrastructure-design`

</td>
<td width="50%" valign="top">

### [Downtime Analyzer](https://github.com/benneberg/downtime-analyzer)
`● Built`

Industrial reliability analysis platform. Correlates heterogeneous sources — PLC alarms, operator logs, maintenance records, production events — using statistical precursor detection across configurable time windows. Identifies recurring failure patterns and generates structured root-cause analysis with AI-assisted reasoning. Designed for containerised deployment on Cloud Run.

`reliability-engineering` `root-cause-analysis` `log-correlation` `industrial-systems` `python`

</td>
</tr>
<tr>
<td colspan="2" valign="top">

### [OmniSign + ScreenMesh](https://github.com/benneberg/omnisign)
`○ Designed` 🌐

Enterprise digital signage platform with a clean **Control Plane / Data Plane** separation. The cloud Control Plane (OmniSign CMS) handles orchestration and fleet management. The edge execution layer (ScreenMesh) is designed to remain operational when cloud connectivity is lost — offline-first, self-healing caches, local state. Reliability mechanisms: RAF Watchdog with millisecond drift detection and auto-recovery · Thundering Herd prevention via jittered heartbeat intervals · Ed25519 cryptographic device provisioning with rotating nonces · SHA-256 integrity verification on all media assets.

*Also relevant to: Edge & IoT · Systems Architecture*

`platform-architecture` `control-plane` `edge-computing` `offline-first` `reliability` `cryptography` `fleet-orchestration`

</td>
</tr>
</table>

---

## ▣ Systems Architecture & Reliability

Projects focused on how systems behave under failure — self-healing, deterministic execution, audit trails, and the engineering patterns behind reliable software.

---

<table>
<tr>
<td width="50%" valign="top">

### [ShadowFrame](https://github.com/benneberg/shadowframe2)
`● Built`

High-fidelity edge runtime simulator for LG webOS and Samsung Tizen hardware. Virtualises SoC constraints, kernel behaviours, and storage systems so signage applications can be developed and tested without physical hardware. Architecture: virtualised kernel with centralised EventBus, Physical Abstraction Layer, hardware storage bridge, async logging buffer with circular rotation (~200KB cap). Resolved a synchronous I/O bottleneck in the logging module during development.

`embedded-linux` `edge-runtime` `event-driven` `memory-management` `webos` `tizen`

</td>
<td width="50%" valign="top">

### [bldr](https://github.com/benneberg/bldr)
`● Built` 🌐

Execution layer for developer intent. Single mutation authority — the only layer permitted to write to the filesystem. Every mutation recorded in an event-sourced SQLite audit journal with causation IDs, correlation IDs, session IDs, and replay flags. Git session branching per AI interaction. Real-time telemetry via Socket.io. Deterministic dry-run diffs before any disk commit.

*Also relevant to: AI Engineering · Developer Tools*

`event-sourcing` `audit-trail` `deterministic-execution` `developer-platform` `ai-tooling`

</td>
</tr>
<tr>
<td width="50%" valign="top">

### [TaskFlow AI](https://github.com/benneberg/taskflow)
`○ Designed`

Full-stack dashboard for managing AI agents from co-pilot to autonomous squad. Control Plane / Data Plane separation, simulated durable multi-stage pipelines (Temporal.io saga pattern), independent circuit breakers per agent, budget contracts, Human-in-the-Loop gates, and a full audit trail. Designed for production-grade AI operations under real reliability constraints.

`ai-orchestration` `circuit-breaker` `saga-pattern` `human-in-the-loop` `audit-trail`

</td>
<td width="50%" valign="top">

### [Intent Runtime](https://github.com/benneberg/intent-runtime)
`○ Designed`

Execution kernel with six permanent architectural pillars. LLM functions strictly as a stateless reasoning engine — structured intent parsed from natural language, then handed to a deterministic state machine for execution. Fact Reconciliation Engine prevents duplicate states. Observability layer is a first-class system component, not an add-on.

`ai-systems` `state-machine` `deterministic-execution` `ai-kernel`

</td>
</tr>
</table>

---

## ▣ Edge, IoT & Industrial Systems

Software for physical environments: constrained hardware, unreliable networks, industrial protocols, and systems that cannot be reached directly when something goes wrong.

---

<table>
<tr>
<td width="50%" valign="top">

### [PLC AutoDocs AI](https://github.com/benneberg/PLC-AutoDocs-AI)
`● Built`

Parses IEC 61131-3 Structured Text and PLCopen XML to generate documentation via LLM. Includes a **Deterministic Static Safety Analyzer** — checks E-Stop interlocks, motor thermal overloads, jam watchdog timers, and pneumatic safety valve logic. Generates FSM state transition diagrams. Revision control and sign-off audit trail for safety-critical environments.

`industrial-automation` `safety-systems` `iec-61131` `static-analysis` `plc` `audit-trail`

</td>
<td width="50%" valign="top">

### [Signage Toolkit](https://github.com/benneberg/signage-toolkit-nexus)
`● Built`

Browser-based media preparation suite for digital signage content networks. All processing client-side via WebAssembly (ffmpeg-wasm) — no server, no upload, no data leaving the device. Handles raster dimensions, bandwidth budgets, and colour standards for low-spec Android SoCs, web players, and enterprise Linux media engines. Offline-first by design.

`wasm` `ffmpeg` `offline-first` `edge-compute` `media-processing` `signage`

</td>
</tr>
<tr>
<td colspan="2" valign="top">

### [Deterministic Playlist Compiler](https://github.com/benneberg/signage-video-fusion)
`● Built` 🌐

Compiles mixed-media signage playlists into deterministic, gapless MP4 output using ffmpeg.wasm in-browser. Same input always produces the same output regardless of device state or runtime variation. Live tool available.

`deterministic-systems` `wasm` `ffmpeg` `signage` `media-processing`

</td>
</tr>
</table>

---

## ▣ AI Engineering & Intelligent Systems

AI systems where reliability, auditability, and predictable behaviour are design requirements — not afterthoughts.

---

<table>
<tr>
<td width="50%" valign="top">

### [Oppy OS](https://github.com/benneberg/oppy-os)
`● Built`

Evidence-first decision platform for evaluating early-stage venture ideas systematically. Scoring engine with weighted evidence chains and risk vector analysis. WAL-mode SQLite for concurrent read/write under multi-agent load. Enforces the distinction between evidence and assumption at the data model level.

`ai-systems` `evidence-based-reasoning` `scoring-engine` `sqlite-wal` `decision-support`

</td>
<td width="50%" valign="top">

### [Verdict Lab](https://github.com/benneberg/verdict-lab)
`○ Designed`

Reproducible experimentation platform for evaluating LLM behaviour under controlled conditions. Pairwise model experiments, prompt template version control, semantic evaluation. Designed to measure model behaviour systematically, not just observe it.

`llm-evaluation` `ai-research` `experimentation-platform` `prompt-engineering`

</td>
</tr>
<tr>
<td width="50%" valign="top">

### [ARIP](https://github.com/benneberg/codekeeper)
`○ Designed`

Repository bootstrap, audit, and intelligence platform. TypeScript Compiler AST analysis, dependency graph mapping, multi-gateway model router (Groq / Gemini / OpenAI), cosine similarity vector search via embeddings. Designed for codebase understanding at scale.

`static-analysis` `ast` `ai-platform` `dependency-graph` `vector-search`

</td>
<td width="50%" valign="top">

### [bugLet](https://github.com/benneberg/buglet)
`○ Designed`

AI-assisted debugging platform that generates production-ready telemetry instrumentation code and analyses performance anomalies. Designed for Heisenbugs — bugs that disappear under observation. Structured AI-guided debugging workflow with reproducible output.

`ai-tooling` `debugging` `telemetry` `observability` `developer-tooling`

</td>
</tr>
</table>

---

## ▣ Developer Tools & Engineering Productivity

Tools built around the experience of writing, understanding, and operating software.

---

<table>
<tr>
<td width="50%" valign="top">

### [insikt](https://github.com/benneberg/insikt)
`● Built`

Zero-dependency in-browser developer console and debugging overlay. Mobile-first. Console API interception, Fetch/XHR request inspection, storage exploration, runtime REPL, floating overlay UI. Built because no existing tool worked reliably inside locked-down Chromium environments on signage hardware. Used in production.

`developer-tooling` `browser-internals` `zero-dependency` `mobile-debugging` `devex`

</td>
<td width="50%" valign="top">

### [Fleet of Karen](https://github.com/benneberg/fleet-of-karen)
`○ Designed`

Multi-agent code review system. Specialised agents: Security (leaked tokens, insecure patterns) · Performance (algorithmic complexity) · UI consistency · Synthesis. Python CLI + React dashboard. Dual-track review architecture (Optimistic + Conservative). Failure topology visualisation.

`multi-agent` `ai-orchestration` `code-review` `python` `developer-tooling`

</td>
</tr>
<tr>
<td width="50%" valign="top">

### [devstackr](https://github.com/benneberg/devstackr)
`● Built` 🌐

High-performance developer dashboard with 40+ engineering tools across Security, Data, Design, and DevOps. All processing client-side for privacy. AI pipeline engine decomposes natural language intent into executable tool sequences via capability-based matching.

`developer-tooling` `client-side` `ai-assisted` `devex`

</td>
<td width="50%" valign="top">

### [API2UI Studio](https://github.com/benneberg/api-tasks-compiler-studio)
`○ Designed`

Deterministic, schema-constrained compiler that transforms REST and event-driven API specifications into safe, transaction-controlled micro-interfaces. Server-side intent extraction with interactive parameter validation. Designed to make APIs operable without writing code.

`api-design` `schema-compiler` `developer-tooling` `deterministic-systems`

</td>
</tr>
</table>

---

## ▣ Experimental & Games

Not everything I build is infrastructure.

---

<table>
<tr>
<td width="50%" valign="top">

### [MaryDama](https://github.com/benneberg/marydama)
`● Built` 🌐

Browser-based checkers / draughts with human vs human and human vs AI modes. Multiple game variants, move highlighting, undo. Built with HTML, CSS, JavaScript, TailwindCSS.

`game` `ai-opponent` `browser` `javascript`

</td>
<td width="50%" valign="top">

### [HandOff — Architect Paradox](https://github.com/benneberg/handoff)
`◌ Exploring` 🌐

PWA for exploring system design patterns as interactive cards — load balancing, graceful degradation, circuit breaker, eventual consistency. Part reference tool, part exploration of how architectural concepts can be made navigable and interactive.

`system-design` `architecture-patterns` `pwa`

</td>
</tr>
</table>

---

## Currently Building Depth In

```
Kubernetes · Azure · Terraform · OpenTelemetry · Infrastructure as Code
```

Not listed as core skills — that would be inaccurate. Listed because they're the honest next step.

---

<div align="center">

**Karlstad, Sweden**

*This profile is an engineering map. The repositories contain the architecture, tradeoffs, and implementation decisions behind each project.*

</div>
