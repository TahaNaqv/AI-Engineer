# Full-Stack AI/ML Engineer — Course Roadmap

**Learner:** Taha A. Naqvi, Senior Full Stack & Web3 Engineer
**Drafted:** 2026-09-23 · **Updated:** 2026-10-20 (tool and model facts aligned with [04-tooling.md](04-tooling.md)) · **Length:** about 50 weeks at 10–12 hrs/week (Oct 2026 → Sep 2027)
**Runs alongside:** full-time work at Ideofuzion and the MS in Data Science at FAST-NUCES (2026–28)

---

## 1. Where you're starting from

| You already have | Why it counts |
|---|---|
| Production backends: NestJS, Django/DRF, Strapi, Celery + Redis, Postgres/Mongo, Docker, AWS | Most job postings ask for CI/CD (37%), Docker (24%), K8s (24%) and cloud (55%). You already cover this, and most ML-first candidates don't. |
| TypeScript, React and Next.js | "Full-stack AI engineer" postings are mostly TS + Next.js + Postgres/pgvector + RAG + agents, which is close to your current stack. |
| Shipped LLM apps: GPT-4o function calling + Whisper (Zencore), RAG WhatsApp SaaS (AliHelp), LangChain/LangGraph | You're past the "hello world" stage. |
| University ML: gradient-descent regression, LSTM, recommender, OCR model; pandas/numpy | The ideas will come back quickly. |
| Teaching experience (Edversity) | Explaining concepts out loud is part of this course's method. |

| The gap | What the market data says |
|---|---|
| **Evals and observability** | Evaluation shows up in 60% of AI-first roles. Only 52% of teams run offline evals. It's the most-cited thing that separates engineers who build AI systems from people who wire up APIs. |
| **ML/DL fundamentals** (math, classical ML, PyTorch, transformer internals) | 87% of AI-first roles want skills beyond GenAI, and 54% want ML knowledge. Interviews still ask about bias/variance, gradient descent and ML system design. |
| **Fine-tuning and post-training** (LoRA, DPO, GRPO) | Mentioned in 15–27% of postings, but the core of the job in under 5%. It signals depth rather than opening doors. |
| **Inference and serving** (vLLM, quantization, self-hosting) | One of the hardest skill sets to hire for, and rising. |
| **Agent security** (prompt injection, excessive agency) | "Excessive Agency" moved up to #3 in OWASP LLM Top 10 2026. |

**Target role:** an AI Engineer with real ML depth. You build production AI systems end to end: the UI, the backend, the model layer, evals and serving. You understand the models well enough to fine-tune, self-host and debug them. This course doesn't aim at frontier-lab research-engineer roles; that would be a separate 2+ year path.

---

## 2. How the course is structured

**Build first, then go deep.** Phases 1–3 start from your strengths, so you're shipping better AI systems at work within weeks. Phases 4–7 build the ML depth underneath. Phase 8 turns the work into a portfolio and interview readiness.

