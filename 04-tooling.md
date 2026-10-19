# 04 · Tooling

What to learn first, what to learn later, and what to skip, across the AI engineering stack.
This is written for someone strong in TypeScript and moderate in Python. Snapshot date:
**19 October 2026**.

> **Read this chapter with a timestamp in mind.** In the four weeks before this snapshot, two
> Claude models, an OpenAI model, Google's flagship Gemini and Meta's first open-weight model in
> 18 months were all replaced or launched. Model lineups and framework APIs change monthly.
> Postgres, FastAPI, scikit-learn, vLLM's role and eval methodology change over years. Learn the
> stable things in depth. For the volatile things, learn how to read their changelogs.

---

## What changed in the last month

| Area | Change |
|---|---|
| Anthropic | **Sonnet 5.5** ($2/$10 per M tokens) and **Haiku 5.5** (7 Oct; from $0.10/$0.50; 1M context) are current. Sonnet 5 and Haiku 4.5 are now legacy. Fable 5.1 and Opus 5.5 are unchanged. On Haiku 5.5, sampling parameters (`temperature`, `top_p`, `top_k`) return a 400 error |
| OpenAI | Lineup is GPT-6 Astra, **GPT-6.1 Sol**, GPT-6 Luna. A large batch of legacy snapshots (GPT-4, 4o-2024-05-13, o1, o3-mini, o4-mini) **shuts down 23 Oct 2026**. The Assistants API shut down on 26 Aug |
| Google | **Gemini 4 Argon** launched 13 Oct as the flagship. Introductory pricing is reported as $2/$10, rising later. 3.1 Pro is still in preview |
| Meta | **Muse Spark Open** (15 Oct): open weights, 816B total / 42B active parameters. The custom licence has commercial limits, so it is not OSI open source |
| Open weights | GLM-5.3, Kimi K3, Qwen3.8 and DeepSeek V4.1-Flash lead the open rankings. These rankings come from one publisher and are unverified |
| Python tooling | **OpenAI acquired Astral** (uv, ruff, ty), announced 19 Mar. The tools remain open source. uv 0.13 defaults to **Python 3.15**. **Polars 2.0** was released 6 Oct |
| Security | **LiteLLM was compromised** on PyPI on 24 Mar 2026: versions 1.82.7 and 1.82.8 shipped a credential stealer. Pin your dependencies with hashes |
| Agent frameworks | **Pydantic AI 2.0** stable since June. Vercel AI SDK 7, LangGraph 1.2 and Mastra 1.x are all releasing weekly |

---

## 1 · Model APIs and gateways

| Tool | Pick this when | Maturity |
|---|---|---|
| **Anthropic Messages API** | You need agentic or long-horizon work, a 1M context, or the best prompt caching. Cache reads cost 2.5–10% of input | Stable API; models change |
| **OpenAI Responses API** | You're on OpenAI, or want built-in tools and server-side state. Chat Completions survives as the lingua franca for OpenAI-compatible endpoints | Stable; Assistants is gone |
| **Gemini API** | You want cheap multimodal input or long video and audio | Volatile naming; previews retire fast |
| **Vercel AI Gateway** | You work in TypeScript and want zero-markup routing, BYOK, budgets and fallbacks. It exposes OpenAI- and Anthropic-compatible endpoints | Stable (GA) |
| **OpenRouter** | You want the broadest catalogue and quick access to new open models | Stable; 5.5% fee on credit purchases |
| **LiteLLM** | You need a self-hosted gateway for compliance or on-prem deployment | Mature but security-sensitive since March |

- **Learn first:** the raw Anthropic and OpenAI SDKs. Cover streaming, tool calling, structured
  output, prompt caching and effort/reasoning controls. Then put a provider abstraction on top
  (Vercel AI SDK with AI Gateway, or OpenRouter) so that switching models is a config change.
- **Later:** LiteLLM, if a job needs self-hosted routing.
- **Skip:** memorising model names. Keep model IDs in config, and know where the deprecations
  page is.

---

## 2 · Agent frameworks