**Two lanes each week:**
- **Main lane (about 8–9 hrs):** the current phase.
- **Foundations lane (about 2–3 hrs, Phases 1–3 only):** math and ML intuition, a little at a time (3Blue1Brown, then Serrano's Math for ML). By Phase 4 the math won't be new, and it will overlap with your MS coursework.

**One flagship system, built up over the course.** You don't build eight throwaway demos. You build one production system in stages:

```
Ph1 LLM service  →  Ph2 + evals & RAG  →  Ph3 + agents & MCP
      →  Ph6 swap in YOUR fine-tuned model  →  Ph7 self-host it with vLLM  →  Ph8 ship + write up
```

By the end you can show one eval table comparing a frontier API with your own fine-tuned, self-hosted model on quality, cost and latency. That's the kind of project hiring managers say stands out.

**Every module has the same five parts:**
1. **Concepts:** notes I write for you, first-principles and diagram-heavy.
2. **From scratch:** implement the core idea without frameworks, e.g. an agent loop, BM25, backprop, attention, LoRA.
3. **Lab:** use the real production tools.
4. **Project increment:** add to the flagship, with acceptance criteria.
5. **Checkpoint:** interview-style questions. You explain the answers back to me, and I review your code.

---

## 3. The roadmap

### Phase 0 — Setup & Orientation · 1 week
- Set up the environment: `uv` (now defaults to Python 3.15) and `ruff`, Jupyter/VS Code notebooks, PyTorch, Hugging Face account. Use hash-pinned lockfiles from day one; the March 2026 LiteLLM compromise on PyPI is the reason. For GPUs: Colab for free work, Modal or RunPod for rented H100/L40S time.
- Watch Karpathy's *Deep Dive into LLMs like ChatGPT* (3.5 hrs) to get the mental model.
- Take a baseline self-assessment (math, ML, LLM systems) so I can adjust how fast we go.
- Choose the flagship project domain (see §5).

---

### Phase 1 — LLM Application Engineering, Done Properly · 6 weeks
*You've used these APIs before. Now learn how they work and what they cost.*

- How LLMs work at the level an app builder needs: tokens, sampling, context windows, and why models hallucinate.
- The three big providers (Claude, OpenAI Responses API, Gemini) and provider-agnostic layers: Vercel AI SDK 7 with AI Gateway or OpenRouter on the TS side, a thin in-house client on the Python side. Keep model IDs in config: in the four weeks before this update, Anthropic, OpenAI and Google all replaced models, and some newer models reject sampling parameters such as `temperature`.
- Tool calling and **strict structured outputs** (JSON-schema constrained).
- Reasoning and effort controls. Multimodal input: PDFs, images, audio.
- **Prompt caching economics**, batch APIs, streaming, and working out cost and latency per request.
- **Context engineering:** prompt structure, what goes in the context window, compaction, long context vs. retrieval.
- Choosing a model with an evaluation harness instead of benchmark leaderboards.
- Reading: Chip Huyen, *AI Engineering*, chapters 1–5.

**Project increment:** the flagship's core LLM service in Python (FastAPI) with a Next.js front end. Streaming, structured outputs, tool calls, a cost/latency dashboard, and prompt caching you've measured.
**Checkpoint:** estimate the cost of a 10-turn tool-using conversation, with and without caching.

---

### Phase 2 — Evals, Observability & Retrieval · 5 weeks
*This is the biggest gap in most candidates, and the most important part of the course.*

- **Evals:** error analysis on real traces first, then:
  - code-based assertions
  - golden datasets
  - LLM-as-judge calibrated against human labels (rubric vs. pairwise judging, judge bias)
  - synthetic test data
  - regression evals in CI
  - online evals on sampled production traffic
- **Observability:** tracing with OpenTelemetry GenAI semantic conventions (pin the version; they're not stable yet), Langfuse (open source), and a look at LangSmith, Braintrust and Arize Phoenix.
- **Retrieval, built properly:**
  - embeddings (what they are geometrically)
  - BM25 implemented by hand
  - pgvector with HNSW indexes
  - **hybrid search plus a cross-encoder reranker as the baseline**
  - chunking: recursive splitting, contextual retrieval, late chunking
  - metadata filters and multi-tenancy
- **Retrieval metrics:** recall@k, MRR, nDCG. Faithfulness and groundedness for generated answers.
- When *not* to use RAG: long context plus caching, or fine-tuning instead.
- Electives: GraphRAG, visual-document retrieval (ColPali-style).
- Reading: *AI Engineering* ch. 3–4, 6. Hamel Husain & Shreya Shankar's Evals FAQ, and their new book *Evals for AI Engineers* (O'Reilly, Oct 2026). Their paid Maven course is optional and the best paid item on this list.

**Project increment:** add RAG to the flagship, plus a full eval suite (a golden set of at least 100 cases, a calibrated judge, a CI gate that fails the build on regression) and Langfuse tracing.
**Checkpoint:** your judge's agreement with your own labels is ≥ 0.8 by Cohen's κ. You can explain where each point of recall improvement came from.

---

### Phase 3 — Agents, MCP & AI Security · 5 weeks
- **The agent loop from scratch**, no framework: plan → call tool → observe → repeat, with stop conditions.
- Tool design: naming, schemas, errors the model can recover from, idempotency.
- Workflow patterns vs. autonomous agents. Subagents. Memory. Compaction.
- **Human-in-the-loop approvals**, durable execution and checkpointing.
- Frameworks, compared after you've built the loop yourself:
  - Python: LangGraph 1.x, Pydantic AI 2.x (stable since June 2026), Claude Agent SDK, OpenAI Agents SDK
  - TypeScript: Vercel AI SDK 7 (`toolApproval`, `WorkflowAgent`), Mastra 1.x
  - All of these ship releases weekly. Learn the concepts and read the changelogs; don't memorise APIs
- **MCP in depth:**
  - write your own MCP servers and clients against the **2026-07-28 stateless spec** (older tutorials describe the session-based version)
  - what changed in that spec: no `initialize` handshake or session ID, a mandatory `server/discover` call, Tasks and MCP Apps as extensions, OAuth/OIDC alignment
  - A2A at the concept level
- Computer use and browser agents, treated as high-risk capabilities.
- **Security:** OWASP LLM Top 10 2026 and the OWASP Agentic Top 10.
  - Prompt injection can't be fully prevented, so the defense is architectural: least-privilege tools, trust boundaries, sandboxing, and approval before side effects.
  - MCP tool poisoning.
  - Guardrail classifiers as one layer, not the whole defense. Red-teaming with promptfoo or DeepTeam.
- **Agent evals:** trajectory evals, tool-call accuracy, task success rate. Inspect.
- Reading: Anthropic's *Building Effective Agents*, the Hugging Face Agents and MCP courses, Claude Academy, and *AI Engineering* ch. 6.

**Project increment:** turn the flagship into an agent that uses 2+ MCP servers you wrote, requires approval before any write action, has cost caps and retry/backoff, is red-teamed, and has an agent eval suite.
**Checkpoint:** design an agent system on a whiteboard, covering failure modes and the security threat model.

---

### Phase 4 — Math & Classical Machine Learning · 7 weeks
*Coordinate with your MS: when a course covers a topic, we skip it here and work on applying it instead.*

- **Math, just enough and applied:**
  - linear algebra: vectors, matrices as transformations, eigenvectors, SVD/PCA
  - calculus: gradients, the chain rule
  - probability and statistics: distributions, Bayes, MLE, hypothesis tests, confidence intervals (these are what make eval results trustworthy)
- **The ML workflow:** framing the problem, splits, leakage, cross-validation, the bias/variance trade-off, regularization.
- Algorithms, each implemented from scratch once and then used through scikit-learn:
  - linear and logistic regression
  - trees, random forests, **gradient boosting (XGBoost/LightGBM, still the default for tabular data)**
  - k-means, PCA
- Metrics: precision/recall/F1, ROC-AUC, calibration, and choosing metrics that reflect business cost.
- Data tooling: pandas → **Polars 2.0 and DuckDB**, feature engineering.
- Recommenders and ranking, at the basics level. These are common ML system design interview questions.
- Resources:
  - Géron, *Hands-On ML with Scikit-Learn and PyTorch* (the Dec 2025 PyTorch edition, not the TensorFlow 3rd edition), Part I
  - Serrano's Math for ML
  - StatQuest when something doesn't click
  - Kaggle Learn

**Project:** one Kaggle tabular competition taken end to end, plus a classical ML model added to the flagship (e.g. intent classification or ticket routing) that competes with the LLM on cost.
**Checkpoint:** an ML-fundamentals interview drill.

---

### Phase 5 — Deep Learning from Scratch · 9 weeks
- PyTorch fundamentals: tensors, autograd, `nn.Module`, the training loop, GPU use.
- **Karpathy's *Neural Networks: Zero to Hero*, the whole series, coding along:** micrograd → makemore (MLP, BatchNorm, backprop by hand) → build GPT → the tokenizer → reproduce GPT-2.
- Theory alongside it: Prince, *Understanding Deep Learning*. Covers optimizers, initialization, normalization, residual connections, overfitting.
- CNNs and vision basics, only as much as you need to read the field (CS231n is an optional elective).
- Attention and transformers derived yourself. Tokenization (BPE).
- Embeddings and contrastive learning: this explains how the retrieval you built in Phase 2 actually works.
- Experiment tracking starts here: W&B or MLflow.

**Project:** train your own small GPT. Then do a **nanochat** run on rented GPUs (tokenizer → pretraining → SFT → chat UI). Finish by writing microgpt from memory.
**Checkpoint:** explain the full backward pass through attention on a whiteboard.

---

### Phase 6 — LLM Internals, Fine-Tuning & Post-Training · 6 weeks
- Modern architectures: RoPE, GQA/MLA, MoE, the KV cache, long context. Use Stanford CME295 as the survey and selected CS336 lectures for depth.
- The training pipeline: pretraining → SFT → preference tuning → RL.
- **LoRA/QLoRA:** implement LoRA by hand once, then use HF TRL 1.x and Unsloth. Axolotl for reproducible configs. Tinker (Thinking Machines) for managed LoRA on open models.
- **DPO** for preferences. **GRPO / RL with verifiable rewards** (reasoning models after DeepSeek-R1).
- **Distillation** from frontier models to small open models. Building synthetic datasets.
- **When to fine-tune:** only after prompting, RAG and evals have stopped improving. It's for format, latency, cost and narrow tasks. It is *not* a way to add knowledge.
- Open-weight models (Oct 2026): Qwen 3.6/3.8, Gemma 4 (Apache 2.0), DeepSeek V4.1, GLM-5.3, Kimi K3, Mistral. Meta's Muse Spark Open (Oct 2026) has open weights but a restrictive licence. Llama is no longer the default choice.
- Fine-tuning is moving to open weights. OpenAI reportedly closed its fine-tuning platform to new sign-ups in May 2026 (unverified; see [07-risks-and-resources.md](07-risks-and-resources.md)).
- Resources:
  - Raschka's *LLMs-from-scratch* repo (modern-architecture notebooks) and *Build a Reasoning Model (From Scratch)*
  - the HF LLM Course
  - Maxime Labonne's llm-course as an index

**Project increment:** fine-tune a small open model (e.g. Qwen 3.6 or Gemma 4 in the 4B–27B range) on a narrow task from the flagship, distilled from the frontier model. Run it through your Phase 2 eval suite and compare quality, cost and latency against the API.
**Checkpoint:** defend in writing whether the fine-tune should go to production.

---

### Phase 7 — Inference, Serving & MLOps · 5 weeks
- **Inference internals:**
  - prefill vs. decode
  - KV cache and prefix caching
  - continuous batching
  - speculative decoding
  - TTFT/TPOT, and throughput vs. latency
- **Serving:** vLLM (the default) and SGLang, through OpenAI-compatible endpoints. TGI has been archived and torchtune is no longer developed, so we skip both.
- **Quantization:** FP8 (H100 and newer), AWQ INT4, GGUF Q4_K_M for local use, NVFP4 at the concept level. Local serving: llama.cpp, Ollama, MLX.
- GPU cloud: Modal, RunPod, Lambda. **Self-host vs. API cost math.** Autoscaling and cold starts.
- **MLOps:**
  - MLflow 3 (a model registry, plus GenAI tracing)
  - data and model versioning
  - drift and quality monitoring
  - Docker, K8s concepts including GPU scheduling
  - Ray at the awareness level
- Elective, since it plays to your frontend strength: **in-browser AI** with Transformers.js v4 + WebGPU.
- Reading: Chip Huyen, *Designing ML Systems*, skimmed for the lifecycle, monitoring and distribution shift.

**Project increment:** serve your fine-tuned model with vLLM on a GPU cloud, quantized and load-tested, with a monitoring dashboard. The flagship routes between the API and your model based on eval-measured quality.
**Checkpoint:** a production-readiness review of the flagship, run by me.

---

### Phase 8 — Capstone, Portfolio & Interview Readiness · 6 weeks
- Finish the flagship: live URL, README with architecture diagram, **eval table**, cost analysis, a write-up of design trade-offs, and a 5-minute Loom walkthrough.
- A technical blog post based on the flagship's results. That's the easiest place to start given your teaching experience.
- **Interview preparation:**
  - LLM system design: design an agent or RAG system, with evals, cost and security
  - ML system design: problem → metrics → data → model → evaluation → deployment and A/B testing → monitoring
  - practical coding on LLM-adjacent problems (a retrieval scorer, a token-budget allocator, a tool orchestrator), not LeetCode
  - 2–3 timed take-home simulations ("build a RAG app/agent from this brief")
  - a project deep-dive defense
  - for forward-deployed roles: a customer discovery-call role-play
- Target markets: remote roles for US and EU companies (check whether they hire outside the US), UAE and KSA (strong AI hiring demand), and AI/ML roles at Pakistani product companies. Also AI + Web3, where you have an unusual advantage.

---

## 4. Timeline at a glance

| Phase | Weeks | Approx. dates | Main output |
|---|---|---|---|
| 0 Setup | 1 | Late Sep 2026 | Environment, baseline assessment, chosen domain |
| 1 LLM App Eng. | 6 | Oct – mid Nov | Flagship core service |
| 2 Evals + RAG | 5 | mid Nov – Dec | Eval suite + CI gate + hybrid RAG |
| 3 Agents + MCP + Security | 5 | Jan 2027 | Agent with MCP servers, approvals, red-teaming |
| 4 Math + Classical ML | 7 | Feb – mid Mar | Kaggle competition + classifier in the flagship |
| 5 Deep Learning | 9 | mid Mar – mid May | Your own GPT + a nanochat run |
| 6 Fine-tuning | 6 | mid May – Jun | Fine-tuned model vs. API eval table |
| 7 Serving + MLOps | 5 | Jul – early Aug | Self-hosted, monitored model in production |
| 8 Capstone + Career | 6 | Aug – Sep 2027 | Portfolio, blog post, interview readiness |

Buffer: move dates back around MS exam weeks. The course is sequenced by milestones, not by calendar.

**Useful for your job before the end:** after Phase 3 (about 4 months) you can credibly apply to "Full-Stack AI Engineer" roles. The later phases build the depth for "AI/ML Engineer" roles.

---

## 5. Flagship project domains (pick one in Phase 0)

1. **Web3 + AI:** a DeFi/on-chain analytics agent, or a smart-contract audit assistant with a fine-tuned vulnerability classifier, scored on **EVMbench** (OpenAI + Paradigm, 2026), which gives the project objective numbers. See [05-roadmap-and-portfolio.md](05-roadmap-and-portfolio.md), project #3. Combines your two specialties, and few candidates can do this.
2. **Urdu / Roman-Urdu customer-support agent** (AliHelp, rebuilt properly). Low-resource-language fine-tuning is a real technical challenge and fits the Pakistani and Gulf markets.
3. **Document intelligence for spreadsheets and insurance** (building on Sigma 17): extraction, a fine-tuned small model and actuarial Q&A. An enterprise-shaped problem.
4. **Audit/compliance copilot** (building on AuditSence): RAG over policies, an agent that drafts findings, human approval.

---

## 6. What we're deliberately skipping

- OpenAI Assistants API (shut down 2026-08-26), OpenAI legacy snapshots such as GPT-4, o1 and o3-mini (shut down 2026-10-23), TGI (archived), torchtune (no longer developed), AutoGen and Semantic Kernel (replaced by Microsoft Agent Framework), Humanloop (sunset).
- poetry, pyenv, black, isort and flake8. `uv` and `ruff` replace them.
- MCP tutorials written before the 2026-07-28 spec. Llama as the default open model.
- Full Stack Deep Learning 2022/23 and d2l.ai (outdated or redundant). Géron's TensorFlow edition.
- Choosing one of each overlapping pair: Ng's ML Specialization *or* Géron Part I; Karpathy *or* Raschka's *Build an LLM* as the main resource; Serrano *or* Imperial for math.
- CUDA and llm.c, and frontier-scale distributed training. These are optional deep dives only.

**What to expect to change:** model names, prices and framework versions go out of date within about 3 months. Phase 1's model and pricing material gets a refresh each quarter. Concepts are taught so they don't depend on a vendor.

---

## 7. Research this roadmap is based on (Sep 2026)

- **Job-market data:**
  - Grigorev, *AI Engineering Field Guide*: 6,964 postings, Feb–Aug 2026 — github.com/alexeygrigorev/ai-engineering-field-guide
  - LinkedIn *Jobs on the Rise 2026*
  - 365 Data Science Glassdoor analysis (Apr 2026)
  - LangChain *State of Agent Engineering* survey
  - Axial Search, 43k US postings
- **Curricula reviewed:**
  - Karpathy's Zero to Hero, nanochat and microgpt
  - Stanford CS336 (Spring 2026) and CME295
  - Chip Huyen's *AI Engineering* and *Designing ML Systems*
  - Géron (PyTorch edition, 2025)
  - Prince, *UDL*
  - Raschka's LLMs-from-scratch and reasoning-from-scratch
  - Hugging Face LLM, Agents and MCP courses
  - Hamel Husain & Shreya Shankar's evals course
  - Made With ML, MLOps and LLM Zoomcamps
  - roadmap.sh
- **Tooling state:**
  - Anthropic, OpenAI and Google model docs
  - MCP spec 2026-07-28 changelog
  - OpenTelemetry GenAI semantic conventions
  - TRL 1.x, vLLM and SGLang comparisons
  - OWASP LLM Top 10 2026 and Agentic Top 10
  - Vercel AI SDK 7, Mastra 1.x, Pydantic AI 2.x
- **Could not verify:** Pakistan and MENA salary figures (low-quality sources), official Anthropic and OpenAI job-posting text (third-party summaries used instead), and the exact OWASP 2026 ordering (check it against the PDF).
- **October 2026 refresh:** the full re-researched dossier ([02](02-market-data.md)–[07](07-risks-and-resources.md), [sources.md](sources.md)) supersedes the figures above where they differ.