| Framework | Language | Pick this when | Maturity |
|---|---|---|---|
| **Vercel AI SDK 7** | TS | You're building TypeScript or Next.js product features: streaming UI, tools, `toolApproval`, `WorkflowAgent` for durable runs, OTel. ESM-only, Node 22+ | Stable, with high API churn (v7 renamed `system`→`instructions`; a codemod exists) |
| **Mastra 1.x** | TS | You want a batteries-included TypeScript agent server: memory, workflows, evals, tracing | Stable, releases weekly |
| **LangGraph 1.x** | Py/TS | You need explicit graph orchestration, checkpointing and human-in-the-loop. It's the framework named most often in job posts | Stable; no breaking changes until 2.0 |
| **Pydantic AI 2.x** | Py | You want type-safe Python agents that feel like FastAPI | Stable |
| **OpenAI Agents SDK** | Py/TS | You want lightweight multi-agent setups with handoffs, guardrails and sessions. Provider-agnostic | Pre-1.0, widely used |
| **Claude Agent SDK** | Py/TS | You want to embed the Claude Code harness (files, bash, hooks, subagents) in your product. *Claude Managed Agents* is the hosted version | Pre-1.0, fast-moving |
| **Microsoft Agent Framework** | Py/.NET | You work in an Azure or .NET shop. It replaced AutoGen and Semantic Kernel | Stable (1.0 Apr 2026) |
| **CrewAI** | Py | You want quick role-based multi-agent prototypes | Stable; less favoured for production |
| **LlamaIndex** | Py/TS | You have document-heavy agents. The company is now focused on LlamaParse | Shifting |

- **Learn first:**
  1. **Vercel AI SDK 7**, since TypeScript is your strongest language.
  2. **One agent loop written from scratch** with no framework, so you know what every framework
     is hiding.
  3. **Pydantic AI**, which builds your Pydantic and FastAPI skills at the same time.
- **Later:** **LangGraph**, for job-market literacy. The Claude and OpenAI agent SDKs, when you
  need to embed a coding-agent harness.
- **Skip:** CrewAI, AutoGen and LangChain "chains" as a primary abstraction, unless an employer
  uses them.

---

## 3 · Protocols

| Protocol | Status | Notes |
|---|---|---|
| **MCP, spec 2026-07-28** | Current. Stewarded by the Linux Foundation's Agentic AI Foundation (with goose and AGENTS.md) | **Stateless:** no `initialize` handshake and no session ID. Each request carries the protocol version in `_meta`; a mandatory `server/discover` call replaces the handshake. Works behind ordinary load balancers. Formal 12-month deprecation policy. OAuth/OIDC alignment. Not fully backward-compatible with earlier specs |
| **A2A v1.0** | Shipped in early 2026; reportedly moved under the same Agentic AI Foundation (unverified) | Agent-to-agent delegation across vendors. Signed agent cards. An AP2 extension for payments. Supported by Bedrock AgentCore, Azure AI Foundry and Google ADK |
| **AGENTS.md** | Agentic AI Foundation project | Repository instructions for coding agents. It takes five minutes to learn, so use it |

- **Learn first:** build and deploy **one remote MCP server in TypeScript** with the official
  SDK and OAuth, targeting the 2026-07-28 spec. For a full-stack engineer this is the most
  transferable agent skill.
- **Later:** A2A, once you work on enterprise multi-agent interop.
- **Skip:** any MCP tutorial that predates July 2026. Those describe the session-based protocol.
- **Watch:** AGNTCon + MCPCon North America runs 22–23 Oct 2026.

---

## 4 · Retrieval

### Vector stores

| Tool | Pick this when |
|---|---|
| **pgvector** (0.8.x) | You already run Postgres and have under roughly 10–50M vectors. **This is the default.** Upgrade past 0.8.2 for CVE-2026-3172 |
| **Qdrant** (1.19) | You want a dedicated open-source engine with strong filtering, sparse vectors and 4-bit storage |
| **turbopuffer** | You need cheap, multi-tenant, object-storage-backed search at very large scale |
| **Pinecone** | You want fully managed serverless with no ops |
| Weaviate / LanceDB / Chroma / Elasticsearch | Built-in modules / embedded and multimodal / prototypes / when you already run it |

### Embeddings, rerankers, parsing

| Category | Leading options |
|---|---|
| Embeddings, API | Gemini Embedding, **Voyage-4** (vendor-reported scores), Cohere |
| Embeddings, open | **Qwen3-Embedding** (Apache 2.0), BGE-M3 |
| Embeddings, in the browser | Transformers.js 4.3 with EmbeddingGemma 2, on WebGPU |
| Rerankers, managed | **Cohere Rerank 4**, Voyage rerank-2.5, ZeroEntropy zerank |
| Rerankers, self-hosted | **Qwen3-Reranker**, BGE-reranker-v2-m3. Jina v2 weights are non-commercial |
| Document parsing | **Docling** (MIT; best open-source option), LlamaParse (hosted), Unstructured (widest range of formats), MinerU, or a vision LLM ("PDF in, markdown out") |

- **Learn first:** **pgvector + Postgres full-text search (hybrid) + one reranker API + Docling**,
  with a retrieval eval that measures recall@k and MRR. That combination covers about 80% of RAG
  work.
- **Later:** Qdrant or turbopuffer for scale. Self-hosted Qwen3 embeddings and rerankers.
  Late-interaction retrieval (ColPali).
- **Skip:** comparing five vector databases. Chunking, hybrid search and evals matter far more
  than which store you pick.

---

## 5 · Evals and observability

| Tool | Pick this when | Notes |
|---|---|---|
| **Langfuse** | You want open-source, self-hostable tracing, prompt management and evals. **The default** | Acquired by ClickHouse (Jan 2026); licence unchanged |
| **LangSmith** | You use LangGraph or LangChain | Evaluators count against the same trace meter, which inflates bills |
| **Braintrust** | You want eval-first CI gates and a strong playground | A reported 2026 security incident is unverified |
| **Arize Phoenix** | You want OTel- and OpenInference-native open-source tracing | Stable |
| **MLflow 3** (3.17) | You're in a Databricks or classical-ML shop and want GenAI tracing alongside experiments | Stable |
| **promptfoo** | You want YAML/CLI eval suites and red-teaming in CI. It suits TypeScript users | MIT. OpenAI announced an acquisition (Mar 2026); keep an eye on its neutrality |
| **Inspect AI** (UK AISI) | You need rigorous agentic or safety evals in sandboxes | Research-grade |
| **OTel GenAI semantic conventions** | Instrumenting anything | Moved to their own repo; **still unreleased and unstable**. Use them anyway, and pin the version |

- **Learn first:** the method: error analysis, golden sets, calibrated LLM judges, CI
  regression gates. Practise it with **promptfoo** or AI SDK/Mastra evals, sending traces to
  **self-hosted Langfuse** over OTel.
- **Later:** whichever of Braintrust or LangSmith an employer uses. Inspect for agents.
- **Skip:** learning more than two observability vendors in depth. The concepts transfer between
  them.

---

## 6 · Guardrails and security

| Tool | Use |
|---|---|
| **OWASP Top 10 for LLM Applications 2026** and the **OWASP Agentic Top 10** | Threat-modelling every feature. In 2026, *Excessive Agency* moved up to #3, *Unbounded Consumption* to #6, and *System Prompt Leakage* became *Hidden Context Exposure* |
| Llama Guard / PromptGuard 2 / LlamaFirewall | Cheap safety and injection classifiers that work with any model |
| LLM Guard | Python input/output scanners for PII, injection and toxicity |
| NeMo Guardrails | Dialogue-flow control for regulated chatbots |
| Guardrails AI | Output validation. It is **not** an injection defence |
| promptfoo red-team / garak / PyRIT | Adversarial testing in CI |
| Vercel Sandbox / E2B / Modal Sandboxes / Docker | **Essential** for running agent-generated code |
| Hash-pinned lockfiles (`uv`), `.pth` auditing | Supply chain hygiene. The LiteLLM compromise is the case study |

- **Learn first:** the two OWASP lists and the **architectural** defences: least-privilege tools,
  human approval (`toolApproval` in AI SDK 7), sandboxing, output encoding, spending caps. Then
  add one classifier layer.
- **Skip:** treating any guardrail library as a fix for prompt injection. None of them is.

---

## 7 · Fine-tuning

| Tool | Pick this when |
|---|---|
| **TRL** (Hugging Face, 1.x) | You want the reference stack for SFT, DPO and GRPO. 1.16 added async GRPO with tree attention |
| **Unsloth** | You're on one GPU or Colab and want LoRA/QLoRA about 2× faster with less VRAM. Multi-GPU support is in alpha |
| **Axolotl** | You want config-driven, reproducible multi-GPU recipes |
| **Tinker** (Thinking Machines) | You want managed LoRA post-training on open models with low-level control (GA Dec 2025) |
| Provider fine-tuning (Together, Fireworks) | You want managed SFT without your own GPUs. **OpenAI reportedly closed fine-tuning to new sign-ups in May 2026** (unverified; see chapter 07) |
| torchtune | **Discontinued.** Skip |

Base libraries: `transformers` 5.x, `torch` 2.14.

- **Learn first:** nothing deep yet. When you start, do **one Unsloth QLoRA SFT run** on a small
  open model (Gemma 4 E4B or a small Qwen) and **one DPO or GRPO run in TRL**, and evaluate both
  against a prompt-only baseline.
- **Later:** RL with verifiable rewards, and distillation from frontier models.
- **Skip:** pretraining from scratch, except as a learning exercise. torchtune.

---

## 8 · Inference and serving

**Engines:**
- **vLLM** 0.32: Model Runner V2, NVFP4/FP8 KV cache. Note that CORS is no longer open by
  default.
- **SGLang** 0.5.x.
- **TGI was archived** on 21 Mar 2026.

**Quantisation formats:** FP8 and NVFP4 (Hopper and Blackwell GPUs), AWQ/GPTQ (INT4 on GPU), GGUF
(llama.cpp).

| Provider | Pick this when |
|---|---|
| **Modal** | You want Python-first serverless GPUs, sandboxes and batch jobs as code |
| **Baseten** | You need production dedicated deployments of open or custom models |
| **Fireworks / Together** | You want fast serverless open models plus fine-tuning |
| **Groq / Cerebras** | You need very low latency or very high tokens/second on open models |
| **RunPod / Lambda** | You want raw GPU pods for training or self-hosted vLLM at low $/hour |
| Bedrock / Vertex / Azure AI Foundry | You face enterprise procurement or data-residency requirements |

- **Learn first:** call open models through OpenRouter, Together or Fireworks, which needs no
  ops. Then **deploy vLLM on Modal once**, so you feel batching, the KV cache, quantisation and
  the tokens/second-per-dollar trade-off yourself.
- **Later:** SGLang, speculative decoding, multi-GPU parallelism.
- **Skip:** TGI, and writing your own CUDA kernels.

---

## 9 · Local models

| Tool | Pick this when |
|---|---|
| **Ollama** (0.40) | You want one-command local models and an OpenAI-compatible endpoint for development and tests |
| **llama.cpp / GGUF** | You need maximum portability across CPU, Metal and Vulkan. The ggml team joined Hugging Face in Feb 2026; it remains MIT-licensed |
| **LM Studio** | You want a GUI for exploring models, plus a headless server |
| **MLX** | You're on Apple Silicon and want the fastest local inference and LoRA |
| **Transformers.js v4 / WebLLM** | You want in-browser inference on WebGPU, which now works in Chrome, Firefox and Safari 26+. This is a natural fit for a frontend engineer |

- **Learn first:** **Ollama** with Gemma 4 or Qwen for offline development. **Transformers.js**
  for client-side embeddings.
- **Skip:** running frontier-sized open models locally. Muse Spark Open needs about 700 GB.

---

## 10 · Classical ML, MLOps and data

| Layer | Learn |
|---|---|
| DataFrames | **Polars 2.0 and DuckDB**. Learn pandas well enough to read other people's code |
| Classical ML | **scikit-learn** (1.9), XGBoost and LightGBM |
| Deep learning | **PyTorch** 2.14, Hugging Face Transformers 5.x |
| Tracking and registry | **MLflow 3** or W&B |
| Orchestration | Whichever of Prefect, Dagster or Airflow the employer uses |
| Notebooks | Jupyter; **marimo** for reactive, git-friendly notebooks |

- **Learn first:** pandas basics → Polars and DuckDB, then scikit-learn pipelines with proper
  splits and metrics. This lines up with the MS coursework.
- **Skip:** Kubeflow, SageMaker Pipelines in depth, and Spark, unless a job needs them.

---

## 11 · AI coding tools

These are part of the job now. Mentions in postings went from 3.5% to 8.9% in six months.

| Tool | Notes |
|---|---|
| **Claude Code** | Terminal-native agent with plugins, blocking hooks, subagents, skills and MCP |
| **Codex** (CLI and cloud) | OpenAI's agent. Defaults to GPT-6.1 Sol |
| **Cursor 3** | IDE-first, with an agents window and its own Composer model |
| **GitHub Copilot** | Largest installed base, losing share. Survey figures conflict |

- **Learn first:** become fluent in **one terminal agent and one IDE agent**, including their
  extension points: AGENTS.md/CLAUDE.md, hooks, MCP servers, subagents, skills, headless/CI mode.
  These tools also double as case studies in agent-harness design.
- **Skip:** switching tools every month.

---

## 12 · Python tooling for a TypeScript developer

| Tool | TypeScript analogy | Recommendation |
|---|---|---|
| **uv** | pnpm + nvm + npx | Learn first: `uv init`, `uv add`, `uv run`, `uvx`, lockfiles |
| **ruff** | eslint + prettier | Learn first |
| **pyright / basedpyright** (watch **ty**) | tsc | Use pyright now. `ty` is pre-1.0 |
| **Pydantic v2** | zod | Learn first. It's the backbone of FastAPI, Pydantic AI and structured output |
| **FastAPI** | Hono/Express + zod-openapi | Learn first for Python AI services |
| pytest, httpx, asyncio | vitest, fetch, Promises | Learn. Async is the main conceptual gap |

**Skip:** pip, virtualenv, poetry, pyenv, black, isort and flake8. `uv` and `ruff` replace all of
them. The one exception is conda, which you still need where CUDA dependencies force it.

---

## Learning order

1. **Weeks 1–3, TypeScript core.**
   - Anthropic and OpenAI SDKs.
   - Vercel AI SDK 7: tools, structured output, streaming UI, approvals. Route through AI
     Gateway or OpenRouter.
   - One MCP server on the 2026-07-28 spec.
2. **Weeks 3–6, retrieval and evals.**
   - pgvector hybrid search, a reranker and Docling.
   - A promptfoo eval suite in CI.
   - Traces to Langfuse over OTel.
3. **Weeks 6–10, Python.**
   - uv, ruff, Pydantic and FastAPI.
   - A Pydantic AI agent, then LangGraph.
   - Polars, DuckDB and scikit-learn alongside the MS.
4. **Later.** vLLM on Modal, Unsloth/TRL fine-tuning, Ollama and MLX, A2A, the Claude and OpenAI
   agent SDKs, guardrail classifiers.

## Deprecated or fading: do not learn

| Item | Status |
|---|---|
| OpenAI Assistants API | Shut down 26 Aug 2026 |
| OpenAI legacy snapshots (GPT-4, o1, o3-mini, …) | Shut down 23 Oct 2026 |
| Hugging Face TGI | Archived 21 Mar 2026 |
| torchtune | Development wound down |
| AutoGen, Semantic Kernel | Folded into Microsoft Agent Framework |
| Humanloop | Acquired by Anthropic; product sunset |
| MCP tutorials from before July 2026 | Describe the old stateful protocol |
| poetry, pyenv, black, isort, flake8 | Replaced by uv and ruff |
| Llama as the default open model | The open-weight lead has moved to Qwen, GLM, Kimi, DeepSeek and Gemma |

## Claims in this chapter that are not fully verified

- The open-weight leaderboard positions.
- A2A moving under the Agentic AI Foundation.
- Whether OpenAI's acquisition of promptfoo has closed.
- Market-share figures for coding tools.
- Valuation and revenue figures for GPU providers.
- The reported Braintrust security incident.
- Gemini 4 Argon's pricing schedule.
